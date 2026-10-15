
5. 在命令提示符下，输入 `systemctl start bootscript.service` 并按回。接着，在命令提示符下输入 `cat /tmp/bootscript.txt` 并按回。`bootscript.` 执行了吗？

6. 在命令提示符下，输入 `journalctl | grep boot` 并按回车。注意指示 `bootscript` 服务成功启动的行。

7. 在命令提示符下，输入 `systemctl enable bootscript.service` 并按回车。为什么在 `/etc/systemd/multi-user.target` 目录下创建了一个符号链接？

8. 在命令提示符下，输入 `reboot` 并按回车。系统重启后，按下 `Ctrl+Alt+F5` 并使用用户名 `root` 和密码 `LINUXRocks` 登录终端。

9. 在命令提示符下，输入 `journalctl | grep bootscript` 并按回车。注意时间戳。你的脚本在启动期间成功执行了吗？

10. 在命令提示符下，输入 `exit` 并按回车退出你的 shell。

# 项目 8-4

预估时间：40 分钟
目标：配置挂载单元（mount units）。
描述：在本次实践项目中，你将配置一个挂载单元，用于在 Fedora Linux 上通过系统初始化过程挂载文件系统。

1. 按下 `Ctrl+Alt+F5` 切换到命令行终端 `tty5`，并使用用户名 `root` 和密码 `LINUXRocks!` 登录终端！
2. 在命令提示符下，输入 `vi /etc/systemd/system/newmount.mount` 并按回。添加以下行，将 `UUID` 替换为你在第 2 步中记录的 UUID（使用命令：`r : lsblk -f grep newmount | awk '{print $3}'`）：在命令模式下将此 UUID 插入 `vi` 编辑器。完成后，保存并退出 `vi` 编辑器。
3. 在命令提示符下，输入 `vi /etc/fstab` 并按回。删除你在实践项目 5-3 中添加的行。

```
[Unit]

Description=Mount filesystem in graphical target

[Mount]

What=/dev/disk/by-uuid/UUID

Where=/newmount

Type=ext4

Options=defaults
```

4. 在命令提示符下，输入 `systemctl enable newmount.mount` 并按回以启用你的挂载单元。

5. 在命令提示符下，输入 `vi /etc/fstab` 并按回。删除你在实践项目 5-3 中添加的用于挂载 `/newmount` 文件系统的行。完成后，保存并退出 `vi` 编辑器。

# 第 8 章 系统初始化、X Windows 与本地化

6. 在命令提示符下，输入 `telnet 6` 并按回重启你的系统。一旦系统重启后，使用名称 `root` 和密码 `LINUXRocks!` 登录 `tty5`！

7. 在命令提示符下，输入 `df -h` 并按回。你的 `/newmount` 文件系统被系统挂载了吗？如果你将系统重启到救援模式或多用户目标，`/newmount` 还会被挂载吗？

8. 在命令提示符下，输入 `exit` 并按回退出你的 shell。

# 项目 8-5

预估时间：30 分钟

目标：检查 X Windows、辅助功能和本地化选项。
描述：在本次实践项目中，你将通过 GDM 启动 X Windows，并检查 X Windows 配置、辅助功能选项和本地化。

1. 按下 `Ctrl+Alt+F5` 切换到命令行终端 `tty`，并使用用户名 `root` 和密码 `LinuxRocks!` 登录终端！
2. 在命令提示符下，输入 `init 3` 并按回切换到运行级别 3（多用户目标）。
3. 在命令提示符下，输入 `start` 并按回。默认加载了桌面环境，这是为什么？
4. 点击 GNOME 桌面右上角的电源图标，点击“Power Off / Log Out”（关机/注销），然后点击“Log”（注销）。点击“Log Out”注销 GNOME 桌面。你返回了 `tty5` 上的 BASH shell！
5. 在命令提示符下，输入 `who` 并按回切换到运行级别 5（图形目标）。注意 `tty1` 中没有加载 GDM。选择你的账户并点击设置（齿轮）图标。确保 GNOME 已启用默认的 Wayland 并支持 LinuxRocks！
6. 点击“Show Applications”（显示应用程序）并点击“Settings”（设置）。在左侧格中突出“Displays”（显示器），注意你可以配置当前显示器的分辨率，这由你的合成器决定。在左侧格中突出“Keyboard”（键盘），注意你可以可选配置不同的键盘本地化设置，或添加第二个键盘本地化设置供 GNOME 选择。接下来，在左侧格中突出“Accessibility”（辅助功能）。探索可用辅助技术并在完成后关闭窗口。
7. 点击“Activities”（活动）菜单并导航到“Show Applications”、“Terminal”（终端）以打开命令行终端。在命令提示符下，输入 `su -` 并按回切换到 `root` 用户。使用密码 `LinuxRocks!`！
8. 在命令提示符下，输入 `cat /etc/X11/xorg.conf.d/keyboard.conf` 并按回查看 X 使用的键盘布局。
9. 在命令提示符下，输入 `locale` 并按回。所有类型默认使用哪种本地化？接下来，输入 `locale -a | less` 并按回查看系统上的本地化设置。
10. 在命令提示符下，输入 `localatectl` 并按回。接下来，输入 `/etc/localtime` 查看时区信息
11. 在命令提示符下，输入 `poweroff` 并按回关闭 Fedora 机器

# CompTIA Linux+ 与 LPIC-1：Linux 认证指南

# 发现练习

## 发现练习 8-1

预估时间：10 分钟
目标：解释运行级别和目标。
描述：描述如果将系统的默认运行级别/目标改为运行级别 6 会发生什么。

## 发现练习 8-2

预估时间：40 分钟
目标：配置定时单元（timer units）。
描述：在你的机器上创建一个定时单元，每天中午运行你在项目 8-3 中创建的 `bootscript.service`。重启系统并检查 `journalctl | grep boot` 以验证你的定时单元是否成功运行。

## 发现练习 8-3

预估时间：50 分钟
目标：将章节概念应用于 Ubuntu。
描述：在项目 6-1 中安装的 Ubuntu 机器上：

- a. 执行你在项目 8-1 中执行的步骤。为了完成这些，你需要记住 Ubuntu 使用不同的文件名和命令。
- b. 使用相应的命令查看、启动和停止守护进程，并配置它们在特定的运行级别/目标下启动。
- c. 使用相应的命令探索本地化文件、命令和选项。

## 发现练习 8-4

预估时间：60 分钟
目标：使用 init init。
描述：从 `ubuntu.com` 下载 Ubuntu Server 14.04 LTS 的 ISO。接下来，从此 ISO 安装一个名为 Legacy Ubuntu 的新虚拟机，使用 1 GB 内存（非动态分配）和 50 GB SAS/SSD 虚拟硬盘（动态分配）。安装后，设置 `root` 密码并切换到运行级别。接下来，使用相应的命令探索系统初始化系统。确保执行了以下操作：

- a. 查看并配置配置文件。
- b. 查看、启动和停止守护进程。
- c. 配置启动守护进程在特定的运行级别启动和停止。

## 发现练习 8-5

预估时间：180 分钟
目标：配置 i3 窗口管理器。
描述：在你的 Fedora 机器上，以 `root` 用户运行 `dnf install i3-gaps` 命令安装支持间隙的 i3 窗口管理器。安装完成后，重启系统并使用 GDM 登录 i3 窗口管理器。按照提示使用默认选择生成 i3 配置。接下来，参考 `i3.wm/docs/userguide.html` 的指南了解如何使用和配置它。

## 第 9 章

## 管理 Linux 进程

### 章节目标

- 1 分类 Linux 系统上不同类型的进程。
- 2 使用标准的 Linux 工具查看进程。
- 3 解释常用杀进程信号（kill signals）之间的区别。
- 4 描述二进制程序和 shell 脚本是如何执行的。
- 5 创建并操作后台进程。
- 6 使用标准的 Linux 工具修改进程的优先级。
- 7 使用守护进程（daemon）调度未来执行的命令。

一个典型的 Linux 系统可以同时运行数千个进程，其中包含了你在之前的章节中探索过的进程。在本章中，你将关注进程的查看和管理。在章节的第一部分，你将检查 Linux 系统上不同类型的进程以及如何查看和终止它们。然后你将发现进程如何在系统中在后台执行以及如何进行优先级排序。最后，你将检查用于调度未来执行命令的各种方法。

## Linux 进程

在本书中，“程序”（program）和“进程”（process）这两个术语是互换使用的。在工作中也是如此。然而，这两个术语之间存在细微的区别。从技术上讲，程序是文件系统上的一个可执行文件，你可以运行它。而进程是运行在内存和 CPU 上的一个过程。换句话说，进程是运行中的程序。

如果你在终端中启动一个进程，该进程将保留在该终端中，并由用户进程终止。用户进程的示例包括 `grep` 和 `find`，而不是你在整本书中所执行的大多数命令。记住，进程通常在系统启动时启动，或由守护进程启动。大多数进程提供系统服务，如打印、调度和维护，以及网络服务器服务，如 Web 器、数据库服务器、文件服务器和打印服务器。

每个进程都有一个进程 ID（PID），允许内核对它进行标识。此外，每个进程可以启动无限数量的其他进程（子进程）。相反，每个进程必须由一个已存在的进程（父进程）启动。因此，每个进程都有一个父进程 ID（PPID），用于标识启动它的进程。父子进程之间的关系示例如图 9-1 所示。

**CompTIA Linux+ 和 LPIC-1：Linux 认证指南**

**图 9-1** 父进程和子进程

![](img/12ad6df66c6622b4ab7acf53dfd7f646_376_0.png)

> **注意** PID 并不一定按顺序分配给新进程；每个 PID 都是根据 Linux 内核使用的进程表空条目生成的。

> **注意** 记住，尽管每个进程可以有无限数量的子进程，但它只能有一个父进程。

Linux 内核启动的第一个进程是初始化（或 init）守护进程，它的 PID 为 1，另一个 PID 为 0，后者指的是内核本身。`init` 守护进程在系统初始化过程中启动其他守护进程，包括允许用户登录的守护进程。当你登录系统后，登录进程会启动一个 shell。`shell` 解释用户命令并启动所有用户进程。因此，Linux 系统上的每个进程都可以通过检查一系列 PPID 追溯到 `init` 守护进程，如图 9-2 所示。

**图 9-2** 进程谱系

![](img/12ad6df66c6622b4ab7acf53dfd7f646_376_1.png)

## 第 9 章 管理 Linux 进程

**注意 4**
在运行 SysV 初始化进程的 Linux 系统上，`init` 守护进程会在命令输出中列为 `init`。在运行 Systemd 初始化进程的 Linux 系统上，`init` 守护进程会在命令输出中列为 `init` 或 `system`。

## 查看进程

虽然有多种 Linux 工具可以查看进程，但最通用且最常用的是 `ps` 命令。在不带参数的情况下，`ps` 命令仅显示在当前 shell 中运行的进程列表。下面的示例显示了用户登录 `tty2` 时该命令的输出：

```
[root@server1 ~]# ps
PID TTY TIME CMD
2159 tty2 00:00:00 bash
2233 tty2 00:00:00 ps
[root@server1 ~]#
```

执行输出显示启动的进程正在执行 `tty2` 命令的终端中运行。命令（CMD）列在 CPU 上花费的时间（TIME）、PID 和终端（TTY）旁边。在这种情况下，一个进程运行时间不到两秒，且经过的时间不需要任何内容。要找到更多关于这些进程的信息，你可以使用 `ps` 命令的 `-f` 或 `full` 选项，如下：

```
[root@server1 ~]# ps -f
UID PID C STIME CMD
root 2159 0 00:16 tty2 00:00:00 -bash
root 2233 3 00:16 tty2 00:00:00 ps -f
[root@server1 ~]#
```

列表提供了关于每个进程的更多信息。它显示了启动进程的用户（UID）、PID 和 STIME，以及 CPU 占用率（C），该值从零开始，并在每个在 CPU 上运行的进程周期中增加。

基础进程（PID = 2159）显示一个 shell 提示符并解释用户输入；启动的 ps 进程（PID = 2233）显示 ps 进程的 PID 为 2159。因为守护进程未关联终端，因此 `ps -f` 命令不会显示它们。要显示跨所有终端包括守护进程的列表，可以在任何 `ps` 命令中添加 `-e` 选项，如下所示：

```
[root@server1 ~]# ps -ef
UID PID C STIME CMD
root 1 0 01:22 00:00:00 /usr/lib/systemd/systemd
root 2 0 01:22 00:00:00 [kthre]
root 3 0 01:22 00:00:00 [kworker/0]
root 5 0 01:22 00:00:00 [worker2/0]
root 7 0 01:22 00:00:00 [migration]
root 8 0 01:22 00:00:00 [rc_bash]
```
