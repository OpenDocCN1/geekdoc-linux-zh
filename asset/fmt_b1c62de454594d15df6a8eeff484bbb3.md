
看到列左侧的每个字母了吗？`c`、`b`、`p` 和 `s`？

这些代表：

- `c` - character
- `b` - block
- `p` - pipe
- `s` - socket

字符设备逐字符地传输数据，并与数据流工作。`/dev/null` 是一个字符设备。打印机也是通过字符设备表示的。

块设备程序按固定块访问。硬盘和文件系统都是块设备的一种类型。

管道设备或命名管道与字符设备类似。它们允许两个或
更多的通信进程。
套接字设备（Socket Devices）允许像管道设备一样进行进程间的通信。它们通常允许同时多个进程或程序通信。这些文件通常位于我们一直在查看的 `/dev` 之外。

### 设备命名

如果你探索 `/dev` 中的设备名称，你会看到一些看起来很奇怪的名称。存储设备常见的设备名称有 `/dev/sda`、`/dev/sdb` 和 `/dev/sdba2`。这些名称意味着 SCSI 设备 a、SCSI 设备 b 和 SCSI 设备 a 分区 2。这些名称源于 SCSI（读音类似“scuzzy”）协议或小型计算机系统接口（Small Computer System Interface）。尽管 SCSI 接口已不再广泛使用，但这种命名方案仍然保留了下来。

### 什么是守护进程（daemon）？

`daemon`（读音 DAY-MAN、DAY-MON 或有时 DEE-MON）是一个在 Linux 上持续运行的后台进程。当我们说后台时，是指程序在没有任何用户交互的情况下运行。它在“后台”运行。

守护进程的示例如 Apache（Web 服务器）、Nginx（一个 Web 服务器）、PostgreSQL（数据库服务器）和 SSHD（安全外壳守护进程）。如果你是维护任何类型 Web 服务的企业或个人，你可能希望它一直运行，且不需要太多的麻烦或管理。你希望它在服务器启动时启动并永远运行。这种进程就会充当守护进程的角色。

### 启动过程与 Init、systemd

#### Linux 如何启动？

每个操作系统都有启动过程。Linux 也不例外。在本节中，我们将介绍启动过程的基础知识并解释每个组件。
在启动 Linux 系统到它最终出现空白提示符之间，有大量的进程在运行。启动过程可以非常简单地解释，我们将深入探讨。

以下是总结：

- BIOS 或 UEFI 启动固件运行引导加载程序（bootloader）
- 引导加载程序从磁盘找到内核镜像，将其加载到内存或 RAM 中，并带有内核参数启动它
- 内核初始化与设备通信所需的硬件设备和驱动程序，并挂载根文件系统。
- 内核接着启动一个名为 `init` 的进程，并赋予其进程 ID 1。在较新的系统中，这现在被 `systemd` 代替。
- Init 开始启动其他所需的系统进程，如网络服务、Web 守护进程和日志服务。
- Init 最后允许你在启动序列的接近尾声处加入。

#### Linux 启动过程 - BIOS 和 UEFI

为了进一步理解 Linux 启动过程，我们应该熟悉 BIOS 和 UEFI 以及这两个系统之间的区别。

##### BIOS

BIOS 代表基本输入输出系统（Basic Input/Output System）。BIOS 是在启动过程中使用的固件，用于在更改启动磁盘顺序和网络设置等其他次级系统中寻找引导加载程序。BIOS 固件存储在 EPROM 芯片上，允许制造商对固件进行更新。

一旦 BIOS 启动，它的目标是搜索主引导记录（MBR）并执行它。MBR 包含磁盘的前 512 字节，用于主引导加载程序。

##### UEFI

UEFI 或统一扩展固件接口（Unified Extensible Firmware Interface）较新，其目标与 BIOS 相同都是启动系统。然而，UEFI 将初始化数据存储在 `.efi` 文件中，而不是存储在固件中。这个 `.efi` 文件存储在系统的磁盘名为 UEFI 系统分区的分区上，与引导加载程序在一起。UEFI 系统使用 GUID 分区表（GPT）格式。UEFI 的开发是为了改进 BIOS 的某些缺点，例如：

- 更快的启动速度
- 对更大磁盘容量的支持：BIOS 支持 2.2 TB，而 UEFI 支持 zettabytes（巨大的！）截至今天……
- 安全启动（Secure Boot）——UEFI 可以利用安全启动功能要求引导加载程序经过数字签名，防止恶意软件加载到系统中。

今天，UEFI 是标准，而 BIOS 已经变得过时陈旧。

#### 引导加载程序（Bootloader）

一旦 BIOS 或 UEFI 找到并执行了引导加载程序，引导加载程序就会接。引导加载程序的主要目标是启动 Linux 内核。它通过找到内核、将其加载到内存并传递任何可能需要的内核参数来实现。

在此过程中，内核尚未被加载，因此访问磁盘必须通过比系统启动后使用的慢的设备程序。

最常见且无处不在的引导加载程序是 GNU GRUB（grand Unified Bootloader）。还有其他 Linux 引导加载程序，如 LILO（Linux Loader）、BURG、Syslinux 和 core boot。这些引导加载程序的开发是为了比 GRUB 更快、更简单或具有不同的功能。

#### Init 与用户空间启动

引导加载程序将内核加载到内存后，它会启动第一个用户空间进程 `init`。这通过启动基本服务触发了其余进程以使系统完全启动。`init` 进程始终会被分配进程 ID 1。一旦 `init` 启动，它的目标是启动运行系统所需的其余程序。

`Systemd` 是现代 Linux 发行版中 `init` 最新且当前的标准。System V `init` (SysV) 于旧版本的 Red Hat Enterprise Linux 发行版中。Upstart 是旧版 Ubuntu（15.04 之前）使用的 `init`。还有其他几个用于嵌入式应用、手机手机和其他设备的 `init` 系统。我提到的这三个是你应该最熟悉的：`Systemd`、`SysV` 和 `Upstart`。我们将学习并涵盖 `systemd`。

#### systemd

`systemd` 与目标（targets）协同工作，目标可以被视为 `systemd` 需要达到的终点。目标是一种类型的单元（units），用于组合其他单元并定义应该到达的系统状态。单元（unit）是一个文件，包含关于如何启动守护进程或系统服务的指令，以及启动它的依赖项。服务的依赖项也是单元。

例如，考虑像 Nginx 这样的 Web 服务器。如果系统网络尚未上线且正常运行，那么启动服务器是没有意义的。Web 服务器或 Nginx 单元将对网络单元文件有依赖。

让我们看看 `systemd` 如何启动系统：

- `Systemd` 加载配置文件或单元，这些通常位于 `/etc/systemd/system` 或 `/usr/lib/systemd/system`
- 根据配置文件，`systemd` 确定其启动目标（target），这通常是 `default.target`。然后 `systemd` 找出出启动目标的依赖关系并激活它们。
- 单元是用于描述由 `systemd` 管理的资源的配置文件。单元可以是服务、套字、设备等。`Systemd` 单元根据它们定义的依赖关系并行启动。
- 服务是最常见的单元，这些定义了运行在系统上的守护进程或后台进程。如果这些是单元文件的依赖项，`systemd` 也会启动它们。

#### 示例单元文件（Unit File）

让我们来看流行的 Web 服务器 Nginx 的示例 `systemd` 单元文件。此文件通常位于 `/lib/systemd/nginx.service`

```
[Unit]

Description=The NGINX HTTP and reverse proxy server

After=syslog.target network-online.target remote-fs.target nss-lookup.target

Wants=network-online.target

[Service]

Type=forking

PIDFile=/run/nginx.pid

ExecStartPre=/usr/bin/nginx -t

ExecStart=/usr/bin/nginx

ExecReload=/usr/bin/nginx -s reload

ExecStop=/bin/kill -s QUIT $MAINPID

PrivateTmp=true

[Install]

WantedBy=multi-user.target
```
