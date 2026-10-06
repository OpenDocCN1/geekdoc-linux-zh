
`xm command targetdomain`

其中 `command` 是你想应用于 `targetdomain` 的操作。`targetdomain` 可以是域名称或数字 ID。`options` 值表示如果特定命令需要可以包含的额外参数。

要检查 dom-0 和任何 dom-U 域是否运行，请在终端运行 `xm list` 命令，`xm` 将显示系统上运行的所有域。`xm list` 的示例输出如图 18-4 所示。

列表 18-4.

| Name | Mem(MiB) | VCPUs State | Time(s) |
| :--- | :--- | :--- | :--- |
| Dom-0 | 0 | 942 | 1 r----- | 38.8 |

图 18-4. `xm list` 命令显示 Domain-0 正在运行。如果你的 dom-0 不在列表中，你将无法运行客体。

在图 18-4 中，如果你看不到此表，你需要通过以下命令启动 `xend` 守护进程：

```
xend start
```

图 18-4 显示了五列，描述了当前运行域的状态：

Name（名称）：此列显示域的名称。在图 18-3 中，仅显示了 Domain-0。Domain-0 始终存在于管理程序上，并始终显示为第一个域。

ID：ID 列是域的数值值。你可以使用此 ID 或域名称作为要求你指定域的 Xen 命令的参数。

Mem(Mib)：此列显示分配给虚拟机的内存量。

VCUs：此列显示了为该域分配了多少个虚拟 CPU。状态被分为六个位置，每个位置代表域可以处于的一种状态。从左侧第一个位置开始依次是：阻塞（blocked）、暂停（paused）、关机（shutdown）和崩溃（crashed）。例如，如果域当前处于暂停状态，暂停位置上方将出现一个字母 p。空状态显示为连字符 `-`。

- Running (r)（运行）：域当前正在 CPU 上运行。如果你使用的是单 CPU 计算机，则除 Domain-0 之外的所有域此处将留空。

- Blocked (b)（阻塞）：域处于被阻塞状态，既不在运行也不可运行。这种状态可能是由于域等待来自网络连接的某些输入或输出。如果域无事可做，它也可能进入睡眠状态。

- Paused (p)（暂停）：域已被暂停，通常是管理员运行了 pause 命令。暂停的域仍会分配内存和 CPU 等资源，但无法被管理程序调度运行。

- Shutdown（关机）：域正在关机、重启或重新启动。当域处于销毁过程中，也会显示关机状态。

- Crashed (c)（崩溃）：域已崩溃。通常，只有当域被配置为不重启时，才会出现此种状态。

- Dying (d)（正在死亡）：域处于死亡过程中，但尚未完全关机或崩溃。

Time(s)（时间）：此列告诉你是由 Xen 计算的域运行时间（以秒为单位）。

`xdom` 的 `list` 命令是你可以用于管理 Xen 域的许多命令之一。在安装第一个客机后，你将学习额外的 xen 命令。

# 使用 virt-install 创建客机

有许多方法可以创建用于你的 Xen 设置的虚拟机。一种方法是将主机系统的文件系统克隆到目录或镜像文件中。另一种方法是使用远程仓库启动安装来创建虚拟机。该仓库可以是以 YUM 仓库或类似格式的形式存在。另一种替代方案是使用 QEMU 镜像创建器从由 Xen 处理的操作系统源代码创建镜像。如果你想知道为 Xen 创建虚拟机的其他方法，可以在 http://www.xen.org 找到。

如果这些选择看起来很令人生畏，那么 `virt-install` 脚本设计用于从支持 Xen 的操作系统创建虚拟机，对于新接触 Xen 的管理员来说非常棒。该脚本是你与 Xen 包一起安装的 libvirt 包的一部分。大多数现代 Linux 发行版（包括 CentOS）都带有 Xen 内核，可以在非特权域中创建虚拟机。你将使用 CentOS 安装 CD 或 DVD 在你的系统中创建一个 Xen 内核的实例。

**注意：** 你不能使用 Fedora 9 或 10 作为你 Xen 设置中的客机操作系统。这两个发行版的安装介质中都没有 Xen 内核，如果你想将其中一个作为客机，必须自己创建镜像。Fedora 8 的安装介质中带有 Xen 支持，你可以在后续示例的 CentOS 中使用它。

你可以通过 NFS、HTTP 和 FTP 使用 `virt-install` 安装半虚拟化域。遗憾的是，你不能直接使用本地 CD 或 DVD 驱动器作为安装源，因为 `virt-install` 假设安装是通过客机协议分发的。我们将安装半虚拟化域的方法是使用其中一种协议来“分发”本地 CD 或 DVD 驱动器，供 `virt-install` 使用安装文件。此外，你可以直接使用 CD 或 DVD 驱动器的唯一时间是你准备使用硬件辅助虚拟化方法添加未修改的客机。

在本节中，你将使用 NFS 并你的安装 DVD 作为源创建一个包含另一个 CentOS 实例的虚拟机。

**注意：** 当你运行 `virt-install` 时，系统会针对新客机询问一系列问题：

- 你的虚拟机名称是什么？你必须给出一个唯一的名称以帮助 Xen 识别不同的客机。使用它来启动此域。

- 应该分配多少内存（单位为 MB）？

- 域正在关机、重启或重新启动。当域处于销毁过程中，也会显示关机状态。

- 域已崩溃。通常，只有当域被配置为不重启时，才会出现此种状态。

- 域处于死亡过程中，但尚未完全关机或崩溃。

- 域正在关机、重启或重新启动。

- Crashed (c)（崩溃）：域已崩溃。通常，只有当域被配置为不重启时，才会出现此种状态。

- Dying (d)（正在死亡）：域处于死亡过程中，但尚未完全关机或崩溃。

Time(s)（时间）：此列告诉你是由 Xen 计算的域运行时间（以秒为单位）。

（此处重复原文重复导致的翻译错误）

安装过程将开始。安装界面将类似于图 18-5 所示，你应该在最初在系统中安装 CentOS 时回想起它。之所以使用 Anaconda 安装程序的图形版本，是因为你在“你是否想要启用图形支持？”上选了“是”。

![](img/57e3c53e2eeaac1ba18c095c31e37c47_474_0.png)

图 18-5. 在 Xen 下安装 CentOS

> 注意：如果你只是刚开始使用 Xen，最好不要在虚拟机中包含桌面环境。Xen 所需的内存可能会变得不足，导致虚拟机运行显著变慢。在安装 CentOS 虚拟机期间，当你看到图 18-5 所示的界面时可以通过取消勾选“Desktop – GNOME”和“Desktop – KDE”来实现这一点。这就是我在为本章安装 CentOS 虚拟机时所做的。

安装过程完成后，安装程序将重启，并由 Xen 处理 CentOS 虚拟机的启动。图 18-6 显示了你新虚拟机的运行会话。

## 第 18 章 LINUX 虚拟化

![](img/57e3c53e2eeaac1ba18c095c31e37c47_475_0.png)

图 18-6. 你的新虚拟机！

在 Xen 虚拟机程序上运行 CentOS 虚拟机，你可以登录它、运行 shell 脚本、打包安装以及设置服务器——就像另一个系统一样。

让我们使用 `xm list` 命令查看你的 Xen 环境上运行的当前域（domains）。输出应该类似于图 18-7。

```
[root@localhost ~]# xm list
Name ID Mem(MiB) VCPUs State Time(s)
Domain-0 0 747 1r----- 764.9
MyCentOS 4 255 1-b---- 22.7
```

图 18-7. 你的虚拟化系统中运行着两个域。

## 理解访机配置文件

当使用 `virt-install` 创建虚拟机时，系统会根据域名称为每个虚拟机创建一个虚拟机配置文件。这些配置文件存储在 `/etc/xen` 中。虚拟机配置文件使用指令来更改域运行时的行为。每个指令使用以下形式：

```
directvename = givenvalue
```

其中 `directvename` 是你想使用的指令名称，`givenvalue` 是你想要赋值给该指令的值。某些值需要包含引号，而另一些不需要。务必查阅 `xmdomain.cfg` 的帮助页面以查找选项及其值的格式。以井号（`#`）开头的行是注释，并会被 Xen 工具忽略。

如果你浏览 `/etc/xen` 目录，你将找到你创建的第一个域 MyCentOS 的配置文件。`virt-install` 命令使该文件名与你的域名相同。此文件将用于启动 MyCentOS 域，并通过更改其指令来影响其性能。当你用文本编辑器打开此文件时，列表 8-2 显示了 `virt-install` 生成的 MyCentOS 配置文件的内容。

### 列表 8-2：MyCentOS 配置文件的内容

```
name = "MyCentOS"
uuid = "57fd6e9-bf47-016d-a9b0-5d9ce1a62e8f"
maximum = 256
memory = 2
vcpus = 1
bootloader = "/usr/bin/pygrub"
on_poweroff = "destroy"
on_reboot = "restart"
on_crash = "crash"
vfb = ["type=vnc,vncuncoded=1"]
disk = ["tap:/var/lib/xen/images/MyCentOS.iso,xvada,w"]
vif = ["mac=00:16:3e:3f:2db;bridge,xenbro"]
```

这些是启动 MyCentOS 域时需要的指令：

- name：此指令标识域的名称，名称必须唯一，以避免与其他域冲突。

- uuid：此指令具有该域的 128 位 UUID（通用唯一标识符），Xen 用它识别域。如果你不提供值，默认行为是在每次调用 `xm create` 时创建一个 UUID。

- maximum：这指定了虚拟机可以使用的额外内存的最大量。由于 xen 进程通过气球技术（ballooning）增加运行中访机的内存，因此使用内存是可能的。

- memory：此指令指定了 xen 分给该虚拟机的内存量。

- vcpus：此指令指定了该域可以使用虚拟 CPU 的数量。

- bootloader：此指令指定了启动该域必须使用的引导加载程序。默认使用 py grub 脚本，但如果你需要使用其他的，可以在这里指定。

- on_poweroff：指定了当访机执行关机或或调用 shutdown 时将执行的操作。在本例中，访机通过 `destroy` 值进行清理。

- on_reboot：此指令指定了当访机执行重启或调用 reboot 时将执行的操作。在这种情况下，访机将通过 `restart` 值重启。

- on_crash：在这里，你指定了访机崩溃时将执行的操作。

- vfb：此指令指定了虚拟帧缓冲区。

- disk：此指令指定了虚拟机的磁盘镜像。

- vif：此指令指定了虚拟接口和桥接。

## 使用 vncviewer

当你启动一个虚拟机时，Xen 也会为其启动一个虚拟网络计算（VNC）服务器。通过 VNC，你可以使用 virt-viewer 连接到该虚拟机并获得图形化控制台会话。在使用 vnc 连接之前，你必须在系统中安装好 vncviewer。要安装它，请使用命令 `yum install vncviewer`。

在连接到虚拟机之前，你必须了解关于它的两点：运行该虚拟机的宿主机，以及虚拟机 VNC 服务器监听的端口号。要查找虚拟机 VNC 服务器的端口号，你可以使用以下命令：

```
ps ax | grep target_domain
```

其中 `target_domain` 是虚拟机的名称。如果你想知道 CentOS 虚拟机的 VNC 端口号，将使用 `ps ax | grep CentOS`，它将显示类似下面的输出：

```
7249 ? S 0:37 /usr/lib/xen/qemu-dm -M -d 2 -
domain-name CentOS -vnc 127.0.0.1:-vncused
```

**加粗部分**是这里重要的条目。你将在 vncviewer 命令中使用该参数，如下：

```
vncviewer 127.0.0.1:
```

运行后，屏幕看起来将类似于图 18-9 所示。

![](img/57e3c53e2eeaac1ba18c095c31e37c47_479_0.png)

你可以以 root 用户登录你的 MyCentOS 虚拟机并浏览系统。在探索系统后，你可以关闭窗口。

## 关闭虚拟机

你可以通过两种方式关闭运行中的虚拟机。第一种进入虚拟机操作系统并使用其原生的关闭命令（`shutdown -h now`）。第二是使用 xm 的 shutdown 命令。你通过以下方式使用 xm 安全地关闭虚拟机：

```
xm shutdown target
```

其中 `target` 是目标域的名称或 ID 数字。现在使用以下命令正确关闭 MyCentOS 域：

```
xm shutdown MyCentOS
```

你可以通过 `xm list` 命令监控已正在关闭的域。

## 启动虚拟机

要启动一个未运行的虚拟机，可以使用 `xm create` 命令。`xm create` 命令使用以下语法：

```
xm create target
```

其中 `target` 是其配置文件中 `name` 选项所注的虚拟机名称。要启动 MyCentOS 域，你将使用 `xm create MyCentOS`。之后你可以使用 `xm list` 监控它在虚拟机程序上的加载情况。

如果你希望在主宿主机启动时自动启动虚拟机，可以通过将虚拟机配置文件复制到 `/etc/xen/auto` 目录下来实现。例如，如果你想在 Xen 系统启动时自动运行 MyCentOS 虚拟机。你只需要通过 `cp /etc/xen/MyCentOS /etc/xen/auto` 将 MyCentOS 配置文件复制到该 auto 目录即可。下一次 Xen 重启时，你可以预期 MyCentOS 虚拟机将自动启动。

## 克隆虚拟机

如果你需要对现有虚拟机进行复制且不想重复执行 `virt-install` 命令，可以使用 `virt-clone` 实现。`virt-clone` 命令通过复制由 `virt-install` 创建的虚拟机镜像文件来克隆虚拟机，并为其创建一个具有相同硬件配置的新配置文件。该命令还会为克隆配置中的某些选项设置新值，例如 `name` 选项和 `uuid` 选项，以避免与原始实例同时运行时发生冲突。`virt-clone` 的语法如下：

```bash
virt-clone --original source_domain --name new_domain --file target
```

其中 `--original` 标志必须指向你想要复制的源域。`--name` 标志将新副本的名称。`--file` 标志指示新副本虚拟机镜像文件的名称和位置。在使用 `virt-clone` 之前，确保原始虚拟机没有在运行；否则它将不允许你进行复制。这种限制防止了原始内容的更改，并使副本与原始内容保持一致。

例如，你将 CentOS1 克隆为 MyCentOS-1。虚拟机将是 MyCentOS-1.img 并放置在 `/var/lib/xen/images/`。运行以下命令：

```
virt-clone --original MyCentOS --name MyCentOS-1
--file /var/lib/xen/images/MyCentOS-1.img
```

克隆一个虚拟机所需的时间取决于其虚拟机或镜像文件的大小——文件越大，克隆速度越慢。当你使用 `virt-install` 时，CentOS 的配置文件的名称将是它的名称 MyCentOS-1。

完成克隆后，你可以使用 `xen create MyCentOS-1` 启动克隆的虚拟机，并使用 `virt-view MyCentOS-1` 查看它。在图 18-10 中，MyCentOS 和 MyCentOS-1 虚拟机都在运行且具有不同的 IP 地址：MyCentOS 为 192.168.1.103，而 MyCentOS-1 为 192.168.1.104。

![](img/57e3c53e2eeaac1ba18c095c31e37c47_481_0.png)

## 清理

在实验完 Xen 后，你应该关闭：

- 1. 停止 NFS

- 2. 打开 /etc/

- 3. 从驱动器中弹出光盘。

## 总结

在本章中，我们涵盖了多种虚拟化类型，还学习了如何启动、关闭和克隆虚拟机。在下一章中，我们将研究出现问题时如何进行故障排除。

# 第 19 章 Linux 故障排除

![](img/57e3c53e2eeaac1ba18c095c31e37c47_486_0.png)

救援环境现在将尝试查找你的 Linux 安装并将其挂载到 `/mnt/sysimage` 目录下。然后你就可以对系统进行任何所需的更改。如果你想继续此步骤，请选择“Continue”（继续），你也可以通过选择“Read-Only”（只读）将你的文件系统挂载为只读而不是读写。

如果由于某些原因此过程失败，你可以选择“Skip”（跳过），系统将跳过此步骤并直接进入命令行 shell。

<Tab>/<Alt-Tab> 在元素间切换 | <Space> 选择 <F12> 下一页屏幕

图 19-2. 救援环境挂载分区

“Continue”和“Read-Only”都会安装已安装的 Linux 系统的分区，并将它们挂载到 `/mnt/sysimage` 目录。你可以切换到该目录并执行所需的修复，例如恢复配置或移除故障内核。“Continue”选项允许你在挂载后对 Linux 系统进行更改。“Read-only”选项允许你浏览挂载分区的内容以进行观察。这对于调查系统为何突然停止正常启动非常有帮助。

“Skip”不挂载你的 Linux 文件系统。如果救援环境未能找到分区，或者你想手动挂载分区，则这很有用。“Skip”选项最适合能够处理其他 Linux 发行版的经验 Linux 管理员。通过针对经验丰富的 Linux 管理员的此选项，你将在本章后续部分学习可以使用它完成的一些工作。

现在，选择“Continue”并按下空格键，让救援环境找到你的 Linux 系统分区并将其挂载到 `/mnt/sysimage` 目录（见图 19-3）。
