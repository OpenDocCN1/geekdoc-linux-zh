
这就完成了。你可以从容地重启系统并尝试选择 USB 设备（如有必要请调整你的 UEFI 或 BIOS 设置），以确保你确实创建了一个可启动的 USB 设备。

## 引导自举 (Bootstrapping)

本节假设你已经熟悉其他操作系统的启动过程，因此已经了解硬件的启动周期。我们将涵盖操作系统的引导过程。我们将从 Linux 引导加载程序（PC 通常使用 GRUB）开始。

## 内核加载 (Kernel Loading)

一旦 GRUB 启动并且你选择了 Linux 作为启动操作系统，需要加载的就是内核。请记住，此时内存中不存在任何操作系统，且 PC 无法轻松访问所有内存。因此，内核必须完全加载到第一个兆字节的可用 RAM 中。为了实现这一点，内核需要必要的代码将 CPU 引入保护模式（移除内存限制）并解压内核的剩余部分。

## 内核执行 (Kernel Execution)

内核进入内存后，就可以开始执行。需要记住的一点是，内核本质上一个程序（尽管是一个非常复杂且智能的程序），需要被执行。内核仅执行其内置的功能，这意味着任何编译为模块的内核部分在此时都是没用的。至少，内核必须足够的代码来设置其虚拟内存子系统并访问根文件系统（通常是 ext3、ext4、Btrfs 或 XFS 文件）。一旦内核启动，硬件探测将检测应该初始化哪些设备驱动。从这里开始，内核可以挂载根文件系统。这类似于 Windows 系统识别并访问其 C 盘的操作。内核挂载根文件系统并启动一个名为 `init` 的程序，将在下一节中讨论。

## 第 7 章 启动与关机 145

| SysV init 运行级别 (Runlevel) | systemd 目标 (Targets) |  |
|---|---|---|
| 0 | poweroff.target, runlevel0.target | 停止系统 |
| 1 | rescue.target, runlevel1.target | 进入单用户模式 |
| 2 | runlevel2.target, multi-user.target | 多用户模式，传统上不支持网络文件系统 (NFS) |
| 3 | multi-user.target, runlevel3.target | 全多用户模式（正常） |
| 4 | multi-user.target, runlevel4.target | 未使用或用户定义 |
| 5 | graphical.target, runlevel5.target | 与运行级别 3 相同，但使用 X 窗口（图形）系统登录而非文本登录 |
| 6 | reboot.target, runlevel6.target | 重启系统 |
| emergency | emergency.target | 紧急 shell |

**表 7-2** SysV 运行级别与 systemd 目标

### init 进程

在传统的 System V (SysV) 风格 Linux 发行版中，`init` 进程是第一个启动的非内核进程；因此它总是获得进程 ID 1。`init` 读取其配置文件 `/etc/inittab` 并确定它应该启动的*运行级别* (`runlevel`)。基本上，一个运行级别（由 0 到 6 之间的整数指定）具有特定的目的。如果存在 `initdefault` 运行级别，则选择它；否则系统将提示你提供运行级别值。

大多数现代 Linux 发行版已使用一个名为 `systemd` 的新启动管理器取代了以前由 SysV init 提供的功能。在 `systemd` 中，运行级别的概念是不同的，而是被称为*目标* (`targets`)。表 7-2 显示了传统 SysV 世界中的不同运行级别及其在 `systemd` 世界中的等效目标。

### systemd 脚本

在基于 `systemd` 的发行版中，控制启动什么、如何启动以及*何时*启动的配置文件被称为单元文件 (`unit files`)。这些文件存储在文件系统的某些位置。例如，`/usr/lib/systemd/system/` 存放随安装包提供的任何相关文件，而 `/etc/systemd/system/` 通常存放由系统管理员（隐式或显式）安装的单元文件。

## 146 第二部分 单机管理

这些单元文件共同负责在启动过程后的某个固定点启动、管理或停止各种服务和进程。在许多情况下，这些单元的执行顺序非常重要。例如，你可以：

- `/usr/lib/systemd/system/` 存放随安装包提供的任何相关文件
- `/etc/systemd/system/` 通常包含由系统管理员（隐式或显式）安装的单元文件。

# 第二部分 单机管理

注意：我们的演示 `carpald.sh` 脚本需要一种机制来实际上将电子邮件发送到收件者邮箱地址 (`root@localhost`)。这涉及设置本地邮件服务器，或配置系统使用外部邮件服务器或其他机制来发送电子邮件。由于这只是概念验证，我们还没有准备好完全投入。因此，现在请忽略在系统日志中可能看到的任何“消息未发送”（message not sent）错误！第 20 章涵盖了安装和设置功能完整的邮件服务器的内容。如果你不信任或仅仅是无法等待脚本，可以使用 `dnf`、`yum` 或 `apt` 快速安装 `postfix` 软件包。

## 创建 carpald 服务单元

在这里，你将创建一个在系统启动和关闭期间执行的实际启动脚本。你在这里创建的文件名为 `carpald`。该文件启用了 systemd，这意味着它将使用 systemd 领域特定语言/语法。这是一个非常实用且节省时间的功能。

1. 启动你任选的任何文本编辑器并输入以下文本：

```ini

[Unit]

Description=The Carpald Notice Daemon

After=syslog.target

[Service]

ExecStart=/usr/local/bin/carpald.sh

Type=simple

[Install]

WantedBy=multi-user.target

```

关于上述示例 `carpald.service` 单元文件的几点说明。方括号中的字段（如 `[Unit]`、`[Service]` 和 `[Install]`）标记了文件中新段落的开始：

- `[Unit]` 部分包含影响各种 systemd 对象的通用参数，例如 `Description`、`After` 等。在这里，我们指定了一个描述我们 carpald 服务的简单字符串，并且还指定了该单元可以在 `syslog.target` 之后启动。
- `[Service]` 部分包含对特定单元更具针对性的参数。在其中，它指定了这是一个服务类型的单元。`ExecStart` 参数被设置为我们之前创建的 `carpald.sh` 脚本的路径。
- `Type` 参数指定了服务在启动后应如何通知系统。`Type` 的一些示例值是 `simple`、`forking` 和 `exec notify`。
- 最后，`[Install]` 部分包含指定此单元启动的条件（又称触发器）的指令。`WantedBy` 的值被设置为 `multi-user.target`，这意味着每当请求 `multi-user.target`（或运行级别）时，我们的 `carpald.service` 单元就会自动启动。

2. 将脚本文本保存到名为 `carpald.service` 的文件中。

## 第7 章启动与关闭

3. 将脚本复制或移动到 `/etc/systemd/system/` 目录，systemd 将在那里找到它：

```
[master@fedora-server ~]$ sudo mv -f carpald.service /etc/systemd/system/
```

4. 现在通过重载 systemd 守护进程让 systemd 知道新单元的存在：

```
[master@fedora-server ~]$ sudo systemctl daemon-reload
```

这些可能相当繁琐，但好消息是你只需要设置一次，然后就可以忘记它了。由于脚本/守护进程/服务/进程正在执行其设计的功能，并且在应该执行的时候执行，因此不需要对其进行监控。具体来说，在我们的示例中，脚本将在启动和关闭期间自动运行——多亏了 systemd。初期的开销完全值得为了避免 carpald 隧道综合征而带来的长期利益！

我们已经搭建了 carpald 基础设施的“基础组件”，但在实际让它运行之前，它并不完善。现在我们使用该服务手动启动守护进程：

1. 使用服务查看 `carpald.sh` 程序的状态：

```
[master@fedora-server ~]$ sudo service carpald status
```

2. 我们不想等到下次系统重启时才测试 carpald 脚本，所以让我们使用服务命令手动启动 carpald 程序：

```
[master@fedora-server ~]$ sudo service carpald start
```
