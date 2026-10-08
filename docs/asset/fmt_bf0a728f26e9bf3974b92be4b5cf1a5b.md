
## 技术细节

输出目录（Spool Directory）为 `/var/spool/HostA_q`。默认情况下，根据惯例，它反映了打印队列的名称。由于分配了别名，每个输出目录只允许一个打印机。

每个输出目录包含四个文件——`errors`、`lock` 和 `status`。这些权限非常重要，如果发生更改将导致进程失败。`printtool`、`lpc` 和 `lpr` 工具会为你处理此任务，但如果你正在从备份恢复系统或手动尝试创建打印场景，可能会出现问题。例如，我们建议不要删除此目录中的文件。

`lpd` 服务应该配置为系统启动时启动。这是安装后的默认行为，但你应该检查它。在 `lpd` 启动期间，会读取 `/etc/printcap` 文件以识别适用于任何打印机的节。只有当你更改任何配置时，才需要刷新 `lpd` 服务。

## 远程打印

在本节中，假设你已经成功完成了前面的示例并且本地打印正常。对于我们的配置，此本地打印机是 HostA。我们计划让 HostC 使用 HostA 打印机。因此，我们将为 HostC 配置远程打印（见图 6.10）。设置本地打印是远程打印的前提。

## 先决条件

远程打印的基础是 TCP/IP 配置。在处理远程打印之前，你应该测试并确认两个系统之间的 TCP/IP通信。确保你可以从一个系统 `ping` 到另一个系统。你还必须确认名称解析正常，这意味着你应该能够通过主机名 `ping`。

# 187

![](img/cf6993b0699c37d6fb92721201c599d8_205_0.png)
所有提交到 `HostC_rq` 的作业将进入 `HostA_q`。

**图 6.10** 远程打印配置。

### 步骤 1 确认 TCP/IP 设置

在示例中，我们使用静态 TCP/IP 主机文件：`etc/hosts` 文件已更新以包含 HostC，并进行了 `ping` 测试：

```bash
[root@HostA /root]# cat /etc/hosts
# 不要删除以下行，否则各种需要网络功能的
# 程序将失败。
127.0.0.1          localhost           localhost
192.168.1.206      HostA               #此系统是打印服务器
192.168.1.208      HostB               #使用 HostA 上的打印机
192.168.1.101      MCS_Skills
[root@HostC /root]# ping HostC
PING HostC (192.168.1.222) from 192.168.1.206 : 56 (84) bytes of data.
Warning: time of day goes back, taking countermeasures.
64 bytes from HostC (192.168.1.222): icmp_seq=0 ttl=255 time=547 ms
64 bytes from HostC (192.168.1.222): icmp_seq=1 ttl=255 time=255 ms
--- Host ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/mdev = 0.402/0.474/0.075 ms
```

### 步骤 2 定义主机队列

登录到远程系统，在我们的案例中是 HostC。确保你是 `root` 用户，并执行 `printtool` 工具。为了清晰起见，我们定义了队列名称 `HostC_rq`，提醒我们此队列位于 HostC 且是远程队列。我们还为此队列定义了别名，即 `draft_rq`（见图 6.11）。

TEAM LinG - Live, Informative, Non-cost and Genuine!

## 配置打印机 189

### 步骤 3. 定义队列类型为远程

这次，选择 Remote Unix (lpd) Queue 选项。注意此选项对 `lpd` 的引用。我们将使用 `lpd` 守护进程来方便两个计算机系统之间的打印。打印机所在的服务器称为 HostA。因此，我们必须确保 TCP/IP 和名称解析正常工作。如果名称解析无法工作，则就无法将服务器 HostA 映射到 IP 地址。在这里需要的队列不是 HostC 队列，而是 HostA 上的队列名称。HostA 的队列名为 `HostA_q`。我们在这里也可以使用别名。详见图 6.12。

### 步骤 4. 定义相同的打印机驱动程序

选择相同的打印机驱动程序至关重要。这样做可能会导致某些不可预知的结果。你不希望的是 HostC 队列使用 `lj5gray` 驱动程序将作业过滤为 LaserJet 5，而 HostA 队列却使用 `left4` 驱动程序将作业过滤为 LaserJet 6l。如果你处于无法在两端启用相同打印机驱动程序的情况下，可以将 HostA 上的接收队列设置为 Raw Print Queue（原始打印队列）设备。如果你选择此操作，请确保 HostA 上的用户也有一个配置了打印机的本地队列用于打印。

**图 6.12** 定义远程服务器和队列名称。

在此项配置中，你将有两个打印队列向 HostA 上的打印机发送作业。详见图 6.13。

## 190 Linux 的自定义与升级

**图 6.13** 定义打印机驱动程序。

### 步骤 5. 定义相同的驱动选项

我们也建议保持驱动选项的参数也相同（见图 6.14）。

### 步骤 6. 刷新 lpd 守护进程

你可以使用此方法在此刷新 `lpd` 守护进程。然而，在此之前，你应该确保 `/etc/hosts.lpd` 文件中有 HostA 的条目，以便 HostA 能够通过网络访问并与此队列通信。如果你还没有 `/etc/hosts.lpd` 文件，可以等到下一步。要刷新 `lpd` 守护进程，你可以使用 Apply（应用）或文件菜单下的 Restart lpd（重启 lpd）。详见图 6.15。

### 步骤 7. 更新 /etc/hosts.lpd 文件

```
[HostC /root] # cat /etc/hosts.lpd
HostA
```

**图 6.14** 定义额外的驱动选项。

**图 6.15** 启动或重启 lpd 守护进程。

## 自定义与升级 Linux

你可以通过 `printtool` 刷新 `lpd` 守护进程，或者可以在 `/etc/rc3.d` 目录下启动和停止 `s60lpd` 服务。两者没有区别。

```
root@HostC [/root]# /etc/rc3.d/s60lpd stop      [ OK ]
Stopping lpd:
root@HostC [/root]# /etc/rc3.d/s60lpd start      [ OK ]
Starting lpd:
```

注意，某些系统管理员会使用 `hosts.equiv` 而不是 `hosts.lpd` 文件。只需要其中一个即可。关于使用哪种文件，有两种流派观点。`hosts.lpd` 文件仅为 `lpd` 守护进程提供特定授权，而 `hosts.equiv` 则为系统使用的额外工具提供通用授权。某些系统管理员不希望为了实现一个简单的打印功能就提供超出所需的访问权限。另一些人则说，他们在任何地方特定功能都需要 `hosts.equiv`，且不想增加额外的文件。由于 `hosts.lpd` 文件是 `lpd` 守护进程的配置，其源目录是 `/etc`，对于所有包含 IP 地址或主机名的守护进程配置文件都是如此。记住关于配置文件的以下规则：你不能在无法通过扁平主机文件、NIS 或 DNS 预先解析到网络中的配置文件中引用 IP 地址或主机名。

### 步骤 8. 验证打印

`lpq` 命令的后续输出显示 `HostC_rq` 队列已分配目标为 `HostA_q@HostA`。你刚刚创建的队列中没有作业，但我们接下来可以测试。

```
root@HostC [/root]# lpq
Printer: HostC_rq 'craft_rq' (dest HostA_q@HostA)
Queue: no jobs in the queue
root@HostC [/root]# lpq
Printer: HostC_rq 'craft_rq' (dest HostA_q@HostA)
Queue: no jobs in the queue
Status: job 'cfa489Hostc' removed at 19:16:31
root@HostC [/root]# lpq
Printer: HostC_rq 'craft_rq'
Queue: no jobs in the queue
Status: job 'cfa489Hostc' removed at 19:16:48
```

HostC 上的用户只需将他们的作业提交到名为 `HostC_rq` 的队列。`lpd` 守护进程将负责将作业传输到 HostA 上的 `HostA_q`。一旦作业传输到 `HostA_q`，它将被引导至本地打印机，速度快到你看不见作业的堆积。

## 配置打印机 193

```
root@HostC [/root] lpr list.txt
root@HostC [/root] lpq
Printer: HostC 'draft_rq' (dest HostA_q@HostA)
Queue: no jobs in the queue
Status: job 'cfa698Hostc' removed at 19:58
root@HostC [/root] lpq
Printer: HostC 'draft_rq'
Queue: no jobs in the queue
```

因此，我们将对 HostA 上的 `HostA_q` 队列进行挂起（hold），以便我们可以确认一切运行正常。以 `root` 身份登录 HostA，我们将执行以下命令：

```
root@HostC [/root] lpq
Printer: HostA 'draft_q'
Queue: no jobs in the queue
Status: job 'cfa698Hostc' removed at 19:58
root@HostA /root] holdall
Printer: HostA_q@HostA
kill server 0 with User defined 1
HostA_q@HostA: hold on
root@HostA /root] lpq
Printer: HostA 'draft_q' (holdall)
Queue: no jobs in the queue
```

登录回 HostC，我们将恢复打印作业：

```
vern@HostC $ lpr poetry.txt
vern@HostC $ lpq
Printer: HostC 'draft_rq' (dest HostA_q@HostA)
Queue: no jobs in the queue
Status: job 'cfa757Hostc' removed at 20:03:38
Printer: HostA 'draft_q' (holdall)
Queue: no jobs in the queue
Holding: 1 held jobs in queue
```

## 添加、替换和升级 RPM 包

本章专门介绍 RPM 包。RPM 是可以简化系统管理人员工作的软件包。我们首先定义 RPM 和 RPM 包，并向你展示如何管理和查询它们。

我们讨论了如何确定是否需要向系统添加 RPM 包或升级已有的包，并提供了安装和升级说明。我们专注于两个示例：一个是新系统并希望对任何过时的 RPM 应用最新的维护；另一个使用 XFree86 RPM 包作为主要示例（因为视频是一个常见问题）。

在本章后面，我们将安装 XF86Setup，这是一个在 RedHat 发行版 V 6.2 及更早版本运行良好的视频配置工具，它是通过 RPM 包实现的。XF86Setup 是过去的一个非常好视频配置工具。由于某些原因，他们停止了对 XF86Setup 的支持，并用 Xconfigurator 和 xf86cfg 取代了它。由于要求很大，我们保留了上一版的内容未动。这样做是因为有些文档告诉你有四种配置和设置视频的替代方案：

+   - Xconfigurator
- Xf86cfg

## 定制与升级 Linux

- XFree86Setup
- 手动编辑 `/etc/X11/XF86Config`

此外，在本章的最后，我们记录了如何向完全没有 X 的系统读取 X 窗口。

## RPM 定义与包管理

RPM 是一个开放的软件包系统，软件供应商、开发者等人使用它来向用户、程序员和管理员组织并交付二进制、源码、配置和其他文件。该系统用于组织和交付文件的机制是 RPM 包。RPM 包通常包含二进制文件、可执行代码和程序文件。它们还包含相关的配置和文档行，可以使用 `rpm` 工具进行读取。它们分发程序更新和升级的有效方式。

RPM 系统通过 `rpm` 工具在 RPM 数据库中跟踪机器安装的所有软件包及其相关文件。`rpm` 工具是一个强大的工具，用于用于安装、查询、验证、更新、删除和构建符合特定 RPM 格式的软件包。例如，你可以使用 `rpm` 工具查询 RPM 数据库，以确定系统中是否存在特定软件包、该包是否已安装、是否应该升级等。`rpm` 工具同时具有图形界面（GUI）和命令行版本。

RPM 数据库和二进制文件直接构建在发行版中。这一特性非常重要，因为软件包之间存在依赖关系。这些依赖在共享代码中解决。例如，在新的 2.X Linux 内核中，GNU 标准 C 库被称为 `glibc` 或 `libc6`。此内核版本的所有可执行文件都链接了此库。因此，如果你尝试从不同的发行版安装二进制文件，它们可能无法运行——最好的情况下，直到你使用 `lib5` 库进行向后兼容。

以下是一个用于向你的系统安装额外的 XFree86 RPM 包的可用语法示例。该命令及其选项将在稍后解释。

```bash
rpm -ivh XFree86-76dpi-fonts.rpm
```

在升级或安装任何 RPM 包之前，`rpm` 手帮助页应该是必读的。特别是，务必确保你理解如何使用 `rpm` 工具卸载和删除软件包，以防 RPM 包证明不是你所需要的。

## 添加、替换和升级 RPM 包

RPM 包的命名规范是识别包的关键。每个包名由 `Name-version.arch` 组成，其中 `Name-version` 是该包的当前版本，`arch` 是平台标识（例如 Intel）。Intel `i386` 标准可能指示 `i586` 或 `i686`，尽管某些内核包可能是（依此类推）。

```bash
# ls | less
X886-1000dpi-fonts-3.3.6-20.i386.rpm
X886-3.3.6-20.i386.rpm
X886-3DLabs-3.3.6-20.i386.rpm
X886-75dpi-fonts-3.3.6-20.i386.rpm
X886-8514-3.3.6-20.i386.rpm
```

你安装的软件包必须与该系统可用的共享库版本匹配。如果你尝试安装与共享库不匹配的 RPM 包，你将在屏幕上看到错误。此时，你可以“强制”安装。但在这种情况下，你必须确保没有影响其他 RPM 软件包。当然，在应用这种技术之前备份系统是恰当的。

# SRP 与 RPM

SRP 文件包含用于构建 RPM 二进制文件的原始源码。这对于需要为自己的系统修改和编译 RPM 包的开发者来说是有意义的。许多程序员会将 SRP 文件提供给其他程序员，以促进 Linux 社区内的自由软件开发理念。RPM 二进制文件是系统管理员需要应用到系统的文件。

## 确定软件包的功能和内容

Linux 用户通常对 RPM 包的功能感到好奇。你可以使用 `rpm` 工具查询 RPM 包的功能，如下例所示：

```bash
# rpm -qip kernel-2.2.14-5.0.i586.rpm
Name : kernel Relocations: (not relocatable)
Version : 2.2.14 Vendor: Red Hat Inc.
Release : 5.0 Build Date: Wed Jun 20 07:09:08 1999
Install date: (not installed)
Build Host : porky.devel.redhat.com
Group : System Environment/Kernel
Source : kernel-2.2.14-5.0.src.rpm
Size : 12145883
License : GPL
Packager : Red Hat Inc.
<http://bugzilla.redhat.com/bugzilla>
Summary : The Linux kernel (the core of the Linux system).
```

描述
内核包含 Linux 内核 (`vmlinux`)，它是你的 Red Hat Linux 操作系统的核心。内核处理操作系统的基本功能：内存分配、进程分配、设备输入和输出等。

`rpm` 语法如下：

```bash
rpm -qip <package-name>
```

本节使用的查询选项有：

- -q: 查询数据库。
- -i: 显示有关软件包的信息。
- -p: 查询软件包文件而不是数据库。

# 添加、替换和升级 RPM 软件包 201

某些系统管理员会将更新下载到包含原始 RPM 的目录中，但我们发现这个目录太大了，已经无法看出哪些是新的，哪些是原始的。将所有信息记录下来也是一个好主意，以防你必须重建此系统或创建一个完全相同的系统。

注意所有不同的发行版都有各自的目录。导航到你文件所在的 `i386` 目录。查看内容：

```bash
[root@HostA /#] cd LinuxV71Downloads
