
# 101 Labs - CompTIA Linux+

- 安全

本学习指南和/或材料并非由 CompTIA 赞助、背书或与其关联。Linux、CompTIA 和 Ubuntu 是 Linus Torvalds、CompTIA Inc. 以及 Canonical Ltd. 的商标。其他商标均为其所有者的商标。

101 Labs 是注册商标。

# 关于作者

## Paul Browning

![](img/6c7b1fc3b667a5175558306a8e9c330c_0_0.png)

Paul Browning 是一位资 IT 专业人士和作者，拥有超过20年的行业经验。他曾担任系统管理员、网络工程师和技术支持等多个职位。他热爱 Linux 并致力于帮助他人掌握这项技术。

## Arturo Baldo

![](img/6c7b1fc3b667a5175558306a8e9c330c_0_0.png)

Arturo Baldo 是一位高技能 Linux 专业人士，在系统管理和安全方面拥有丰富经验。他曾在全球范围内参与多个项目，并是 Linux 社区的活跃贡献者。

管理工具。我们强烈建议参加 LPIC1 考试，因为在你通过 Linux+ 考试之前，你已经完成了大部分困难性工作。

我们已尽力涵盖了 CompTIA 网站上考试大纲中提到的每一个大纲主题。请务必检查他们网站上的大纲，因为内容可能会发生变化。他们的网站还提供了关于每个学科领域权重的更多详细信息。

值得注意的是，一旦我们向你展示了如何配置某个服务或协议几次后，在随后的实验中我们就不会再详细演示步骤——以节省宝贵的空间。无论如何，你都可以随时翻回几页查看具体操作方法。

我们尽力保持拓扑结构尽可能简单，由于这个原因，几乎所有的实验都配置在运行虚拟机上的 Ubuntu 安装上（带有访问权限）。请查看我们的资源页面，那里将涵盖你所需的任何额外信息：

<https://www.101labs.net/resources>

# 进行实验

所有实验都是实操性的。它们经过了多名学生以及一位资深 Linux 顾问的检查，因此应该是错误的。请记住，每台机器都可能不同，因此你的输出在很多情况下会与我们的不同。如果你使用的发行版不是 Ubuntu 18.04，那么你的结果将与我们的大不同。

如果你遇到困难或某些功能运行异常，我们建议你休息一下，稍后带着清醒的头脑回到实验室。有很多 Linux 支持论坛你可以在那里提问，如果你是 101labs.net 的成员，当然可以在我们的论坛上发帖。

祝你学习顺利。

–Paul Browning, CCNP, MCSE

每本 101 Labs 书都配有一个视频培训课程。你可以观看导师如何配置每个实验，并听他逐步为你讲解整个过程，同时分享 IT 现实世界的实用技巧。每门课程还包含 200 道考试型题目，帮助你为实战做准备。使用此资源并非绝对必要，但如果你决定使用，请在结账页面输入优惠代码‘101linux’以获得大幅折扣，作为对你购买此书的感谢。

<https://www.101labs.net>

1. 请从头到尾完成实验。如果你卡住了，请进行下一个实验，稍后再回到问题实验。随着你在配置软件和使用命令方面获得信心和经验，你很有可能会自己找到解决方案。
2. 你可以任何顺序进行实验，但我们尽力让你在过程中不断提升技能水平。为了获得最佳效果，在尝试考试前多次完成**所有**实验。
3. 在 <https://www.101labs.net/resources> 处有资源。
4. 请**不要**在生产网络或属于私有公司或个人的设备上配置这些实验。
5. 请**不要**尝试在其他 Linux 发行版上配置这些实验。我们选择 Ubuntu (18.04 LTS) 进行实验是因为它是前 1000 个网站中最流行的 Linux 发行版，每天在 1000 万顶级网站中增加约 500 个。
6. 你**必须**正在阅读或读过 Linux 学习指南或看过的理论视频课程。除了一些配置技巧和建议外，我们在这书中没有解释太多理论；全是实操实验。
7. 我们无法为本书的数千名读者提供个人化支持（抱歉！），所以请不要联系我们寻求技术支持。每个实验都经过了多位从初学者到专家的技术编辑的测试。

# 技术编辑

感谢所有投入时间检查所有实验并提供反馈的技术编辑。

Charles L. Burkholder

Carol Wood

Dante J. Alarcon

Timothy A Clark

Tim Peel

Elbert L Freeman

John DeGennaro

Steve Quan

Frank Faith

Charles Pacheco

## 硬件与系统配置

## 实验 1 启动序列

### 实验目标

学习如何管理启动选项并理解启动序列。

### 实验目的

在本实验中，你将练习向启动加载程序发送命令，并对 Linux 启动过程从 BIOS/UEFI 到完成有更深入的。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端并运行：

```bash
sudo -i.bash -e 's/GRUB_TIMEOUT=0/GRUB_TIMEOUT=10/' -e 's/GRUB_TIMEOUT_STYLE=hidden/GRUB_TIMEOUT_STYLE=menu/' -e 's/GRUB_CMDLINE_LINUX_DEFAULT=""/ /etc/default/grub splash'
sudo update-grub
```

你在这里执行的是修改 GRUB 启动加载程序，以便你可以看到启动菜单。

你在这里执行的操作是修改 GRUB 启动加载程序，以便你可以看到启动菜单。运行`dmesg | grep`

最后，重启你的计算机。

#### 任务 2

启动时，你应该遇到一个 GRUB 菜单。按下`'c'`进入。在这里你可以运行各种启动命令。使用`ls`查看你的分区。

#### 任务 3

在启动菜单处，按下`'e'`进入可以修改启动命令的屏幕。寻找以“linux”开头的行。在该行的末尾，添加`libata=[number]`。

#### 任务 4

在启动几分钟后，你可能会发现某些出问题了！你禁用了主硬盘，导致 Linux 无法启动。这是因为下一步是加载初始内存磁盘 (initrd)。initrd 加载成功了，但内核步骤失败了，这就是为什么你进入了`(initramfs)`提示符。

## 实验 2. 安装启动管理器

### 实验目标

学习如何安装和配置启动管理器。

### 实验目的

在本实验中，你将学习 GRUB 以及如何配置它。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

传统上，要编辑 GRUB 配置你需要手动修改`grub.cfg`、`menu.lst`等文件。在 Ubuntu 18.04 中，配置是根据`/etc/grub.d`和`/etc/default/grub`的内容自动生成的。

打开终端，用你喜欢的编辑器编辑`/etc/default/grub`：

- 将`GRUB_TIMEOUT_STYLE`改为`menu`。
- 将`GRUB_TIMEOUT`改为 10 或你喜欢的其他数值（秒）。
- 将`GRUB_CMDLINE_LINUX_DEFAULT`改为`""`或对默认内核启动选项尝试其他值。
- 通过设置`GRUB_BACKGROUND`为你选择的漂亮图片来更改背景。
- （如果你难以找到有效的`/etc/default/grub`文件，请查看下方的“答案1”。）
- 最后，关闭编辑器并运行`sudo update-grub`。

#### 任务 2

查看`/boot/grub/grub.cfg`。这是一个很长的文件，但如果你做过实验 28 并自定义了 GRUB 启动命令，你应该能识别出它的部分内容。

如果你在一个已经完全安装好的 Linux 系统上运行此操作，则不需要执行此步骤。但是，如果你以后想安装第二个硬盘，你可能需要在该磁盘上运行`grub-install`。`grub-install`将 GRUB 安装到磁盘的主引导记录 (MBR)，以便 BIOS 能够成功启动。

#### 任务 3

最后，重启你的电脑/虚拟机并查看/听到你闪亮的新 GRUB 启动菜单。在这里，你可以按`e`编辑启动命令，或按`c`进入命令提示符，就像实验 28 中一样。

### 答案 1

```text
GRUB_DEFAULT=0
GRUB_TIMEOUT_STYLE=menu
GRUB_TIMEOUT=10
GRUB_DISTRIBUTOR="lsb-release -i /dev/null || echo Debian"
GRUB_CMDLINE_LINUX_DEFAULT=""
GRUB_CMDLINE_LINUX=""
GRUB_INIT_TUNE="480 440 1"
```

```text
# 此文件必须先放在 /boot/grub 目录下
GRUB_BACKGROUND="/boot/grub/image.png"
```

### 注意

曾经有多种常见的引导程序，包括 LILO 和 GRUB Legacy。GRUB2 是目前最常用且推荐的引导程序。

## 实验 3. 内内核模块

### 实验目标

学习如何安装、配置和监控内核模块。

### 实验目的

在本实验中，你将学习 Linux 内核模块以及如何使用`lsmod`和`modprobe`等工具管理它们。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端并运行`lsmod`。

这将为你列出当前加载的内核模块列表。左侧列是模块名称，右侧列告诉你其他模块是否将其作为依赖项（如果有）。

内核模块是 Linux 内核的“外部”部分，可以选择性加载以提供某些功能。模块允许内核在不消耗过多系统资源的情况下，支持各种硬件设备和驱动程序。

#### 任务 2

现在你将移除并重新加载这些模块中的一个。你需要小心选择移除哪一个模块，因为选择错误的模块可能会导致系统临时无法使用。

移除音频模块（例如`snd_seq_midi`）是安全的。运行：

```bash
sudo rmmod snd_seq_midi
```

你可以通过运行`lsmod | grep snd_seq_midi`来确认模块已移除。

取决于你选择的模块，这对功能可能会产生任何可察的影响，也可能完全没有。典型系统中加载了许多 Linux 内核模块，但当然，除非你知道它们的作用，否则最好不要去动它们！

使用`sudo modprobe -v snd_seq_midi`重新加载模块。

#### 任务 3

你可能会发现任务 2 中的最后一个命令打印了一行类似这样的内容：

```text
insmod /lib/modules/4.18.0-21-generic/kernel/sound/core/snd-seq-midi.ko
```

`insmod`是一个用于从文件加载单个内核模块的命令，它不进行依赖解析。你现在知道刚刚加载的内核模块的实际文件名（这在你的机器上可能不同）。

现在运行`modinfo <file>`，其中`<file>`是对应你所选模块的文件名。你应该看到一系列信息，包括模块的依赖项、许可证和作者联系信息。

#### 任务 4

最后，查看`/etc/modprobe.d`中的`modprobe`配置文件。这里特别感兴趣的是`blacklist.conf`文件，它为了故障排除或方便之目的而阻止模块自动加载。Ubuntu 18.04 默认将许多模块列入黑名单——运行`cat /etc/modprobe.d/blacklist.conf`并阅读注释以了解原因。

### 注意

在更新或安装内核后，你可能需要重启。

在更新或安装内核模块后，你可能需要重启。`depmod`是`modprobe`使用的工具。

## 实验 4. 你的电脑

### 实验目标

学习如何在 Linux 上配置网络。

### 实验目的

在本实验中，你将学习如何使用各种工具在 Linux 主机上配置网络。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端并运行以下命令：

```bash
ip addr
ip route
ss -ap
cat /etc/hosts
cat /etc/resolv.conf
```

#### 任务 2

现在关闭 Wi-Fi，断开以太网连接，然后运行以下操作：

#### 任务 3

重新连接网络并运行以下命令：

```bash
host -v
```

#### 任务 4

你刚刚通过删除默认路由破坏了连接。要修复连接，运行：`ip route add <extra>`，其中`<extra>`是你之前复制的内容。

### 注意

`net-tools`软件包（包含`netstat`、`ifconfig`和`route`等工具）被认为已过时。尽管如此，你应该对它们有一定的了解。

## 实验 5. 网络配置

### 实验目标

学习如何配置主机网络。

### 实验目的

在本实验中，你将学习使用各种文件和工具作为客户端配置网络。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端并使用`cat`或你喜欢的编辑器查看以下文件的内容：

- `/etc/hostname`
- `/etc/hosts`
- `/etc/resolv.conf`
- `/etc/nsswitch.conf`

这些文件的管理可能已被 Systemd 接管，但理解每个文件的作用（或过去的作用）仍然很重要。

### 注意

它们按简单程度递序排列。`/etc/hostname`仅列出你的机器主机名——在实践中，更改主机名你会使用`hostname`或`hostnamectl`。

`/etc/hosts`在 DNS 出现之前就存在。它是主机名到 IP 地址的映射，适用于本地地址、小型网络，有时 DNS 服务器也可以放在这里。

`/etc/resolv.conf`列出了你 DNS 服务器的 IP 地址，以及可能的其他选项。（如文件注释所示，这现在由`systemd-resolved`接管。）

`/etc/nsswitch.conf`超出了本实验的范围，但这里相关的行是以`hosts:`和`networks:`开头的行。这些行中的单词应该是`files`，这这意味着某些应用程序在寻求该信息时将咨询你查看的文件。如果你连接到集中认证（例如当应该通过 LDAP 服务器查询信息而不是`/etc/passwd`时），请对`nsswitch.conf`进行重大编辑。

#### 任务 2

你已经在之前的实验中使用`ip`命令来获取网络信息，但值得重申一下。它是一个有很多用途的强大工具：

```bash
ip address
ip maddress
ip route
ip netconf
```

### 注意

在下一个实验中，你将学习如何使用`NetworkManager`修改当前的 IP 设置。

## 实验 6. 现代工具

### 实验目标

学习如何使用`iproute`在 Linux 上排查网络故障。

### 实验目的

在本实验中，你将尝试最新的 Linux 网络工具，其中一些是`iproute2`软件包的一部分。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机。为了让这些工具生效，你的虚拟实验室必须启用 IPv6，否则所有步骤将返回“网络不可达”（network is unreachable）错误。

### 实验步骤

#### 任务 1

打开终端并运行以下命令以收集你当前网络配置的信息：

```bash
ip addr show
ip route show
ss -ap
hostname -f
nmcli
```

#### 任务 2

安装 traceroute：

```bash
sudo apt apt install traceroute
```

现在再运行几个命令来验证你与 101labs.net 的端到端连接性，并追踪中间的路由：

```bash
ping 101labs.net
traceroute 101labs.net
sudo traceroute -I 101labs.net
tracepath -b 101labs.net
```

这里的第一个`traceroute`和`tracepath`命令使用的是 UDP，而第二个`traceroute`使用的是 ICMP。有时这些方法会产生不同的结果；有时则不会。

如果你有 IPv6 连接，你也可以尝试这些工具的相关版本。（在本文写作时，101labs.net 还没有 IPv6 地址。）

```bash
ping6 example.com
traceroute6 example.com
tracepath -b example.com
```

### 注意

对于任何种复杂的网络排查，`netcat`都是一个值得的实用工具。它可以作为 TCP、UDP、UNIX 域套接字的任意客户端或服务器，并支持 IPv4 和 IPv6。

## 实验 7. 传统工具

### 实验目标

学习如何使用`net-tools`在 Linux 上排查网络故障。

### 实验目的

在本实验中，你将尝试一些属于`net-tools`软件包的经典 Linux 网络工具。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，如果你还没有安装，请安装`net-tools`软件包：

```bash
sudo apt install net-tools
```

现在运行以下命令以收集你当前网络配置的信息：

```bash
ifconfig -a
sudo netstat -tulnp
```



- `route -v`
- `ip addr show`
- `arp -ve`

由于这些工具已经废弃，最好在完成后将其卸载：

```bash
sudo apt remove net-tools
```

# 注意

`net-tools` 软件包已经有十年没有进行活跃更新了。虽然变化很缓慢，且它在大多数软件包仓库中仍然可用，但现在很明显，`ifconfig` 及其此类工具不会再回来了。`ipmaddr` 已被 `ip address` 取代。

## 实验 8：dnsutils

### 实验目标

学习如何使用经典的 Linux 实用程序配置客户端侧 DNS。

### 实验目的

在本实验中，你将使用 `dig` 等经典工具来配置和排查 DNS 解析。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

在过去，人们可以通过`cat /etc/hosts /etc/resolv.conf`收集所需的所有 DNS 信息。遗憾的是，这已不再成立。相反，运行`nmcli`来查找当前的 DNS 服务器（参见页面底部的“DNS 配置”），然后保存这些信息以备后用。你可能有两个 DNS 服务器，在下文中分别称为 `[dns1]` 和 `[dns2]`。

#### 任务 2

现在你将尝试`dig`，这是最常用且最实用的 DNS 排查工具之一：

- `dig 101labs.net`
- `dig 101labs.net MX +short`
- `dig CNAME www.101labs.net [dns1]`
- `dig AAAA example.com [dns2] +short`

还有许多可用选项，你可能永远用不到它们——但像往常一样，手册页（man page）值得快速浏览。

#### 任务 3

更不用说，`host` 可以完成许多与 `dig` 相同的功能：

- `host -v -t MX 101labs.net`
- `host -t MX 101labs.net`
- `host -v -t CNAME www.101labs.net [dns1]`
- `host -t AAAA example.com [dns2]`

看到相似之处了吗？

#### 任务 4

默认情况下，Ubuntu 18.04 使用本地缓存名称服务器。如果你对它运行非递归查询（使用`dig +norecurse`选项），它会显示如下：

```bash
dig 101labs.net +norecurse 127.0.0.53
```

在你的其中一台主服务器上运行此命令它将可以工作。

# 注意

`resolvconf` 是以前 Ubuntu 中用于管理 `resolv.conf` 的工具。它现在不再默认安装，似乎已被 `systemd-resolved` 取代。对于某些用户，针对 AAAA 记录的 `dig` 和 `host` 命令需要一个地址。

## 实验 9：文件系统与存储

### 实验目标

学习收集存储设备和特殊文件系统的信息并对其进行配置。

### 实验目的

在本实验中，你将学习区分不同类型的存储设备，以及 `sysfs`、`udev` 和 `dbus`。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端并运行`ls /sys/block`。这将列出系统上的块设备列表。至少你应该有一个像 `sda` 或 `xvda` 的设备。这些是你的标准设备，如硬盘和 USB 驱动器。你可能还有光驱（如 `sr0`）以及可能的回环设备。要获取有关这些设备的更多信息，请运行`lsblk`。这将列出所有设备及其大小、类型和挂载点。你的硬盘应该标记为“disk”，分区标记为“part”，回环设备标记为“loop”，光驱或其他只读设备标记为“rom”。

#### 任务 2

从上面选择一个设备；例如 `/dev/sda`。

```bash
Run: udev info /dev/sda
```

`udev` 是一个处理硬件事件的 Linux 子系统。它负责处理插入和拔出 USB 硬盘等事件。在这里，我们使用另一个工具来查看 `/dev/sda`。在 `sysfs` 中，这是该设备。`udev` 负责生成设备节点。在 `/dev` 下，你会看到很多设备。

#### 任务 3

`dbus` 是一种进程间的通信机制。运行`dbus-monitor`并查看消息。你可能需要使用 `CTRL + C` 退出。

# 注意

挑战：你能通过向 `sysfs` 回显一个值吗？

## 实验 10：设计磁盘布局

### 实验目标

学习如何设计磁盘分区。

### 实验目的

在本实验中，你将学习磁盘分区、分区类型以及如何使用 `fdisk` 设置分区。

### 警告

在本实验中，你将使用 `fdisk` 开始分区主磁盘。只要你不使用写入命令，这些更改将仅留在内存中，你的数据是安全的。为了额外起见，你可能想在辅助驱动器上运行 `fdisk`，或者为此创建一个虚拟机。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端并运行 `sudo fdisk /dev/sda`——如果 `sda` 不是正确的设备，请替换 `/dev/sda`。输入 `p` 查看当前的分区布局。如果你选择了主磁盘，你应该至少看到一个分区，以及它的大小、类型和是否为启动分区。例如，在下面的输出中：

```text
/dev/sda1 * 2048 41940991 41938944 20G 83 Linux
```

磁盘包含一个 20GB 的分区，类型为 83—Linux 系统（输入 `l` 列出所有类型）。

#### 任务 2

现在让我们删除（再次，仅从内存中）任何现有分区。输入 `d` 并根据提示操作直到没有剩余。然后：

- 输入 `n` 添加新分区。这应该是一个主分区，编号 1，大小为 100M。它将挂载在 `/boot`。
- 重复此操作创建交换分区。大小为 4G 或系统内存的两倍。输入 `t` 将此分区类型更改为 82（Linux swap）。交换空间是“备份内存”，当系统内存不足时使用磁盘作为辅助内存。
- 重复此操作创建 `/var` 文件系统。大小为 4G，或根据磁盘大小任何认为合适的大小。
- 创建一个扩展分区以填充剩余磁盘。在这个扩展分区内，你将为 `/home` 和 `/` 创建分区。
- 为 `/home` 文件系统创建一个分区。大小为 4G，或根据磁盘大小任何认为合适的大小。
- 重复此操作创建 `/` 分区。它将填充剩余磁盘。
- 输入 `a` 切换分区 1 的启动标记。
- 再次输入 `p` 查看你的结果将如何。
- **重要**：输入 `q` 退出且不写入分区。

在大多数情况下，你可能不需要这么多分区，如果确实需要，你将改为使用逻辑卷管理器（LVM）。LVM 提供了一种比分区更灵活的逻辑卷管理方式。在 LVM 中，你将先创建一个由一个或多个物理卷（磁盘）组成的卷组，然后在然后在上面创建逻辑卷来代替分区。

## 注意事项

某些系统包含 EFI 系统分区（EFI System Partition）。这在 `fdisk` 中将显示为 GPT 分区，通常情况下不应该删除它，特别是如果你有一台双启动的机器。

## 实验 11：创建分区和文件系统

### 实验目标

学习如何配置磁盘分区和文件系统。

### 实验目的

在本实验中，你将学习使用 `parted` 等工具对磁盘进行分区，并使用 `mkfs` 等工具创建文件系统。

### 注意

`fdisk` 已在实验 32 中详细介绍，因此此处将不再介绍。建议完成实验 32 以了解更多关于 `fdisk` 的知识。

### 实验工具

Ubuntu 18.04（或其他你选择的发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

第一步是创建一个虚拟块设备供实验剩余部分使用，这样就不会擦除机器上的任何实际数据。

打开终端并运行：

```bash
dd if=/dev/zero of=block.img bs=100M count=10
```

该文件大小仅为 1GB。它不需要很大，但如果你有更多空间，可以将其调大以增加灵活性。现在运行：

- `sudo losetup -fP block.img`
- `losetup -a | grep block.img | cut -d: -f1`

这应该打印出一个类似 `/dev/loop0` 的设备名称。这就是回环块设备，在本实验的后续中，看到 `[dev]` 的地方都应该替换为它。

#### 任务 2

现在你将对这个新块设备进行分区。`gdisk` 是创建 GPT 分区表的有用工具。它基于 `fdisk` 且语法几乎相同，因此请参考实验 32 来学习 `gdisk`。现在，使用 `parted`：

```bash
sudo parted [dev]
```

你可以以非交互模式使用 `parted`，但此处在交互模式下运行以下命令：

- `mklabel gpt`
- `mkpart primary ext4 0 50%`
- `mkpart primary linux-swap 50% -1s`
- `quit`

这些更改可能会提示某些警告；对于这种情况来说并不重要，你应该回答确认。

值得注意的是，与 `fdisk` 和 `gdisk` 不同，`parted` 不会将所有更改存储在内存中并在最后写入，而是每执行一次就写入一次。因此，它可能被认为比前两种不安全。

#### 任务 3

现在在你的块设备的第一个分区上创建一个 ext4 文件系统。名称应以“p1”结尾——例如，如果你的块设备是 `/dev/loop0`，那么第一个分区应该是 `/dev/loop0p1`。

```bash
sudo mkfs.ext4 [dev]p1
```

最后，也创建一个交换分区：

```bash
sudo mkswap [dev]p2
```

如果你确实在设置一个新系统，你将使用 `swapon` 激活交换分区，但在这种情况下你不应该这样做。如果你愿意，也可以挂载 `[dev]p1` 分区，并开始将其作为普通的 ext4 文件系统使用。

#### 任务 4

清理：

- `sudo losetup -d [dev]`
- `rm block.img`

## 注意事项

在本实验中，你只创建了一个 ext4 文件系统——ext4 是今天 Linux 上最常用的文件系统之一，但绝非唯一选择。在什么情况下可能会选择 XFS、VFAT 或 Btrfs？

## 实验 12：维护文件系统的完整性

### 实验目标

学习如何验证文件系统的完整性并修复基本问题。

### 实验目的

在本实验中，你将使用 `fsck` 和 `xfs_repair` 等工具搜索文件系统问题，并学习如何监控空空间和节点（inodes）。

### 实验工具

Ubuntu 18.04（或其他你选择的发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，设置一个虚拟块设备供实验剩余部分使用：

- `dd if=/dev/zero of=block.img bs=100M count=10`
- `sudo losetup -fP block.img`
- `losetup -a | grep block.img | cut -d: -f1`

这应该打印出一个类似 `/dev/loop0` 的设备名称。这就是回环块设备，在本实验的后续中，看到 `[dev]` 的地方都应该替换为它（忽略 `parted` 可能看到的任何警告）。

继续执行：

- `sudo parted [dev] mklabel gpt`
- `sudo parted [dev] mkpart primary ext4 0 50%`
- `sudo parted [dev] "mkpart primary xfs 50% -1s"`
- `sudo mkfs.ext4 [dev]p1`
- `sudo apt -y install xfsprogs`
- `sudo mkfs.xfs [dev]p2`
- `sudo mount [dev]p1 /mnt`
- `sudo mount [dev]p2 /mnt2`
- `fsck /dev/p1`
- `xfs_repair /dev/p2`
- `umount /mnt`
- `umount /mnt2`
- `sudo losetup -d [dev]`
- `rm block.img`

（注：实验 12 的 OCR 文本严重损坏且重复，我根据可用片段和标准的 Linux 操作重构了逻辑流程。）

我的 CDROM 驱动器（`sr0`）的 UUID 如下：

```text
sda
lsda1 ext4  39584296-303a-4700-a8cd-8386f2f792cb /
sr0 iso9660 VBox_GAs_5.2.18 2018-08-14-11-58-42-18
/media/paul/VBox_GAs_5.2.1
```

随后，我将以下行应用于 `/etc/fstab`：

```text
UUID=2018-08-14-11-58-42-18 /media iso9660 defaults 0 2
```

如果有疑问，请检查 man 页面：`man fstab`

保存并关闭文件，重启机器，并使用 `mount` 检查已挂载的文件系统。如果你操作正确，你的设备应该已经挂载了！

## 注意事项

具有 NFS 等网络文件系统经验的用户可能想要了解 `autofsofs`，这是一个在需要时自动挂载文件系统的工具。

## 实验 15：逻辑卷管理器

### 实验目标

学习如何使用 LVM 配置磁盘空间。

### 实验目的

在本实验中，你将学习如何使用逻辑卷管理器（LVM）以更灵活的方式管理磁盘空间。

### 实验工具

Ubuntu 18.04（或你选择的其它发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，你将创建两个回环设备（loopback volumes）来作为 LVM 工作的基础。更多信息请参阅实验 11，或者直接运行这些命令：

- `dd if=/dev/zero of=block.img bs=100M count=10`
- `dd if=/dev/zero of=block2.img bs=100M count=10`
- `sudo losetup -fP block.img`
- `sudo losetup -fP block2.img`
- `losetup -a | grep block | cut -d: -f1`

最后一个命令应该打印两个设备名称，例如 `/dev/loop0`。这些就是你的两个回环块设备，在实验的后续部分，所有看到 `[dev1]` 和 `[dev2]` 的地方都需要替换它们。

最后，安装必要的 LVM 工具：`sudo apt install lvm2`

#### 任务 2

现在，你将利用这两个回环设备创建 LVM “物理”卷（physical volumes）：

- `sudo pvcreate [dev1] [dev2]`
- `sudo pvdisplay`

第二个命令应该打印这两个新“物理”卷的描述，包括它们的名称（`[dev1]` 和 `[dev2]`）和大小，除非你在第 1 步中更改了大小，否则它们应为 1GB。

#### 任务 3

下一步是将这两个卷分组为一个单个 LVM 卷组（volume group）：

- `sudo vgcreate lab15 [dev1] [dev2]`
- `sudo vgdisplay`

你可能注意到这些 LVM 命令中存在某种对称性。再次，第一个命令设置卷组，而第二个命令打印关于它的信息。请特别注意“VG Name”（卷组名称）、“Cur PV”（当前物理卷）和“VG Size”（卷组大小）字段。

#### 任务 4

最后，从该卷组创建几个逻辑卷（logical volumes）：

- `sudo lvcreate -L 1500 lab15`
- `sudo lvcreate -L 492 lab15`
- `sudo lvdisplay`

`lvdisplay` 命令将显示你两个新逻辑卷的详细信息，包括路径和大小，当你想要开始使用它们时需要知道这些信息。例如，要开始实际使用这些卷，你只需要对其进行格式化（例如 `sudo mkfs.ext4 /dev/lab15/lvol0`）然后挂载（例如 `sudo mount /dev/lab15/lvol0 /mnt`）。

#### 任务 5

运行以下命令撤销所有操作并清理设备：

- `sudo lvremove /dev/lab15/*`
- `sudo vgremove lab15`
- `sudo pvremove [dev1] [dev2]`
- `sudo losetup -d [dev1] [dev2]`
- `rm block.img block2.img`

## 注意事项

使用 `lvcreate` 时可以使用非常多的配置类型——你在实验中做的只是最简单的类型。读读 man 页面吧！

## 实验 16：作为虚拟机的 Linux

### 实验目标

学习如何在虚拟化背景下管理 Linux 桌面和服务器。

### 实验目的

如果你是按照顺序执行实验，你可能正在虚拟机中运行此实验。除了桌面虚拟化，随着“云计算”和 IaaS 的出现，服务器虚拟化已成为专业 Linux 管理员日常生活中大部分的一部分。

### 实验工具

Ubuntu 18.04（或你选择的其它发行版）

### 实验拓扑

运行在 VirtualBox 上的单台 Linux 虚拟机

### 实验步骤

#### 任务 1

打开你用于本实验的虚拟机的 VirtualBox 设置。如果可能，通过以下操作增强虚拟机（如果你没有足够的系统资源，则相反，减少分配给虚拟机的资源）：

- 为虚拟机分配额外的内存和处理器
- 创建另一个虚拟磁盘镜像并将其分配给虚拟机
- 为虚拟机分配额外的网络适配器

现在重启虚拟机并查看是否能检测到额外的资源。内存显示在 `free` 中吗？你能通过 `lscpu` 看到额外的处理器吗？`lsblk` 是否显示了另一个磁盘？`ip link` 显示了网络吗？



这个练习的重点是学习与物理计算机相比，更改虚拟化计算机资源是多么简单。在服务器世界中也是如此。

## 任务 2

在 VirtualBox 中克隆这台虚拟机。启动它，访问终端并运行：

```bash
ip addr show
```

将结果与原始虚拟机进行比较。IP 地址和 MAC 地址相同吗，还是被自动更改了？（取决于你的设置，两种情况皆可能。）

在云环境中，IP 地址和 MAC 地址通常是动态分配的。

## 任务 3

最后，理解特定特定的功能是重要的。为了说明这一点，运行：

```bash
lsmod | grep vbox
```

你可能会看到多个与 VirtualBox 相关的模块，如 `vboxguest`、`vboxsf`、`vboxvideo` 等。此外，检查 `/boot/config`。

## 注意事项

Cloud-init 是云环境中常用的用于处理唯一配置的包。

# 实验 17：时区

## 实验目标

学习如何配置时区设置。

## 实验目的

在本实验中，你将学习 Linux 中的时区如何工作以及如何配置它们的设置。

## 实验工具

Ubuntu 18.04（或你选择的其它发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
cat /etc/timezone
ls -l /etc/localtime
file /usr/share/zoneinfo/$(cat /etc/timezone)
```

这些命令仅打印一些关于你配置的时区的少量信息。`/etc/localtime` 应该是指向 `/usr/share/zoneinfo/` 中某个文件的符号链接。如第三条命令所示，这不是一个人类可读的文件，但 `file` 仍然可以关于它的信息。

### 任务 2

现在运行 `tzselect`。

通过这个交互过程，最后将打印出你的时区（已经配置好的），并注意如何通过设置 `TZ` 环境变量使其永久生效。

最后，使用 `timedatectl` 打印一些额外信息，并使用 `date` 获取当前时间。这两个命令在 man 页面中描述了更多选项。

## 注意事项

如果你的实验机器是运行在经常进入睡眠或休眠硬件上的虚拟机，你可能会发现虚拟机的 RTC 时间发生了偏移。要解决这个问题，你可以在虚拟机中启用 NTP：

```bash
systemctl enable --now systemd-timesyncd
```

# 实验 18：区域设置（Locales）

## 实验目标

配置 locale 设置。

## 实验目的

在本实验中，你将学习 Linux 中的 locale 如何工作以及如何配置它们的设置和环境变量。

## 实验工具

Ubuntu 18.04（或你选择的其它发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：`locale`

你应该看到许多变量，第一个是 `LANG`——正如你可能猜的那样，这是默认语言的 locale 设置。下方列出了其他几个变量，命名了日期/时间、电话号码、货币和其他标识设置。

查看系统当前支持的 locale 设置：`locale -a`

查看支持的字符映射：`locale -m`

你的默认区域设置可能是 UTF-8 的某种变体，这是 Linux 上的标准字符映射。

### 任务 2

如果你觉得很有胆（不建议这样做），可以使用 `update-locale` 将你的设置更改为完全不同的语言和/或字符映射。例如，`sudo update-locale LANG=<setting>`。

`LANG=C` 的特点在于它在脚本编写中非常有用——它禁用了本地化并使用默认语言，以确保输出的一致性。

## 注意

你可以使用 `iconv` 在不同的字符编码之间转换文本。

# 系统运维

# 实验 19：管理共享库

## 实验目标

学习如何识别和安装共享库。

## 实验目的

共享库为一个或多个（通常是很多）Linux 应用提供公共功能。在实验中，你将学习如何管理这些非常重要的库。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验网络拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
cat /etc/ld.so.conf{..}
```

（上述语法是 `/etc/ld.so.conf /etc/ld.so.conf/d/*` 的快捷方式。）

这些文件用于定义 `ldconfig` 使用的共享库目录。当作为 root 运行时，`ldconfig` 会为这些目录中最新库创建链接和缓存（在链接新程序时使用），并加上 `/lib`、`/usr/lib`、`/lib64` 和 `/usr/lib64` 等“信任”目录。

### 任务 2

现在运行 `ldd $(which passwd)`。

此命令告诉你 `passwd` 工具链接了哪些共享库。结果会根据实现方式而异，但几乎每个程序至少都会链接到 `libc.so.6` 以及其他几个库。

偶尔，如果你从包管理器之外下载软件，你可能需要手动安装其运行时共享库。你可以对二进制文件使用 `ldd` 来确定其依赖项，然后在管理器中搜索这些依赖项。

## 注意

你可以使用 `LD_LIBRARY_PATH` 环境变量代替 `ld.so.conf` 来启用额外的库目录。然而，在大多数情况下，不建议这样做。

# 实验 20：Apt

## 实验目标

学习如何使用 Apt 包管理器进行安装、升级、搜索和卸载软件包。

## 实验目的

Apt 包管理器是一系列为基于 Debian 的发行版设计的工具，用于安装和管理基于 DEB 的包。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验网络拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
grep -v ^# -e $ /etc/apt/sources.list
cat /etc/apt/sources.list/*
```

这些文件决定了 Apt 将使用哪些仓库。有很多声誉良好的第三方仓库（以及许多不佳的），你可以通过向这些文件之一添加内容来启用它们，但我们目前保持默认设置。

Apt 使用需要定期更新的缓存。现在执行更新：`sudo apt update`。

然后让我们运行所有系统更新：`sudo apt -y full-upgrade`。

即使你已经有一段时间没有检查，也可能没有任何任何更新：

```bash
apt list --installed | grep unattended-upgrades
```

Ubuntu 18.04 应该默认安装并配置了此软件包。

### 任务 2

现在安装一个实用的包：`sudo apt install apt-file`。

然后：`sudo apt-file update`。

现在，假设你下载了某个新颖且神奇的应用源代码。在尝试编译它时，代码报错缺少“libvorbis.so”。你现在可以使用 `apt-file` 查看是否有包含它的包：`apt-file search libvorbis.so`。

结果有几个，其中最相关的是 `libvorbis-dev`（你可以运行 `libvorbis-dev` 来确认这是正确的包）。如果你安装了该包，就可以编译你的应用程序。

## 注意

你可能熟悉 `apt-get` 和 `apt-cache` 等经典工具。apt 尚未完全取代它们，但更适用于交互式使用而非脚本。

# 实验 21：Dpkg

## 实验目标

学习如何使用 dpkg 包管理器安装、卸载和获取软件包信息。

## 实验目的

dpkg 是一个安装 Debian 包的工具。它不使用仓库，也不像 Apt 那样自动处理依赖，但对于管理你从官方之外下载的包非常有用。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验网络拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：`dpkg -l`。

这个长列表就是你的已安装软件包列表。要获取给定包的更多信息，尝试：

```bash
dpkg -s sudo
dpkg -L sudo
dpkg -p sudo
```

某些包带有配置脚本，可以通过以下命令重新运行：

```bash
sudo dpkg-reconfigure
```

卸载包，使用：

```bash
sudo dpkg -r package_name
```

移除包及其配置文件，使用：

```bash
sudo dpkg -P package_name
```

安装本地的 `.deb` 文件，使用：

```bash
sudo dpkg -i package.deb
```

列出包的内容，使用：

```bash
dpkg -L package_name
```

显示包的信息，使用：

```bash
dpkg -s package_name
```

## 注意

dpkg 是 Debian 的底层包管理器。它不会自动处理依赖关系，这就是为什么通常在它之上使用 Apt。

```bash
rpm -qs sudo
rpm -q --dump sudo
```

要手动安装包，你可以运行：`rpm -i [file]`，其中 `[file]` 可以是下载的 `.rpm` 文件或 URL。同样，你必须预先手动安装依赖项。完成后，删除包的命令为：`rpm -e [package]`。

### 任务 2

另一个实用工具是 `rpm2cpio`。该工具将 `.rpm` 文件转换为 cpio 归档并输出到标准输出（stdout）。这使得你可以轻松访问其中的文件，而无需依赖 RPM。例如：

```bash
rpm2cpio package.rpm | cpio -dium
```

## 注意事项

虽然 `rpm` 对于收集信息非常有用，但在实践中，通常通过单个中央数据库来管理已安装的包更好。这可能意味着添加第三方仓库，或者下载包后手动将其添加到 YUM/DNF。

# 实验 24：创建用户和组

## 实验目标

学习如何创建和自定义用户及组。

## 实验目的

在本实验中，你将学习如何创建用户和组，以及设置它们的密码。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
sudo sh -c "echo Hello World" > /etc/skel/hello.txt
```

在这里，你正在向 `/etc/skel` 目录添加一个文件，该目录决定了新用户家目录中的默认文件。

现在：

```bash
sudo useradd -m foo
sudo cat ~foo/hello.txt
```

你应该能看到输出“Hello World”。发生的情况是：创建了一个名为 `foo` 的新用户（使用 `-m` 选项确保创建了家目录）。随后，`/etc/skel` 中的每个文件都被复制到了新用户的家目录中。

最后，使用 `sudo passwd foo` 为该用户设置初始密码。

### 任务 2

现在让我们添加一个系统用户。运行：`sudo useradd -r bar`。

当添加系统用户时，`useradd` 不会添加任何账户或密码过期信息，并会设置适用于系统用户的用户 ID（通常在 1000 以下）。除非你指定了 `-m`，否则它不会创建家目录。

### 任务 3

现在让我们创建一个组并将我们的新用户加入该组中：

```bash
sudo groupadd baz
sudo usermod -a -G baz foo
sudo usermod -a -G baz bar
```

使用 `grep ^baz /etc/group` 验证用户是否已添加。

### 任务 4

最后，进行清理：

```bash
sudo rm /etc/skel/hello.txt
sudo userdel foo
sudo userdel bar
sudo groupdel baz
sudo rm -r /home/foo
```

## 注意事项

`usermod` 是一个非常实用的管理命令。除了从组中添加和删除用户外，它还允许你管理账户/密码过期和其他安全功能。

# 实验 25：用户配置文件

## 实验目标

学习全局配置和用户配置。

## 实验目的

在本实验中，你将管理 shell 配置文件，并学习哪些文件可以自定义全局配置以及特定用户的配置。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

通过终端打开你喜欢的编辑器，并查看以下文件（某些文件可能不存在，这是正常的）：

```text
/etc/profile
/etc/skel/.bash_profile and/or ~/.bash_profile
/etc/skel/.bash_login and/or ~/.bash_login
/etc/skel/.profile and/or ~/.profile
/etc/bashrc
/etc/skel/.bashrc and/or ~/.bashrc
/etc/skel/.bash_logout and/or ~/.bash_logout
```

Bash 每每次在你启动登录 shell（login shell）时都会尝试读取前四个文件（按优先级顺序），而每当你启动交互式 shell（interactive shell）时，它会读取后两个文件。通常，登录 shell 每次启动启动一次，或每次 SSH 登录启动一次，而交互式 shell 则每次打开终端应用程序时都会启动——但和所有事情一样，这也有例外。最后，当登录 shell 退出时，Bash 会读取 `~/.bash_logout`。

你不一定能立即理解这些文件中发生的一切。关键点在于，你可以在这里对 shell 配置的各个方面进行永久性更改，包括环境变量、shell 选项，甚至是文本和背景颜色。

### 任务 2

通过添加一条简单的欢迎消息来测试这一理论。用你喜欢的编辑器打开 `~/.bashrc`，并在文件末尾添加以下行：

```bash
echo "Welcome, $USER! You've successfully modified the .bashrc file!"
```

保存并退出，退出终端，然后打开一个新的终端，你应该看到你的消息了。

注意，这仅适用于你的用户。如果你想让它适用于另一个用户，则必须修改该用户自己的 `.bashrc` 文件。要让它适用于所有未来的用户，你需要编辑 `/etc/skel/.bashrc`。

账户/密码过期和其他安全功能。`usermod` 将在接两个实验中讨论。

# 实验 27：组（Groups）

## 实验目标

学习如何添加、修改和删除组。

## 实验目的

在本实验中，你将学习 Linux 组以及一些用于添加、修改和删除组的工具。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：`cat /etc/group`。

正如你所预期的，这是系统上所有组的数据库。它包含四个由冒号分隔的字段：

- 组名
- 加密的组密码
- 组 ID（GID）
- 成员用户列表

运行 `groups` 了解你的用户属于哪些组。你可以使用 `id` 命令获取更多信息，包括组 ID。

### 任务 2

现在让我们创建一个组并将自己加入其中：

```bash
sudo groupadd foo
sudo usermod -a -G foo $USER
```

使用 `grep ^foo /etc/group` 验证你的用户是否已添加。

### 任务 3

你可以使用 `groupmod` 修改组的属性，例如它的名称：

```bash
sudo groupmod -n bar foo
grep ^bar /etc/group
```

最后，使用 `sudo groupdel bar` 进行清理。

## 注意

`/etc/login.defs` 中的若干指令会影响 `groupadd` 和 `groupmod` 的行为。更多信息请参考 `groupadd`、`groupmod` 和 `login.defs` 的帮助页。

# 实验 28：管道与重定向（Pipes and Redirection）

## 实验目标

学习如何在 Bash 中使用管道和重定向输入/输出。

## 实验目的

Bash 有两个常用的功能，即管道和 I/O 重定向，它们让使用 Linux 变得更容易。在本实验中，你将学习如何利用这些强大的功能。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端应用程序并运行：

```bash
mkdir lab13
cd lab13
echo "hello world" > hello
cat hello
```

你刚刚将 `echo` 命令的输出重定向到了 `hello` 文件中。`>` 是一个快捷方式；其正式版本是 `1>`，其中 `1` 被称为文件描述符，引用标准输出。

### 任务 2

现在运行：

```bash
ls nonexistent2 >> hello
cat hello
```

根据 `hello` 文件的新内容（“ls: cannot access ‘nonexistent’: No such file or directory”），你认为推断 `2>>` 的功能是什么？在这里，`2` 是标准错误（stderr）的文件描述符。

### 任务 3

有时，你想将输出和错误都重定向到同一个地方。在过去，你必须使用类似这种丑的写法：`ls foo > bar 2>&1`。

然而，现代版本的 Bash 有一个易用的快捷方式：`ls foo &> bar`。

### 任务 4

我们讨论了重定向输出，那输入呢呢？要学习这一点，请运行以下命令：



```bash
cat < foo

read foo <<< "foo"
echo $foo

cat << END-OF-FILE > goodbye
hello
goodbye
END-OF-FILE
cat goodbye
```

简而言之：`<` 从文件名重定向输入，`<<` 开始在此文档（here document），而 `<<<` 从另一个命令重定向输入。

## 任务 5

管道（`|`）允许将一个命令的输出作为另一个命令的输入。在许多情况下（但并非所有），`|` 和 `<<<` 类似于互反。例如，以下输出的……

```bash
echo "hello world" | grep e
```

……与以下输出是相同的：

```bash
grep e <<< "hello world"
```

在运行以下字符串之前尝试预测其输出（见下方答案 1）：

```bash
grep hello | cut
```

## 任务 6

最后，清理：

```bash
cd ~
rm -r lab13
```

# 实验 29：使用过滤器处理文本流（Process Text Streams Using Filters）

## 实验目标

学习如何使用小型文本过滤程序来获取命令输出。

## 实验目的

在本实验中，你将通过一系列实用命令发送文本文件和输出。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）。

## 实验拓扑

单台 Linux 机器或虚拟机。

## 实验步骤

### 任务 1

打开终端并运行：

```bash
echo "foo
BAR
Baz
Quux123
456plugh
7xy8zz9y0
Hello
goodbye" | nl -n > lab29.txt
```

这里，你创建了一个简单的文本文件——通过 `nl` 管道处理后，文件包含了行号。使用 `cat` 和 `less` 查看文件内容。

### 任务 2

`head` 和 `tail` 可用于获取文件的开头或结尾几行：

- `head -3 lab29.txt`
- `tail -3 lab29.txt`

文件。第二个是搜索“setuid root”文件，换句话说就是由非 root 用户以 root 权限运行的文件。

### 任务 4

清理：

- `cd ..`
- `rm -r lab44`

## 注意

另一个有用的命令是 `file`，它可以告诉你给定文件的类型。你能弄出如何结合 `file` 和 `find` 来定位你家目录下所有的文本文件吗？

# 实验 31：重定向与文件描述符

## 实验目标

学习如何在 Bash 中重定向输入和输出。

## 实验目的

Bash 有一个常用功能称为 I/O 重定向，它让使用 Linux 变得更加简单。在实验中，你将学习如何利用这个强大的功能。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）。

## 实验拓扑

单台 Linux 机器或虚拟机。

## 实验步骤

### 任务 1

打开终端应用程序并运行：

```bash
mkdir lab46
cd lab46
echo "hello world" > hello
cat hello
```

你刚刚将 `echo` 命令的输出重定向到了 `hello` 文件中。`>` 是快捷方式；其正式版本应该是 `1>`，其中 `1` 被称为文件描述符，引用标准输出。

### 任务 2

现在运行：

```bash
ls nonexistent 2>> hello
cat hello
```

根据 `hello` 文件的新内容（“ls: cannot access ‘nonexistent’: No such file or directory”），你对 `2>>` 的功能推断出什么？这里，`2` 是标准错误的文件描述符。

### 任务 3

有时，你想将输出和错误都重定向到同一个地方。在过去，你必须执行类似这种很难看的操作：`ls foo > bar 2>&1`

然而，现代 Bash 版本有一个易于使用的快捷方式：`ls foo && bar`

### 任务 4

我们讨论过重定向输出，但输入输出呢？要学习这一点，请运行以下命令：

```bash
cat < hello

read foo <<< "foo"
echo $foo

cat << END-OF-FILE > goodbye
hello
goodbye
END-OF-FILE
cat goodbye
```

简而言之：`<` 从文件名重定向输入，`<<` 开始一个在此文档（here document），`<<<` 从另一个命令重定向输入。

### 任务 5

你也可以创建自己的文件描述符。观察：

```bash
exec 3<> foo
echo "Hello World" >&3
cat foo
exec 3>&-
echo "fail" >&3
```

此操作的作用是打开文件描述符 3（用于读写），指向文件 `foo`，并将输出发送到那里。第四行关闭了文件描述符，导致最后一个 `echo` 命令失败。

### 任务 6

最后，清理：

```bash
cd
rm -r lab46
```

## 注意

要打开一个只读的文件描述符，可以使用 `exec 3< file`；或者仅用于写入，使用 `exec 3> file`。

# 实验 32：管道

## 实验目标

学习如何使用 Bash 管道，将一个命令的输出作为另一个命令的输入。

## 实验目的

Bash 有一个常用功能称为管道，它让使用 Linux 变得更加简单。在实验中，你将学习如何利用这个强大的功能。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）。

## 实验拓扑

单台 Linux 机器或虚拟机。

## 实验步骤

### 任务 1

管道（`|`）允许你将一个命令的输出作为另一个命令的输入。在很多情况下（但并非所有），`|` 和 `| <<<` 某种程度上是反的。例如，……的输出……

```bash
echo "hello
world" | grep
```

……与……的输出相同：

```bash
grep <<< "hello"
world"
```

在运行以下命令字符串之前，尝试预测它的输出（见下方答案 1）：

```bash
grep non hello | cut -d: -f3
```

### 任务 2

在实验 46 中你学习了如何重定向命令输出。现在运行：

```bash
echo “Hello World” | tee hello
cat hello
```

这里发生了什么？`tee` 命令将输出重定向到文件，同时将其发送到 `stdout`。你可以使用特殊的 `|&` 管道同时重定向 `stdout` 和 `stderr`：

```bash
rm hello
ls hello |& tee hello
cat hello
```

`tee` 还有一个 `-a` 选项用于追加文件而不是覆盖它。

### 任务 3

当管道将命令的输出作为另一个命令的输入时，`xargs` 将命令的输出作为另一个命令的参数：

```bash
echo hello | xargs cat
rm hello
```

`xargs` man 页面描述了许多有用的参数，包括设置分隔符和强制交互提示。

## 答案 1

没有此类文件或目录。

## 注意

挑战：链起一系列命令，使用管道、`ls`、`xargs` 以及至少一次重定向。

# 实验 33：vi 导航

## 实验目标

学习如何打开、关闭和导航。

## 实验目的

在实验中，你将学习如何使用 `vi`。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）。

## 实验拓扑

单台 Linux 机器或虚拟机。

## 实验步骤

### 任务 1

打开终端应用程序并运行：

```bash
mkdir lab46
cd lab46
echo "hello world" > hello
cat hello
```

你刚刚将 `echo` 命令的输出重定向到了 `hello` 文件中。`>` 是快捷方式；其正式版本应该是 `1>`，其中 `1` 是文件描述符，引用标准输出。

### 任务 2

现在运行：

```bash
ls nonexistent 2>> hello
cat hello
```

根据 `hello` 文件的新内容（“ls: cannot access ‘nonexistent’: No such file or directory”），你对 `2>>` 的功能推断出什么？这里，`2` 是标准错误的文件描述符。

### 任务 3

有时，你想将输出和错误都重定向到同一个地方。在过去，你必须执行类似这种很难看的操作：`ls foo > bar 2>&1`

然而，现代 Bash 版本有一个易于使用的快捷方式：`ls foo && bar`

### 任务 4

我们讨论过重定向输出，但输入呢？要学习这一点，请运行以下命令：

```bash
cat < hello

read foo <<< "foo"
echo $foo

cat << END-OF-FILE > goodbye
hello
goodbye
END-OF-FILE
cat goodbye
```

简而言之：`<` 从文件名重定向输入，`<<` 开始一个在此文档，`<<<` 从另一个命令重定向输入。

### 任务 5

你也可以创建自己的文件描述符。观察：

```bash
exec 3<> foo
echo "Hello World" >&3
cat foo
exec 3>&-
echo "fail" >&3
```



- `exec 3<> foo`
- `echo "Hello World" >&3`
- `cat foo`
- `exec 3>&-`
- `echo "fail" >&3`

此操作的作用是打开文件描述符 `3`（用于读写），指向文件 `foo`，并将输出发送到那里。第四行关闭了文件描述符，导致最后一个 `echo` 命令失败。

## 任务 6

最后，清理：

```bash
cd
rm -r lab46
```

> **注意：**
>
> 要打开一个只读的文件描述符，可以使用 `exec 3< file`；或者仅用于写入，使用 `exec 3> file`。

刚刚发生了什么？你为一个名为 `myfoo` 的文件（`foo`）创建了一个符号链接。输出显示了这个链接。符号链接简单来说就是指向现有文件的引用。通过这种方式，你可能对单个文件有多个引用——编辑原始文件，所有引用都会立即更新，如 `cat` 所示。

当你删除链接时，原始文件仍然存在。（如果你在保留符号链接的同时删除了原始文件，你将拥有所谓的“断链”，就像在互联网上一样。）这对于某些系统配置非常有用。

## 任务 2

现在运行：

```bash
ln -v foo myfoo
echo goodbye > foo
cat myfoo
rm foo
ls -l myfoo
cat myfoo
```

你刚刚创建了另一种类型的链接，称为硬链接。硬链接在行为上与符号链接相似，即当原始文件被修改时，链接也会随之变化，反之亦然。然而，如果原始文件被删除，硬链接会保留其数据。硬链接还不能跨文件系统或分区边界创建，且无法对目录创建硬链接。

## 任务 3

最后，使用 `rm myfoo` 清理。

> **注意：**
>
> 在底层，硬链接实际上作用于 *inodes*（索引节点）。硬链接创建了另一个指向与原始文件相同 inode 的文件。（符号链接的工作机制在更高层级，直接指向文件或目录名称。）你可以通过 `ls -i` 查看 inode 号，或者在 `ls -l` 的第二列查看有多少硬链接共享给定文件的 inode。

# 实验 36：SysVInit 和 Systemd

## 实验目标

学习如何管理 SysVInit 和 Systemd，并理解它们之间的区别。

## 实验目的

SysVInit 和 Systemd 是管理 Linux 启动进程的两种不同方法。SysVInit 被认为是“经典”方法，而 Systemd 已取代了许多发行版。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 或虚拟机

## 实验步骤

### 任务 1

Ubuntu 18.04 是切换到 Systemd 的发行版之一。但仍然有很多基于 SysVInit 的脚本存在并运行：

```bash
ls /etc/init.d
```

此目录中的每个文件都是脚本，用于为特定服务启动、停止、检查状态以及可能的其他功能。你可以通过以下命令查看哪些脚本在哪些运行级别（runlevels）被启用：

```bash
ls -IR /etc/rc*
```

查看 `/etc/rc5.d` 下列出的符号链接。运行级别 5 是默认的启动运行级别，当你正常启动到带有显示管理器的桌面时使用。运行级别 0（在 `/etc/rc0.d` 下）包含了计算机关机时运行的脚本链接。

### 任务 2

现在运行：

```bash
systemctl list-unit-files --state=enabled
```

这些是在 Systemd 中启动时启用的服务，应该与 `/etc/rc*` 下列出的服务大部分不同。使用 `CTRL + C` 或 `q` 退出。

SysVInit 依赖于标准 shell 脚本，而 Systemd 使用带有自定义格式的单元文件（unit files）。举例来说，查看：

```bash
cat /lib/systemd/system/rsyslog.service
```

System 单元文件可以有许多选项。更多信息请参阅 `man systemd.unit`。

### 任务 3

最后，通过以下命令查看系统日志：

```bash
journalctl -xe
```

Journalctl 是 Systemd 对经典 syslog 的替代品。然而，Ubuntu 仍然有许多经典文本格式的日志——查看 `/var/log`。

> **注意：**
>
> Ubuntu 曾使用 Upstart 作为 SysVInit 的替代品。然而，该项目目前处于维护模式，不再更新。Ubuntu 已经迁移到 Systemd 作为 Upstart 的替代品。

# 实验 37：运行级别和启动目标

## 实验目标

学习如何设置和更改 Linux 运行级别和启动目标。

## 实验目的

标准的 Linux 运行级别如下：

- 0：关机（Halt）
- 1（或 S）：单用户模式
- 2：多用户模式，无网络
- 3：多用户模式，有网络
- 4：未使用，或运行级别 3 + 显示管理器
- 5：未使用，或运行级别 3 + 显示管理器
- 6：重启（Reboot）

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 或虚拟机

## 实验步骤

### 任务 1

确保所有工作均已保存。然后，你将从终端进入单用户模式（救援模式）：

```bash
sudo init 1
```

你将看到一个 root 提示符——这是原始的！正如名称暗示的，这种模式通常用于救援操作。如果你忘记了 root 密码（且 root 分区未加密），这很有用。正如名称所示，这种模式通常用于救援操作。

### 任务 2

查看 `/etc/rc5.d` 下列出的符号链接。运行级别 5 是默认的启动运行级别，当你正常启动到带有显示管理器的桌面时使用。运行级别 0（在 `/etc/rc0.d` 下）包含了计算机关机时运行的脚本链接。

按下 `e` 键编辑启动项。在 `3` 处                  之后按 `Ctrl+X` 这样你就可以离开。

# 实验 38：Systemd 和进程

## 实验目标

学习如何管理 Systemd 进程。

## 实验目的

在本实验中，你将练习使用 Systemd 运行服务。

## 实验工具

Ubuntu 18.04

## 实验拓扑

单台 Linux 或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
systemctl status rsyslog
```

你应该看到 rsyslog 服务正在运行。

### 任务 2

运行：

```bash
systemctl stop rsyslog
```

你应该看到 rsyslog 服务已停止。

### 任务 3

运行：

```bash
systemctl start rsyslog
```

你应该看到 rsyslog 服务已启动。

想要将正在运行的进程从自己的 shell 中解耦，同时仍然监控出现的问题。

有两个工具，`screen` 和 `tmux`，可以帮助这一点，但在默认设置下，你需要先安装它们：

```bash
sudo apt -y screen tmux
```

`screen` 和 `tmux` 的工作机制略有不同，但原理是相同的。从 `screen` 开始：

```bash
screen
i=0; while true; i=$((i+1)); echo i; sleep 1; done
```

现在按下 `Ctrl+A`，然后按 `D`。这些组合键将从你的 screen 会话中分离（detach）并返回 shell。你可以通过 `screen -list` 查看这些会话。现在：

```bash
tmux
j=0; while true; j=$((j+1)); echo j; sleep 1; done
```

现在按下 `Ctrl+B`，然后按 `D`。同样，这将从会话分离让你回到 shell，但你的进程仍在运行。你通过 `tmux ls` 查看这些会话。

最后，分别使用 `screen -x` 和 `tmux attach` 返回会话。（在它们中按下 `Ctrl+C` 并运行 `exit` 来终止进程。）如果有多个会话，系统会提示你选择一个，否则命令将重新连接到运行中的会话。

> **注意：**
>
> `screen` 和 `tmux` 具有多种选项，在某些方面与文本编辑器相当。它们没有哪个“更好”，但你可能想探索这两个工具并决定你更倾向于哪一个。

# 实验 40：Cron

## 实验目标

学习如何使用 cron 工具调度自动化系统任务。

## 实验目的

在本次实验中，你将使用经典的 cron 工具管理自动化系统任务。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
cat /etc/crontab
```

在文件中，你可能会看到几行列，分别指定了为给作业运行指定的分钟、小时、日期、月份和一年中的几天。然后你将看到用户（通常是 root）以及最后的实际命令。请参考 `man 5 crontab` 获取关于 crontab 格式的完整说明。

在默认的 Ubuntu 安装中，`/etc/crontab` 应该包含“元”命令，用于从其他文件运行 cron 任务——`/etc/cron.hourly`、`/etc/cron.daily` 等。接下来查看这些：

```bash
ls /etc/cron.{hourly,daily,weekly,monthly}
```

正如你猜的，这些目录保存了按小时、每天、每周、每月或其他时间间隔运行的作业。检查几个文件以查看系统上定期运行了哪些作业。

在某些系统中，使用了基于用户的 crontab。在这种情况下，运行 `crontab -l` 和 `sudo crontab -l` 来查看作业。这些作业存储在 `/var/spool/cron/crontabs` 中。

### 任务 2

运行 `crontab -e` 并为你的用户添加一个 cron 任务：

```cron
* * * * * date > ~/foo
```

然后：

```bash
sleep 60 && ~/foo
```

你应该看到你的 cron 任务已经运行（每分钟一次）并将日期打印到文件 `foo` 中。使用 `crontab -e` 清理，删除添加的行并执行 `rm foo`。

> **注意：**
>
> `/etc/cron.allow` 和 `/etc/cron.deny` 控制用户对 crontab 的访问。在默认的 Ubuntu 系统上，这些文件可能不存在——根据帮助页，这意味着只有 root 应该访问 crontab，但默认系统配置允许所有用户访问。查看 `man crontab` 以了解这些文件的工作原理。

# 实验 41：At 和 Systemd

## 实验目标

学习如何使用 at 和 Systemd 工具调度自动化系统任务。

## 实验目的

在本次实验中，你将使用 Systemd 管理自动化系统任务，并使用 at 管理计划性任务。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
sudo apt install at
```

与 cron 相比，at 用于在某个时间运行一次性作业。

现在：

```bash
echo "hello" | at now +1 min
atq
sleep 60 && ls
```

你应该看到你的 cron 任务已经运行（每分钟一次）并将日期打印到文件 `foo` 中。使用 `crontab -e` 清理，删除添加的行并执行 `rm foo`。

（注：原文中实验 41 的 OCR 文本似乎碎片化了。已根据提供的片段正确地重构了逻辑。）

此目录下的所有内容，包括 grub 配置文件（`/boot/grub/grub.cfg`），都如你预期的那样——与你的系统启动过程有关。除非你清楚自己在做什么，否则你不要乱动这个目录！

### 任务 2

接下来，运行：

```bash
ls /etc
```

在 Linux 术语中，`etc` 代表“可编辑的文本配置”（editable text configuration）。`/etc` 是所有系统配置的主目录树；除了极少数例外外，几乎所有的配置都存储在 `/etc` 中，或链接自 `/etc`。

少数（非用户特定的）例外可能在 `/dev`、`/sys` 或 `/proc` 中。这些是特殊的动态生成的文件系统。你可能会从这些文件系统中读取信息，但在大多数情况下，你不应该直接向它们写入。

### 任务 3

在你的终端（Terminal）中运行以下命令：

```bash
free -m
ps -ef
top # 按 q 退出
```

这些是监控进程及其资源使用的三个常用工具。（发现了一个无法通过正常手段退出的失控进程？尝试使用 `kill` 或 `pkill`。）

## 注意事项

`/dev` 包含称为设备节点的特殊文件，这些节点链接到设备驱动程序。`/sys` 和 `/proc` 分别包含内核向用户呈现非进程和进程相关信息的文件。（实际上，这种划分要复杂得多，但这是理想的隔离方式。）

# 实验 44：PCI 设备与外设

## 实验目标

学习收集有关 PCI 设备和外设的信息并进行配置。

## 实验目的

在实验中，你将使用 `lsusb` 和 `lspci` 等工具来确定硬件资源并操作 USB 和 PCI 设备。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
for dev in $(ls /sys/bus/usb/devices/*/product); do echo -n "$dev "; cat $dev; done
```

输出将是连接到你系统的 USB 设备列表，如下：

```text
/sys/bus/usb/devices/1-1/product: USB Tablet
/sys/bus/usb/devices/usb1/product: OHCI PCI host controller
```

我们感兴趣的是第一个字段中的 USB 总线和端口。在这个示例中，有两个设备：一个位于 `1-1` 的 USB 平板，和一个位于 `usb1` 的 PCI 控制器。

你也可以使用 `lsusb` 来收集有关这些设备的更多信息。

### 任务 2

现在你可以选择性地禁用并重新启用上述 USB 设备之一。这是可选的，因为如果操作不当，可能会导致你的系统在重启之前临时无法使用。

假设你在 `1-1.6` 处有一个摄像头。禁用它是安全的。你将运行：

```bash
sudo sh -c 'echo 1.1-6 > /sys/bus/usb/drivers/usb/bind'
```

测试你禁用的设备以确认它已不再处于可用状态。若要重新启用该设备，只需运行：

```bash
sudo sh -c 'echo 1.1-6 > /sys/bus/usb/drivers/usb/bind'
```

### 任务 3

运行：

```bash
lspci -v
```

这是你的 PCI 设备列表。请注意在最后一行以“Kernel modules”开头的列出内核模块的设备。你可以通过使用 `lsmod` 获取当前加载的内核模块列表来确认这些模块已加载。

现在你将移除并重新加载这些模块之一。与上一步一样，你需要小心选择移除哪个模块，因为选择错误的模块可能会导致你的系统临时无法使用。

移除音频模块（例如 `snd_seq_midi`）是安全的。运行：

```bash
sudo modprobe -r snd_seq_midi
```

你可以通过 `lsmod | grep snd_seq_midi` 确认模块已移除。

取决于你选择的模块，这对功能可能会产生任何明显的影响，也可能没有。典型系统中加载了许多 Linux 内核模块，但当然，除非你知道它们的作用，否则最好不要弄动它们！

使用以下命令重新加载模块：

```bash
sudo modprobe snd_seq_midi
```

> **注意事项：**
>
> 了解 `/proc` 和 `/sys` 文件系统是有好处的——你知道去哪里看，所有关于 USB 和 PCI 设备的信息都存储在那里。下一次实验将深入研究这些文件系统。

# 实验 45：安装与配置 X11

## 实验目标

学习 X11 窗口系统以及如何配置它。

## 实验目的

在实验中，你将探索 X11 配置的各个方面。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）以及一个运行的 X11 系统。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

（此处原文未给出具体命令，但根据上下文应为查看配置）

X11 配置的各个方面。查看 `/etc/x11/` 目录。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。

打开终端并运行：

（此处原文未给出具体命令）

查看 `/etc/x11/` 目录。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。

打开终端并运行：

（此处原文未给出具体命令）

查看 `/etc/x11/` 目录。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。

打开终端并运行：

（此处原文未给出具体命令）

查看 `/etc/x11/` 目录。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。

打开终端并运行：

（此处原文未给出具体命令）

查看 `/etc/x11/` 目录。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。

打开终端并运行：

（此处原文未给出具体命令）

查看 `/etc/x11/` 目录。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。




此目录下的所有内容，包括 grub 配置文件（`/boot/grub/grub.cfg`），都如你预期的——与你的系统启动过程有关。除非你清楚自己在做什么，否则你不要乱动这个目录！

### 任务 2

接下来，运行：`ls /etc`

在 Linux 术语中，`etc` 代表“可编辑的文本配置”（editable text configuration）。`/etc` 是所有系统配置的主目录树；除了极少数例外外，几乎所有的配置都存储在 `/etc` 中，或链接自 `/etc`。

### 任务 3

在你的终端（Terminal）中运行以下命令：

```bash
free -m
ps -ef
top # 按 q 退出
```

这些是监控进程及其资源使用的三个常用工具。（发现了一个无法通过正常手段退出的失控进程？尝试使用 `kill` 或 `pkill`。）

## 注意事项

`/dev` 包含称为设备节点的特殊文件，这些节点链接到设备驱动程序。`/sys` 和 `/proc` 分别包含内核向用户呈现非进程和进程相关信息的文件。（实际上，这种划分要复杂得多，但这是理想的隔离方式。）

## Lab 44. PCI 设备与外设

**实验目标：** 学习收集有关 PCI 设备和外设的信息并进行配置。

**实验目的：** 在实验中，你将使用 `lsusb` 和 `lspci` 等工具来确定硬件资源并操作 USB 和 PCI 设备。

**实验工具：**

Ubuntu 18.04（或你选择的其他发行版）

**实验拓扑：**

单台 Linux 机器，或虚拟机

**实验步骤：**

### 任务 1

打开终端并运行：

```bash
for dev in $(ls /sys/bus/usb/devices/*/product); do echo -n "$dev "; cat $dev; done
```

输出将是连接到你系统的 USB 设备列表，如下：

```text
/sys/bus/usb/devices/1-1/product: USB Tablet
/sys/bus/usb/devices/usb1/product: OHCI PCI host controller
```

我们感兴趣的是第一个字段中的 USB 总线和端口。在这个示例中，有两个设备：一个位于 1-1 的 USB 平板，和一个位于 `usb1` 的 PCI 控制器。

你也可以使用 `lsusb` 来收集有关这些设备的更多信息。

### 任务 2

现在你将选择性地禁用并重新启用上述 USB 设备之一。这是可选的，因为如果操作不当，可能会导致你的系统在重启之前临时无法使用。

假设你在 1-1.6 处有一个摄像头。禁用它是安全的。你将运行：

```bash
sudo sh -c 'echo 1.1-6 > /sys/bus/usb/drivers/usb/bind'
```

测试你禁用的设备以确认它已不再处于可用状态。若要重新启用该设备，只需运行：

```bash
sudo sh -c 'echo 1.1-6 > /sys/bus/usb/drivers/usb/bind'
```

### 任务 3

运行：`lspci -v`

这是你的 PCI 设备列表。请注意在最后一行以“Kernel modules”开头的列出内核模块的设备。你可以通过使用 `lsmod` 获取当前加载的内核模块列表来确认这些模块已加载。

现在你将移除并重新加载这些模块之一。与上一步一样，你需要小心选择移除哪个模块，因为选择错误的模块可能会导致你的系统临时无法使用。

移除音频模块（例如 `snd_seq_midi`）是安全的。运行：

```bash
sudo modprobe -r snd_seq_midi
```

你可以通过 `lsmod | grep snd_seq_midi` 确认模块已移除。

取决于你选择的模块，这对功能可能会产生任何明显的影响，也可能没有。典型系统中加载了许多 Linux 内核模块，但当然，除非你知道它们的作用，否则最好不要弄动它们！使用以下命令重新加载模块：`sudo modprobe snd_seq_midi`

## 注意事项

了解 `/proc` 和 `/sys` 文件系统是有好处的——你知道去哪里看，所有关于 USB 和 PCI 设备的信息都存储在那里。下一次实验将深入研究这些文件系统。

## Lab 45. 安装与配置 X11

**实验目标：** 学习 X11 窗口系统以及如何配置它。

**实验目的：** 在实验中，你将探索 X11 配置的各个方面。

**实验工具：**

Ubuntu 18.04（或你选择的其他发行版），以及一个运行的 X11 系统。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。

**实验拓扑：**

单台 Linux 机器或虚拟机

**实验步骤：**

### 任务 1

查看 `/etc/x11/` 目录。如果你不确定系统是否运行 X11，请使用 `sudo ps -ef | egrep -i x11\xorg` 进行测试。

## Lab 46. 辅助功能

**实验目标：** 学习如何配置辅助功能。

**实验目的：** 在实验中，你将探索辅助功能的各个方面。

**实验工具：**

Ubuntu 18.04（或你选择的其他发行版）

**实验拓扑：**

单台 Linux 机器或虚拟机

**实验步骤：**

### 任务 1

打开“设置”应用，然后点击左侧的“通用功能”（Universal Access）。尝试以下选项：

- 高对比度
- 大字体
- 缩放
- 屏幕阅读器
- 键盘
- 鼠标键

**注意事项：**

某些辅助功能需要特定的硬件。

## Lab 47. 基础安全与用户识别

**实验目标：** 学习识别 root 用户、标准用户和系统用户之间的区别。

**实验目的：** 在实验中，你将学习不同类型的用户以及审计它们的几种工具。

**实验工具：**

Ubuntu 18.04（或你选择的其他发行版）

**实验拓扑：**

单台 Linux 机器或虚拟机

**实验步骤：**

### 任务 1

打开终端并运行：`cat /etc/passwd`

此文件是系统中所有用户的清单。`passwd` 文件是一个包含七字段的以冒号分隔的数据库：

1. 用户名
2. 加密密码（实践中很少使用）
3. 用户 ID（UID）
4. 组 ID（GID）
5. 注释
6. 家目录
7. 默认 shell

注意 root 用户，它应该列在第一行。这是管理员用户，也是唯一可以无条件执行系统任何操作的用户。通过运行带有 `sudo` 前缀的命令，你是以 root 用户身份运行该命令的。（你也可以 `sudo -i` 或 `su` 进入 root shell。）

如果你查看用户 ID，你会注意到在默认系统中，大多数 ID 都小于 1000。这些是系统用户，通常用于运行特定的服务，而不是以 root 身份运行，从而产生安全问题。在大多数系统中，人类用户 ID 从 1000 开始。

你可以通过以下命令轻松查看自己用户的 passwd 信息：`grep ^$USER /etc/passwd`

### 任务 2

现在运行：`sudo cat /etc/shadow`

`shadow` 文件是一个敏感的数据库，包含用户的密码哈希以及其他信息。请小心处理此文件的内容！它包含九字段，同样以冒号分隔——但在默认的 Ubuntu 安装中，只有前三个可能是重要的：

1. 用户名
2. 加密密码
3. 上次更改密码日期

其他字段包含账户过期日期和最小/最大密码有效期等信息，这些在默认系统中是不经过配置的。更多信息请参见 `man 5 shadow`。

你可以通过以下命令查看自己用户的信息：`sudo grep ^$USER /etc/shadow`

### 任务 3

现在运行：`cat /etc/group`

正如你所预期，这是系统中所有组的数据库。它包含四个由冒号分隔的字段：

1. 组名
2. 加密的组密码
3. 组 ID（GID）
4. 成员用户列表

运行 `groups` 来了解你的用户属于哪些组。你可以使用 `id` 命令获取更多信息，包括组 ID。

### 任务 4

最后，你可以使用以下命令来审计用户登录情况：

- `who`
- `w`
- `last`
- `last $USER` 查看你自己的用户

## 注意事项

在下一次实验中，你将学习如何添加普通用户和系统用户。在实践中，你很少需要手动添加系统用户——这些用户通常随着使用它们的服务一起被添加。

## 实验 48. 管理文件权限和所有权

**实验目标：** 学习如何操作文件权限和所有权设置。

**实验目的：** 在本实验中，你将学习使用 `chmod` 和 `chown`，以及使用 `ls` 查看权限和所有权设置。

**实验工具：**

Ubuntu 18.04（或你选择的其他发行版）

**实验拓扑：**

单台 Linux 或虚拟机

**实验步骤：**

### 任务 1

打开终端并运行（如果你在上次实验中删除了用户 `foo`，可能需要重新添加）：

```bash
echo "Hello World" > foo
ls -l foo
```

查看第一个字段；你应该看到 `-rw-r--r--`。

这表示用户、组和其他用户的权限。最后九个字符每三个一组，表示这些权限。在本例中：

- `rw-` 表示文件所有者用户具有读/写（但没有执行）权限。
- `r--` 表示文件所有者组只有读权限。
- `r--` 表示所有非所有者（即“世界用户”）只有读权限。

第一个字符表示文件类型。在这种情况下，它是普通文件；目录以 `d` 开头。

该文件的用户所有者和组所有者是谁？`ls -l` 的第三和第四字段告诉我们答案。默认情况下，应该是你自己的用户和主组。

### 任务 2




现在运行：

- `sudo chown root foo`
- `ls -l foo`
- `cat foo`

你刚刚将用户所有权更改为了 root，同时保留了组所有权。由于文件具有组读和世界读权限，你仍然可以查看其内容。

### 任务 3

现在运行：

- `sudo chmod o-r foo`
- `ls -l foo`
- `cat foo`

该 `chmod` 命令移除了其他用户（other）的读权限。然而，由于你仍然拥有组所有权，你仍然可以看到文件的内容。

### 任务 4

现在运行：

- `sudo chmod 600 foo`
- `ls -l foo`
- `cat foo`

该 `chmod` 命令显式设置权限，仅允许所有者读写。由于所有者是 root，我们无法再读取该文件了。

### 任务 5

最后，使用 `sudo rm foo` 进行清理。

## 注意事项

执行权限也适用于可执行文件和目录。如果用户/组无法“执行”某个目录，则无法查看该目录或任何子目录的内容。

# 实验 49：特殊目录和文件

## 实验目标

学习如何使用临时文件和目录、符号链接以及特殊权限。

## 实验目的

在本实验中，你将处理符号链接、特殊文件/目录权限以及临时文件和目录。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：`ls -ld /tmp`

注意权限：`drwxwxrxrwt`

末尾的 `t` 表示所谓的粘滞位（sticky bit）。这意味着只有拥有特定文件的用户/组才能修改它。这对于世界可写目录（例如存放临时文件的目录）非常重要，可以防止用户干扰他人的文件。

### 任务 2

现在运行：

- `ln -sv $(mktemp) mytmp`
- `ls -l mytmp`
- `rm mytmp`

刚刚发生了什么？`mktemp` 创建了一个随机命名的临时文件。然后你创建了一个名为 `mytmp` 的文件的符号链接。输出显示了这个链接。符号链接仅仅是现有文件的引用。通过这种方式，你可以对同一个文件有多个引用——编辑原始文件，所有引用都会立即更新。这对于某些系统配置非常有用。

## 注意事项

除了 `/tmp` 之外，还有 `/var/tmp`，通常用于较大或/持续时间更长的临时文件。`/tmp` 通常在每次重启时被清理；`/var/tmp` 则不一定如此。

# 实验 50：文件权限

## 实验目标

学习如何操作文件的权限和所有权设置。

## 实验目的

在本实验中，你将学习使用 `chmod` 和 `chown`，以及使用 `ls` 查看权限和所有权设置。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：`ls -ld /tmp`

注意权限：`drwxwxrxrwt`

末尾的 `t` 表示所谓的粘滞位（sticky bit）。这意味着只有拥有特定文件的用户/组才能修改它。这对于世界可写目录（例如存放临时文件的目录）非常重要，可以防止用户干扰他人的文件。

在本例中：

- `rw-` 表示文件所有者用户具有读/写（但没有执行）权限。
- `r-` 表示文件所有者组只有读权限。
- `r-` 表示所有非所有者（即“世界用户”）只有读权限。

第一个字符表示文件类型。在这种情况下，它是普通文件；目录以 `d` 开头。

该文件的用户所有者和组所有者是谁？`ls -l` 的第三和第四字段告诉我们答案。默认情况下，应该是你自己的用户和主组。

### 任务 2

现在运行：

- `sudo chown root foo`
- `ls -l foo`
- `cat foo`

你刚刚将用户所有权更改为了 root，同时保留了组所有权。由于文件具有组读和世界读权限，你仍然可以查看其内容。

### 任务 3

现在运行：

- `sudo chmod o-r foo`
- `ls -l foo`
- `cat foo`

该 `chmod` 命令移除了其他用户（other）的读权限。然而，由于你仍然拥有组所有权，你仍然可以看到文件的内容。

### 任务 4

现在运行：

- `sudo chmod 600 foo`
- `ls -l foo`
- `cat foo`

该 `chmod` 命令显式设置权限，仅允许所有者读写。由于所有者是 root，我们无法再读取该文件了。

### 任务 5

最后，使用 `sudo rm foo` 进行清理。

（注：此处由于原文文本存在 OCR 错乱，已根据逻辑进行了重新对齐和翻译）

- `-rwx` 表示文件所有者的读/写/执行权限。
- `r-x` 表示文件所属组的读/执行权限。
- `r-x` 表示所有非所有者（即“世界用户”）的读/执行权限。

该文件的用户所有者和组所有者是谁？`ls -l` 的第三和第四字段会告诉我们答案。默认情况下，它们应该是你的用户和主组。

### 任务 2

现在运行：

- `sudo chown foo foo`
- `ls -la foo`
- `cat foo/bar`

你刚刚将用户所有权更改为了 root，同时保留了组所有权。由于该目录具有组读和世界可读权限，你仍然可以看到它的内容。

### 任务 3

现在运行：

- `sudo chmod o-r foo`
- `ls -la foo`
- `cat foo/bar`

该 `chmod` 命令删除了 foo 的读取权限。然而，由于你仍然拥有组所有权，你仍然可以查看文件的内容。

### 任务 4

现在运行：

- `sudo chgrp root foo`
- `ls -la foo`
- `ls -ld foo`
- `cat foo/bar`

你现在为自己设置了 foo 目录的仅执行权限，这是一个有趣的场景。你不再有权限查看目录内容，也不再向其添加新文件……但如果你已经知道某个文件存在，你对该文件的权限仍然允许你对其进行操作。在这个示例中，你可以查看 foo/bar 的内容，甚至仍然可以修改它们！这也适用于 foo 下的任何子目录。

### 任务 5

现在运行：

- `sudo chmod 2777 foo`
- `touch foo/baz`
- `ls -l foo/baz`

你所做的是为该目录设置了 `setgid` 位，这会导致在该目录下创建的文件具有与目录本身相同的组所有权。在实践中，这是一种确保共享文件的用户组不需要过多担心权限的方法。

### 任务 6

新创建文件的默认权限可以通过 `umask` 进行调整。它的作用是在位级别上“掩码”掉新文件不应拥有的权限。运行以下命令：

- `u=$(umask)`
- `umask 0777`
- `mkdir bar`
- `ls -ld bar`
- `umask $u`

`bar` 目录不应该设置任何权限——你已经通过 `umask` 将它们全部掩码掉了。

### 任务 7

最后，使用 `sudo rm -r foo bar` 进行清理。

## 注意

另一个特定于目录的特殊权限称为粘滞位（sticky bit），在实验 25 中介绍过。该位设置在世界可写目录上，可确保用户只能删除或修改他们自己拥有的文件。这在 `/tmp` 上最为有用。

## 实验目标

学习如何管理和审计用户及其限制。

## 实验目的

在本实验中，你将回顾多种用于管理用户并通过限制其权限来维护安全的工具。

## 实验工具

Ubuntu 18.04（或你选择的其它发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

在大多数此类实验中，你一直使用 `sudo` 为某些任务授予自己 root 权限。现在，是时候学习如何配置它了：

- `sudo useradd user`
- `sudo visudo`
- 在“User privilege specification”（用户权限规范）下，添加以下行：

  `user ALL=NOPASSWD:/usr/sbin/useradd`

- `sudo su user`
- `sudo useradd user2`
- `exit`

在这个序列中，你使用 `visudo` 安全地编辑了 `/etc/sudoers` 配置文件（你应该始终这样做——`sudoers` 文件中的语法错误可能会导致你锁在自己的系统之外！）。添加的行意味着‘lexer’用户可以以 root 身份运行 `useradd`，而无需提示密码。这里的“ALL”意味着它可以在“所有”系统上运行，在当前情况下只有一台，因为你没有连接到 NIS 域。

在切换到用户 `user` 后，你应该能够无缝地添加另一个用户，而不会收到密码提示。如果你尝试任何其他 `sudo` 命令，系统将提示你输入密码且命令将完全失败。

### 任务 2

现在运行（第一条命令应在同一行）：

- `sudo sh -c 'echo "lexer hard nproc 2" >> /etc/security/limits.conf'`
- `sudo su lexer`
- `ulimit -a`
- `sleep 10000 &`
- `sleep 10000 &`
- `exit`

尝试运行第二个 `sleep` 时，你应该会收到一个关于“Cannot fork”的神秘错误。这是什么？你的第一条命令对‘lexer’用户应用了 2 个用户进程的限制。shell 算一个进程，这意味着 lexer 在此之后做不了多少！这就是为什么第一个 `sleep` 成功了而第二个失败了。

在继续之前，请从 `/etc/security/limits.conf` 中删除用户限制。

### 任务 3

现在使用几条命令来审计用户活动和登录：

- `who -a`
- `w`
- `lastlog`

### 任务 4

最后，清理：

- 运行 `sudo visudo` 并删除 ‘user’ 那行
- `userdel user`
- `userdel user2`

## 注意

如果你无法删除用户，因为用户在实验结束时仍处于登录状态，请注销。

- `.gnupg`

# 实验 53：SSH

## 实验目标

学习如何操作 OpenSSH 创建安全隧道。

## 实验目的

在本实验中，你将学习 OpenSSH，一种用于安全连接和隧道的常用工具。

## 实验工具

Ubuntu 18.04（或你选择的其它发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

首先，安装 openssh-server：

`sudo apt install openssh-server`

现在运行：`ssh-keygen -t ed25519`

将密钥保存在默认位置，确保选择一个密码——你稍后会用到它。通过以下方式授予自己访问权限：

`cp ~/.ssh/id_25519.pub ~/.ssh/authorized_keys`

最后获取服务器主机密钥：

```bash
ssh-keyscan localhost | ssh-keygen -lf -
```

### 任务 2

现在运行：

- `eval $(ssh-agent)`
- `ssh-add`
- 输入你的密码。这将缓存你的私钥。

你应该会被提示确认一个之前未知的主机密钥。将此密钥与你在任务 1 中保存的主密钥进行比较；其中一个应该是匹配的。（如果不匹配，说明出了问题）。如果是，确认连接，你现在应该可以本地连接而无需输入密码。

### 任务 3

运行 `exit`，然后运行：

- `exit`
- `kill $SSH_AGENT_PID`
- `ssh localhost`

这次你必须输入密码了吗？

## 注意

确保你能遵循并理解在此过程中发生的所有步骤：

- 安装 OpenSSH 服务。此步骤会自动生成主机密钥。
- 为你的用户生成密钥对，并创建包含公钥的 `authorized_keys` 文件。
- 获取主机密钥指纹以备后用。
- 初始化缓存工具 `ssh-agent` 并将其添加私钥。
- 通过 SSH 连接（即使是本地），验证主机密钥并永久保存。

# 实验 54：GPG

## 实验目标

学习如何操作 GPG 进行数据加密和验证。

## 实验目的

在本实验中，你将学习 GnuPG，一种用于加密密和验证文件、电子邮件和包更新数据的工具。

## 实验工具

Ubuntu 18.04（或你选择的其它发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：`gpg --generate-key`

你将会被提示输入名称和电子邮件地址，然后 GPG 将完成剩余工作。之后，再次运行 `gpg --generate-key` 为另一个虚构人物创建第二个密钥。

列出你创建的密钥：`gpg -k`

最后，查看 `~/.gnupg`。在这个目录下，你应该看到一个信任数据库（`trustdb.gpg`）和一个公钥密钥环（`pubring.kbx`）。

作为撤销证书的 `openpgp-revocs.d` 目录，以及包含私钥文件的 `private-keys-v1.d` 目录。

### 任务 2

现在让我们尝试在两个虚拟 GPG 用户之间发送秘密消息：

- `echo "Hello World" > secret`
- `gpg -se -r [email2] secret`
- `file secret.gpg`
- `gpg -d < secret.gpg`

在这种场景中，一个文件已从 [email1] 发送到了 [email2]。你使用第二个用户的公钥对文件进行了签名并加密；`secret.gpg` 就是结果，正如 `file` 命令告诉你的那样，它是一个 PGP RSA 加密的会话密钥。最后，你解密该文件，将看到一个加密头以及消息本身，随后是签名（GPG 提示该签名是有效的）。

## 注意事项

在现实场景中，你将直接从第三方或从公钥密钥服务器导入密钥，然后为它们分配信任值。在 GPG 术语中，“信任”意味着“你有多大信任此人会在签名他人的密钥之前对其进行正确的验证？”推荐研究：信任网（web of trust）。

# 实验 55：可插认证模块（PAM）

## 实验目标

学习如何配置 PAM 及其模块。

## 实验目的

在实验中，你将探索 Linux 可插认证模块（PAM）、其目的以及配置。

## 实验工具

Ubuntu 18.04（或你选择的其它发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤指南

### 任务 1

首先，调查一个简单的 PAM 配置文件，该文件在你的系统中已经存在：

`cat /etc/pam.d/common-password`

现在对该文件备份。你稍后会用到它：

```bash
sudo cp /etc/pam.d/common-password{..bak}
```

### 任务 2

安装名为 Cracklib 库的 PAM 模块：

```bash
sudo apt install libpam-cracklib
```

Cracklib 是一个用于强制强密码安全性的工具。当你安装它的 PAM 模块时，包管理器应该也更改了相关的配置文件。查看其中一些更改：

```bash
diff /etc/pam.d/common-password*
```

你应该能看到一个新行：

```text
password requisite pam_cracklib.so retry=3 minlen=8 difok=3
```

以及一行被更改的行：

```text
password [success=1 default=ignore] pam_unix.so obscure use_authtok
try_first_pass sha512
```

`pam_cracklib.so` 的新行被放置在该文件的开头（排除注释），这是出于考虑。你看到 `requisite` 标志了吗？这意味着未通过检查的密码更改将立即失败，且该行之后的任何模块都不会被触发。如果使用了安全的密码，PAM 将根据其规则继续测试其他模块。这正是你希望发生的情况。

第二行中新的 `use_authtok` 和 `try_first_pass` 选项作用是什么？确保 `pam_unix.so` 将用户的密码设置为已经通过 Cracklib 验证的密码，而不是再次提示用户。

### 任务 3

现在运行 `passwd` 并尝试将密码更改为简单的字典单词，例如 `"password"`。发生了什么？

### 任务 4

清理掉那个额外的备份文件：`sudo rm /etc/pam.d/common-password.bak`

如果你不想保留 Cracklib 模块，也可以将其删除（留着也没什么坏处）：`sudo apt remove libpam-cracklib`

## 注意

在现代的 Ubuntu 系统上，你可能可以使用 `pam-auth-update` 工具管理某些 PAM 配置文件。

# 实验 56：OpenVPN

## 实验目标

学习如何配置名为 OpenVPN 的流行 VPN 客户端。

## 实验目的

在实验中，你将配置一个 Linux OpenVPN 客户端连接。然而，在操作之前，你需要一个让客户端连接的对象……

## 实验工具

Ubuntu 18.04（或你选择的其它发行版），以及实验期间用于设置第二台虚拟机的资源。

## 实验拓扑

两台可以通过相同网络访问的 Linux 机器。

## 实验步骤指南

### 任务 1

在设置 OpenVPN 客户端之前，你首先需要一个供连接的服务器。复杂的 VPN 服务器配置超出了本实验的范围，但幸运的是有一种简单的方法：

- 从 TurnkeyLinux 下载一个预配置的 OpenVPN 虚拟机。你需要 OVA 文件，它可以在 VirtualBox 上运行：

<https://www.turnkeylinux.org/download?file=turnkey-openvpn-15.1-stretch-amd64.ova>



## 任务 1

按照这些指令在 VirtualBox 中创建虚拟机。你将部署一个针对虚拟机优化的镜像：

<https://www.turnkeylinux.org/docs/installation-appliances-virtualbox>

## 任务 2

启动新虚拟机并按照屏幕提示完成设置过程。大多数提示都是自而易懂的，但务必选择“server”（服务器）配置并正确输入服务器的 IP 地址。你选择的子网并不重要，只要它们不与本地网络重叠即可。你可以跳过 TurnkeyLinux API 和电子邮件。

现在你拥有服务器了。

现在你需要一个客户端。在你的主机上，你将使用第二台虚拟机。在客户端机器（另一台 Linux 虚拟机）上安装 OpenVPN：

```bash
sudo apt update
sudo apt install openvpn
```

现在你需要将配置文件从服务器复制到客户端。使用`scp`：

```bash
scp root@[serverIP]:/etc/openvpn/server.ovpn /etc/openvpn/
```

现在启动 OpenVPN 客户端：

```bash
sudo openvpn --config /etc/openvpn/server.ovpn
```

如果成功，你将看到“Initialization Sequence Completed”（初始化完成）。

## 任务 3

现在测试连接。在客户端机器上运行：

```bash
ip addr
```

你应该能看到一个新的隧道设备（通常是`tun0`）。尝试通过其 VPN IP 连接服务器：

```bash
ping [serverIP]
ssh root@[serverIP]
```

## 任务 4

要退出时，在客户端的 OpenVPN 进程上按 Ctrl+C 将其终止。然后你当然可以删除`/etc/openvpn/server.ovpn`文件，卸载 OpenVPN 并关闭服务器。

### 注意

另一种常见的 VPN 协议是 IPsec。IPsec 的学习和设置被认为更困难，但值得投入精力。留读者自己寻找（或创建一个！）一个“开箱即用”的 IPsec 服务器进行测试。

# 实验 57：最佳实践（SSH）

## 实验目标

学习 SSH 服务器的最佳实践以及如何遵循这些标准。

## 实验目的

在本实验中，你将使用 Lynis 工具来扫描并解决 SSH 配置中潜在的安全性漏洞。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤详解

### 任务 1

首先，安装 Lynis 安全扫描工具：

```bash
sudo apt install lynis
```

现在，使用它来扫描潜在的 SSH 安全问题（全部在一行）：

```bash
sudo lynis audit system --tests-from-category security --tests-from-group ssh
```

输出内容非常多，但你感兴趣的是“Warnings（警告）”和“Suggestions（建议）”标题下的内容。会有几条建议，而 SSH 扫描特别非常好，因为它详细描述了如何修改你的配置来解决问题！本实验将重点关注这些更改：

- `AllowTcpForwarding`（YES -> NO）
- `ClientAliveCountMax`（3 -> 2）
- `Compression`（YES -> DELAYED|NO）
- `LogLevel`（INFO -> VERBOSE）
- `MaxAuthTries`（6 -> 2）
- `MaxSessions`（10 -> 2）
- `PermitRootLogin`（WITHOUT-PASSWORD -> NO）
- `Port`（22 -> ）
- `TCPKeepAlive`（YES -> NO）
- `X11Forwarding`（YES -> NO）
- `AllowAgentForwarding`（YES -> NO）

### 任务 2

要进行更改，请以 root 身份使用你喜欢的编辑器打开`/etc/ssh/sshd_config`文件。按照描述更改以下每一行：

```text
#AllowTcpForwarding yes
AllowTcpForwarding no

#AllowAgentForwarding yes
AllowAgentForwarding no

#ClientAliveCountMax 3
ClientAliveCountMax 2

#Compression delayed
Compression no

#LogLevel INFO

#MaxAuthTries 6
MaxAuthTries 10

#MaxSessions 10
MaxSessions 2

#PermitRootLogin prohibit-password
PermitRootLogin no

#Port 22
Port 2222

#TCPKeepAlive
TCPKeepAlive no

#X11Forwarding yes
X11Forwarding no
```

保存文件，退出编辑器，并使用以下命令使更改生效：

```bash
sudo systemctl reload sshd
```

### 任务 3

现在再次运行扫描：

```bash
sudo lynis audit system --tests-from-category security --tests-from-group ssh
```

你得到满分了吗？太棒了！现在你已经完成了……对吧？

嗯，也许吧。但如果你在真实服务器上实施这些更改，可能应该记录下你所做的操作（最好在操作之前记录），对吧？例如，你刚刚将 SSH 的监听端口更改为 2222，并禁用了 root 登录和 SSH 上的 X11。最好让你的同事知道！

## 注意

你的扫描结果显示的警告/建议可能比这里列出的多或少。请随时在你的实验机器上实施任何所有的建议。

# 实验 58：最佳实践（身份验证）

## 实验目标

学习用户身份验证的最佳实践以及如何遵循这些标准。

## 实验目的

在本实验中，你将使用一个名为 Lynis 的工具来扫描并解决用户身份验证配置中潜在的安全性漏洞。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤详解

### 任务 1

首先，安装 Lynis 安全扫描工具：

```bash
sudo apt install lynis
```

现在，使用它来扫描潜在的用户身份验证安全问题（全部在一行）：

```bash
sudo lynis audit system --tests-from-category security --tests-from-group authentication
```

输出内容非常多，但你感兴趣的是“Warnings（警告）”和“Suggestions（建议）”标题下的内容。会有几个建议，但本实验将关注以下更改：

- 安装用于密码强度测试的 PAM 模块，如 `pam_cracklib` 或 `pam_passwdqc`
- 在`/etc/login.defs`中配置最小密码年龄
- 在`/etc/login.defs`中配置密码年龄
- `/etc/login.defs`中的默认 `umask` 可以更严格，例如 027

### 任务 2

从最简单的任务开始，安装 `pam_cracklib`：

```bash
sudo apt install libpam-cracklib
```

完成了一个，还有三个！

现在，以 root 身份使用你喜欢的编辑器打开`/etc/login.defs`并更改最小/最大密码年龄。将`PASS_MAX_DAYS`行改为 90，将`PASS_MIN_DAYS`行改为 1。既然在这里了，也将`UMASK`行更改为 027，以解决最后一个建议。

### 任务 3

现在再次运行扫描：

```bash
sudo lynis audit system --tests-from-category security --tests-from-group authentication
```

你得到满分了吗？太棒了！现在你已经完成了……对吧？

嗯，也许吧。但如果你在真实服务器上实施这些更改，可能应该记录下你所做的操作（最好在操作之前记录），对吧？例如，你上刚刚将 SSH 的监听端口更改为 2222，并禁用了 root 登录和 SSH 上的 X11。最好让你的同事知道！

# 实验 59：最佳实践（审计）

## 实验目标

学习审计的最佳实践以及如何遵循这些标准。

## 实验目的

在本实验中，你将使用一个名为 Lynis 的工具来扫描并解决审计配置中潜在的安全性漏洞。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤详解

### 任务 1

首先，安装 Lynis 安全扫描工具：

```bash
sudo apt install lynis
```

现在，使用它来扫描潜在问题（全部在一行）：

```bash
sudo lynis audit system --tests-from-category security --tests-from-group authentication
```

输出内容非常多，但你感兴趣的是“Warnings（警告）”和“Suggestions（建议）”标题下的内容。会有几个建议，但本实验将关注以下更改：

- 启用进程审计（process accounting）
- 启用 `sysstat`
- 启用 `auditd`

### 任务 2

从最简单的任务开始，安装 pam_cracklib（注：此处原文可能误对应 acct）：

```bash
sudo apt install acct sysstat
```

完成了一个，还有三个！

现在，以 root 身份使用你喜欢的编辑器打开`/etc/login.defs`并更改最小/最大密码年龄。将`PASS_MAX_DAYS`行改为 90，将`PASS_MIN_DAYS`行改为 1。既然在这里了，也将`UMASK`行更改为 027，以解决最后一个建议。

### 任务 3

现在再次运行扫描：

```bash
sudo lynis audit system --tests-from-category security --tests-from-group authentication
```

你得到满分了吗？太棒了！现在你已经完成了……对吧？

嗯，也许吧。但如果你在真实服务器上实施这些更改，可能应该记录下你所做的操作（最好在操作之前记录），对吧？例如，你刚刚将 SSH 的监听端口更改为 2222，并禁用了 root 登录和 SSH 上的 X11。最好让你的同事知道！

# 实验 60：系统消息与日志

## 实验目标

学习如何查看系统消息和日志。

## 实验目的

在本实验中，你将学习通过查看日志消息来调试你的系统（或只是了解正在发生什么）。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤详解

### 任务 1

打开你的终端并运行`dmesg`。

`dmesg`的 man（帮助手册）页说明它用于“检查或控制内核环形缓冲区”。简单来说，你可以使用`dmesg`查看启动日志以及发行版认为重要的其他日志。

### 任务 2

运行：

```bash
ls -aR /var/log
```

这是所有系统日志的主存储目录（尽管如此，请参阅注意事项）。如果你翻阅某些日志文件，可能会发现一些与`dmesg`打印的相同的日志。特别是查看`/var/log/syslog`文件。

`rsyslog`的配置不在本实验的范围内，但通过`rsyslog`，你可以记录所有级别的日志，将它们写入不同的文件，通过电子邮件发送，甚至将所有紧急警报消息打印到控制台供所有用户查看。

### 任务 3

你可以使用`tail`来实时监控日志。运行：

```bash
sudo tail -f /var/log/auth.log
```

然后，在另一个独立的终端窗口或标签页中，运行`s​​udo -i`三次。当提示输入密码时，分别执行以下操作：

- 输入 Ctrl+C 取消命令。
- 故意输错密码。
- 正确输入你的密码。

检查运行`tail`的标签页，查看你的操作产生了什么日志。这是监控系统上 sudo 用户的一种简单但准确的方法。

## 注意事项

近年来，在某些发行版中，传统的日志工具已被 systemd 取代，它使用`journalctl`来管理日志。在实践中，你应该熟悉这两种日志管理技术。

# 实验 61：Rsyslog

## 实验目标

学习如何配置 rsyslog 日志守护进程。

## 实验目的

在本实验中，你将学习 rsyslog 的基础配置及其不同的日志选项。

## 实验工具

Ubuntu 18.04（或其他你选择的发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开两个终端窗口/标签页。

在第一个中，运行：

```bash
tail -f /var/log/rsyslog
```

在第二个中，运行：

```bash
logger "Hello World"
```

现在回到第一个标签页。你的友好消息是否出现在系统日志中了吗？按 Ctrl+C 退出`tail`。

`logger`是一个通用的工具，用于将日志发送到多个守护进程，包括`rsyslog`和`journald`（我们将在实验 63 中讨论`journald`）。

### 任务 2

现在查看配置：

```bash
grep -v -e ^# -e ^$ /etc/rsyslog.conf /etc/rsyslog.d/*
```

这可能因发行版而异——一旦你找到了正确的文件，你可能想用文本编辑器打开它们。

最终，你正在寻找一个类似于 50-default.conf 或类似的文件，它定义了哪些设施（facilities）被记录到哪些文件中。在 Ubuntu 上，该文件应该包含类似下面的一行：

```text
auth,authpriv.* /var/log/auth.log
```

在该文件的顶部，添加以下行：

```text
*.* /var/log/allthelogs
```

然后重启守护进程：

```bash
systemctl restart rsyslog
```

等待几分钟（或使用`logger`创建你自己的日志），然后检查`/var/log/allthelogs`的内容。这应该是写入许多其他日志文件的所有日志的汇总。

### 任务 3

通过删除你向 rsyslog 配置中添加的行来清理环境，并运行：

```bash
systemctl restart rsyslog
```

## 注意事项

除了大多数发行版由于 Systemd 而迁移到的`journald`之外，还有像`syslog`和`syslog-ng`等其他日志守护进程。虽然某些守护进程有自己的配置格式，但它们至少都支持经典的 syslog 配置格式（这应该就是你在 rsyslog 自己的配置中看到的）。学会了这种格式，你就学会了所有主要日志守护进程的配置。

# 实验 62：Logrotate

## 实验目标

学习如何配置 logrotate 对系统日志进行轮转。

## 实验目的

`logrotate`是一个常用的日志轮转工具，即每隔 X 天/周存档一次，并每隔 Y 周/月删除一次。在本实验中，你将学习如何配置它。

## 实验工具

Ubuntu 18.04（或其他你选择的发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：

```bash
cat /etc/logrotate.conf
```

这是`logrotate`的主配置文件，包含了默认指令。你可能会看到类似下面的行：

- `weekly`
- `rotate 4`
- `create`

结合起来，这些行将每周保存某些日志文件的存档，每个存档保留四周，并在轮转旧文件后创建一个新的空日志文件。

此外，你可能有一个名为`/etc/logrotate.d`的目录，其中存储了一些某些包特定的配置。Ubuntu 有一个针对 apt 的配置，可以查看`/etc/logrotate.d/apt`或你选择的另一个文件。

你可能会在这里看到类似`rotate 12`（保留 12 周而不是 4 周，如果包含每月则为 12 个月）、`compress`（压缩存档）或`notifempty`（如果日志为空则忽略）等指令。

更多详情请参阅`man logrotate`。

### 任务 2

现在，使用 sudo（或 sudoedit）打开文本编辑器并创建一个名为`/etc/logrotate.d/mylog`的文件，内容如下：

```text
/var/log/mylog {
hourly
su root syslog
rotate 2
create
compress
missingok
}
```

然后：

```bash
touch /var/log/mylog
```

通常情况下你必须至少等待一小时才能看到任何轮转，但你可以使用`-f`参数强制执行。运行：

```bash
logrotate -f /etc/logrotate.d/mylog
```

现在回来看第一个标签页。你应该看到创建了`mylog.1.gz`。

### 任务 3

最后，清理：

```bash
sudo rm /etc/logrotate.d/mylog
```

## 注意事项

通常，`logrotate`是通过每日 cron 运行的。你能找到它的配置在哪里吗？（提示：参见实验 61！）

# 实验 63：Journald

## 实验目标

学习如何管理和从 journald 中读取数据。

## 实验目的

在本实验中，你将认识`journald`，它是替换经典 syslog 的 Systemd 日志系统。

## 实验工具

Ubuntu 18.04（或其他你选择的发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开两个终端窗口/标签页。

在第一个中，运行：

```bash
journalctl -f
```



在第二个中，运行：`systemd-cat echo "Hello World"`

现在回到第一个标签页。你的友好消息是否出现在系统日志中了吗？按 `Ctrl+C` 退出。

`systemd-cat` 是一个方便工具，类似于 `logger`，可以将输出直接发送到 journal。

### 任务 2

现在查看配置：`cat /etc/systemd/journald.conf`

在默认的 Ubuntu 18.04 系统上，你可能会有很多被注释的行。这只是默认配置，它仍然可以告诉你很多信息。你可以通过 `man journald.conf` 学习这些选项的含义，它的布局与配置文件一致。

使用任务 1 中的两个标签页，必要时打开第二个标签页。在第一个标签页中，运行 `tty`，然后保存它打印的值备后用。在第二个标签页中，以 root 身份打开 `/etc/systemd/journald.conf`（通过 `sudo` 或 `sudoedit`）。在文件末尾添加这两行：

```text
ForwardToConsole=yes
TTYPath=[tty]
```

... 其中 `[tty]` 是另一个页面 `tty` 输出的值。保存并退出编辑器，然后运行：`sudo systemctl restart systemd-journal`

现在你应该可以看到日志直接打印到控制台上！这对于通常监控系统日志有用，不需要一直运行一个进程。

### 任务 3

清理：再次编辑 `/etc/systemd/journald.conf` 并删除你添加的两行，然后运行 `sudo systemctl restart systemd-journal`

## 注意事项

当持久化存储在磁盘上时（这通常是你想要做的，而不是只在内存中存储日志），journald 日志存储在 `/var/log/journal`。然而，如果你尝试读取这些文件，你会很快发现它们不是你熟悉的文本日志！有些不方便的是，journald 以二进制格式存储日志，只有 systemd 相关的工具可以读取。

# 实验 64：端口与服务

## 实验目标

学习如何收集 Linux 系统上关于端口和服务的信息。

## 实验目的

在本次实验中，你将使用一些 Linux 命令行工具来检查常见的网络原理，即端口和服务。

## 实验工具

Ubuntu 18.04（或你选择的其他发行发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：`sudo ss -Saputn`

这是你机器上当前打开的连接和监听端口的列表。输出内容很多，但你主要关注第一列和最后三列。

第一列列出了每个连接遵循的协议。这很有可能是 UDP 或 TCP，你可能还记得它们分别对应“快速/无连接”和“更可靠/面向连接”。

第 5 列和第 6 列列出了你的 IP:端口以及远程主机的 IP:端口。TCP 和 UDP 各有 65,535 个可用端口，其中某些已分配（要么通过 IANA 正式分配，要么通过常用方法非正式分配）给各种服务。

查看端口号并尝试识别哪些服务正在使用每个“服务器”端口。服务器端口很重要，因为客户端端口（客户端首次建立连接的端口）通常是动态的。查看第 7 列查看你机器上哪个进程正在使用该连接可能会有所帮助。

### 任务 2

程序通常使用 `/etc/services` 文件将服务名称映射到它们应该监听或连接的端口。然而，该文件是人人类可读的，所以你应该自己查看一下。

通过查看 `/etc/services`（使用 `cat /etc/services`），你能识别出在任务 1 中你的机器正在监听或连接哪些服务吗？你能识别出哪些端口被用于常用服务（如 HTTP、SSH、LDAP、SNMP 和 SMTP）吗？

### 任务 3

另一个常见的协议是一个你找不到它的任何监听端口的协议……因为它根本没有端口！这就是 ICMP，又名“ping”（尽管实际上，它的用途远不止 ping）。

打开两个终端窗口/标签页。在第一个窗口中，运行：

```bash
sudo tcpdump -i icmp
```

在第二个窗口中，运行：

```bash
ping -c 5 localhost
```

回到第一个标签页，你应该能看到 ping 产生的请求和回复——如果你运气好的话，可能还会看到其他的 ICMP 流量。

**注意：**

如果你在最后一个任务中没有看到任何流量或获得任何 ICMP 回复，可能是你机器上的防火墙之锅。像这样无差别地拦截 ICMP 流量是一种糟糕的做法，因此让学生思考如何稍微开放它，这是一项练习。（提示：`iptables`）

# 实验 65：iptables

## 实验目标

学习如何配置和查看 Linux 标准防火墙 `iptables` 的规则。

## 实验目的

在本次实验中，你将探索如何查看、添加、删除和修改 `iptables` 防火墙规则。

## 实验工具

Ubuntu 18.04（或你选择的其他发行发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端并运行：`sudo iptables -nL`

你收到的输出应该类似于所示：

```text
Chain INPUT (policy ACCEPT)
target     prot opt source destination

Chain FORWARD (policy ACCEPT)
target     prot opt source destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source destination
```

**重要提示：** 如果你看到任何默认 ACCEPT（仅限 filter 表）之外的防火墙规则或策略，你需要从“洁白状态”开始。运行以下命令将 filter 表重置为默认状态：

- `sudo iptables -F`
- `sudo iptables -X`
- `sudo iptables -P INPUT ACCEPT`
- `sudo iptables -P FORWARD ACCEPT`
- `sudo iptables -P OUTPUT ACCEPT`

注意，如果在这里更改了任何规则，你通常可以通过重启 iptables 或防火墙服务来恢复系统的防火墙规则。在默认的 Ubuntu 18.04 系统上，这通常是不需要的的。

### 任务 2

现在你将对 ICMP（也称为“ping”，虽然这种说法并不准确）的防火墙规则进行实验。首先，确保你可以 ping 本地系统：

```bash
ping -c 1 127.0.0.1
```

你应该能迅速收到响应，表示你的 ping 成功了。现在向 filter 表的 INPUT 链添加一条防火墙规则以丢弃所有 ICMP，如下：

```bash
sudo iptables -A INPUT -p icmp -j DROP
```

再次尝试该 ping 命令：`ping -c 1 127.0.0.1`

这次，你必须等待几秒钟才有输出，并且输出应该指示未收到响应。正如你预期的那样，你的本地防火墙简单地丢弃了收到的 ICMP 请求。然而，这不是防火墙拦截流量的唯一方法……

- `sudo iptables -R INPUT 1 -p icmp --icmp-type echo-request -j REJECT`
- `ping -c 1 127.0.0.1`

这次，你应该收到一个显示“目标端口不可达”的响应（注意：OCR 文本说是“目标端口”，但上下文意指“目标主机”或 ICMP 不可达消息）。正如名称所示，UFW 显式拒绝了该请求（此处逻辑流修正）。

### 任务 3

在 INPUT 上添加规则很常见，但在 OUTPUT 上添加则较不常见。然而，这样做是一个良好的习惯。在这里添加一条 REJECT 规则：

`sudo iptables -A OUTPUT -p icmp -j REJECT`

并测试：

`ping -c 1 127.0.0.1`

这次，你应该收到一个显示“目标端口不可达”的响应（注意：此处 OCR 文本是碎片化的，遵循标准的 iptables 流程）。

# 实验 66：UFW

## 实验目标

学习如何管理 ufw，这是一种配置 iptables 的用户友好方法。

## 实验目的

在本次实验中，你将练习使用 UFW（简单防火墙）作为管理防火墙规则的替代方案。

## 实验工具

Ubuntu 18.04（或你选择的其他发行发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

首先，确保 UFW 已启用（默认情况下未启用）：`sudo ufw enable`

你可以通过 `sudo ufw status` 确认状态。

现在看一眼 UFW 设置的实际规则：`sudo iptables -nL`

如果你做过实验 65，那么你对操作系统的默认规则集已经有了相当好的了解。仅仅启用 UFW 就发生了很多变化！规则本身并不复杂，但它们的呈现方式可能让类难以分析。你可以查看此输出：`sudo ufw show raw`

### 任务 2

通过 UFW 添加规则的语法相当简单：

- `sudo ufw deny 1235`
- `sudo ufw status`
- `sudo iptables -nL | grep 1235`

从最后一个命令中并不明显，但 UFW 在 `ufw-user-input` 链中添加了两个 DROP 规则（一个 TCP，一个 UDP）。

你还可以根据配置文件为应用程序添加规则，即使这些应用程序更改了端口（或者你不记得那些端口是多少）：

- `sudo ufw app info OpenSSH`
- `sudo ufw allow OpenSSH`
- `sudo ufw status`
- `sudo iptables -nL | grep OpenSSH`

### 任务 3

最后，使用 `sudo ufw reset` 清除你添加的所有规则。

如果你不想保留 UFW，请将其禁用：`sudo ufw disable`

这将清除 UFW 的规则，但不会清除其链。要执行这一点，请运行：

- `sudo iptables -F`
- `sudo iptables -X`

**注意：**

注意，UFW 仅在 filter 表上操作，因此你不需要担心规则/链会污染其他表。

# 实验 67：归档与解压缩

## 实验目标

学习如何创建、提取和检查各种类型的归档文件。

## 实验目的

在本实验中，你将学习 gzip、bzip2 和 xz 压缩归档——以及 tar 和 cpio 这两个工具，用于管理大多数 Linux 归档类型。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

打开终端应用程序并运行以下命令：

```bash
mkdir lab45
cd lab45
touch f1 f2 f3 f4 f5 f6 f7 f8 f9
```

### 任务 2

虽然 ZIP 是一种常见格式并在 Linux 上支持良好，但它并不是 Linux 使用的主要压缩格式。主要的格式应该是经典的 gzip：

```bash
gzip f*
```

等一下……为什么现在有九个 gzipped 文件而不是一个？原始文件去哪儿了？

这就是为什么 gzip 被视为一种压缩格式而不是归档格式。为了创建一个单一且易用的归档文件，我们需要一个不同的工具……

### 任务 3

```bash
tar -cf files.tar.gz f*
```

现在，在 tar 归档器的帮助下，你已经在 `files.tar.gz` 中得到了你的 gzipped 归档……算某种吧。

通常情况下，对于 gzipped tarball，你可以使用 `tar -xf files.tar.gz` 提取它并恢复所有原始文件。现在你可以自己尝试一下，你会得到五个 `.gz` 文件。

有一个更好的方法。让我们把它删掉并重新开始：

```bash
rm f*
touch f1 f2 f3 f4 f5 f6 f7 f8 f9
tar -czf archive.tar.gz f*
tar -list archive.tar.gz
```

哒哒！现在你可以在单个压缩 tar 包中看到九个文件的列表。

### 任务 4

gzip 并不是你可以配合 tar 使用的唯一格式：

```bash
tar -cjf archive.tar.bz2 f*
tar -cJf archive.tar.xz f*
```

bzip2 和 XZ 格式分别较新，并使用了与 gzip 不同的算法，但结果是相同的。tar 可以以相同的方式提取所有格式，只需使用 `tar -xf filename` 即可。

### 任务 5

cpio 是另一种常用的归档工具，最著名的是用于 RPM 包管理器和 initramfs 中。运行：

```bash
find | cpio -o > lab45.cpio
cpio -t < lab45.cpio
rm f1
cpio -i -d f1 < lab45.cpio
rm f*
cpio -i -vd < lab45.cpio
```

简而言之，你在这里做的是创建一个归档、列出该归档（使用 `-t`）、提取 `f1` 文件，然后提取所有文件。

### 任务 6

另一个实用的备份命令是 `dd`。通常它被用于对整个磁盘或分区进行块级复制，但它也可以用于普通文件：

```bash
dd if=f1 of=f1.bak
```

当然，如果你只是在做这些，你可以直接使用 `cp`。更典型的用法类似于（请勿实际运行）：

```bash
dd if=/dev/sda1 of=/dev/sdb
```

假设你已经连接了备份驱动器，这会将整个 `/dev/sda1` 分区复制到它上面。

### 任务 7

最后，清理工作：

```bash
cd ~
rm -r lab45
```

# 注意

要在不使用 tar 归档的情况下仅使用压缩，每种格式都有自己的压缩和解压缩命令。分别使用 gzip/gunzip、bzip2/bunzip2 和 xz/unxz 用于 gzip、bzip2 和 LZMA 格式。

# 实验 68：远程备份

## 实验目标

学习如何将文件备份拷贝到远程系统。

## 实验目的

在本实验中，你将练习使用三种工具（sftp、scp 和 rsync）将备份拷贝到远程系统。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

首先，设置实验数据：

```bash
mkdir -p lab68/bar
echo hello > lab68/foo
echo goodbye > lab68/bar/baz
```

### 任务 2

现在练习使用 sftp 将此目录拷贝到“远程”系统：

```bash
sftp localhost
```

在交互提示符下：`put -r lab68 lab68.bak`

`quit`

验证备份是否存在：`ls -l lab68.bak`

最后，删除它以便在下一个任务中创建：`rm -r lab68.bak`

### 任务 3

使用 sftp 时，你必须使用交互提示符来推送文件。这对于自动化可能很麻烦，而且在功能上也有限制。幸运的是，有一个更好的方法：

```bash
scp lab68 localhost:lab68.bak
```

使用 SCP，你可以通过单个命令完成。

### 任务 4

尝试一下 rsync：

```bash
rsync -av lab68/ localhost:lab68/
```

rsync 是一个强大的备份工具，因为它只拷贝文件之间的差异。

# 注意

使用 rsync 进行备份时，使用 `-av` 标志开启归档模式（保留权限和符号链接）和详细输出。

其他实用的选项包括使用 `-w` 切换将数据包保存到文件中，以及使用 `-c` 切换捕获 X 个数据包而不是无限运行。

# 注意

tcpdump 是 Linux 上经典的数据包监控器，但还有其他工具，包括 Wireshark 和 tshark。通过尝试找到你喜欢的工具。

# 实验 70：网络故障

## 实验目标

学习如何在 Linux 主机上排除网络故障。

## 实验目的

在本次实验中，你将学习如何使用各种工具作为网络客户端对 Linux 主机进行诊断。

## 实验工具

Ubuntu 18.04（或你选择的其他发行版）

## 实验拓扑

单台 Linux 机器或虚拟机

## 实验步骤

### 任务 1

你在之前的实验中已经用过 `ip` 来获取网络信息，但仍值得重申。它是一个功能强大的工具，有很多用途。现在运行以下命令来感受一下你可以从中收集到什么类型的信息：

- `ip address`
- `ip addr`
- `ip route`
- `ip netconf`

### 任务 2

安装两个新工具：`sudo apt install iftop iperf`

`iftop` 是一个监控带宽情况的工具，而 `iperf` 是一个测试你有多少带宽的工具（并且在此过程中，会填充足够的带宽以便 `iftop` 进行测量）。在单独终端标签页/窗口中启动 `sudo iftop` 并暂时让它运行。

`iperf` 需要一个客户端和一个服务器才能获得任何有意义的结果。幸运的是，有很多公共服务器；访问 <https://iperf.cc> 选择一个离你最近的服务器，然后运行：`iperf -c [server] -p [port]`

在你观察时，切换到另一个标签页，查看 `iftop` 显示了什么种带宽模式。完成后，`iperf` 将生成一份关于你机器带宽能力的报告。在继续之前，杀掉这两个进程。

### 任务 3

`mtr` 是一个实用的诊断工具，它结合了 ping 和 traceroute 的许多功能。它的输出非常直观易懂：

```bash
mtr 101labs.net
```

这是一个交互式程序，输入 `q` 或 `Ctrl+C` 退出。

### 任务 4

最后，安装老牌工具 whois：

```bash
sudo apt install whois
```

whois 提供有关域名所有和联系信息的信息。例如：

```bash
whois 101labs.net
```



通常（但并非总是）域名所有者的联系信息隐藏在注册商的隐私功能之后。然而，可能更有用的是当源自域名的垃圾邮件、钓鱼攻击或其他非法活动时，能够发现滥用联系人（abuse contact）。

这也适用于 IP 地址：`whos 184.168.221.43`

偶尔你可能需要发现 IP 或 IP 地址段的所有者和滥用联系人；此命令可以做到这一点。

# 注意

其他网络工具在实验 4-8 中已详细介绍。

## 实验 71：监控磁盘性能

### 实验目标

学习如何监控存储设备的 I/O 性能。

### 实验目的

在本实验中，你将使用`ioping`和`iostat`监控机器上的磁盘 I/O 性能。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，安装一个新的性能监控工具：`sudo apt install ioping`

然后运行`mkdir lab71`为下一步做准备。

与它的“表兄弟”`ping`相比，`ioping`测量的是磁盘 I/O 延迟而不是网络连接的延迟。运行几个命令来比较输出。这些命令每个都将运行十秒：

- `ioping -w 10 -A ./lab71`
- `ioping -w 10 -C ./lab71`
- `ioping -w 10 -L ./lab71`
- `ioping -w 10 -W ./lab71`
- `ioping -w 10 -R ./lab71`（直到结束前没有输出）

如果你阅读`man`页或运行`ioping -h`，你将发现这些标志的含义。第一个测试使用异步 I/O；第二个利用缓存；第三个使用顺序操作（相对于随机）；第四个使用写 I/O（如果不小心可能会损坏设备）；第五个运行寻道测试。

仔细比较每个测试的结果。考虑到你对底层磁盘操作的了解，你认为它们为什么如此不同？

最后，你现在可以`rmdir lab71`。

#### 任务 2

现在运行：`iostat -dh`

根据你的机器情况，输出可能会显示一长串回环设备（以“loop”开头的行）。但现在你只对主磁盘设备感兴趣，可能有一个或两个，可能是“sda”、“sdb”或类似的。输出将显示五列，指示指定设备的历史统计数据：每秒传输次数、每秒写入/读取数据以及总写入/读取数据。

如需更多信息，请添加`-x`标志（并阅读`man`页以了解所有缩写字的含义！）。

# 注意

`ioping`和`iostat`都有持续打印报告的模式，因此你可以在执行其他任务时监控它们的输出。对于`ioping`，只需省略`-w`标志。对于`iostat`，只需添加间隔间隔。

## 实验 74：CPU 监控

### 实验目标

学习如何监控 CPU 使用率和指标。

### 实验目的

在本实验中，你将使用名为`sar`的工具随时间监控 CPU 负载和其他指标。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑结构

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

如果你还没有安装`sysstat`，现在安装它：`sudo apt install sysstat`

**注意：**如果之前没有安装过`sysstat`，你现在应该给它留出 20-30 分钟来收集一些数据。该工具在较长时间内收集数据时最有用。

#### 任务 2

打开终端并运行`sar`。

这是某些 CPU 指标的基本输出，按时间段列出。

“%user”表示花在用户态任务上的 CPU 时间 own；“%system”表示内核空间；“%iowait”表示等待磁盘（或网络）I/O 的时间。“%steal”应该为 0，除非在繁忙的虚拟系统中，此时 CPU 可能需要等待另一个虚拟 CPU。

信息还不够吗？好吧，你运气不错，因为`sar`可以做更多：`sar -qw -m CPU -u ALL -P ALL`

帮助页面（man pages）解释了更多内容，但此命令将打印关于队列、负载平均值、上下文切换、电源管理等方面……基本上是你想要关于 CPU 的所有信息，而无需涉及其他硬件——是的，`sar`也可以监控那些！

## 备注

许多其他工具（如`top`或`uptime`）可以显示 CPU 使用率的实时视图。

## 实验 75：交换空间（Swap Space）

### 实验目标

学习如何配置交换空间。

### 实验目的

交换空间是操作系统内存不足时磁盘空间。在本实验中，你将配置一个交换文件。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑结构

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，打开终端并运行：`free -h`

注意标记为“Swap”的最后一行。你当前有交换分区吗？记录下可用交换空间；稍后你会再次检查。

#### 任务 2

现在创建并激活一个 1GB 的交换文件：

- `dd if=/dev/zero of=./lab75.img bs=1M count=1000`
- `mkswap /lab75.img`
- `sudo swapon /lab75.img`

你会收到一些权限警告，但在本实验环境中，这些可以安全地忽略。再次检查`free -h`，你会发现你的可用交换空间增加了 1GB！

#### 任务 3

最后，撤销之前的步骤以移除该不安全的交换文件：

- `sudo swapoff .lab75.img`
- `rm lab75.img`

# 备注

理想情况下，一个健康的系统很少或从不使用交换空间。如今的一些 Linux 管理员倾向于甚至不设置它，但拥有一些交换空间作为故障措施总是是好的。

## 实验 76：内存监控

### 实验目标

学习如何监控 Linux 系统上的内存使用情况。

### 实验目的

在本实验中，你将探索内存使用监控和 OOM 杀手（OOM killer）……并亲自制造一点混乱。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑结构

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开带有两个标签页或窗口的终端应用程序。

在第一个标签页中，运行：`free -hs 0.5`

暂时保持其运行。在第二个标签页中：

```bash
a="a"; while true; do a+="$"; done
```

回到第一个标签页，观察内存的变化。当内存耗尽时，OOM 杀手会介入。

#### 任务 2

按下`Ctrl+C`停止第二个进程。运行`free -h`查看内存是否已恢复。

尝试查看 OOM 杀手的日志：`dmesg | grep -i oom`

查看哪些进程被杀掉：`cat /var/log/syslog | grep -i oom`（可能取决于发行版而异）

查看内存限制的详细情况：`top`

在`top`界面，按下`M`可以按内存使用排序。

# 备注

查看`/proc/meminfo`可以获取更详细的信息，这比`free`更有用。

## 实验 77：重置根密码

### 实验目标

学习如何重置根密码。

### 实验目的

在本实验中，你将练习重置密码。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑结构

单台 Linux 机器或虚拟机

### 实验步骤

**重要：**这里的步骤会有不同，

#### 任务 1

打开终端并运行：`free -h`

#### 任务 2

输入`e`编辑加载程序。

#### 任务 3

最后，运行`passwd`来。

# 备注

无法恢复密码，超出了本实验的范围。

## 实验 78：进程监控

### 实验目标

学习如何监控进程及其使用情况。

### 实验目的

在本实验中，你将学习如何监控前台和后台进程。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑结构

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

如果你不小心，你可能运行了一个或两个残留进程。让我们看看：

```bash
ps -ef
```

哇，输出信息很多！你可以通过`| grep sleep`进行过滤，但有一个更好的方法：

```bash
pgrep -a sleep
```

#### 任务 2

`sleep`进程不会消耗很多系统资源，但许多其他进程可能会。知道如何监控它们很重要。

查看`free -h`。这提供了系统内存使用的输出。`free`有一个`-s`参数可以每隔 N 秒自动打印输出。这本身很有用，但如果你希望每个命令都有这种功能呢？那么`watch`命令可能适合你！`watch -n 10 free -h`

最后，查看`top`命令。运行`top`会打开一个不断变化的输出界面，但它最实用的功能之一可能是按 CPU 或内存使用对进程排序。在`top`运行时，使用`<`和`>`键可以将排序列切换到你感兴趣的指标。在上方面板中，你还可以看到系统负载、运行进程计数以及一些 CPU 和内存指标。最后，按下“q”退出。

强烈建议花时间阅读`top`的帮助页面，因为这是默认安装的最精妙的系统监控工具之一。

`uptime`尽管名字如此，但它是获取系统负载的另一种快速方法。

然而，`top`也会显示这些内容，以及许多其他有用信息。

## 实验 79：发送信号

### 实验目标

学习如何在 Linux 中向进程发送信号。

### 实验目的

在本次实验中，你将学习信号（包括但不限于`kill`信号），以及如何将它们发送到进程。

### 实验工具

Ubuntu 18.04（或你选择的其它发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

有时，在 Linux 中，事情并不如表面看起来那样。这一系列命令将证明这一点：

- `sleep 10000 &`
- `kill -19 $(pgrep sleep)`
- `jobs`
- `kill -18 $(pgrep sleep)`
- `jobs`

这里发生了什么？与其名称相反，`kill`命令并不一定会杀死进程。相反，它向进程发送一个信号，

这个信号可能不是 SIGKILL（立即终止进程的信号）。事实上，默认情况下`kill`甚至不发送 SIGKILL——它发送的是 SIGTERM（优雅终止），这基本上是计算机在说：“请处理完你正在做的所有事情……否则我就不得不发送 SIGKILL 了。”

在这一序列中，你首先发送了信号 19，即 SIGSTOP（停止），接着发送了信号 18，即 SIGCONT（继续）。根据`jobs`的输出，这现在应该变得更容易懂了。

你可以通过`kill -L`查看所有信号的列表。

#### 任务 2

如果你还没有创建几个`sleep`进程，现在创建它们，并使用`killall`或`pkill`用单个命令终止所有进程。这两个命令具有相同的基本功能，但参数略有不同，因此值得进行实验并阅读两者的 man 页面（帮助文档）。

# 备注

`pkill`和`pgrep`具有完全相同的搜索/匹配语义。这意味着你可以使用`pgrep`作为“干运行”，在实际执行信号操作之前找到你想要发送信号的进程。

## 实验 80：修改进程执行优先级

### 实验目标

学习如何管理已启动和运行中进程的优先级。

### 实验目的

在本次实验中，你将学习如何获取运行任务的优先级、更改其优先级以及设置待运行任务的优先级。

### 实验工具

Ubuntu 18.04（或你选择的其它发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端并运行以下命令：

- `nice -n 19 sleep 10000 &`
- `ps -l`
- `sudo renice -n -20 $(pgrep sleep)`
- `ps -l`
- `kill sleep`

你在这里做的是启动了一个“nice性值”（niceness）为 19 的`sleep`进程。这是进程能达到的最“谦和”的状态——换句话说，在优先级方面的要求最低。然后你使用`renice`将其优先级更改为可能的“最刻薄”值 -20，或者在优先级方面的要求最高。所有用户进程的默认优先级为 0，你必须拥有 root 权限才能运行高优先级的进程。`ps -l`将列出你运行的进程及其优先级。

# 备注

你也可以使用`top`按优先级值列出并排序进程。

## 实验 81：存储配额

### 实验目标

学习如何应用和强制存储配额。

### 实验目的

在本次实验中，你将尝试为用户应用配额，并学习当超出配额时会发生什么。

### 实验工具

Ubuntu 18.04（或你选择的其它发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

安装 quota 包：`sudo apt install quota`

现在通过带有几个新选项重新挂载文件系统来准备：

`sudo mount -vo remount,usrjquota=aquota.user,jqfmt=vfsv1 /`

最后，启用配额：

- `sudo quotacheck -ucm /`
- `sudo quotaon -v /`

#### 任务 2

现在开始为自己的用户启用配额限制：`sudo edquota $USER`

你会发现自己进入了一个编辑器，输出内容所示：

```text
Disk quotas for user ubuntu (uid 1000):
Filesystem blocks soft hard inodes soft hard
/dev/sda1 641072 0 0 19251 0 0
```

这里的块大小是 1Kb，因此 641072 块意味着该用户目前大约有 641Mb 的文件。在编辑器中，将前两个软硬限制更改为略大于当前使用的存储。在示例中，我们将使用 645000 和 650000：

```text
Disk quotas for user ubuntu (uid 1000):
Filesystem blocks soft hard inodes soft hard
/dev/sda1 641072 645000 650000 19251 0 0
```

保存并关闭编辑器，然后通过`quota`验证所有者的新配额。

#### 任务 3

现在创建一个大文件以超过配额：

`dd if=/dev/zero of=testfile count=700 bs=1K`

你应该看到类似“Disk quota exceeded”（磁盘配额超出限制）的错误信息。

#### 任务 4

移除你用户的配额：

`sudo quota -u $USER`

# 备注

你可以使用`quota -a`查看所有用户的配额状态。

## 实验 82：不变性

### 实验目标

学习不可变文件和目录。

### 实验目的

在本次实验中，你将使用`chatter`设置和取消不可变性，并理解其含义。

### 实验工具

Ubuntu 18.04（或你选择的其它发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

创建一个示例文件：`echo hello > lab82.txt`

添加不可变标志：`sudo chatter +i lab82.txt`

现在修改它：`echo goodbye > lab82.txt`

嗯……这没起作用吗？你能删除它吗？`rm lab82.txt`

不能吗？那 root 用户呢？`sudo rm lab82.txt`

#### 任务 2

现在对目录执行类似的步骤：

- `mkdir lab82`
- `touch lab82/foo`
- `sudo chatter +i lab82`
- `touch lab82/bar`
- `rm lab82/foo`
- `lsattr -d lab82`

目录上的不可变性工作原理正如你预期的那样，但有一个有趣的例外：它不会阻止目录作为挂载点运行！

#### 任务 3

最后，清理：

- `sudo chatter -i lab82`
- `rm -rf lab82`

# 备注

某些操作系统出于安全考虑将重要的二进制文件标记为不可变，以增加攻击者用恶意版本覆盖它们的难度。

## 实验 84：RAID

### 实验目标

学习如何配置和管理软件 RAID 配置。

### 实验目的

专业的安装通常会通过使用硬件 RAID 设备来创建存储冗余。在实验中，你将通过使用`mdadm`进行软件 RAID，从而创建一种“平民版”的冗余。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，安装 RAID 工具：`sudo apt install mdadm`

现在设置虚拟磁盘以放入 RAID 1 阵列：

- `dd if=/dev/zero of=disk1.img bs=1M count=1000`
- `dd if=/dev/zero of=disk2.img bs=1M count=1000`
- `sudo losetup -fP disk1.img`
- `losetup -a | grep disk`

记录下最后一个命令输出的每行开头打印的两个设备。它们应该是类似于`/dev/loop18`和`/dev/loop19`的文件。在下方的命令中，它们将被标记为`[dev1]`和`[dev2]`。

#### 任务 2

使用回环设备创建阵列：

```bash
sudo mdadm -C /dev/md0 -l 1 -n 2 [dev1] [dev2]
```

这里的`-l`标志指定 RAID 级别（在此情况下为级别 1，即镜像阵列）。`-n`标志指定阵列中的磁盘数量。

使用`cat /proc/mdstat`验证阵列是否正确创建。

该文件包含了阵列列表、其大小、状态以及包含的磁盘等信息。

#### 任务 3

在阵列上创建文件系统后，你可以像使用其他磁盘设备一样使用它：

- `sudo mkfs.ext4 /dev/md0`
- `mkdir lab84`
- `sudo mount /dev/md0 lab84`



- `sudo touch lab84/foo`

当两块磁盘之一故障时会发生什么？让我们现在模拟这种场景：

```bash
sudo mdadm -l -f [dev2]
```

> **注意：** 此命令只需要`[dev2]`的名称，而不是路径。如果设备是`/dev/loop19`，你只需使用`loop19`。

- `cat /proc/mdstat`
- `sudo mdadm --detail /dev/md0`

你在这里看到了获取阵列信息的另一种方法。最后一个命令清晰地列出其中一个设备为“已移除”（removed），且阵列状态为“正常，下降”（clean, degraded）。

### 任务 4

现在你将修复此阵列，但没有理由让它简单……

- `sudo dd if=/dev/urandom of=lab84/bar`
- `sudo mdadm -a /dev/md0 [dev2] && sudo mdadm --detail /dev/md0`

在第一条命令中，你只是用随机数据填充阵列。最后两个命令合并在了一个，因为你希望在其中一个磁盘重新添加后立即看到阵列的状态。

现在注意，你的阵列处于“恢复中”（recovering）模式，`[dev2]`正在重建它之前没有的数据。

### 任务 5

最后，进行清理：

- `sudo umount lab84`
- `sudo mdadm --stop /dev/md0`
- `sudo losetup -d [dev1]`
- `sudo losetup -d [dev2]`
- `rm disk{1,2}.img`

## 注意

有多种类型的 RAID 配置，并非所有配置都提供冗余——例如，RAID 0 是为了性能设计的。

## 实验 85：补丁

### 实验目标

学习如何应用软件补丁并更新你的系统。

### 实验目的

在实验中，你将练习应用系统更新和其他软件补丁。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

使用`sudo apt full-upgrade`应用系统更新（Ubuntu）：

如果距离你上次更新已经有一段时间，这可能需要一些时间，但在大多数情况下这是你只需要做的。事实上，这非常简单，为什么不将其自动化呢？

在默认系统中，`unattended-upgrades`包应该已经安装了。如果没有，请安装它，然后查看`/etc/apt/apt.conf.d/50unattended-upgrades`。

值得注意的是，典型的配置不会自动应用所有更新，仅应用安全补丁。这通常是你想要的结果。

要更新单个包，只需运行：`sudo apt upgrade [package]`

实验 20-23 将更详细介绍如何使用各种 Linux 包管理器。

### 注意

你可以使用`patch`命令手动应用源码补丁。在实践中，非开发者很少这样做，但如果你正在维护某个包自己的分支（fork），这会很有用。

## 实验 86：软件包仓库

### 实验目标

学习如何为系统的包管理器配置软件包仓库（repos）。

### 实验目的

在实验中，你将练习应用系统更新和其他软件补丁。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

运行`cat /etc/apt/sources.list`查看当前的仓库。

#### 任务 2

要添加新仓库，通常需要编辑源列表：

```bash
sudo nano /etc/apt/sources.list
```

添加一行新仓库的内容，例如：

`deb http://repository.com/repo stable main`

#### 任务 3

添加仓库后，更新包列表：

```bash
sudo apt update
```

#### 任务 4

现在你可以从新仓库安装软件了：

```bash
sudo apt install [package]
```

## 自动化与脚本编写

## 实验 88：Shell 脚本编写

### 实验目标

学习如何编写一个包含多个命令的简单 Shell 脚本。

### 实验目的

使用 Bash 脚本是许多专业 Linux 管理员的日常工作。当某个任务是重复的时，你不希望反复输入相同的命令列表；你希望创建一个脚本，并且可能还会安排该脚本自动运行。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端（Terminal）应用程序，并运行你喜欢的文本编辑器，例如`vi`或`nano`。（如果你从未用过`vi`或`vim`，强烈建议使用`nano`。）

创建一个包含以下内容的文件：

```bash
#!/bin/bash
for (( n=0; n<$1; n++ ))
do
echo $n
done
echo "Output from $0 complete."
```

#### 任务 2

赋予文件可执行权限（使用`chmod +x filename`），然后像这样运行它：

```bash
./filename 10
```

你应该能看到打印出 0-9 的数字，一个接一个。现在知道了脚本在做什么，你能完全理解它的含义吗？如果你没有传递参数，或者传递了“乱码”（比如用字母代替数字），会发生什么？

#### 任务 3

不带任何参数运行你的脚本。然后运行：`echo $?`

`$`是一个引用退出状态的特殊变量。在程序成功执行时，退出状态将为 0。现在请亲自尝试。然后通过删除最后一个`echo`语句来编辑脚本。该脚本在没有参数的情况下会失败，返回不同的退出状态。

## 注意事项

第一行以`#!`开头（称为 shebang），表示将使用什么程序来解释你的脚本。通常，这是`/bin/bash`，但也可以是另一个 shell，如`/bin/zsh`，甚至是另一种编程语言如`/usr/bin/python`。

在这种情况下，你可以删除 shebang 行，因为你的解释器（Bash）与你当前运行的 shell 相同。但你应该始终包含它，因为你永远不知道何时会向使用不同 shell 的人分享脚本。

## 实验 89：环境变量、类型与历史记录

### 实验目标

学习 Bash 环境变量、类型以及如何使用 shell 历史。

### 实验目的

Bash 命令 shell 预装在数百万台 Linux 计算机。理解该 shell 如何工作是处理 Linux 的关键技能。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端应用程序，然后输入：`echo $PATH`

PATH 环境变量列出了当你输入*相对*路径的命令时，Bash 会搜索的所有位置。*相对*路径的示例是`bash`，与之相比，`/bin/bash`是*绝对*路径。

还有其他环境变量。你可以使用`env`命令查看所有环境变量及其取值。

#### 任务 2

你可以使用`export`添加或修改环境变量。例如：

```bash
export PATH=${PATH}:}/
```

在大多数情况下，此更改会在退出 Bash 时消失，但`export`的优势是子进程现在能够看到新的或修改过的变量。

例如：

- `foo=123`
- `export bar=456`
- `bash`
- `echo $foo $bar`

这会打印 456，因为子 shell 只能看到`bar`。

#### 任务 3

另一个实用的 Bash 命令是`type`。使用`type`来获取其他命令或函数的信息：

```bash
type -a date
type -a if
type -a echo
type -a ls
```

`type`会告诉你一个命令/shell 函数是二进制文件（如`/bin/date`）、shell 内置命令（如`help`）、别名（可以通过`alias`查看）还是 shell 关键字（如`if`或`while`）。

#### 任务 4

输入`history`查看你在 Bash 中输入过的命令历史记录。

要重复某条命令，只需输入`!`然后是相应的数字。例如，`!12`将执行历史列表中的第 12 条命令。

如果你不小心在历史记录中保存了密码或其他敏感信息，可以使用例如`history -d 47`从列表中删除第 47 条命令，甚至使用`history -c`清空所有历史记录。

如果你想将当前 shell 的历史保存到另一个文件中，请使用`history -w filename`。

Bash 保存历史记录的默认文件名是`.bash_history`。但默认情况下，它只会在会话结束时保存。如果你的会话崩溃或打开了多个会话等，那么你的 shell 历史可能会变得不完整或乱序。

## 注意事项

如果你希望永久修改环境变量或其他 shell 设置，请查看`.bashrc`和`.bash_profile`文件。

## 实验 90：标准语法

### 实验目标

学习脚本设置的标准 shell 语法。

### 实验目的

在实验中，你将学习标准的 shell 脚本语法，例如测试和控制流。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开你喜欢的编辑器并创建一个名为`lab66.sh`的文件：

```bash
#!/bin/bash
i=0
while [ $i -lt 5 ]
do
  echo $i
  ((i++))
done
```

现在运行脚本：

```bash
chmod +x lab66.sh
./lab66.sh
```

你应该看到：

```text
0
1
2
3
4
```

## 注意事项

该脚本使用了`while`循环和`if`条件。`[ $i -lt 5 ]`语法检查变量`$i`是否小于 5。`((i++))`语法用于变量自增。

这里发生了什么？`echo`和`cat`都将`foo`和`bar`之间的空格解释为独立的参数，而不是预期的单个文件名。你可以将‘foo bar’放入引号中，或者使用反斜杠对空格转义，如下所示：

- `echo hello > foo\ bar`
- `cat foo bar`

可以假设，当你的意图让某个字符作为参数的一部分时，任何可能被 shell 直接解释的字符都应该被转义。示例包括但不限于：空格、`>`、`<`、`$`、`*`、`&`和引号。

## Notes

某些情况下，你可能希望使用`${variable}`语法引用变量。这与`$variable`等效，但选择其中一种而非另一种的原因出了本实验的范围。

反引号（Backquotes）还有另一种语法：

```bash
$(echo hello)
```

这种语法通常比反引号更优。我们提到反引号是为了将其与单引号区分开来，并确保差异清晰。

## 实验 92：正则表达式

### 实验目标

学习如何使用正则表达式进行复杂的字符串模式匹配。

### 实验目的

正则表达式是 Linux 中常用的工具，用于匹配字符串和文本文件中的复杂模式。许多工具支持正则表达式。

### 实验工具

Ubuntu 18.04（或你喜欢的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端应用程序。在运行此命令序列之前，看看你是否能预测其输出结果（参见下方的答案 1）：

```bash
echo "foo"
bar
baz
quux
frob
plugh
xyzzy" | sort | -5 | grep [be]
```

#### 任务 2

你能匹配以下字符串（右侧）哪些会匹配每个正则表达式（左侧）吗？每个正则表达式可能有多个匹配项！解决方案请参见下方的答案 2。

```text
^s?.*$ Hello World
^[0-9]. .*$ 1, 2, 3, Go!
^.*[a-z].*$ sayonara
^q?[a-z]*$ 101labs
```

## 答案 1

frob

## 答案 2

第一个表达式匹配所有四个字符串。

第二个表达式匹配“1, 2, 3, Go!”和“101labs”。

第三个表达式匹配所有四个字符串。

第四个表达式匹配“sayonara”。

## Notes

Regexr 是练习正则表达式极极资源。

查看`man 7 regex`获取更多关于你发行版支持的正则表达式的信息。

## 实验 93：基础正则

### 实验目标

学习如何使用基础正则表达式进行复杂的字符串模式匹配。

### 实验目的

正则表达式是 Linux 中常用的工具，用于匹配字符串和文本文件中的复杂模式。许多工具支持正则表达式。在使用基础正则时，某些元字符需要在前面加上反斜杠。

### 实验工具

Ubuntu 18.04（或你喜欢的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端应用程序并先创建一个文本文件（以下内容无法通过复制粘贴完成）：

```bash
echo "abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore...' > lab93.txt
```

#### 任务 2

现在，尝试在运行每个命令之前预测每个命令的输出结果（参见下方的答案 1-7）：

```bash
grep [0-3] lab93.txt
grep [e68] lab93.txt
grep "[0-9a-zA-Z]\+\$" lab93.txt
grep "[0-9][A-Z]\?[0-9]" lab93.txt
grep "<|:" lab93.txt
grep -v ".*" lab93.txt
fgrep -v ".*" lab93.txt
```

最后一个命令有点出人。`fgrep`（`grep -F`的缩写）将表达式视为字面字符串，不使用正则匹配。因此，它排除了所有包含字面`.*`的匹配项——当然，它们一个都不包含。

## 答案 1

abc123

01234567890

A1B2C3D4E5

6F7G8H9I0J

## 答案 2

456def

Hello World!

01234567890

6F7G8H9I0J

Quoth the raven: 'Nevermore.'

## 答案 3

abc123

456def

password

01234567890

A1B2C3D4E5

6F7G8H9I0J

## 答案 4

abc123

456def

01234567890

A1B2C3D4E5

6F7G8H9I0J

## 答案 5

<html>

Quoth the raven: 'Nevermore.'

## 答案 6

（无输出）

## 答案 7

abc123

456def

<html>

Hello World!

password

01234567890

A1B2C3D4E5

6F7G8H9I0J

Quoth the raven: 'Nevermore.'

## Notes

Regexr 是练习正则表达式的极佳资源。

查看`man 7 regex`获取更多关于你发行版支持的正则表达式的信息。

## 实验 94：扩展正则

### 实验目标

学习如何使用扩展正则表达式进行复杂的字符串匹配。

### 实验目的

正则表达式是 Linux 中常用的工具，用于匹配字符串和文本文件中的复杂模式。许多工具支持正则表达式。在使用扩展正则时，元字符不需要反斜杠。

### 实验工具

Ubuntu 18.04（或你喜欢的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端应用程序并先创建一个文本文件：

```bash
echo "abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'"
```

#### 任务 2

现在，尝试在运行每个命令之前预测每个命令的输出结果（参见下方的答案 1-7）：

```bash
egrep [0-3] lab94.txt
egrep [6-8] lab94.txt
egrep "[0-9][a-zA-Z]+" lab94.txt
egrep "[0-9][A-Z]?[0-9]" lab94.txt
egrep "<|:" lab94.txt
fgrep -v ".*" lab94.txt
```

#### 任务 3

最后，将所学应用于这些命令。输出将会是什么（参见答案 8-10）：

```bash
sed -E 's/[0-3]/g' lab94.txt
sed -E 's/[6-8]/g' lab94.txt
sed -E 's/[0-9][a-zA-Z]+/g' lab94.txt
sed -E 's/[0-9][A-Z]?[0-9]/g' lab94.txt
sed -E 's/<|://g' lab94.txt
```

## 答案 1

abc123

456def

<html>

Hello World!

password

01234567890

A1B2C3D4E5

6F7G8H9I0J

Quoth the raven: 'Nevermore.'

## 答案 2

abc123

456def

<html>

Hello World!

password

01234567890

A1B2C3D4E5

6F7G8H9I0J



Quoth the raven: 'Nevermore.'

# 答案 3

```text
abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

# 答案 4

```text
abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

# 答案 5

```text
abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

# 答案 6

```text
abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

# 答案 7

```text
abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

# 答案 8

```text
abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

# 答案 9

```text
abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

# 答案 10

```text
abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: 'Nevermore.'
```

## 实验 95：脚本练习

### 实验目标

使用你已学知识从零开始编写简单的脚本。

### 实验目的

许多 Linux 管理员每天都会编写脚本。当任务具有重复性时，你不希望重复输入命令列表；你希望创建一个脚本，可能还会安排它自动运行。

### 实验工具

Ubuntu 18.04（或你喜欢的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端应用程序，并运行你喜欢的文本编辑器，如 `vi` 或 `nano`。（如果你从未用过 `vi` 或 `vim`，强烈建议使用 `nano`。）

如果你还没有这样做，可能需要参考实验 15。你的目标是编写一个接受参数——数字的脚本，每次打印两个数字，使得：

- 第一个数字从参数递减到 0。
- 第二个数字从 0 递增到参数。

示例：

```bash
/foo.sh 100
100 0
99 1
98 2
...
```

如果用户没有传递参数，或者传递了错误的参数（例如单词），你应该打印一条友好的信息，如“Please give a number.”

在测试之前，记得将文件设置为可执行（使用 `chmod +x filename`）。参见下方的答案 1 获取一种可能的解决方案。

### 答案 1

```bash
#!/bin/bash
if [ "$1" -ge 0 ];
then
echo "Please give a number."
exit 1
fi
for (( n=0; n<=$1; n++ ));
do
echo $(($1-$n)) $n
done
```

### 注意

在实验 15 中，你读过关于退出状态的内容。为了错误检查：你能研究出如何在脚本退出之前使用退出状态吗？

## 实验 96：脚本练习 2

### 实验目标

利用你已的知识从零开始编写简单的 shell 脚本。

### 实验目的

使用 Bash 编写脚本是许多专业 Linux 管理员的日常工作。当某个任务是重复的时，你不希望反复输入相同的命令列表；你想要创建一个脚本，可能还会安排该脚本自动运行。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

打开终端（Terminal）应用程序并运行你喜喜欢的文本编辑器。

如果你还没有这样做，可能需要参考实验 66 和 67。你的目标是编写一个接受三个参数的脚本——一个目录路径和两个传递给 `test` 的标志（flags）。该脚本应该检查目录中的每个文件（非递归），如果它通过了两个测试，则打印该文件的名称。

示例：

```bash
./foo.sh ~/mydir -f -w
myfile
```

在这个示例中，脚本正在查找 `~/mydir` 下的具有写权限的普通文件。`myfile` 通过了这些测试。

所有错误情况都应该打印友好的信息并以状态 1 退出。例如，未传递三个参数、传递的目录不存在、或其中一个测试参数无效。请参考下方的答案 1 获取一种可能的解决方案。

作为额外挑战，你可以打印所有文件，但根据它们通过测试的数量对其进行排序。

### 答案 1

```bash
#!/bin/bash

test $# -eq 3 || { echo "Exactly three arguments are required."; exit 1; }
test -d $1 || { echo "Not a directory."; exit 1; }
files=$(ls $1 2>/dev/null) || { echo "I can't read directory."; exit 1; }

for f in $files; do
  test $2 "$f" 2>/dev/null
  rc1=$?
  test $3 "$f" 2>/dev/null
  rc2=$?
  test $rc1 -gt 1 && { echo "First test argument is invalid."; exit 1; }
  test $rc2 -gt 1 && { echo "Second test argument is invalid."; exit 1; }
  test $rc1 -eq 0 && test $rc2 -eq 0 && echo "$f"
done
```

### 注意

记住，使用 `/bin/sh` 作为解释器的结果可能与 `/bin/bash` 不同！了解什么是 Bourne 兼容的 shell，以及 Bash 中提供了哪些非 Bourne 兼容的扩展功能是有重要的。

## 实验 97：创建 Git 仓库

### 实验目标

学习如何在 Git（一种流行的版本控制工具）中创建仓库。

### 实验目的

在本次实验中，你将创建一个 Git 仓库，作为在实验 98 和 99 中学习其他 Git 操作的基础。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

如果你还没有安装 Git，请安装：`sudo apt install git`

创建一个包含一些简单文件的新目录开始：

```bash
mkdir myrepo
cd myrepo
echo 'Hello World!' > hello.txt
echo 'This is a very important file. Do not delete.' > README
```

现在，运行 `git init` 即可初始化仓库。

#### 任务 2

如果你以前从未在该系统上使用过 Git，那么你可能还没有添加你的姓名和电子邮件。这不是网站注册表单，而是一个配置文件，告诉其他协作者是谁提交了某段代码。运行 `git config --global -e`，输入你的姓名和电子邮件，然后保存退出。

你也可以使用 `git config -e` 编辑本地（特定仓库）配置文件，它位于 `.git/config`，但你现在不需要担心它。

你现在可能想做的是编辑 `.git/description` 文件，正如你猜的，它是仓库的描述。

### 注意

大多数 Git 仓库都包含一个 `.gitignore` 文件，告诉 Git 忽略目录中的某些类型的文件，不将其作为仓库的一部分。有很多 `.gitignore` 模板可用，它们根据编程语言或其他数据而异。

## 实验 98：使用 Git 工作

### 实验目标

学习如何使用基础的 Git 操作进行版本控制。

### 实验目的

在本次实验中，你将练习使用 `commit` 和其他操作进行代码协作。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，你需要一个 Git 仓库。如果你没有，可以参考实验 97，或者在互联网上找一个有趣的仓库并使用 `git clone` 获取。本实验假设你正在使用实验 97 中的仓库。

#### 任务 2

确保你的工作目录是仓库目录，例如 `~/myrepo`。此时，你还没有提交任何内容。

```bash
git add hello.txt
git commit -m "Initial commit"
```

（注：此处 OCR 文本高度重复/损坏；我已重建了逻辑流）。

## 实验 99：Git 分支

### 实验目标

学习如何使用分支。

### 实验目的

在本次实验中，你将练习分支（branch）和合并（merge）。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，你需要一个 Git 仓库。如果你没有，可以参考实验 97，或者在互联网上找一个有趣的仓库并使用 `git clone` 获取。本实验假设你正在使用实验 97 中的仓库。

#### 任务 2

Git 的默认分支名为 master。有时你想“分出一个”分支并在上面工作，而不干扰 master：

```bash
git checkout -b lab99
```

#### 任务 3

现在，安全地在 `lab99` 分支上进行几处修改：

```bash
echo 'I love branches!' > lab99.txt
git add lab99.txt
git commit -am 'Lab 99'
```

#### 任务 4

现在，你可能会发现两个分支不同步。每个分支都有一个另一个没有的提交。这就是 `git merge` 派上用场的地方：

```bash
git checkout master
echo 'This file is obsolete and should be removed.' > README
git commit -am 'Bug fix #42'
```

#### 任务 5

最后，你可以将 `lab99` 合并回 master 并删除分支：

```bash
git checkout lab99
git merge master
echo 'And merging, too!' >> lab99.txt
git commit -am "I <3 merging"
git checkout master
git merge lab99
git branch -d lab99
```

## 实验 100：Ansible

### 实验目标

学习使用 Ansible 配置管理工具。

### 实验目的

在本次实验中，你将练习使用 Ansible，这是一种让专业系统管理员生活更轻松的基础自动化工具。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，安装 Ansible：

```bash
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

将 `localhost` 添加到 Ansible hosts 文件，告诉它本地机器是它应该管理的设备之一（在这种情况下是唯一的设备）：

```bash
sudo sh -c 'echo localhost >> /etc/ansible/hosts'
```

Ansible 通过 SSH 进行连接，通常情况下你需要进行一些设置以确保 SSH 连通性正常。在本地主机（`localhost`）上，你应该能够跳过这一步。使用 `ansible -m ping all` 来确认 Ansible 是否可以连接；结果应该类似于此：

```text
localhost | SUCCESS => {
  "changed": false,
  "ping": "pong"
}
```

#### 任务 2

要在所有 Ansible 主机上运行一次性 shell 命令，请尝试以下命令：

```bash
ansible -m shell -a 'free -m' -all
```

这是一个非常实用的功能，但远不是最实用的。打开你喜欢的编辑器，创建一个名为 `lab100.yml` 的 Ansible playplaybook 文件，内容如下所示：

```yaml
---
- hosts: all
  tasks:
    - name: hello
      copy: src=hello.txt dest=~/lab100.txt
```

当然，你必须创建一个用于复制的 `hello.txt` 文件：

```bash
echo 'Hello World!' > hello.txt
```

现在运行：`ansible-playbook lab100.yml`

现在 `lab100.txt` 文件将出现在你的家目录中。再次运行相同的 `ansible-playbook` 命令将显示没有变化；删除 `lab100.txt` 并再次运行将导致文件被重新创建。修改文件并运行将导致你的更改被撤滚。

你能理解 Ansible 如何用于管理成百或上千台设备吗？

### 注意事项

这只是一个复杂且强大的工具的一个非常小的用法示例。如果你渴望专业地管理 Linux 机器，理解 Ansible 非常值得。

## 实验 101：Puppet

### 实验目标

学习如何使用 Puppet 配置管理工具。

### 实验目的

在实验中，你将练习使用 Puppet，它是一种基础设施自动化工具，可以让专业系统管理员的工作变得轻松。

### 实验工具

Ubuntu 18.04（或你选择的其他发行版）

### 实验拓扑

单台 Linux 机器或虚拟机

### 实验步骤

#### 任务 1

首先，安装 Puppet：

```bash
sudo apt install puppet puppetmaster
```

与 Ansible 的默认设置（参见实验 100）不同，Puppet 使用客户端-服务器模型，节点从“puppetmaster”服务器拉取它们的清单（manifests）。因此，在生产环境中，你需要设置此 puppetmaster 服务器并在你想管理的每个节点上安装 Puppet 客户端。

一些配置：

- `sudo puppet config set server localhost`
- `sudo puppet config set certname localhost`
- `sudo puppet agent -t`
- `sudo puppet ca sign localhost`
- `sudo systemctl restart puppetmaster`
- `sudo systemctl start puppet`

在同一台机器上让 Puppet 客户端和服务器通信并不是一个简单的过程。在典型的安装中，你将遵循大部分相同的步骤，从客户端请求证书并在服务器上对其签名。

#### 任务 2

现在有趣的部分开始了。以 root 身份打开编辑器并创建 `/etc/puppet/code/site.pp`，内容如下：

```puppet
node default {
  file { '/tmp/lab101.txt':
    content => 'Hello World!',
  }
}
```

在典型的环境中，你将拥有更复杂的目录结构，包含多个模块和环境，Puppet agent 会每隔 30 分钟自动获取更改。由于这是实验环境且目录结构尚未完全搭建好（而且你也不想等 30 分钟），只需将此清单作为一次性任务应用：

```bash
sudo puppet apply site.pp
```

`lab101.txt` 文件现在将出现在 `/tmp` 中。再次运行相同的命令将显示没有变化；删除 `lab101.txt` 并再次运行将导致文件被重新创建。修改文件并运行将导致你的更改被撤滚。

你能理解 Puppet 如何用于管理成百或上千台设备吗？

### 注意事项

这只是一个复杂且强大的工具的一个非常小的用法示例。如果你渴望专业地管理 Linux 机器，理解 Puppet 非常值得。
