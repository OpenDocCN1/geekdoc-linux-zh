
有几个精简版的直接专门设计用于提供此类服务，包括 SmoothWall 和 Mandrake 单网络防火墙，等几个……

James, 邮件

## 回答 | LINUX | 55

## 网络

...调试此类问题的方法是在运行正常的 Linux 机器上使用 `mi-tool`。你可以通过观察集线器上的各种小指示灯来检查集线器。然后你可以使用 `mi-tool` 修改 NIC 配置，将双工设置设置为集线器认为应该是的值。

`www.scyld.com/network/via-rhine.html`，它可以很好地针对 2.2 内核进行编译。你应该完全按照网站上的说明操作，然后你就能编译并安装新模块，在此过程中完全覆盖现有的模块，NIC 应该按预期工作。当然，更新模块并不意味着 YaST 工具能够检测到该 NIC。事实上，它使用的是不同版本的控制器。如果网卡本身工作正常，YaST 不会自动检测网卡本身。

这通常没什么什么大能做的，因为这往往是集线器和 NIC 之间的兼容性问题。对于笔记本电脑，你会有不同的 NIC，所以你应该能够……

## 网络

我曾尝试（简短地）移除 squid 上所有的控制项，并将 `iptables` 简化为简单的 `MASQUERADE`（伪装）指令，但它仍然不起作用。

jmang 通过邮件

在众多的 DNS 服务器中，要确保主机的主名遵循通过 DSL 或电缆租给你的 DHCP 设置。邮件可以通过众多服务器之一提供，发送 `smpd`、`qmail`、`exist` 等，因此这纯粹是一个找到可以确保其安全性的问题；出于安全考虑，不建议在 DNS 服务上运行入站邮件服务器，你可以避免远程邮件服务器的此类攻击。Linux 有 `POP3` 和 `IMAP4` 服务器，你可以在自己的机器上运行它们，使用自己的邮件客户端从箱中收集邮件。

> 看起来 Windows 机器上的 DNS 设置不正确，尽管这将影响所有依赖 DNS 查找的网络服务，如网页浏览，当然还有接收电子邮件。Windows 中的 DNS 服务器应该设置为你的 ISP（服务提供商），除非你的机器上运行了缓存 DNS 服务器。

尝试从 Linux 机器通过 `telnet` 端口 `110` 访问邮件服务器，看看是否可行。

## 老最爱的

我正准备搬进谢菲尔德的一个八人学生宿舍，那里有四台 PC 和一台 Mac，最好的办法是我们直接买一个 ADSL 或电缆调制解调器供大家共享。那么，用我的 Pentium 750 和 SuSE 7.2，可以将我的电脑作为大家共享的互联网连接吗？我还可以将其设置为 Web 服务器和邮件服务器吗，因为假设 ADSL 或电缆调制解调器有静态 IP。

> 你有，或者你不知道在哪里可以找到英国 Linux 免费 ISP 的最新列表？如果有靠谱的，我将使用 SuSE 7.1。James Baldwin

## 学生网络

我需要做什么才能实现这个？

来自论坛。

> 在 Linux 中设置连接是轻而易举的，你在内核中编译了 `ipchains` 真是太棒了。

所有的 ISP 都能支持 Linux，至少是那些使用 PPP 或 SLIP 进行连接的。绝大多数 ISP 将使用 PAT 进行认证，其他如 BTnet 和 Internet Connect。如果你使用基础 0845 ISP，`uklinux.net` 是一个不错的选择，因为它使用 Linux 提供其托管、邮件和 DNS 服务，并且在用户遇到问题时也非常专业。如果你需要从一台机器向另一台机器传输大量文件，`rsync.samba` 是最佳方法。

使用 `FORWARD -MASQUERADE` 并将所有其他机器指向 Linux 盒子作为网关。如果你运行的是 2-4 内核，设置伪装略有不同，但剩余的 `iptables` 过滤系统要安全得多，因此纯粹为了升级内核可能是更优的。

许多 ISP 对使用 Linux 使用他们服务的人并不感兴趣，因为他们缺乏资源来训练员工掌握 Unix 知识。在 ISP 的支持下，存在很多问题，从拨号失败到反向 DNS 问题应有，他们会立即将问题归咎于你自己的配置，因此需要一些时间、耐心和决心才能让他们明白这不是你的问题。当然，像 Demon 这样更传统的 ISP 非常乐意指导 Linux 用户——而其他的 显然不。。

至于 Web 服务器和邮件服务器——`Apache` 是一个完全胜任的 Web 服务器，你可以使用它来学习如何设置你的机器连接到他们的服务，但出现故障时，他们至少会听你解释。

在 Konqueror 的代理配置部分中，你需要以以下格式设置代理：

```
user:password@proxy.domain.com
```

用户名和密码认证框的行为不像你预期的那样，而且它在 KDE21 版本的 Konqueror 中无法正常工作。你可能需要检查 `kde.org` 上的邮件列表，看看是否其他人也有类似的问题，或者检查是否有新的 Konqueror 版本提供了对身份验证代理的正确支持。

来自论坛

设置伪装最快的方法是使用 `ipchains`。只需：

```bash
echo 1 >/proc/sys/net/ipv4/forward
## No No net
```

我正尝试配置我的 SuSE 7.1 网络以与内部网络共享互联网连接。我正在使用 Firewall，我的问题是我不知道 `FW_DEV_WORLD` 的值（我正通过 56k 调制解调器连接）。我尝试了几种选项，但每次启动日志都显示找不到特定模块。值应该是多少？

```
ipchains -A forward -s 10.0.10.24 -j MASQ
```

`'10.0.10.24'` 是你的内部网络使用的子网。你自然需要确保它在引导启动时运行，所以你可能想将其放入 `/etc/rc.d/local`，同时设置内部机器让你的 Linux 盒子成为它们的默认网关。

## Live 与点击

我安装了 SuSE Linux 7.1 Live 版。现在它不是完整版，因为我是从杂志封面附 CD 安装的，我想知道这个版本是否可以设置调制解调器来连接互联网？我只用一个普通的 US 56.6k 调制解调器进行拨号。我尝试了 X-Windows 中的 YaST 调制解调器连接程序，但它不起作用。（此处省略重复的失败描述）

## 网络

与 `'www.domain.com'` 完全不同的站点

## 调制解调器问题

服务器，可以使用 `mod_rewrite` 将外部网络服务器的请求重定向到内部机器，方法类似于：

我有一台 P233MHZ CPU、64MB 内存、ESS1868 声卡、S33 virge 4B、Rockwell HCF 56 PCI 调制解调器（在 COM3 上）；我在 Windows Me 上安装了 WinLinux2000。

Rewrite On

- 1. Linux2000 已检测到我的调制解调器，但它仍然无法工作。在电轴拨号时，我收到“modem is busy”的消息，但当我尝试使用 `minicom` 并将 `tty1` 更改为 `tty2` 来解决这个问题时，我的电脑就死机了。我是 Linux 新手，请尽可能提供详细说明。

RewriteRule(?) http://10.11.2.160/S1 [L]

`mod_rewrite` 是 Apache 的一部分——启用 `-enable-module-rewrite`，或者通过将其编译为 D5 并让 Apache 安装程序运行它，并使用 P 选项代理 `'mod_proxy'`，后者应该以完全相同的方式通过 `-enable-module-proxy` 构建。

- 2. Linux2000 没有检测到我的声卡，所以我强制使用之前使用的相同 IRQ、DMA、IO 和内存范围来设置它，但仍然无法工作。当我尝试使用 `mixer: cd; chmod a+rw=/dev/mixer;` 且操作得当时，什么也没有发生。

## 现在升级！

- 3. 当我尝试用 CD 自带的版本 Linux2000 内核 2.2.13 时，通过 `'patch-link'` 我收到了“can't detect kernel version”的消息。

当我运行 2.2.16 内核时，互联网连接的 KPPP 没有任何问题。这封邮件是使用 2.2.16 内核发送给您的。然而，如果我重启并使用新编译的 2.4.0 内核，我收到了可怕的“PPPD died unexpectedly”消息。我还得到了以下 PPPD 日志：

- 4. 有 Linux 的阿拉伯语版本吗？我发现了 Sun 提供的 StarOffice，它比我的 Office 好用，但它不支持阿拉伯语。有支持它的版本吗？

```
pppd 2.3.1 started by root, 0

Perms of /dev/ttyS0 are; no mesg necessary.

ioctl(FTIOCFLLAGS): Invalid argument

tsetattr: Invalid argument
```

感谢来信，Abbas。首先，尽管没有人特别熟悉 WinLinux，但答案应该适用于任何版本的 Linux，我们并不确切知道 WinLinux 与标准发行版有何不同。你应该检查随你的发行版附的任何文档。

我无法定位或识别出此问题。坦率地说，我不知道从何处开始。
