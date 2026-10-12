
socks4 127.0.0.1 1080

```
列表 960 - 配置 proxychains
```

^759 (OpenBSD Foundation, 2019), https://man.openbsd.org/ssh#R_S

此时，我们应该拥有一个稳定的隧道来访问 `10.5.5.0/24` 网络，并且可以继续下一个目标，即我们在 Zora 上挂载的共享中发现的 Poultry。

## 24.6 针对 Poultry

在我们继续之前，回顾一下我们知道和不知道的内容会有帮助。我们知道 Ajla 通过数据库服务器 Zora 连接到内部网络。我们还刚刚了解到，在内部网络中，从另一台名为 Poultry 的计算机挂载了一个共享到 Zora。我们怀疑 Poultry 运行的是 Windows，但我们还不确定。我们还发现了沙箱域内一个用户的凭据。这意味着某处应该存在一个域控制器。

![](img/ec25e59d75726b7041242a56d3376832_793_0.png)

在尝试使用发现的凭据之前，我们将首先枚举 Poultry，以确定我们的下一步行动应该是什么。

#### 24.6.1 枚举

我们假设 Poultry 运行的是 Windows。通过进行一些网络枚举，例如使用 `Nmap` 扫描，我们可以更加确信这一点。如果 `Nmap` 发现了任何应用程序，我们也可以对其进行枚举。

## 24.6.1.1 网络枚举

为了运行 `Nmap` 扫描，我们需要使用 `ProxyChains`。通过 `ProxyChains` 进行网络扫描速度会比较慢，因此我们将仅扫描前 20 个端口，如有必要再扩大扫描范围。

> 你可以通过修改 `/etc/proxychains.conf` 中的 `tcp_read_time_out` 和 `tcp_connect_time_out` 值来调整超时时间，从而加快通过 `proxychains` 进行网络扫描的速度。但是，不要将这些值设置得过低，否则你会得到错误的结果。

要通过 `ProxyChains` 运行 `Nmap`，我们需要在想要运行的 `nmap` 命令前加上 `proxychains` 前缀。我们将使用 `--top-ports=20` 标志仅扫描前 20 个端口，并使用 `-sT` 标志进行连接扫描。SOCKS 代理需要建立 TCP 连接，因此半开或 SYN 扫描不能与 `ProxyChains` 一起使用。[740] 由于 SOCKS 代理需要 TCP 连接，ICMP 数据包也无法通过，因此我们必须使用 `-Pn` 标志禁用 ping。

```bash
kali@kali:~$ proxychains nmap --top-ports=20 -sT -Pn 10.5.5.20

ProxyChains-3.1 (http://proxychains.sf.net)

Starting Nmap 7.80 ( https://nmap.org ) at 2019-12-10 20:52 MST

S-chain|<-->127.0.0.1:1080<->><>->10.5.5.20:110<---timeout

S-chain|<-->127.0.0.1:1080<->><>->10.5.5.20:139<--->OK

S-chain|<-->127.0.0.1:1080<->><>->10.5.5.20:3389<->->OK

S-chain|<-->127.0.0.1:1080<->><>->10.5.5.20:443<->->OK

S-chain|<-->127.0.0.1:1080<->><>->10.5.5.20:143<->->OK

S-chain|<-->127.0.0.1:1080<->><>->10.5.5.20:8080<---timeout

...

Nmap scan report for 10.5.5.20

Host is up (1.4s latency).

PORT     STATE SERVICE

21/tcp   closed ftp

22/tcp   closed ssh

23/tcp   closed telnet

25/tcp   closed smtp

53/tcp   closed domain

80/tcp   closed http

110/tcp  closed pop3

111/tcp  closed rpcbind

135/tcp  open  msrpc

139/tcp  open  netbios-ssn

143/tcp  closed imap

443/tcp  closed https

445/tcp  open  microsoft-ds

993/tcp  closed  imaps

995/tcp  closed  pop3s

1723/tcp closed pptp

3306/tcp closed mysql

3389/tcp open ms-wbt-server

5900/tcp closed vnc

8080/tcp closed http-proxy

Nmap done: 1 IP address (1 host up) scanned in 25.48 seconds
```

[740] (Wikipedia, 2019), https://en.wikipedia.org/wiki/SOCKS#Comparison_to_HTTP_proxying

> 清单 961 - 使用 nmap 扫描 Poultry

在清单 961 中，`Nmap` 发现端口 `135`、`139`、`445` 和 `3389` 处于开放状态。然而，端口 `53` 是关闭的，而在域控制器上该端口通常是开放的。这很可能不是我们要找的域控制器，但其他端口仍然表明这是一个 Windows 操作系统。前 20 个端口没有显示任何正在运行的 HTTP 应用程序，因此让我们尝试通过 RDP 登录并“利用”这台 Windows 机器，使用我们发现的凭据。

## 24.6.2 利用（或者仅仅是登录）

现在我们已经更加确信该主机上运行的是 Windows，并且发现 RDP 处于开放状态，我们将使用 `xfreerdp` 进行连接。就像对 `Nmap` 所做的那样，我们需要在 `xfreerdp` 前加上 `proxychains` 命令前缀。我们分别使用 `/d:sandbox` 和 `/u:alex` 标志提供域名和用户名。为了重定向剪贴板，我们将使用 `+clipboard` 标志，这将允许我们向 Poultry 复制和粘贴内容。最后，我们还将使用 `/v:10.5.5.20` 标志提供主机地址。

```bash
kali@kali:~$ proxychains xfreerdp /d:sandbox /u:alex /v:10.5.5.20 +clipboard

ProxyChains-3.1 (http://proxychains.sf.net)

...

Certificate details for 10.5.5.20:3389 (RDP-Server):

  Common Name: POULTRY.sandbox.local

  Subject:    CN = POULTRY.sandbox.local

  Issuer:     CN = POULTRY.sandbox.local

  Thumbprint: 10:9c:cc:64:c6:ad:9a:bb:78:4d:b3:04:b4:fb:77:0c:1a:c6:d2:b0

The above X.509 certificate could not be verified, possibly because you do not have

the CA certificate in your certificate store, or the certificate has expired.

Please look at the OpenSSL documentation on how to add a private CA to the store.

Do you trust the above certificate? (Y/T/N) Y

Password:
```
