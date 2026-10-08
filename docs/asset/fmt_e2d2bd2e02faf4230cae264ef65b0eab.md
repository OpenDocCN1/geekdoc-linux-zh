
# 这是 HostA 的 exports 文件

`/mnt/cdrom` * `(ro)`

`/home/inst_files` * `(ro)`

`/home/monthly/reports` `HostB(rw)`

`[root@HostA /root#]`

```
/etc/exports` 文件中的项表示 `HostB` 对 `/home/monthly/reports` 读写权限。这里的 NFS 假设很重要。假设是如果没有定义主机或 `*` 符号，则所有主机都可以访问。然而，一旦定义了单个主机，只有该主机可以访问，其他都被拒绝。因此，前两个导出语句允许任何主机，但底部的项限制了对系统 `HostB`（即 `192.168.1.208`）的访问。NFS 提供的安全性中等。例如，有人可能会等待你的系统宕机，然后通过启动另一个 IP 地址为 `192.168.1.208`、主机名为 `HostB` 的系统来伪装你的系统，从而破坏信任关系。由于由于原因，系统管理员限制了 NFS 的使用。NFS 系统通常位于防火墙内部或可以控制的更安全环境中。这里只有两个任务：只读和读写。我们设置此用户场景是为了演示读写行为。

以下示例显示了如何停止和启动 NFS 守护进程并刷新系统以识别 `/etc/exports` 文件的更改：

```
[root@HostA /root#] cd /etc/rc3.d

[root@HostA rc3#]# .S60nfs stop

Shutting down NFS mount:      [ OK ]

Shutting down NFS daemon:     [ OK ]

Shutting down NFS services:   [ OK ]
```

TEAM Ling - 现场、互动、免费且正版！

# 通过 NFS 安装 Linux

```
Shutting down NFS quotas:

[root@HostA rc3]# /.s60nfs start

Starting NFS services: OK

Starting NFS quotas: OK

Starting NFS mountd: OK

Starting NFS daemon: OK

[root@HostA rc3]#

[root@/root]# exports -ua

[root@/root]# exports -a

[root@/root]# exports

/home/monthly/reports
```

`HostA` 现在可以挂载 `HostB` 的 `/home/monthly/reports`。接下来的示例均取自 `HostB`，即 NFS 客户端。确认成为 NFS 客户端的假设是：

在本地系统上挂载 NFS 系统或目录之前，你需要创建一个挂载点。挂载点应该是一个空目录，因为当你挂载 `HostA:/home/monthly/reports` 目录时，它将覆盖所有内容作为挂载点。换句话说，如果你选择将 `HostA:/home/monthly/reports` 挂载到 `/home/alan`，那么用户 alan

...将再也无法看到其家主目录中的文件。某些系统管理员创建了一系列名为 `/mnt1` 和 `/mnt2`（此类此类）的目录。其他系统管理员则使用其他方法。作为下一步，我们将创建一个名为 `/home/final` 的空目录。然后，我们将 `HostA:/home/monthly/reports` 挂载到 `/home/final`。因此，在 `HostB` 上，远程挂载的直接路径就变成了 `/home/final/monthly/reports`。

```
[root@HostB /root]$# mkdir /home/final
```

有几种方法可以通过 NFS 挂载远程文件系统。你可以在 `/etc/fstab` 文件中创建如下的条目，然后执行 `mount` 命令。或者，你也可以直接在命令行输入带有完整条目的 `mount` 命令。这种知识对于临时挂载非常有用，因为 `/etc/fstab` 中没有该条目。后者的命令语法如下：

```
[root@hostb /root]$# mount -t nfs HostA:/home/monthly/reports /home/final
```

如果此挂载将被反复使用，那么在 `/etc/fstab` 文件中创建条目将是合适的。该文件系统可以在每次启动时自动挂载。

```
[root@hostb /root]$# cat /etc/fstab

LABEL=/ - ext2 defaults 1 1

LABEL=/boot /boot ext2 defaults 1 2

/dev/fd0 /mnt/floppy auto noauto,owner 0 0

none /proc proc defaults 0 0

none /dev/pts devpts gid=5,mode=620 0 0

/dev/sda6 swap defaults 0 0

/dev/cdrom /mnt/cdrom iso9660 noauto,owner,kdu,ro 0 0

HostA:/home/monthly/reports /home/final exec,devid,suid,rw 1 1

[root@hostb /root]$# mount /home/final

[root@hostb /root]$# mount

/dev/sda6 on type ext2 (rw)

none on /proc type devpts (rw)

/dev/hd1 on /boot type ext2 (rw)

one on /dev/pts devpts (rw,gid=5,mode=620)

automount (pid627) on /misc type

autofs(rw,fd=5,pgpr=627,minproto=2,maxproto=3)

HostA:/home/monthly/reports on /home/final file types

rw,addr=192.168.1.206

[root@hostb /root]$
```

# TEAM LinG - 现场、信息丰富、无成本且真实！

# 使用 NFS 安装 Linux 117

当你熟悉了语法后，NFS 挂载变得简单且有许多用途。系统管理员通常将日常使用的所有软件和工具保留在一个单一系统中。当他们需要访问文件时，会快速设置 NFS 导出和挂载。应用程序利用 NFS 文件系统挂载是非常典型的用法。例如，Web 服务器群中的几个 Web 服务器都可以访问相同的 Web 根目录内容，而不是将内容复制到每个位置。数据库服务器可以配置为将数据的目录导出到一系列客户端，以平衡负载。

你必须意识到 NFS 服务器和 NFS 客户端之间通信的本质。NFS 客户端依赖于 NFS 服务器，如果 NFS 服务器关闭或不可用，NFS 客户端守护进程将不断重试连接。这种连接会导致 NFS 客户端的利用率高到系统无法使用的程度。你可以通过调整计时参数在某种程度上缓解这种情况，但真正的解决方案是确保 NFS 服务器保持可用。由于这些依赖关系和时机问题，不应在不稳定的网络介质或可能减慢连接的路由器上执行 NFS 挂载。你必须开始记录哪些系统是导出器（exporter），哪些系统是监控器（monitor），以便确保在任何一个系统关闭之前所有挂载都已卸载。例如，在关闭 NFS 客户端之前，你应该先卸载 NFS 文件系统。在关闭 NFS 服务器之前，你必须在所有 NFS 客户端上卸载所有的 NFS 文件系统。

这里涉及权限问题。此时，如果你正在使用我们的示例来创建 NFS 挂载，你会发现任何用户（包括 root 用户）都无法访问挂载的目录。

## 定制和升级 Linux

我们选择此产品是因为它支持所有 Windows 平台，而不仅仅是 NT。Xlink 的人员还提供试用版，让您在购买之前评估该产品。

## 设置 NFS 服务器

### 第 1 步下载并安装 NFS 服务器代码

为了在 Windows 上演示 NFS 服务器，我们从 `www.xlink.com` 下载了测试代码。下载的可执行文件名为 `nfse2k.exe`。在安装过程中我们接受了所有默认设置。安装成功后，你应该会在“服务”面板中看到一个新服务。首先启动 Omni-NFS Server 服务（参见图 4.4）。

### 第 2 步导出 Windows 目录

你基本上可以导出任何需要的目录。我们有一个名为 `c\downloads` 的直接目录。点击“开始 ... 程序 ... Omni-NFS Enterprise V5.02 ... NFS 服务器”。将出现以下面板。导航到你想要导出到 Linux 系统的目录并点击确定。在我们的示例中，我们将此导出设置为对所有 NFS 客户端“只读”，以确保无人修改 Windows 系统上的文件。请确保在 Windows 系统上停止并重新启动 NFS 服务，以使导出生效（参见图 4.5）。

![](img/cf6993b0699c37d6fb92721201c599d8_138_0.png)

图 4.4 在 Windows 上启动 NFS 服务。

## 使用 NFS 安装 Linux

![](img/cf6993b0699c37d6fb92721201c599d8_139_0.png)

图 4.5. 通过服务器配置中心导出 Windows 目录。

## 设置 NFS 客户端

### 第 1 步更新 /etc/hosts

我们将 Linux `HostA` 配置为 NFS 客户端，但首先我们应该更新 hosts 文件，以便 `HostA` 能够找到位于 IP 为 `192.168.1.101` 的名为 `WCS_SKILLS` 的 NFS 服务器：

```
linda@HostA~$ su - root

Password:

[root@HostA /root]# cat /etc/hosts

# 不要删除以下行，否则各种需要

# 网络功能的程序将会失败。

127.0.0.1        localhost.localdomain   localhost

192.168.1.206      HostA

192.168.1.101      WCS_SKILLS
```

### 第 2 步创建挂载点

我们决定将挂载的文件系统设为 `/upgrade/files`。在下一步挂载 NFS 文件系统之前，该目录将是一个空目录。

```
[root@HostA /root]# mkdir -p /upgrade/files

[root@HostA /root]# ls -l /upgrade/files

0
```

## 定制和升级 Linux

### 第 3 步挂载 NFS 导出目录

我们将 Windows 系统上名为 `\\downloads` 的 NFS 导出目录挂载到新创建挂载点 `/upgrade/files` 上。为了完成此任务，我们将使用名为 `linuxconf` 的工具。该工具会在 `/etc/fstab` 文件中添加 NFS 挂载条目。如果你知道语法，可以编辑 `/etc/fstab` 文件。

`linuxconf` 工具默认未安装，其 `rpm` 包在发行版 CD 中提供。使用 `rpm` 工具安装 `linuxconf`。安装 `linuxconf` rpm 后，你还必须启动 `linuxconf` 服务。使用 `ntysav` 工具启动 `linuxconf` 服务。4.6。

### 第 4 步挂载 NFS 目录

如前所述，`linuxconf` 工具并没有挂载目录。它只是配置了 `/etc/fstab` 文件中的条目。

```
root@HostA[/root]# cat /etc/fstab

LABEL=/             ext2 defaults 1 1

LABEL=/boot /boot ext2 defaults 1 2

/dev/d0 /mnt/floppy auto noauto,owner 0 0

none /proc defaults 0 0

none /dev/pts devpts gid=5,mode=620 0 0

/dev/hda swap defaults 0 0

/dev/cdrom /cdrom iso9660 noauto,owner,kudzu,ro 0 0

WCS_SKILLS: /downloads/upgrade/files nfs exec,dev,rw 1
```
![](img/cf6993b0699c37d6fb92721201c599d8_140_0.png)

图 4.6 使用 linuxconf 配置 NFS 挂载。

```
[root@HostA /root]# mount /upgrade/files

[root@HostA /root]# ls -l /upgrade/files

total 25913

-rwxxr-x 1 429467294 429467294 2534489 Jun 26 15 linux-2.4.5.tar.gz
```

现在 Windows 系统 `c:\downloads` 中的所有文件对 Linux 系统可用。

#

![](img/cf6993b0699c37d6fb92721201c599d8_143_0.png)

## 配置视频

在第 3 章中，设置显示器期间，我们选择了通用的 SVGA 驱动，稍后会对视频模式和色深进行调整。本章专门介绍第 3 章遗留的视频配置。我们讨论了 XConfig 文件（它是服务器的基础），以及如何生成视频适配器。我们简要讨论了另一个程序。

在讨论视频配置之前，我们为理解电视和视频显示奠定了技术基础，因为有几个名称描述了相同的概念。

## 视频生成

当数据首次在中央处理器（CPU）的主板（也称为 RAM）生成时，它们被格式化为数字信号。发往显示器的信号是通过主板本身或组件连接（PCI）、工业标准架构（ISA）、加速图形端口（AGP）或其他插槽设计并安装的。在图 5.1 中，我们画了一个非常简化的视频适配器。显存（也称为 VRAM 或缓冲区）通常由与主内存不同的芯片组成。

![](img/cf6993b0699c37d6fb92721201c599d8_144_0.png)

图 5.1 视频适配器。

## 配置视频 127

在 AGP 技术的情况下，视频硬件可能直接访问计算机系统的主 RAM 以补充显存。关于需要多少显存，所需的量是色深和分辨率的函数。我们接下来主要通过示例定义这些概念。

仔细观察你的显示器，你可以看到数千个点。这些点是像素（picture elements 的缩写），是电子束通过光栅罩聚焦到显示器涂光屏幕内部的结果。每个像素由三种颜色组成：红、绿、蓝。根据你的显示器容量和驱动它的视频硬件，你的屏幕可能有 480 行 640 像素，或 1200 行 1600 像素。每个像素代表存储在显存中的数据。

每个像素代表多少数据？这取决于你在屏幕上想要多少颜色。假设对于非常基本的表格、文字处理文档或其他简单图像只需要 16 种颜色。对于 16 色，每个像素需要 4 位（半字节）显存。另一方面，如果你有 256 色，每个像素需要 8 位数据（即一个字节显存）。如果你有 65536 色（通常称为高色），则你需要 16 位（两个字节）显存，如果你需要 1768 万种颜色（真色彩），则每个像素需要 24 位（三个字节）内存。甚至有一种基于 32 位或四字节显存的颜色定义级别，可以提供高达 43 亿种颜色。这些 4 位、8 位、16 位、24 位或 32 位（或者，如果你喜欢，分别为半字节、一字节、双字节、三字节或四字节）的每像素规格被称为色深。

正如刚才提到的，你的屏幕可能由 480 行 640 像素或 1200 行 1600 像素组成（或介于之间）。这些维度通常通过宽度和行数来描述——例如 640 × 480、1024 × 768、1600 × 1200 等——被称为分辨率。

另一个你会遇到的术语是视频模式。显示器显示能力的描述是分辨率和色深的组合。例如，“16 位，800 × 600”就是一个视频模式。

在本章的后面，当你使用 `Xconfigurator` 时，你会遇到一个标题为“选择视频模式”的对话框。该对话框提供了多个选项，你可以根据需要选择一个或多个。

分辨率和色彩深度。表 5.1 列出了你在对话框中找到的选项，以及其他一些选项，并提供了实现这些模式所需的显存估计值。底线是，如果你没有所需的内存，就不要期望你的视频硬件和显示器的组合能提供你请求的模式。另一方面，如果你拥有大量的显存，你可能会对 Linux 能够让你显示的图像如此精良且真实感到惊讶。

以下是我们用于计算表 5.1 中每个视频模式所需显存的公式：

```
VRAM required = color depth x line width x number of lines / 1,048,576
```

```
color depth 是每个像素的字节数；line width 是每行的像素数；number of lines 是屏幕的行数；1,048,576 是兆兆中的字节数。例如，你可以这样计算 8 位、800 × 600 视频模式所需的 VRAM 数量：
```

```
1 x 800 x 600 / 1,048,576 = 0.458 MB
```
