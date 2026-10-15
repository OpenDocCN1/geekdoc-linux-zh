
当 `catalyst` 命令运行完成后，它将根据 `livecd/iso` 项的内容创建 live CD（在我的示例中为 `/root/mylcd-x86-2006.1.iso`）。然后你可以使用工具（如 `qemu` 或 `VMware`）进行测试，并按照附录 B“构建、测试和刻录 ISO”中的描述使用 `cdrecord` 或 `k3b` 工具刻录 live CD。

当你第一次尝试此程序时，肯定不会得到一个干净的构建。如果 `catalyst` 失败，查找最后的错误消息并尝试修正问题。你可能会收到错误消息建议更改标志，或缺少某些组件的通知。如果你无法自己解决问题，可以像前面提到的那样在 `gentoo-catalyst` 邮件列表中寻求帮助。先读几篇帖子并尝试提出具体问题。存档可以在 `http://archives.gentoo.org/gentoo-catalyst` 获取。

### 总结

Gentoo 是构建 live CD 较具挑战性的 Linux 系统之一。本章中制作 Gentoo live CD 的程序为你的 live CD 目录结构设置了一个 `chroot` 环境。一旦进入该 `chroot` 环境，你就可以根据意愿为你的 live CD 添加或删除任何软件软件包。

为了给 live CD 节省空间，目录结构通过将其转换为 `squashfs` 文件系统进行压缩。虽然可以使用 `isolinux` 作为引导程序，但本程序描述了如何使用 GRUB 来实现相同的结果。

制作 live CD 的活跃开发主要与 Catalyst 项目相关。使用 Catalyst 和 spec 文件，你可以制作高度定制的 live CD。用于制作 live CD 的 Catalyst 开发已多年。然而，你应该密切关注 Catalyst 邮件列表和其他资源，了解在使用 Catalyst 构建 Gentoo CDs 时应使用的最新组件。

本页特留空白

本页特留空白

## 定制 Linux

本页特留空白

## 探索安全 live CD

今天已经有许多安全 Linux CD，因此你很有机会可以基于现有的安全导向发行版创建自己的 live CD。流行的 live CD 包括一些基于 Knoix、Slackware 和 Gentoo 的。你可以根据 Linux 发行版以及每个 CD 提供的工具来选择从哪里开始。

为了开始演示你可能在安全 CD 上发现的功能和特性，本章从 BackTrack (`www.remoteexploit.org`) 开始。第 2 章“玩转 live CD”包含了对 BackTrack 的介绍，帮助你开始并学习基础知识。本章查看 BackTrack 并关注以下方面：

- 理解它是如何启动的——你将学习 BackTrack 如何引导并启动服务，以及用户开始 live CD 的状态（如运行级别、图形和文本界面，以及用户账户）。
- 学习它包含哪些工具——你将熟悉 BackTrack 中包含的功能和工具，帮助你组合你自己的自定义安全工具集。

> 注意
> Track 与其他基于 Slax 的 live CD 一样，包含了 Linux Live CD/USB Scripts (`www.linux-live.org`) 提供的许多启动文件。参考该网站了解更多关于如何使用 linux-live.org 的脚本、内核和其他组件从已安装的 Linux 系统制作 live CD 的信息。

图 9-1 展示了 BackTrack 引入其安全工具军库的功能。因为 BackTrack 是由另外两个流行的安全导向 live Linux 发行版（Auditor 和 Whax）的工具组合而成的，你可以很好地了解你自己的 live CD 中需要的工具。

如果你正在使用 BackTrack，打开 BackTrack 菜单（屏幕左下角）选择要尝试的安全工具。在图 9-1 中，显示的应用程序包括 Autopsy 取证浏览器、用于创建和恢复磁盘镜像的自动化镜像和恢复 (`AIR`) 工具，以及用于探索网络的 AutoScan 实用程序。

# 第 9 章 定制安全 Live CD

25

![](img/6b7a4aaf8c4f76728e9b63b90222dd8e_275_0.png)

图 9-1 使用 BackTrack 进行系统规模评估、漏洞搜索和网络探索。

由于安全 Live CD 通常不是为了游戏或其他高端图形应用设计的，因此通过包含一个简单的窗口管理器（或完全不包含窗口管理器）可以节省大量的磁盘空间。由于 Fluxbox 窗口管理器非常轻量，且包含了启动许多有用 X 应用所需的特性，因此它在许多较小的 Live CD（50MB 到 180MB）中可用。BackTrack 为想要使用 Fluxbox 的用户内置了 Fluxbox，但 BackTrack 默认使用 KDE 界面。

为了理解构建此安全工具箱的基础，接下来的章节将引导你了解启动过程以及支持安全工具的基本型设置。

# 启动 BackTrack 安全 Live CD

要开始探索 BackTrack 是如何配置的，请查看它使用的启动文件。与大多数 Linux Live CD 一样，BackTrack 使用 Isolinux 引导加载程序。该引导加载程序的配置非常简单，基本上与你在基于 Slax (`www.slax.org`) 的其他 Live CD 中的配置相同。

### Live Linux CDs

`isolinux.cfg` 文件存储在 Live CD 的根目录 (`/`) 下，用于引导启动过程。这里存在三个标签：`slax`、`linux` 和 `memtest`。`memtest` 标签仅运行 `memtest` 命令以检查你的 RAM。默认的 `slax` 标签与 `linux` 标签相同，不同之处 `slax` 标签将默认 VGA 模式设置为 1024×768、16 色（`vga=03x17`，791 的十六进制等效值）。以下是可以在启动提示符处使用的启动选项（通过使用 `linux` 或 `slax` 标签），这些选项在按下 F1 键时的消息屏幕上描述：

- `linux debug`—在几次情况下中断启动过程并打开一个 shell（终端）以检查进度。
- `linux copyram`—将整个文件系统复制到 RAM。这只有在可用足够 RAM 时才能使用。
- `linux floppy`—在启动时启用自动挂载软盘。
- `linux load-modules`—从 `/optional` 目录加载模块。

你可以从启动提示符向 BackTrack 传递其他启动选项，包括 `nocod`、`nohd` 和 `nodma`。

你可以设置 `probeusb` 参数以比通常更早地找到 USB 设备。你还可以通过设置 `size=` 参数（以字节为单位），设置 BackTrack 在挂载根目录 (`/`) 时允许使用的特定 RAM。默认情况下，60% 的可用 RAM 用于 `tmpfs` 文件系统，该系统最终将存放 CD 的根文件系统。

# 启动组件

这些引导组件在 BackTrack 启动过程中使用：

- 启动屏幕（Splash screen)—BackTrack 启动时出现的第一个屏幕由 `boot/splash.cfg` 文件定义。该文件读取 BackTrack 启动屏幕 (`boot/splash.1ns`) 和指示用户按回车行的文本。在启动之前，用户可以选择按下 F1（查看 `boot/splash.txt` 文件包含的几个启动选项）以及按下 F2 返回原始启动屏幕。
- RAM 磁盘—通过 `slax` 标签的附加选项，创建一个 4MB 的 RAM 磁盘 (`ramdisk_size=4444`)。
- 内核（Kernel)—内核从 `boot/mlinuz` 文件启动。该内核是 2.6 内核，包含了对 Unionfs 和 Squash 系统的支持。
- 初始 RAM 磁盘（Initial RAM disk)—初始 RAM 磁盘文件和目录由 `initrd.gz` 提供 (`initrd=boot/initrd.gz`)。该文件被解压并挂载为 RAM 磁盘上的根文件系统。在该文件解压后

# 第 9 章定制安全 Live Linux CD

内核引导 `linuxrc` 文件（位于该文件系统的根目录下）继续启动过程。

### linuxrc 脚本

`linuxrc` 脚本为 Live CD 系统做了大量工作。由于 `linuxrc` 脚本源自 Slack 自带的脚本，BackTrack 设置文件系统的方式与 Slack（以及其他基于 linux-live.org 脚本的发行版）相似。

`linuxrc` 脚本的大部分处理是通过 `liblinux` 脚本定义的函数完成的（也在 `initrd` 根目录下）。以下是 `linuxrc` 脚本在 BackTrack 中执行的一些操作：

- 挂载 `/proc` 和 `/sys` 文件系统。
- 检查在启动提示符处是否给了 `debug` 选项。如果是，脚本其余部分将在调试模式运行。
- 运行 `modprobe` 以加载外部模块。加载的许多模块用于支持的文件系统类型（`isofs`, `squashfs`, `unions` 和 `vfat`）。如果存在 NTFS 文件系统，则会添加 NTFS 支持。如果给了 `probeusb` 启动选项，也会为 USB 存储设备添加支持。
- 根文件系统 (`/`) 最终被设置为 `tmpfs` 文件系统。首先，代表 `/bin`, `/etc`, `/root`, `/usr`, `/var` 等的单个 `squashfs` 文件系统从 CD 的 `/base` 目录只读挂载。然后，它们与可写的 `/UNIONFS` 目录合并。（参见第 5 章“Inside Live CD Components”中关于 UnionFS 和 Squashfs 的描述。）

## 第 280 页

启动过程完成后，用户会在屏幕上看到登录提示和一些信息。这些信息包含了 root 密码以及启动 GUI 或网络的方法。

## 登录

在 BackTrack 中，你需要从文本的登录提示符以 root 用户身份登录。没有其他用户账户可以作为登录账户。

BackTrack 已经分配了一个 root 密码。该密码会在首次启动时显示在屏幕上。虽然这看起来可能是一个安全隐患，但请记住，此时还没有网络接口，因此你可以在启动网络接口允许任何远程登录服务访问机器之前，运行 `passwd` 命令更改 root 密码。你也可以输入 `passwd` 作为启动选项，以便在启动过程中提示输入 root 密码。

尽管存在其他用户账户，但没有一个被启用供你登录。Knoppix 启动后进入由 knoppix 拥有的桌面（该用户可以无密码请求权限），但你需要添加一个新用户来以非 root 用户操作运行 CD（运行 `adduser username` 步骤将引导你完成此过程）。

如前所述，登录提示是基于文本的，并在前面有说明（列出了 `/etc/issue` 的内容）。这些说明包括 root 密码以及配置桌面 (`xconf`)、启动桌面 (`startx`)、启动更简单的桌面 (`gui`) 以及使用 DHCP 获取 IP 地址 (`dhcpcd`) 的命令。图 9-2 显示了上述的登录界面。

配置登录过程的方法包括：

- 通过编辑 `/etc/issue` 文件来更改登录提示符之前显示的文本。
- 设置其他用户账户，这样你就不以 root 登录。
- 配置用户环境。你可以通过编辑 `/etc/profile` 文件来修改用户环境变量。
- 配置用户家目录。`/root` 目录填充了在 `/etc/skel` 目录中预先设置的配置文件。你可以从那里添加或更改配置文件。

如果用户能够成功作为 root 用户登录，接下来需要关注的区域是设置桌面环境以及配置必要的外设（网络接口、打印机、声卡等）的功能区域。

## 第 9 章 定制安全运行 CD

![](img/6b7a4aaf8c4f76728e9b63b90222dd8e_281_0.png)

图 9-2 文本登录界面包含来自 `/etc/issue` 文件的信息。

> 注意
> 在 `/etc/profile` 中设置的一个你可能会查看的变量是 PATH 变量。BackTrack 在 PATH 中添加了一个点 (`.` )。这允许从当前目录运行命令（这种活动通常需要显式请求，输入如 `./command` 等内容）。BackTrack 需要此功能作为其让你从 BackTrack 菜单运行命令的一部分。它基本上是打开一个终端窗口，并将 shell 打开到包含命令的目录。它期望你能够从那里运行命令。

## 配置桌面

虽然许多 BackTrack 功能可以在 shell 中使用，但 BackTrack 通过为桌面创建一个名为 Back-Track 的菜单，帮助用户浏览成百上千的命令和实用程序。在为 BackTrack 配置桌面时采用的一些设计决策，在你定制自己的安全 CD 时是值得考虑。

## 桌面环境或窗口管理器

BackTrack 默认使用 KDE 作为桌面环境。因为 BackTrack 没有像微型安全发行版那样受限于 50MB 可启动业务质卡或 180MB 微型磁盘的尺寸限制，因此有空间运行更大的桌面环境，如 KDE。这些微型发行版倾向于使用轻量级窗口管理器（如 Fluxbox）来提供简单的 GUI。

BackTrack 提供了其他窗口管理器，包括 Fluxbox (`lfbox`)、Motif (`mom`) 和 Twm (`twm`)。因此，在 CPU 慢或内存低的情况下，用户可以切换到另一个窗口管理器。当然，如果你切换到简单的窗口管理器，将失去一些 KDE 功能和工具。

特别是，Fluxbox 用于许多运行版 Linux CD。例如，Fluxbox 是其他面向安全的运行版 CD 上的主管理器，如 INSERT (`www.inside-security.de/insert_en.html`)、PHLAK (`www.phlak.org`) 和 Knoppix-STD (`www.knoppix-std.org`)。它也作为窗口管理器提供在某些运行版 CD 上，例如 Damn Small Linux (`www.damnsmallux.org`)。

要将默认桌面环境从 KDE 更改为更简单的 Fluxbox 窗口管理器，请编辑 `/etc/issue`。

## 第 283 页

## 第 9 章 定制安全运行 CD

![](img/6b7a4aaf8c4f76728e9b63b90222dd8e_281_0.png)

图 9-3 BackTrack 上的安全工具分为 15 类。

## KDE 设置

因为 KDE 是 BackTrack 的默认桌面，大多数工具都可以从桌面访问。要定制桌面的外观和感觉，请参考 KDE 菜单中的设置。

## 配置网络接口

因为网络接口是 BackTrack 的默认配置，在使用工具之前，这里有两种方法配置标准以太网：

- **从 shell**——你可以通过输入 `dhcp` 命令从 DHCP 服务器获取 IP 地址。要关闭接口，可以使用 `ifconfig eth0 down`。
- **从 KDE 菜单**——选择 KDE 按钮 -> Internet -> 设置 IP 地址。网络配置窗口允许你输入静态 IP 地址、子网掩码和默认网关。你还可以输入 DNS 服务器地址。对于其他类型的网络接口，也提供了 GUI 工具。配置拨号连接，选择 KDE 菜单 -> Internet -> 拨号工具。配置无线局域网连接，选择 KDE 菜单 -> Internet -> 无线管理器。

## 第 284 页

再次，由于 BackTrack 使用 KDE，还有图形化工具用于配置和管理网络接口。通过选择 KDE 按钮 -> 设置 -> 控制中心 打开控制中心。选择 Internet & Network 来选择无线网络（自动检测或手动）和网络监视。

## 第 9 章 定制安全实时版 Linux CD

这意味着寻找用于检查系统和网络的工具，评估并修补安全漏洞，以及处理问题，例如损坏或被利用的系统。

再次，BackTrack 被用于说明你可能包含在自己的安全向型实时版 Linux CD 中的类工具。BackTrack 内置了数以百的实用程序、资源（如漏洞数据库）和服务，你可能会发现它们对你自己的 Live CD 很有用。

图 9-4 展示了 BackTrack 包含的功能特性类型。

![](img/6b7a4aaf8c4f76728e9b63b90222dd8e_285_0.png)

图 9-4 BackTrack 中的功能范围从远程利用工具到密码破解工具。

正如从图 9-4 中所示，向安全向型实时 CD 中添加的功能可以超出密码检查器和端口扫描器。为了支持 BackTrack 中的安全工具，还有诸如安全信息存档、检查已知漏洞等功能。这些工具用于追踪特定类型设备（如蓝牙或无线局域网卡）的问题。

接下来的章节将分别介绍图 9-4 所示的安全主题。你可以利用这些章节简要了解这些工具的工作原理，并帮助评估你想要在自己的安全实时 CD 上具备的功能。

## 运行枚举工具

枚举工具（Enumeration tools）用于发现潜在入侵者可以获取有关系统、网络或服务的信息。在实时 CD 上包含枚举工具可以让你测试网络上的计算机，从而关闭入侵者可能用来对你造成伤害的信息的访问。

BackTrack 包含了数十种枚举工具，可用于查找有关你的 Internet 域名、LDAP 服务器、操作系统、路由和其他服务的信息。以下枚举工具随 BackTrackget提供。

### 检查域信息

要运行从域名 (DNS) 服务器检查 Internet 域信息的命令，请选择 K 菜单 -> Enumeration -> DNS。约有六个菜单项可可用，用于检查 DNS 信息。

- DNS -> Walk 让你能够运行 `dnswalk` (`www.visi.com/~bar/dnswalk`) 来对你的 DNS 服务器的区域数据库进行调试。`dig`（K 菜单 -> Enumeration -> DNS -> Dig）是一个用于查找范围 DNS 信息的常用程序。`dsapenum.pl`（Perl 实用程序）是另一个检查你域的有用工具。通过它，你可以找到 DNS 服务器，尝试区域传输，并根据你提供的列表检查主机名。

### 检查 LDAP 信息

使用 `1ldapenum` Perl 脚本 (`http://sourceforge.net/projects/ldapenum`)，你可以从运行在 Windows 2000 和 2003 系统上的 LDAP 服务获取密码和系统信息。你可以通过选择 K 菜单 -> Enumeration -> LDAP -> Ldap Enum 进入脚本。同一个工具还可以用于尝试登录它发现的账户。`1ldapenum` 命令还可以用于检查组和成员。

Luma (`http://luma.sourceforge.net`) 图形化 LDAP 管理工具（K 菜单 -> Enumeration -> LDAP -> L）包含了八个插件，用于查找和处理 LDAP 服务器上的数据。插件允许你搜索 LDAP 地址录、搜索选定的 LDAP 服务器、管理用户，并从 LDAP 服务器访问其他类型的信息。

### 确定操作系统

来自操作系统枚举枚举菜单（K 菜单 -> BackTrack -> Enumeration -> Operating System）的工具可以帮助确定正在运行的操作系统类型。从该菜单中选择 `Pof`，使用被动指纹识别技术根据该计算机发送的 TCP/IP 数据包来确定其运行的操作系统类型。`pof` 命令 (`http://lcamut.coredump.com/pof.shtml`) 被认为是被动的，因为它通过读取网络上的 TCP/IP 数据包来发现系统信息，从而确定主机的操作系统类型和其他属性。

如 `pof` 之类的工具可以在不实际接触的情况下获取远程系统的信息。`pof` 工具可以研究任何连接你网络的系统的 TCP/IP 数据包。它还可以根据系统获取信息，而无需接受或拒绝运行 `pof` 的系统发起的连接。

`nmap` 命令 (`www.secure.org/nmap`) 是另一个常用于探索远程系统的工具。通过 `nmap`，你可以扫描网络或单个主机。通过扫描数据包，`nmap` 可以确定主机运行的是什么操作系统以及这些主机提供哪些服务。它还可以学习每个主机运行的是什么种防火墙。

Nmap 前端 (`nmap` 命令）为 nmap 提供了图形化界面。9-5 显示了扫描局域网上 Linux 机器的结果。系统名称为 `einstein`，TCP 端口 21 (ftp)、22 (ssh)、rbind (111) 和 X11 (6000) 是开启的。ftp 和 ssh 服务显示为红色，表示端口上的这些服务是激活的。

`sinfp.p1` Perl 脚本 (`gom.org/sinfp`) 可以根据你给命令的 IP 地址确定计算机运行的操作系统类型。对于 Linux 系统，你还可以确定有关当前内核版本的信息。

`probe2` 命令 (`http://probe.sourceforge.net`) 仅通过提供系统 IP 地址即可收集大量关于计算机操作系统的信息。它使用几种不同的信息收集技术来获取所选系统的信息。它尝试确定到远程系统的距离，检查系统上的开放端口，并检查确定运行的操作系统类型。

### 确定网络路由

用于发现网络路由信息的工具（来自 Routing/Network 菜单）包括自治系统扫描器命令 (`www.phenenoit.de/iraps/doc.html`)、防火墙命令 (`www.packetfactory.net/projects/firewall`)。要追踪数据包到达目的地，你可以使用 `itrace` 命令 (`http://ftp.sourceforge.net/itrace`)、`traceroute` 命令 (`ftp://ftp.ee.lpl.gov`) 或 `tcaceroute` 命令 (`www.phenenoit.de/iraps/doc.html`)。`itrace` 使用 ICMP 请求；`tctrace` 使用 TCP SYN 包追踪数据包到达目的地。

## 实时版 Linux CD

![](img/6b7a4aaf8c4f76728e9b63b90222dd8e_288_0.png)

Nmap 4.03 ( `http://www.insecure.org/nmap/` ) 于 2006-07-21 08:38 GMT。
einstein (10.0.0.50) 上有趣的开启端口：
（扫描的 1790 个端口中未显示的状态为：关闭）

| PORT | STATE |
| :--- | :--- |
| 21/tcp | open ftp |
| 22/tcp | open ssh |
| 111/tcp | open unbound |
| 6000/tcp | open X11 |

MAC 地址：00:08:62:EC:98 (Asiarock Incorporation)
设备类型：通用
运行 Linux：2.4.X|2.X
OS 详情：Linux 2.4 - 2.50, Linux 2.7 - 2.61

Nmap 完成：1 个主机在线，耗时 3.843 秒
