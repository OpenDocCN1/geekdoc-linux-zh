
# 插件架构：易于为特定任务添加插件

代码带有一个用于 `IP`、`TCP` 和 `UDP` 校验和的插件以及一个占位插件。通过插件机制，Netude 为编写 `tcpdump` 追踪文件提供了良好的便利。来自 Debian 3.0r0 APT http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## netenv

为不同的网络环境配置你的系统。`netenv` 创建一个包含反映当前环境赋值的文件。它对于笔记本电脑特别有用，因为它被 Debian `debcm-` 包中的 `PCMCIA` 设置以及此包中示例的 `slip` 设置脚本使用（如果配置了）。你也可以使用 `netenv` 配置你的窗口管理器或打印环境。注意，你必须指定内核参数或在硬启动时选择环境。引导启动过程会停止，直到你输入内容。来自 Debian 3.0r0 APT

http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## nethack

开销地下城爬行游戏（虚拟包）`Nethack` 是一款奇妙愚蠢但又上瘾的地下与城风格冒险游戏。你扮演战斗者、法师、巫师或其他许多类别的角色，一路向下战斗为你的神取回 `Yendor` 护符（试着倒过来读这个词！）。在途中，你可能会遇到量子机制二，也许一个微型空间舰队，或者——如果你真的非常幸运的话——`Traul` 的贪婪巨兽。此包仅仅是一个依赖于 `net-common` 和 `net-x11` 以方便升级的虚拟包。你可以安全地从系统中删除它。Debian 3.0r0 APT

## Netiquette

网络礼仪。为了避免违反网络礼仪，请确保你调查了新闻组的任何常见问题（FAQs）或新用户，并且不要电子邮件。来自远程教育与互联网术语表

http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## netkit-ftp

来自 Watham 的互联网传输协议

http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## netkit-inetd

互联网超级服务器。`inetd` 服务器是一个专门用于管理传入连接的网络守护程序。它的配置文件告诉它在接收到传入连接时应该运行哪些程序。任何服务端口都可以配置为使用 `tcp` 或 `udp` 协议。来自 Debian 3.0r0 APT http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## netkit-ping

`uint` 工具 `ping` 通过向主机发送 `ICMP` `ECHO_REQUEST` 数据包，以测试该主机是否可以通过网络触达。来自 Debian 3.0r0 APT

http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## netlets-applet

`GNOME` 网络小组件。`NetLeds` 是一个 `GNOME` 应用，用于显示网络设备的 `LED`。它显示接收（`RX`）、发送（`TX`）、冲突和错误。来自 Debian 3.0r0 APT

## netmask

位掩码，类似于子网掩码，用于确定 `IP` 地址的网络部分。来自 Debian 3.0r0 APT

http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

# Linux 词典

此软件包使用 `SVM` 协议测量网络性能。`SVM` 是一种在并行处理中频繁使用的并行虚拟机接口，并将 `TCP` 作为其底层传输层。在 Debian 系统上，通过其独立的 `svm` 软件包提供 `SVM` 支持。来自 Debian 3.0r0 http://www.tld.org/LDP/Linux-Dictionary/index.html

# netpipe-tcp

使用 `TCP` 协议的网络性能测量工具 `NetPipe` 是一种协议无关的工具，它封装了 `netpipe` 的优点，并视觉化地表示了各种条件下的网络性能。通过从网络的端到端视角，`NetPipe` 清晰地显示了与不同协议相关的开销。`NetPipe` 解答以下问题：大小为 `k` 的给定数据块将如何到达目的地？哪种网络和协议将传输大小为 `k` 的块？给定网络的有效吞吐量和饱和水平是多少？是否存在一个大小为 `k` 使得吞吐量最大化？多少通信是由于网络通信协议层引起的？小型（< 1 字节）控制消息将多快到达，哪种网络和协议最适合此目的？此软件包使用原始 `TCP` 测量网络性能。来自 Debian 3.0r0 http://www.tld.org/LDP/Linux-Dictionary/index.html

# netplan

`'plan'` 的网络服务器是 `X/it` 的调度器和规划器。`Netplan` 使用 `IP` 服务器扩展了 `plan` 的多播能力。警告：`netplan` 在其版本中提供的最佳身份验证级别是身份。这种是弱的，因此请务必管理指标并仔细调整配置。来自 Debian 3.0r0 http://www.tld.org/LDP/Linux-Dictionary/index.html

# netris

`T*tris` 的免费网络版本 `Netris` 是俄罗斯方块（Tetris）的免费变体。目前单人模式很糟糕，因为它永远变快，而且没有评分。这将在某个时候得到修正。两个玩家可以相互对战。如果你屏幕底部有三行或两行未空行。如果你用一个碎片玩了四行，你的对手将获得四行未空行。此版本至少支持机器人。你可以在文档中找到协议描述，并在示例中找到样例。来自 Debian 3.0r0 APT http://www.tld.org/LDP/Linux-Dictionary/index.html

# netsaint

一种主机/服务的监控和管理系统。`NetSaint` 是一个主机/服务的监控和管理系统。它具有以下功能：

- 网络服务的监控（通过 `TCP` 端口、`SMTP`、`HTTP`、`NNTP`、`PING` 等）

- 插件允许在问题发生和解决时进行用户服务检查或发送通知（通过电子邮件、传真机或用户定义方法）

- 能够定义在服务或主机事件期间运行的事件（用于主动解决解决方案）

- Web 输出（当前状态、通知、历史日志、日志文件）。`NetSaint` 用 `C` 语言编写，易于理解和修改以适应自己的需求。来自 Debian 3.0r APT http://www.tld.org/LDP/Linux-Dictionary/index.html

# Netscape

一种 `WWW` 浏览器及其名称。`Netscape` (tm) 最初基于在国家超级计算机应用中心 (`NCSA`) 开发的 `Mosaic` 浏览器。来自 Matisse http://www.tld.org/LDP/Linux-Dictionary/index.html

# netscape

流行的万维网浏览器（基础支持）`Netscape`（发音为 "`Mozilla`"）是一个具有许多功能的图形化万维网浏览器。它支持 `HTML` 的高级功能以及来自 Sun Microsystems 的 "`Java`" 等新技术。如果你希望对 `netscape` 直接不支持的图像类型获得内联支持，则需要安装 "`ImageMagick`" 软件包。来自 Debian 3.0r0 http://www.tld.org/LDP/Linux-Dictionary/index.html

# Netscape(tm)

用于 `X–Windows`、`MS–Windows` 和 `Macintosh` 的商业 `GUI` 万维网浏览器，由 `Netscape Communications` 提供。来自 KADOWKEV http://www.ldp.org/LDP/Linux–Dictionary/html/index.html

网络数据包修改编辑器 `NetSED` 是一个小巧实用的实用程序，用于实时修改转发到你网络的数据包内容。它对于网络黑客在以下应用中非常有用：

- 黑客协议审计——每当有两个或多个私有设备通过无定向协议通信时（出于安全目的），

- 模糊类算法、完整性测试——每当你更改转换时（你将能够测试应用程序是否真的安全），当你想要测试应用程序的稳定性以及它如何确保数据完整性时，

- 其他常见应用——感受他人、内容过滤等等等——随你心意。完美适配 `ngrep`、`netcat` 和 `tcpdump` 工具。来自 Debian 3.0r APT http://www.ldp.org/LDP/Linux-Dictionary/html/index.html

# netsed

自动选择最优版本。这是 `nestled`，一种针对“`ping`”的超快速智能并行化二分查找工具。你给它一个（可能很长的）服务器列表，它会自动选择最优质/最近的一个。它非常适合寻找最快的 `ftp.ldp.org` 镜像、最不懒的 `IRC` 服务器或 `squid` 后的代理服务器。此版本还包含了 `netselect-apt`，它可以根据镜像列表自动创建 `apt.sources.file`。来自 Debian 3.0 APT http://www.ldp.org/LDP/Linux-Dictionary/index.html

# netselect
