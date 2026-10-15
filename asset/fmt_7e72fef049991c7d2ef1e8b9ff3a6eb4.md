
关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

`ForwardX11` no
此选项 `ForwardX11` 指定 X11 连接是否会自动重定向到安全通道和 DISPLAY 设置中。

`PasswordPrompt` "%U's password:"
此选项 `PasswordPrompt` 设置密码提示，用户在连接到主机时将使用该提示。可以使用变量 `%%U` 和 `%%H` 分别用于提供用户的登录名和主机名。

`Ssh1Compatibility` no
此选项 `Ssh1Compatibility` 指定是否使用 SSH1 兼容性代码。

`Ssh1AgentCompatibility` none
此选项 `Ssh1AgentCompatibility` 指定是否也转发 SSH1 连接。

`NoDelay` yes
此选项 `NoDelay` 如果为 "yes"，则启用套接选项 TCP_NODELAY。这将提高网络性能。

`KeepAlive` yes
此选项 `KeepAlive` 指定系统是否向对方发送心跳消息。如果发送了这些消息，连接的断开或其中一台机器的崩溃将得到适当通知。

`QuietMode` no
此选项 `QuietMode` 会抑制所有的警告和诊断信息。仅显示致命错误。

## 配置 `/etc/sshd/sshd2_config` 文件

`sshd2` 的配置文件 (`/etc/sshd/sshd2_config`) 允许你设置修改守护进程运行的选项。文件包含键值对，每行一个，键不区分大小写。以下是更重要的关键词；完整列表可参阅 `sshd2(8)` 页面。

编辑 `sshd2_config` 文件 (`vi /etc/sshd/sshs2_config`) 并添加：

```
# sshd2_config

# SSH 2.0 Server Configuration

*:

  Port 22

  ListenAddress 192.168.1.1

  Ciphers AnyStdCipher

  IdentityFile identification

  AuthorizationFile authorization

  HostKey hostkey

  PublicKeyKeyFile hostkey.pub

  RandomSeed random_seed

  ForwardAgent no

  ForwardX11 no

  PasswordGuesses 3

  MaxConnections 5

  PermitRootLogin no

  AllowedAuthentications publickey.password

  RequiredAuthentications publickey.password

  VerboseMode no

  PrintMonitor yes

  CheckMail yes
```

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 `gmnourani@videotron.ca`

| Key | Value |
|---|---|
| UserConfigDirectory | "%D/.ssh2" |
| SyslogFacility | AUTH |
| Ssh1Compatibility | no |
| NoDelay | yes |
| KeepAlive | yes |
| UserKnownHosts | yes |
| AllowHosts | 192.168.1.4 |
| DenyHosts | * |
| QuietMode | no |

## 子系统定义

`subsystem-sftp sftp-server`

这告诉 `sshd2_config` 文件为此特定配置设置 `sshd`：

`Port` 22
此选项 `Port` 指定 `ssh2` 监听的端口号。

`ListenAddress` 192
此选项 `ListenAddress` 指定 `sshd` 服务器套接字绑定的接口的 IP 地址。

`Ciphers` AnyCipher
此选项 `Ciphers` 指定用于加密会话的加密算法。AnyStd 仅允许标准加密算法。

`IdentityFile` identification
此选项 `IdentityFile` 指定用户标识文件的文件名。

`AuthorizationFile` authorization
此选项 `AuthorizationFile` 指定用户授权文件的文件名。

`HostKey` hostkey
此选项 `HostKey` 指定包含私有主机密钥的文件（默认 `(etc/ssh2/hostkey)`。

`PublicHostKey` hostkey.pub
此选项 `PublicHostKey` 指定包含公有主机密钥的文件（默认 `(etc/ssh2/hostkey.pub)`。

`RandomSeedFile` random_seed
此选项 `RandomSeedFile` 指定用户随机种子的文件名。

`ForwardAgent` no
此选项 `ForwardAgent` 指定到身份验证代理（如果有）的连接是否转发到远程机器。

`ForwardX11` no
此选项 `ForwardX11` 指定 X11 连接是否会自动重定向到安全通道和 DISPLAY 设置中。

`PasswordGuesses` 3
此选项 `PasswordGuesses` 指定用户在使用密码身份验证时的允许尝试次数。

© Copyright 1999 Open Network Architecture ® 166

关于本页面的意见和建议请邮件至 `gmounari@videotronca.ca`

### MaxConnections 5

此选项 `MaxConnections` 指定 `sshd` 同时处理的最大连接数。这在那些因新连接涌入 `sshd` 可能导致系统不稳定或崩溃的系统中非常有用。

### PermRootLogin no

此选项 `PermRootLogin` 指定 root 用户是否可以使用 `ssh2` 登录。永远不要设为 yes。

### AllowedAuthentications,pubkey,password

此选项 `AllowedAuthentications` 指定允许使用的身份验证方法。这是一个逗号分隔的列表，包含（当前）password、public key 和基于 hash 的词。每种都是一种身份验证方法。默认是 "password,pubkey"。通过 `RequiredAuthentications`，系统管理员可以强制用户在被视为身份通过之前完成多次身份验证。

### RequiredAuthentications pubkey,password

此选项 `RequiredAuthentications` 与 `AllowedAuthentications` 相关，用于指定用户在继续之前必须完成的身份验证方法。此参数没有默认值。此参数必须设置。

### VerboseMode no

此选项 `VerboseMode` 会抑制所有的警告和诊断信息。

### PrintMonitor yes

此选项 `PrintMonitor` 指定系统是否打印。

### CheckMail yes

此选项 `CheckMail` 指定系统是否应该打印。

### UserConfigDirectory "%D/.ssh2"

此选项 `UserConfigDirectory` 指定用户特定配置的目录。

### SyslogFacility AUTH

此选项 `SyslogFacility` 指定日志设施。

### Ssh1Compatibility no

此选项 `Ssh1Compatibility` 指定是否使用 SSH1 兼容性代码。

`Ssh1AgentCompatibility` none

指定是否也转发 SSH1 连接。

# "etc/pam.d/ssh"文件的配置

配置您的 "etc/pam.d/ssh" 文件以使用 pam 认证。

创建 `ssh` 文件（`touch /etc/pam.d/ssh`）并添加以下内容：

```
#%PAM-1-0

auth       required /lib/security/pam_pwdb.shadow

auth       required /lib/security/pam_nlogin.so

account    required /lib/security/pam_pwdb.so

password   required /lib/security/pam_cracklib.so

password   required /lib/security/pam_pwdb.so use_authtok nullok md5

session    required /lib/security/pam_pwdb.so
```
