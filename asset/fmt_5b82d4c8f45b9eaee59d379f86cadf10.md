
- d. Boot your computer from the Linux installation CD. When prompted, enter the IP address of the network server with your Linux installation files.

答案 b 正确。`rawrite`程序是一个基于 MS-DOS 的程序，用于将磁盘映像复制到软盘。这些映像允许你启动 Linux 系统并安装适当的网络文件。使用这些启动磁盘后，你应该能够连接到适当的网络服务器。通过电话调制解调器安装 Linux 并不可行；因此，答案 a 不正确。基于 Linux CD-ROM 的安装程序通常不允许你连接到网络下载安装文件；它们已在 CD-ROM 上提供。因此，答案 c 和 d 不正确。

### 问题 4

以下哪项陈述是 Linux 发行版的特征？

- a. Every Linux distribution can be installed in an MS-DOS partition.
- b. Some Linux distributions use Red Hat kernels.
- c. Some Linux distributions are based on other distributions.
- d. Every Linux distribution can be installed in a Linux swap partition.

答案 c 正确。根据 GPL 的规定，任何人都可以重新打包他人的 GNU/Linux 发行版。因为 Linux 通常不能安装在 MS-DOS 分区中，所以答案 a 不正确。没有专属于 Red Hat 的内核；因此，答案 b 不正确。尽管 Linux 发行版使用交换分区，但其文件安装在各种目录下。因此，答案 d 不正确。

## 问题 5

以下哪个命令可用于将引导映像复制到格式化的 1.44MB 软盘？文件名是 `boot.img`。

- a. `rawrite boot.img a:`
- b. `rawrite`
- c. `dd if=/mnt/cdrom/images/boot.img a:`
- d. `copy boot.img a:`

答案 b 正确。当你在 MS-DOS 模式下运行此命令时，会提示你输入要复制的映像以及软盘驱动器的位置。因为答案 a 中的命令不起作用，所以不正确。有关 `rawrite` 语法的更多信息，输入 `rawrite -h` 命令。`dd` 命令是 Linux 命令。虽然你可以在 Linux 中创建启动盘，但在 Linux 计算机中没有 `a:` 驱动器；因此答案 c 不正确。映像文件是多个不同文件的归档。你不能直接复制映像；你需要像 `rawrite` 这样的命令将文件解包到你的软盘。因此，答案 d 不正确。

## 问题 6

以下哪个命令可用于格式化或激活 Linux 交换文件？

- a. `mkswap`
- b. `mke2fs`
- c. `ext2fs`
- d. `swapon`

答案 d 正确。你可以使用 `swapon` 命令激活 Linux 交换文件。`mkswap` 命令格式化 Linux 交换分区（不是文件）；因此，答案 a 不正确。因为 `mke2fs` 命令格式化常规 Linux 卷（不是交换分区），所以答案 b 不正确。第二扩展文件系统有时被称为 `ext2fs`，但它不是一个命令，所以答案 c 不正确。

## 问题 7

在 Linux 安装期间，应在何时将 LILO 安装到软盘上？[勾选所有正确答案]

- [ ] a. 当你不想将 LILO 写入你的 MBR 时。
- [ ] b. 当 Linux 是你计算机上唯一的操作系统时。
- [ ] c. 当你希望如果未安装你的 Linux 启动软盘，计算机启动到另一个操作系统时。
- [ ] d. 当你始终希望使用 LILO 在多个操作系统之间进行选择时。

答案 a 和 c 正确。将 LILO 安装在软盘上是安装 LILO 到你的 MBR 的一种可行替代方案。如果不插入启动软盘，你的计算机将启动你的原始操作系统。如果 Linux 是你计算机上唯一的操作系统，你希望每次打开计算机时都启动 Linux。如果你只在软盘上设置 LILO，你的计算机不会每次打开时都启动 Linux。因此，答案 b 不正确。如果没有你的 Linux 启动软盘，你的其他操作系统将从 MBR 启动。因此，答案 d 不正确。

## 问题 8

你正在 TCP/IP 网络中的计算机上安装 Linux。在安装 Linux 时，设置网络时需要以下哪些项目？提示：你的网络已连接到其他网络，并且你没有 DHCP 服务器。[勾选所有正确答案]

- [ ] a. 计算机的 IP 地址
- [ ] b. 网关计算机的 IP 地址
- [ ] c. DHCP 服务器的 IP 地址
- [ ] d. 名称服务器的 IP 地址
- [ ] e. 网络上所有其他计算机的 IP 地址

答案 a、b 和 d 正确。因为你的计算机不是从 DHCP 服务器获取其地址，所以你需要指定计算机的 IP 地址。你需要网关计算机的 IP 地址来访问其他连接的网络。你需要至少一个名称服务器的 IP 地址来将名称如 `coriolis.com` 翻译为 IP 地址。因为你已经需要计算机的 IP 地址，DHCP 服务器不会帮助你。因此，答案 c 不正确。虽然拥有网络上所有其他计算机的 IP 地址很有用，但在安装过程中连接你的计算机到网络时不需要提供此信息。因此，答案 e 不正确。

### 问题 9

在安装期间应在哪里配置不同的 Linux 分区？

- a. 你应该将更频繁访问的信息，例如交换分区，尽可能靠近硬盘中心放置。
- b. 硬盘上分区的位置相当不重要。
- c. 你应该将更频繁访问的信息，例如交换分区，尽可能靠近硬盘边缘放置。
- d. 你应该将更频繁访问的信息，例如 `/root` 目录，尽可能靠近硬盘中心放置。

答案 b 正确。鉴于当前硬盘的速度，任何特定分区的位置并不非常重要。将交换分区更靠近硬盘中心确实有帮助；然而，速度提升微不足道。因此，答案 a 不正确。将交换分区放在硬盘边缘会减慢数据传输。即使差异不显著，答案 c 也不正确。因为以 root 用户登录应很少见，对 root 用户的主目录 `/root` 的访问应不频繁。任何 `/root` 目录都可以远离硬盘中心。即使差异不显著，答案 d 也不正确。

### 问题 10

你已在生产服务器上安装了 Linux。它也是管理你网页的服务器。你每天收到数百次对你网页的访问。你听说有一个新的 Linux 内核，版本 2.5.45。你理解它将帮助你更有效地管理你的流量和日志文件。你应该用此内核升级你的计算机吗？以下哪种解释最有意义？

- a. 不。因为最后一位数字是奇数，你知道此内核不适合生产。你应该等待内核版本 2.5.46。
- b. 是。因为最后一位数字是奇数，你知道此内核完全经过测试且可靠，适合你的用途。
- c. 不。因为中间数字是奇数，你知道此内核不适合生产。你应该等待内核版本 2.6。
- d. 是。因为中间数字是奇数，你知道此内核完全经过测试且可靠，适合你的用途。

答案 c 正确。最后一位数字是补丁号，并不决定内核是否适合生产。虽然较高的补丁号表示内核更成熟，但答案 a 和 b 仍然不正确。当内核版本的中间数字为奇数时，它是开发版内核，不适合生产。因此，答案 d 不正确。

## 需要了解更多？

访问 `www.caldera.com`，这是 Caldera Systems 的网站，其自我描述的重点是面向企业的 Linux。Caldera 网站提供硬件兼容性列表（HCLs）和知识库以及 Caldera 最新版 Linux 的下载。

查看 Corel Linux 社区的网站 `http://linux.corel.com`。Corel Linux 专注于桌面市场，并积极参与 Windows Is Not an Emulator（WINE）项目。最新版 Linux 的下载也可在该网站获取。Corel Linux 版本的 Linux 公开基于 Debian 发行版构建。

探索 Debian GNU/Linux 的网站 `www.debian.com`。这可能是 Linux 开发人员最流行的 Linux 发行版。Debian 的创建者主要是志愿者。你也可以从该网站下载 Debian GNU/Linux。

调查 Linux 文档项目网站 `www.linuxdoc.org`，它是 Linux 手册、HOWTOs 以及其他多本长度文档的中央存储库。本章相关的 HOWTO 是“Linux Installation-HOWTO”。

访问 `www.linux-mandrake.com`，这是 MandrakeSoft 创建的 Linux-Mandrake 网站。其 Linux 版本基于 Red Hat Linux，并配有多个额外的图形和其他安装工具。你可以从该网站下载其 Linux 版本。

访问 `www.redhat.com`，这是 Red Hat, Inc. 的网站。其 Linux 版本是当前市场领导者。Red Hat 网站提供 HCLs 和知识库以及最新版 Linux 的下载。
