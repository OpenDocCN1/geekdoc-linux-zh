
```
RhostsAuthentication no
RhostsRSAAuthentication no
RSAAuthentication yes
PasswordAuthentication yes
```

绝不允许 root 远程登录是明智的。超级用户访问应通过使用 `sudo` 实现。为了鼓励这种行为，使用以下选项

```
PermitRootLogin no
```

第一次通过 SSH 连接到新系统时，会提示你接受远程主机的公钥（该公钥通常在 OpenSSH 安装到服务器时，或不久之后生成）。一个真正偏执的用户可能会手动验证它，但我们大多数人都会盲目接受该密钥，然后将其存储在 `~/.ssh/known_hosts` 文件中以供将来使用。除非密钥发生变化，否则 SSH 不会再次提及服务器的密钥。不幸的是，用户对新系统的密钥进行橡皮图章式确认，如果主机密钥实际上是由攻击者系统提供的，你就会容易受到中间人攻击。

一种名为 SSHFP 的 DNS 记录已被开发出来以解决此漏洞。其前提是服务器的密钥存储为 DNS 记录。当客户端连接到未知系统时，SSH 会查找 SSHFP 记录以验证服务器的密钥，而不是要求用户进行验证。

`sshfp` 实用程序，可从 `xelerance.com/software/sshfp` 获取，可通过扫描远程服务器或解析 `known_hosts` 文件中先前接受的密钥来生成 SSHFP DNS 资源记录。（当然，这两种选择都假设密钥的来源是已知的正确。）使用方法非常简单：使用 `-s` 标志从网络扫描生成密钥，或使用 `-k` 扫描 `known_hosts` 文件（默认值）。例如，以下命令为 solaris.booklab.atrust.com 生成一个 BIND 兼容的 SSHFP 记录：

```
solaris$ sshfp solaris.booklab.atrust.com
solaris.booklab.atrust.com. IN SSHFP 1 1 94a26278ee713a37fa78110f1ad9b...
solaris.booklab.atrust.com. IN SSHFP 2 1 7cf72d02e3d3fa947712bc5f6d0e0a3i...
```

将这些记录添加到域的区域文件（注意名称和 `$ORIGIN`），重新加载域，并使用 `dig` 验证密钥：

```
solaris$ dig solaris.booklab.atrust.com. IN SSHFP | grep SSHFP
; <<>> DiG 9.5.1-P2 <<>> solaris.booklab.atrust.com. IN SSHFP
; solaris.booklab.atrust.com. IN SSHFP
solaris.booklab.atrust.com. 38400 IN SSHFP 1 1 94a26278ee713a37fa78110f1ad9b...
solaris.booklab.atrust.com. 38400 IN SSHFP 2 1 7cf72d02e3d3fa947712bc5f6d0e0a3i...
```

`ssh` 默认不会查询 SSHFP 记录。将 `VerifyHostKeyDNS` 选项添加到 `/etc/ssh/ssh_config` 以启用它。与大多数 SSH 客户端选项一样，你也可以在首次访问新系统时在 `ssh` 命令行上通过 `-o "VerifyHostKeyDNS yes"` 传递。

SSH 具有几个对系统管理员有用的辅助功能。其中之一是通过加密的 SSH 通道安全地隧道传输 TCP 连接，从而允许连接到远程站点上的不安全或被防火墙限制的服务。此功能在 SSH 客户端中无处不在，配置也非常简单。展品 A 显示了 SSH 隧道的典型用法，应该有助于阐明其工作原理。

### 展品 A 用于 RDP 的 SSH 隧道

![](img/14d78e3cecac4581d37024baf1e94cca_977_0.png)

在此场景中，远程用户希望建立到企业网络上 Windows 系统的 RDP（远程桌面）连接。防火墙阻止了对该主机或端口 3389 的访问，但由于用户具有 SSH 访问权限，他可以通过 SSH 服务器路由其连接。

要设置此操作，用户使用 `ssh` 登录到远程 SSH 服务器。在 `ssh` 命令行上，他指定一个任意的（但特定的；在这种情况下为 9989）本地端口，`ssh` 应将其通过安全隧道转发到远程 Windows 机器的端口 3389。（对于标准的 OpenSSH 实现，要求此行为的选项只是 `-L localport:remotemachine:remoteport`。）此示例中的所有源端口均标记为随机，因为程序会从其中发起连接的任意端口中选择。

要访问 Windows 机器的桌面，用户然后打开远程桌面客户端（此处为 `rdesktop`）并输入 `localhost:9989` 作为要连接的服务器地址。本地 `ssh` 在端口 9989 上接收连接并通过现有连接将流量隧道传输到远程 `sshd`。反过来，`sshd` 将连接转发到 Windows 主机。

当然，这样的隧道也可能是有意或无意的后门。系统管理员应谨慎使用隧道，并应注意用户对该功能的未经授权的滥用。

近年来，SSH 已成为常规暴力密码攻击的目标。攻击者会以 root、joe 或 admin 等常见用户身份反复尝试认证。攻击的证据可以在日志中看到，表现为数百甚至数千次登录失败。禁用密码认证是对这些攻击的最佳保护措施。目前，攻击者似乎只针对 22 端口，因此将 SSH 服务器迁移到其他端口是一种有效的对策。但历史表明，这种“通过 obscurity 实现安全”的方式很少能长期有效。在系统上运行密码检查可以揭示那些可能被暴力攻击破解的弱密码。

### Stunnel

`Stunnel` 由 Michal Trojnara 创建，是一个开源软件包，可加密任意 TCP 连接，其方式与 SSH 类似。它使用 SSL，即安全套接层，通过加密的端到端隧道将数据传递到和来自未加密的服务。它已知能很好地与 Telnet、IMAP 和 POP 等不安全服务配合使用。

`stunnel` 守护进程同时运行在客户端和服务器系统上。本地 `stunnel` 通常在服务的传统端口上接受连接（例如 SMTP 的 25 端口），并通过 SSL 将其路由到远程主机上的 `stunnel`。远程 `stunnel` 接受连接，对传入数据进行解密，并将其路由到服务器正在监听的远程端口。该系统允许未加密的服务在无需任何软件更改的情况下利用加密提供的保密性和完整性。客户端软件只需配置为在本地系统而非最终提供服务的服务器上查找服务即可。

Telnet 协议是一个很好的例子，因为它由一个监听单个端口的简单守护进程组成。要对 Telnet 链接进行 `stunnel` 化，首先需要创建一个 SSL 证书。`Stunnel` 不依赖 SSL 库，因此任何基于标准的实现都可以使用；我们喜欢 `OpenSSL`。生成证书的方法如下：

```
server$ sudo openssl req -new -x509 -days 365 -nodes -out stunnel.pem
  -keyout stunnel.pem
Generating a 1024 bit RSA private key
++++++
writing new private key to 'stunnel.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank.
For some fields there will be a default value,
If you enter '.', the field will be left blank.
Country Name (2 letter code) [GB]: US
State or Province Name (full name) [Berkshire]: Colorado
Locality Name (eg, city) [Newbury]: Boulder
Organization Name (eg. company) [My Company Ltd] Booklab, Inc.
Organizational Unit Name (eg. section) []:
Common Name (eg. your name or server's hostname) [] server.example.com
Email Address []:
```

该命令创建了一个自签名、无密码短语的证书。虽然不使用密码短语是一种便利（真正的用户不必在每次 `stunnel` 重启时输入密码短语），但它也引入了安全风险。请务必使用强权限保护证书文件。
