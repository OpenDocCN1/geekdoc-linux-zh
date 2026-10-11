
子系统 sftp /usr/lib/openssh/sftp-server
PasswordAuthentication yes

表 9.2 描述了可在 sshd_config 文件中配置的一些常用选项：

| **SSH 选项** | **描述** |
|---|---|
| AllowTcpForwarding | 指定是否允许 TCP 转发。选项为 *yes*（默认）、*no* 和 *local*。 |
| AllowUsers | 以空格分隔的允许的用户名列表。 |
| AuthenticationMethods | 指定允许的认证方法。 |
| Ciphers | 指定允许的加密算法。多个加密算法必须用逗号分隔。 |
| DenyGroups | 以空格分隔的拒绝的组名列表。 |
| DenyUsers | 以空格分隔的拒绝的用户名列表。 |
| DisableForwarding | 禁用所有转发功能，包括 X11、ssh-agent(1)、TCP 和 StreamLocal。 |
| ListenAddress | 指定应监听的本地地址。 |
| PasswordAuthentication | 指定是否允许密码认证。默认为 *yes*。 |
| PermitRootLogin | 指定 root 是否允许登录。参数必须是 *yes*、*prohibit-password*、*forced-commands-only* 或 *no*。默认为 prohibit-password。 |
| Port | 指定监听的端口号。默认为 22。 |
| Subsystem | 配置外部子系统（例如，*文件传输守护进程*）。 |
| UseDNS | 指定是否应将客户端 IP 解析为主机名。 |
| UsePAM | 启用 *可插拔认证模块* 接口。 |
| X11Forwarding | 指定是否允许 X11 转发。参数必须是 *yes* 或 *no*。默认为 *no*。 |

*表 9.2：SSH 客户端选项及描述*

在安装 SSH 服务器期间，会生成私钥和公钥，它们位于 /etc/ssh/ 目录中。这些密钥使用不同的加密算法。文件名的格式为 ssh_host_ALGORITHM_key 和 ssh_host_ALGORITHM_key.pub：

- **ECDSA：** 代表 **椭圆曲线数字签名算法**，使用椭圆曲线加密。
- **Ed25519：** EDSA 代表 **爱德华兹曲线数字签名算法**，Ed25519 是使用 SHA-512 和 Curve25519 的签名方案。
- **RSA：** 代表 **Rivest-Shamir-Adleman**，是 SSH 中广泛使用的私钥/公钥算法。

系统中客户端的全局配置文件位于 /etc/ssh/ssh_config。然而，通常用户会在 ~/.ssh/config 文件中定义自己的客户端配置。以下常用选项可用，如表 9.3 所示：

| 选项 | 描述 |
|---|---|
| Host | 将选项限制于该主机。 |
| Match | 将选项限制于匹配该模式的参数。 |
| Ciphers | 指定允许的加密算法及其优先级顺序。 |
| ForwardAgent | 指定与认证代理的连接。 |
| Hostname | 指定要登录的实际主机名。 |
| IdentityFile | 指定读取用户 ECDSA、Ed25519 或 RSA 认证身份的文件。 |
| Port | 指定连接远程主机所使用的端口号。 |
| ProxyCommand | 指定用于连接服务器的命令。 |
| ProxyJump | 指定一个或多个跳板代理，形式为 [user@][host:port] 或 ssh URL。 |
| User | 指定登录所使用的用户。 |

*表 9.3：SSH 选项及描述*

SSH 服务器可作为堡垒主机或跳板机，用于连接无法从外部访问的内部服务器。ProxyCommand 和 ProxyJump 参数即用于此目的。客户端配置示例如下所示：

```
Host 192.168.122.43
  User agonzalez
  IdentityFile ~/.ssh/id_rsa
  Port 22
Match User cloud-user
  IdentityFile ~/.ssh/id_rsa_cloud_user
  Port 2222
Host *
  User admin
  IdentityFile ~/.ssh/id_rsa_admin
  Port 22
```

使用 SSH 进行通信需要目标主机、端口（默认为 22）以及用于连接的用户名（如果未定义，将使用运行该命令的用户名）。如果 SSH 服务允许密码认证，则当未使用 SSH 私钥/公钥时，可以通过指定用户密码来登录。这一概念将在本章后续部分介绍。

首次连接到远程目标时，SSH 客户端会询问用户 SSH 服务器指纹是否符合预期，以及用户是否希望继续连接。**图 9.17** 显示了所示消息的一个示例：

```
[root@rhel ~]# ssh 192.168.122.43
The authenticity of host '192.168.122.43 (192.168.122.43)' can't be established.
ED25519 key fingerprint is SHA256:y4Jc7BdqKxwZvVxFrsj59/YkdiJ23F/tneG9pQzILYWa.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

# *图 9.17：命令 ssh 的输出示例*

如果对此提示的回答是 yes，则**指纹**将被添加到 ~/.ssh/known_hosts 文件中，并在后续连接中进行检查。如果指纹相同，则不会有任何提示。文件 **known_hosts** 的内容将包含 IP 地址和指纹列表；以下示例显示了上述指纹关系：

```
192.168.122.43 ssh-ed25519
    AAAAC3NzaC1lZDI1NTE5AAAAIC1YjZSS/Ek7pK6AQeC0I/kjHgzmJJkQxDNmEcTdNrN5m
```

如果对此提示的回答不是 yes，则连接将被关闭。客户端 ssh 允许使用 -v 选项来增加详细程度。可以指定多次（最多 3 次）以提高调试级别。以下摘录显示了一个连接示例，其中公钥未被接受，但服务器允许使用密码进行连接：

```
[root@rhel ~]# ssh -v 192.168.122.43
OpenSSH_8.7p1, OpenSSL 3.0.1 14 Dec 2021
debug1: Reading configuration data /root/.ssh/config
debug1: /root/.ssh/config line 1: Applying options for 192.168.122.43
debug1: Reading configuration data /etc/ssh/ssh_config
(… Omitted …)
debug1: Connecting to 192.168.122.43 [192.168.122.43] port 22.
debug1: Connection established.
debug1: identity file /root/.ssh/id_rsa type 0
debug1: identity file /root/.ssh/id_rsa-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_8.7
debug1: Remote protocol version 2.0, remote software version OpenSSH_8.9p1 Ubuntu-3
```

```
(... omitted ...)
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ssh-ed25519
(... omitted ...)
debug1: Server host key: ssh-ed25519
SHA256:y4Jc7BDqKxwzVxFRsJ59/YkdJ23F/tneG9pQzLLYW4
(... omitted ...)
debug1: Host '192.168.122.43' is known and matches the ED25519 host key.
debug1: Found key in /root/.ssh/known_hosts:1
(... omitted ...)
debug1: Authentications that can continue: publickey,password
debug1: Next authentication method: publickey
debug1: Offering public key: /root/.ssh/id_rsa RSA
SHA256:ewmC9n\LMXVmqxFkROaYf/IVmicjw3nsJ2PxBi24qi+TE explicit
debug1: Authentications that can continue: publickey,password
debug1: Next authentication method: password
gonzalez@192.168.122.43's password:
```

如果认证成功，远程系统的 *shell 控制台* 将会出现，以便输入将在远程节点上执行的命令。可以将命令作为参数传递给 *ssh* 命令，从而使其在远程节点上执行，并在执行后注销。图 9.18 展示了如何连接到系统并仅执行一条命令，而不是打开会话：

```
[root@rhel ~]# ssh 192.168.122.43 uname -a
gonzalez@192.168.122.43's password:
Linux ubuntu 5.15.0-47-generic #51-Ubuntu SMP Thu Aug 11 07:51:15 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
```

![](img/863afa537de4eed7deb11978bfbfa90e_296_0.png)

可以使用 *-i* 选项和包含私钥的文件来指定另一个 SSH 私钥。私钥的权限需要设置为 0600 或 0400 以进行保护。如果权限*过于开放*，将会显示以下消息，并且该密钥将不被使用：

```
WARNING: UNPROTECTED PRIVATE KEY FILE!
Permissions 0640 for '/root/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/root/.ssh/id_rsa": bad permissions
```
