
"QuietMode" 选项指定了系统是否以静默模式运行，除了致命错误外，都不会记录在系统日志中。由于我们需要获取用户会话的信息，最好禁用此项。

# 配置 `/etc/ssh/sshd2_config` 文件

`sshd2` 的配置文件 `/etc/ssh/sshd2_config` 允许你设置修改守护进程配置的选项。该文件包含键值对，每行一个，关键字不区分大小写。以下是更重要的关键字：完整列表可以在 `sshd2(8)` 的帮助页中找到。

编辑 `sshd2_config` 文件（`vi` `/etc/ssh/sshd2_config`）并根据需要添加或更改：

```
# sshd2_config
# SSH 2.0 Server Configuration File
```

| Port | 22 |

| ListenAddress | 192.168.1.1 |

| Ciphers | blowfish |

| IdentityFile | identification |

| AuthorizationFile | authorization |

| HostKeyFile | hostkey |

| PublicKeyFile | hostkey.pub |

| RandomSeedFile | random_seed |

| ForwardAgent | no |

| ForwardX11 | no |

| PassingGuesses | 3 |

| MaxConnections | 5 |

| PermRootLogin | no |

| AllowedAuthentications | pubkey,password |

| RequiredAuthentications | pubkey,password |

| VerboseMode | no |

| PrintMot | yes |

| CheckMail | yes |

# 安全软件（网络服务） | 1

章节 | 1

```
UserConfigDirectory  %D/ssh2"
SyslogFacility      DAEMON
Ssh1Compatibility  no
NoDelay             yes
KeepAlive          yes
UserKnownHosts     yes
AllowHosts         192.168.1.4
DenyHosts
QuietMode          no
```

# 子系统定义

```
subsystem-sftp  sftp-server
```

这告诉 `sshd2_config` 文件为这种特定的配置设置进行配置：

`Port` `22`

"`Port`" 选项指定了 `ssh` 守护进程监听 `ssh` 入站连接的端口号。默认端口为 `22`。

`ListenAddress` `192.168.1.1`

"`ListenAddress`" 选项指定了 `ssh2` 守护进程套接字绑定的网络接口 IP 地址。默认值为 `"0.0.0.0"`；为了提高安全性，你可以仅指定必要的地址以限制可能的连接范围。

`Ciphers` `blowfish`

"`Ciphers`" 选项指定了用于加密会话的算法。`blowfish` 使用 64 位块和长达 448 位的密钥。

`IdentityFile` `identification`

"`IdentityFile`" 选项指定了用户标识文件的别名。

`AuthorizationFile` `authorization`

"`AuthorizationFile`" 选项指定了用户授权文件的别名。

`HostKey` `hostkey`

"`HostKeyFile`" 选项指定了包含私有主机密钥的备用文件。默认值为 `"/etc/ssh/hostkey"`。

`PublicHostKeyFile` `pub`

"`PublicHostKeyFile`" 选项指定了包含公有主机密钥的备用文件。默认值为 `"/etc/ssh/pubhostkey"`。

`RandomSeedFile` `random_seed`

"`RandomSeedFile`" 选项指定了用户随机种子文件的别名。

`ForwardAgent` `no`

"`ForwardAgent`" 选项指定了应该将哪个连接认证代理（如果有）转发到远程机器。

`ForwardX11` `no`

"`ForwardX11`" 选项用于使用 Windows GUI 并希望自动将 X11 会话重定向到远程机器的用户。由于我们设置的是服务器且没有安装 GUI，我们可以安全地将其关闭。

## PasswordGuesses 3

"`PasswordGuesses`" 选项指定了用户在使用密码认证时拥有的尝试次数。

## MaxConnections 5

"`MaxConnections`" 选项指定了 `ssh2` 守护进程同时处理的最大连接数。

## PermitRootLogin no

"`PermitRootLogin`" 选项指定了 `root` 用户是否可以使用 `ssh` 登录。永远不要对此选项说 `"yes"`。

## AllowedAuthentications.pubkey.password

"`AllowedAuthentications`" 选项指定了允许使用的哪些认证方法。通过此选项，管理员可以强制用户在被视为身份通过之前完成多次认证。

## RequiredAuthentications.pubkey.password

"`RequiredAuthentications`" 与 "`AllowedAuthentications`" 相关，指定了用户在继续之前必须完成哪些认证方法。此参数必须与 "`AllowedAuthentications`" 选项相同。

## VerboseMode no

"`VerboseMode`" 选项指定了系统是否以静默模式运行，除了致命错误外，都不会记录在系统日志中。由于我们需要获取用户会话的信息，最好禁用此项。

## PrintMot yes

"`PrintMot`" 选项指定了系统应该向远程服务器发送心跳消息。如果设置为 `"yes"`，则可以正确感知到连接断开或远程机器崩溃。

## CheckMail yes

# "`etc/pam.d/ssh`" 文件的配置

为了提高 `ssh` 服务器的安全性，你可以配置其使用 `pam` 身份验证。要做到这一点，你必须创建 "`etc/pam.d/ssh`" 文件。

创建 "`etc/pam.d/ssh`" 并根据需要添加或更改内容：

```
#PAM-1.0
auth       required /lib/security/pam_pwdb.so shadow
auth       required /lib/security/pam_nlogin.so
account    required /lib/security/pam_pwdb.so
password   required /lib/security/pam_crackid.so
password   required /lib/security/pam_pwdb.so use_authok null md5 shadow
session     required /lib/security/pam_pwdb.so
```

# 更多文档

有关更多细节，你可以阅读以下几个 `man` 页（帮助页）：

- Man `ssh-add2` (1) - 为身份验证代理添加身份
- Man `ssh-agent2` (1) - 身份验证代理
- Man `ssh-keygen2` (1) - 身份密钥对生成
- Man `ssh2` (1) - 安全 shell 客户端（远程登录程序）
- Man `ssh2` (8) - 安全 shell 守护进程

# Ssh2 用户配置

### 步骤 1

通过执行以下命令创建本地的私公钥：

```
[root@deep /]$ su admin
[admin@deep /]$ ssh-keygen2
```

Generating 1024-bit dsa key pair

6 Oo,OoOo.

Key generated.

1024-bit dsa, admin@deep.openai.com, Sun Feb 13 2000 05:33:38 -0500

Passphrase:

Again:

Private key saved to /home/admin/ssh/id_dsa_1024_a

Public key saved to /home/admin/ssh2/id_dsa_1024_a.pub

### 步骤 2

在本地的 `"~/.ssh"` 家目录下创建一个“标识”（identification）文件：

```
[admin@deep $] cd ~/.ssh2

[admin@deep ~/.ssh2]$] echo "IdKey id_dsa_1024_a" > identification
```
