
表 2.1 描述了 sshd_config 文件中的前四个选项。

## 表 2.1 sshd_config 文件中的选项

| 选项 | 描述 |
| :--- | :--- |
| Port | 设置 SSH 监听的端口号。默认端口为 22；不过，监听多个端口（包括其他非标准端口，如 80、443 或 8080）可能是最佳选择，因为商务旅行者可能无法使用 22 端口建立出站连接，而 80 或 443 端口通常可用。若要监听多个端口，请添加以下行：<br>Port 22<br>Port 80<br>Port 443<br>Port 8080 |
| Protocol | 允许仅使用 SSH 版本 1、SSH 版本 2 或两者兼用。由于 SSH 版本 1 的安全性较低，仅使用版本 2 可能是一个不错的选择；然而，仍有部分设备尚不支持 SSH 版本 2。若仅使用 SSH 版本 2，请添加以下行：<br>Protocol 2 |
| ListenAddress | 设置 SSH 守护进程监听的 IP 地址。默认值为 0.0.0.0，这会在所有接口上启用 SSH 服务。如果存在不应监听 SSH 的接口（例如防火墙的外部接口），请移除 0.0.0.0 并添加相应的 IP 地址。若仅监听特定接口，请添加以下行：<br>ListenAddress 172.16.1.1<br>ListenAddress 192.168.0.1 |

下一节讨论主机密钥部分。主机密钥部分讨论了与 SSH 服务器主机密钥相关的参数，该密钥的指纹用于识别 SSH 服务器。

```
# HostKey for protocol version 1
# HostKey /etc/ssh/ssh_host_key
# HostKey for protocol version 2
# HostKey /etc/ssh/ssh_host_rsa_key
# HostKey /etc/ssh/ssh_host_dsa_key
```

sshd_config 文件的这一部分相当直接明了。它仅说明了 SSH 版本 1 格式和 SSH 版本 2 格式的主机密钥文件的位置。此外，对于 SSH 版本 2，该部分还说明了 RSA 和 DSA 密钥的位置。

下一节涉及服务器密钥：

```
# Lifetime and size of ephemeral version 1 server key
#KeyRegenerationInterval 3600
#ServerKeyBits 768
```

本节详细规定了服务器密钥的设置。KeyRegenerationInterval 是重新生成服务器密钥的时间间隔（以秒为单位）；ServerKeyBits 是要使用的位数。

下一节涉及日志记录：

```
# Logging
#obsoletes QuietMode and FascistLogging
#SyslogFacility AUTH
#LogLevel INFO
```

本节设置 SSH 服务的日志记录选项。QuietMode 和 FascistLogging 的区别在于，QuietMode 仅记录致命错误，而 FascistLogging 启用详细日志记录。SyslogFacility 指定记录来自 SSH 的消息时使用的 syslog 代码，例如 Daemon 和 Auth。LogLevel 指定记录来自 SSH 的消息时使用的级别，例如仅记录信息性消息（INFO）。

下一节涉及 SSH 的认证选项：

```
#Authentication
#LoginGraceTime 120
#PermitRootLogin yes
#StrictModes yes

#RSAAuthentication yes
#PubKeyAuthentication yes
#AuthorizedKeyFile         .ssh/authorized_keys
```

表 2.2 描述了 SSH 服务器可用的认证选项。

## 表 2.2 认证选项

| 选项 | 描述 |
| :--- | :--- |
| LoginGraceTime | 用户完成认证过程所允许的时间长度。具体而言，是从用户发起连接到用户输入其用户名/密码或公钥/私钥密码的时间为止。 |
| PermitRootLogin | 选项用于允许（yes）或禁止（no）root 用户登录 SSH 会话。最佳实践是限制 root 访问权限，仅允许用户通过 'su' 或 'sudo' 获取 root 权限。此外，如果 root 账户必须能够直接登录，则值 "nopwd" 可以允许 root 直接登录，但仅限通过公钥认证。 |
| StrictModes | 在接受认证前，启用（yes）或禁用（no）对用户主目录和 rhosts 文件中权限的检查。应将其设置为 yes，以保护主目录免受全局可写文件的危害。 |
| RSAAuthentication | 选项用于允许 RSA 认证。 |
| PubkeyAuthentication | 选项用于允许公钥认证；可能的值为 yes 和 no。 |
| AuthorizedKeysFile | 用户公钥存储的目录。默认为 .ssh/authorized_keys，即用户主目录中的 .ssh 文件夹（例如，在 Windows 的 Program Files\OpenSSH 中为 /home/<username>/.ssh/authorized_keys）。 |

在 ssh_config 文件的认证部分下，有一个使用 rhosts 进行 RSH 认证的选项。尽管由于 rhosts 安全性较差而不推荐使用，但以下行涉及 root 配置选项：

```
# rhosts authentication should not be used
#RhostsAuthentication no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes
# For this to work you will also need host keys in
/etc/ssh/ssh_known_hosts
#RhostRSAAuthentication no
# similar for protocol version 2
#HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for
# RhostRSAAuthentication and HostbasedAuthentication
#IgnoreUserKnownHosts no
```

表 2.3 描述了 SSH 服务器可用的 rhost 认证选项。

## 表 2.3 Rhost 配置选项

| 选项 | 描述 |
| :--- | :--- |
| RhostAuthentication | 允许 rhosts 认证 |
| Ignore Rhosts | 忽略（yes）或读取（no）用户主目录中的 rhosts 文件，这些文件存储为 .rhosts 或 .shosts 文件 |
| RhostsRSAAuthentication | 尝试使用 RSA 主机密钥进行 rhosts 认证 |
| HostbasedAuthentication | 在 SSH 版本 2 下启用（yes）或禁用（no）基于主机的认证 |
| IgnoreUserKnownHosts | 忽略（no）或读取（yes）用户主目录中的 known hosts 文件 |

sshd_config 文件的最后一个认证部分涉及更多密码选项，包括 Kerberos 的使用：

```
# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no
```

```
# Change to no to disable s/key passwords
#ChallengeResponseAuthentication yes
```

```
# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
```

```
#AFSTokenPassing no
```

```
# Kerberos TGT Passing only works with the AFS kaserver
#KerberosTgtPassing no
```

表 2.4 描述了 SSH 服务器可用的密码和 Kerberos 认证选项。

## 表 2.4 密码和 Kerberos 选项

| 选项 | 描述 |
| :--- | :--- |
| PasswordAuthentication | 启用（yes）或禁用（no）密码认证。 |
| PermitEmptyPasswords | 允许（yes）或禁止（no）使用空白密码。 |
| ChallengeResponseAuthentication | 启用（yes）或禁用（no）挑战/响应认证。挑战/响应认证发生在服务器向客户端发送挑战时；客户端的响应将决定是否允许认证。 |
| KerberosAuthentication | 启用（yes）或禁用（no）Kerberos 认证，该认证涉及会话票据。 |
| KerberosOrLocalPasswd | 允许（yes）使用 Kerberos 或本地系统密码进行认证。 |
| KerberosTicketCleanup | 启用（yes）或禁用（no）在注销时自动删除 Kerberos 票据的功能。 |
| AFSTokenPassing | 启用（yes）或禁用（no）使用 AFS 令牌进行认证的功能。 |
| KerberosTgtPassing | 启用（yes）或禁用（no）使用 Kerberos 票据授予票据（TGT）进行认证的功能。 |

sshd_config 文件的下一节涉及可用于转发的 X11 选项：

```
X11Forwarding no
X11DisplayOffset 10
X11UseLocalhost yes
```

在 sshd_config 文件的这一部分中，可以启用或禁用 X11 转发。如果启用了 X11 转发，则可以设置偏移量，其中 10 是默认值，并且可以启用使用 localhost 的选项，这是 X11 转发最典型的安装方式。使用 localhost 转发 X11 连接允许所有 X11 流量从本地机器传播。

sshd_config 文件的最后一节涉及可以与该服务配合使用的各种选项，例如打印、横幅信息和子系统：

```
PrintMotd yes
PrintLastLog yes
KeepAlive yes
UseLogin no
UsePrivilegeSeparation yes
PermitUserEnvironment no
Compression yes
```

