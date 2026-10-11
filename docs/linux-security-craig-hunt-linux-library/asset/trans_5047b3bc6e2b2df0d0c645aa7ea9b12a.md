

以下是一个完整的 `sshd_config` 文件示例，我通常在 Linux 服务器上使用该文件：

```
[ramon]$ more /etc/sshd_config
# This is ssh server systemwide configuration file.

IgnoreRhosts yes

RhostsAuthentication no

StrictModes yes

AllowTcpForwarding no

Protocol 2

PermitRootLogin no

RSAAuthentication yes

PasswordAuthentication no
```

请注意，前三行在之前已经讨论过。此外，我禁用了 TCP 连接转发，因为这使得追踪用户通过 SSH 隧道传输连接变得困难，可能导致安全漏洞。我还将使用的协议版本限制为 v.2，即使我的 sshd 守护进程也编译为接受 v.1；这是因为在 v.1 中发现了多个漏洞。然后，我进一步限制通过 SSH 进行的 root 登录，这是为防止攻击者获取远程 root 访问权限而采取的额外措施；我随时可以普通用户身份登录并使用 `sudo`。最后，在上述示例的最后两行中，通过禁用密码认证，我将认证方法定义为仅基于 RSA 密钥。RSA 认证易于管理，且完全不需要用户暴露其密码。

除了服务器配置文件外，SSH 还包含一个客户端配置文件（/etc/ssh/ssh_config），用于设置希望使用 ssh 应用程序的客户端的默认值。表 12.2 列出了 /etc/ssh/ssh_config 文件中最有用的指令。

### 表 12.2 /etc/ssh/ssh_config 指令

| 选项 | 含义 | 默认值 |
| :--- | :--- | :--- |
| BatchMode | 在无人值守脚本中禁用 SSH 的用户名/密码提示。 | N/A |
| Ciphers | 指定要使用的加密算法（SSH v.2）。 | 3des-cbc, blowfish-cbc, arcfour, cast128-cbc |
| Compression | 指定是否使用压缩。 | N/A |
| CompressionLevel | 要使用的压缩级别（1=最快 至 9=最好）。 | 6 |
| DSAAuthentication | 指定是否应尝试 DSA 认证（SSH v.2）。 | N/A |
| FallBackToRsh | 指定如果 ssh 不成功，连接是否应回退到普通的 rsh。 | N/A |
| KerberosAuthentication | 指定是否应尝试 Kerberos 认证。 | N/A |
| PasswordAuthentication | 指定是否应尝试密码认证。 | N/A |
| Protocol | 指定 SSH 客户端是否应尝试 SSH 协议的 v.1 和/或 v.2。 | 1,2 |
| RhostsAuthentication | 指定是否应尝试 .rhosts 认证。 | N/A |
| RSAAuthentication | 指定是否应尝试 RSA 认证。 | N/A |
| SKeyAuthentication | 指定是否应尝试 S/Key 认证。 | N/A |
| StrictHostKeyChecking | 绝不自动将远程主机密钥添加到 $HOME/.ssh/known_hosts。依赖其存在以确保连接成功。 | N/A |

在这些客户端选项中，您应始终指定以下设置：

```
RhostsAuthentication no
FallBackToRsh no
StrictHostKeyChecking yes
```

前两项设置禁用了 rhosts 认证和不安全的 rsh 命令的使用。第三项设置强制您的客户端预先知道远程主机的公钥。这使得入侵者无法实施中间人攻击，冒充您试图连接的服务器。缺点是，您必须收集您通常连接的所有服务器的所有主机密钥，并将它们存储在你的 $HOME/.ssh/known_hosts 文件中。

## 关于 RSA 认证

截至 2000 年 9 月，RSA Security, Inc. 不再持有 RSA 公钥认证算法的专利。这意味着您可以在客户端机器上创建一对公钥/私钥 RSA 密钥，并将公钥分发给您希望安全认证的任何 Linux 服务器的管理员。

首先运行 `ssh-keygen` 以在主目录中生成密钥对。此命令作为普通用户运行。您的每个用户都应运行 `ssh-keygen` 以创建他们自己的密钥集。以下是 `ssh-keygen` 命令的一个示例：

```
[ramon]$ ssh-keygen
Generating RSA key: Key generation complete.
Enter file in which to save the key (/home/ramon/.ssh/identity):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ramon/.ssh/identity.
Your public key has been saved in /home/ramon/.ssh/identity.pub.
The key fingerprint is:
b7:35:6b:f9:4a:7b:40:f4:70:30:d2:4a:98:5c:25:00
ramon@redhat.example.com
```

`ssh-keygen` 命令生成两个身份文件，如清单 12.4 所示。

### 清单 12.4 由 `ssh-keygen` 命令创建的身份文件

```
[ramon]$ cd $HOME/.ssh
[ramon]$ ls -l identity*
-rw-------  1 ramon   users    540 Feb  7 17:01 identity
-rw-r--r--  1 ramon   users    344 Feb  7 17:01 identity.pub
[ramon]$ more identity.pub
1024  35
2390480234952851043183643051819290088224038895772645807372356589735
37083178043675381748121970375946993871941884887547481017847954020737
163386241481285585013471308852361826616046589881194193949102793923
5137895964935103899640241917125040533909054580817125603441182010953
71662846509718109183189   ramon@redhat.example.com
```

这两个文件的用途如下：

- $HOME/.ssh/identity 文件包含您的 RSA 密钥的私钥部分。在任何情况下，您都不应与他人共享此文件。
- $HOME/.ssh/identity.pub 是您应提供给需要访问的远程 SSH 系统管理员的文件。当远程 SSH 服务器允许 RSA 认证（使用表 12.1 中的 `RSAAuthentication` 指令）时，您登录系统时无需输入密码。

在远程系统上，只需将 identity.pub 的完整内容粘贴到相应用户的 $HOME/.ssh/authorized_keys 文件中。例如，假设您希望使用 RSA 认证从 caldera.example.com 和 redhat.example.com 以 ramon 身份登录到 suse.example.com。只需获取 caldera.example.com 和 redhat.example.com 上 identity.pub 文件的内容，并将它们插入到 suse.example.com 的 .ssh/authorized_keys 中，如下所示：

```
[ramon]$ more .ssh/authorized_keys
1024  35  26176632424407803465195431089535298792515594463718945638870
09604555778782718989579135711356899802512356584624119858367310429373
619374038515642525995896839408208733045515172702470073209042978615
060322444446644529326292l876776658946288815292526320347023048092384
080921427992348792734979234701 ramon@caldera.example.com

1024 35 239048023495285104318364350181929090082244038957726458073723
565897353708317804367538174812197037594693987194l8848857474810l78479
54020737l6338624148l285585501347l3088523618l26l6l60458988l194l99349l
027939235137895964935l038996402419l71l520040453399005458087l2560344ll
802109537l6628465097l8l09183l89 ramon@redhat.example.com
```

请注意，您在远程机器上使用了两个不同的用户名（caldera.example.com 上的 ramon 和 redhat.example.com 上的 ramon）。只要您将这些密钥正确输入到 `suse.example.com` 的 .ssh/authorized_keys 文件中，这样完全没有问题。

## 使用 OpenSSH

第一次启动 sshd 守护进程时，您会看到以下内容：

```
[ramon]$ sudo /etc/rc.d/init.d/sshd start
Generating RSA keys:  Key generation complete.
Your identification has been saved in /etc/ssh/ssh_host_key.
Your public key has been saved in /etc/ssh/ssh_host_key.pub.
The key fingerprint is:
96:26:e0:4b:4e:9b:28:6d:e7:b9:92:65:lb:7a:7c:09 root@redhat.example.com
Generating DSA parameter and key.
Your identification has been saved in /etc/ssh/ssh_host_dsa_key.
Your public key has been saved in /etc/ssh/ssh_host_dsa_key.pub.
The key fingerprint is:
09:92:6c:84:28:54:8b:45:7d:a7:d6:76:80:ld:2l:b2 root@redhat.example.com
Starting sshd: [ OK ]
```

如前所述，守护进程知道这是它第一次运行，并创建了两组密钥，即 RSA 和 DSA 密钥，以兼容旧版本。从现在开始，sshd 守护进程将使用这些密钥向远程主机进行身份验证，类似于在用户级别使用 RSA 进行身份验证的方式。

