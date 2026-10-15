
第一次连接到新系统时，会提示你接受密钥并将其存储在你的 `~/.ssh/known_hosts` 中。偏执的用户可能会验证它，但我们大多数人盲目接受，如果密钥是由攻击者提供的，你将面临中间人攻击。DNS 记录已被开发用来解决这一漏洞。其前提是服务器密钥存储在 DNS 记录中。当客户端连接到未知系统时，SSH 会查找 `SSHFP` 记录来验证服务器密钥，而不是让用户验证。来自 `sshfp` 工具可以通过扫描远程服务器或解析已接受的密钥生成 `SSHFP` 记录。当然，任何一种选择都很简单：使用 `-s` 标志从扫描生成密钥，或使用 `-k` 扫描 `known_hosts`（默认）。例如，以下命令为 `solaris.booklab.astrust` 生成兼容 `BIND` 的 `SSHFP` 记录：

```
solaris$ sshfp solaris.booklab.astrust
```

```
solaris.booklab.astrust.com IN SSHFP 1 1 94a2687ee713a37fa6781101fad9bd.
solaris.booklab.astrust.com IN SSHFP 2 1 7cf7d20e2d3fa35947712c56fd00ea...
```

将这些记录添加到域名区域文件（注意名称和 `ORGIN`），重新加载域名，并使用 `dig` 验证密钥：

```
solaris$ dig solaris.booklab.astrust.com IN SSHFP | grep SSHFP
```

```
;>> dig 9.5.1.2 <<>> solaris.booklab.astrust.com IN SSHFP
; solaris.booklab.astrust.com IN SSHFP
solaris.booklab.astrust.com 38400 IN SSHFP 1 1 94a2687ee713a37fa6781101fad9bd...
solaris.booklab.astrust.com 38400 IN SSHFP 2 1 7cf7d20e2d3fa35947712c56fd00ea...
```

# SSH: 安全外壳

在首次访问新系统时，请在 `ssh` 命令行也加上 `-o "VerifyHostKeyDNS yes"`。

`SSH` 具有几个对系统管理员非常有用的辅助功能。其中之一是能够通过加密的 `SSH` 通道对 `TCP` 连接进行隧道，允许连接到远程站点不安全或被防火墙拦截的服务器。此功能在 `SSH` 客户端中无处不在，且配置简单。示例 A 显示了 `SSH` 隧道的典型用法，并可以解释其工作原理。

## 示例 A 用于 RDP 的 SSH 隧道

![](img/9b33263d3e7e36cd43da7756018c8735_977_0.png)

在这种场景下，远程用户想要对企业企业网络上的一个 Windows 系统建立 RDP（远程桌面）连接。对该主机或端口 `3389` 的访问被防火墙拦截了，但由于用户拥有 `ssh` 访问权限，他可以通过 `ssh` 服务器路由连接。

要建立此设置，用户首先使用 `ssh` 登录到远程 `SSH` 服务器。在 `ssh` 命令行上，他指定了一个任意（但特定的；在本例中为 `9989`）本地端口，`ssh` 将该端口通过安全隧道转发到远程 Windows 机器的端口 `3389`。（对于标准的 `OpenSSH` 实现，请求此行为的选项是 `-L localport:remotehost:remoteport`。）此示例中的所有源端口都标记为随机，因为你选择了一个任意端口来发起连接。

要访问 Windows 机器的桌面，用户随后打开远程桌面客户端（此处为 `rdesktop`），并输入 `localhost:9989` 作为要连接的服务器地址。本地 `ssh` 在端口 `9989` 上接收连接，并通过现有连接将流量隧道化到远程 `ssh`。反之，`ssh` 将连接转发到 Windows 主机。

当然，这类隧道也可能成为有意或无意的后门。系统管理员应谨慎使用隧道，并留心用户对该功能进行任何未经授权的滥用行为。

# 第 22 章 安全

近年来，`SSH` 已成为定期的暴力破解密码攻击的目标。攻击者以普通用户（如 `root`、`joe` 或 `admin`）的身份反复进行身份验证尝试。攻击的证据可以在日志中看到，表现为数百或数千次失败登录。禁用密码认证似乎是防御此类攻击的最佳保护措施。目前，攻击者似乎只关注端口 `22`，因此将你的 `SSH` 服务器移动到另一个端口是一个有效的应对措施。但历史表明，这种“通过隐蔽实现安全”的方法很少能长期有效。在你的系统上运行密码检查可以削弱可能被暴力破解的薄弱密码。

## Stunnel

`Stunnel` 由 `Michal Trojnara` 创建，是一个开源包，可以对任意 `TCP` 连接进行加密，方式类似于 `SSH`。它使用 `SSL`（安全套接层）创建端到端隧道，通过隧道将数据传递给加密服务。它众名于与 `Telnet`、`IMAP` 和 `POP` 等不安全服务配合良好。

`stunnel` 守护进程同时运行在客户端和服务器系统上。本地 `stunnel` 通常在服务的传统端口（例如 `SMTP` 的端口 `25`）上接收连接，并通过 `SSL` 将它们路由到远程主机上的 `stunnel`。远程 `stunnel` 接收连接、解密数据并将其路由到服务器监听的远程端口。该系统允许未加密的服务在无需更改任何软件的情况下，利用机密性和完整性。客户端软件只需要配置为在本地系统查找服务，而不是在最终提供服务的服务器上查找。

`Telnet` 协议是一个很好的例子，因为它由一个在单端口监听的简单守护进程组成。要对 `Telnet` 链路进行加密，你需要创建一个 `SSL` 证书。`Stunnel` 不依赖于库，因此任何基于标准的实现都可以；我们使用 `OpenSSL`。生成：

```
server$ openssl req -new -x509 -days 365 -nodes -out stunnel.pem -keyout stunnel.pem
```

```
Generating a 1024 bit RSA key
++++++++++++
```

```
writing new private key to 'stunnel.pem'
```

你将被要求输入将整合到证书请求的信息：
你即将输入的内容被称为名称（Distinguished Name，简称 `DN`）。
有很多字段可以留空。
某些字段会有默认值，
如果你输入 ''，该字段将留空。
国家名称（两个字母代码） [GB]:US
州或省份名称（全称） [Berkshire] Colorado
地区名称（例如，城市） [Newbury] Boulder
组织名称（例如，公司） [My Company Ltd]:Booklab, Inc.
组织单位名称（例如，部门） []
通用名称（例如，你的名称或服务器主机名） [] server.example.com
电子邮件地址 []:

此命令创建了一个自签名、无密码保护的证书。虽然不使用密码保护是一种便利（每当 `stunnel` 重启时都不需要人类现场输入密码），但它也引入了安全风险。请务必使用强权限保护证书文件。

接下来，为服务器和客户端 `stunnel` 定义配置。标准配置文件路径为 `/etc/stunnel/stunnel.conf`，但如果你想运行多个隧道，可以创建多个配置。

```
cert = /etc/stunnel/stunnel.pem
chroot = /var/run/stunnel/
pid = /stunnel.pid
setuid = nobody
setgid = nobody
debug = 7
output = /var/log/stunnel.log
client = no
```

```
[telnets]
accept = 23
connect = server.example.com:992
```

几个指令相对于服务器配置是反的。`client = yes` 告诉程序发起连接而不是接收连接。本地 `stunnel` 监听 `992` 并连接到 `23`。`connect` 指令中的主机名应与我们在创建证书时指定的项匹配。

客户端和服务器 `stunnel` 都可以通过命令行参数启动。如果你使用 `netstat -an` 进行检查，你应该能看到服务器在端口 `992` 上等待，而客户端在 `23` 上等待。

要访问隧道，用户只需 `telnet` 本地主机：

```
client$ telnet 23
Trying 127.0.0.1...
Connected to localhost (127.0.0.1)
Escape character is '^'.
Red Hat Enterprise Linux release 4 (Nahant Update 2)
Kernel 2.6.9-5.EL on i686
```
