
j. 在 shell 提示符处，使用 `vi` 编辑 `/etc/inittab` 文件，将默认运行级别改回 5。
k. 在 shell 提示符处输入 `init 0` 以关闭系统电源。
l. 重新开启系统电源，并以普通用户身份重新登录系统。
6. 练习在系统的运行级别 3 和 5 上启用 ntp 守护进程。ntp 守护进程用于将本地 Linux 系统的时钟与其他计算机系统的时钟进行同步。完成以下操作：
   a. 打开一个终端会话并切换到 root 用户账户。
   b. 在 shell 提示符处，使用 `rpm` 实用工具验证 ntp 包是否已安装在你的系统上，输入命令为 `rpm -q ntp`。如果 `rpm` 命令返回包名称和版本号，则 ntp 已安装。如果没有返回任何内容，则 ntp 包尚未安装。
   
   **注意** 如果尚未安装，请使用第 8 章中介绍的步骤从发行版 DVD 安装 ntp 包。
   
   c. 在 shell 提示符处，查看 `/etc/ntp.conf` 文件。
   d. 向下滚动到如下所示的行：
   ```text
   server 127.127.1.0 local clock (LCI)
   fudge 127.127.1.0 stratum 10 #LCI is unsynchronized
   ```
   e. 按下 INSERT（插入）键。
   f. 在 fudge 行下方添加一个新行。
   g. 在新行中添加以下指令：
   ```text
   server bigben.cac.washington.edu
   ```
   
   此指令配置 ntp 服务，使本地计算机时间与互联网上 bigben.cac.washington.edu 公共 ntp 服务器上的时间同步。
   h. 按下 ESC；然后输入 `:wq`。
   i. 通过在 shell 提示符处输入 `/etc/init.d/ntp restart` 或 `/etc/rc.d/init.d/ntp restart` 来启动 ntp 服务。你应该看到守护进程正在启动且正在从 bigben.cac.washington.edu 获取时间的消息，如下所示：
   ```text
   ws1:~ # /etc/init.d/ntp restart
   Shutting down network time protocol daemon (NTPD)            done
   Time synchronized with bigben.cac.washington.edu
   Starting network time protocol daemon (NTPD)                  done
   ws1:~ #
   ```
   j. 通过在 shell 提示符处输入 `chkconfig --s ntp 35` 来配置 ntp 守护进程，使其在运行级别 3 和 5 自动启动。
   k. 通过在 shell 提示符处输入 `chkconfig -l ntp` 来检查 ntp 守护进程的状态。你应该看到运行级别 3 和 5 被设置为 on（开启），如下所示：
   ```text
   ws1:~ # chkconfig -l ntp
   ntp                    0:off   1:off   2:off   3:on   4:off   5:on    6:off
   ws1:~ #
   ```

## 关闭系统

与其他操作系统一样，你需要正确关闭 Linux 系统。这确保在关闭系统电源之前，所有待处理的磁盘写入操作实际上已提交到磁盘。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_260_0.png)

**警告** 如果你意外关闭 Linux 系统电源，可能会引入文件系统的损坏和不一致。始终使用正确的关机程序。此外，我强烈建议在你的系统中配备不间断电源（UPS）。它们价格低廉，如果断电，能拯救你的系统。相信我，我知道。我有一次因为停电失去了一个未受保护的服务器，不得不通宵从备份磁带中恢复它。再也不要了！

你可以使用几个命令来正确关闭 Linux 系统，包括以下命令：

- **init 0**：将系统切换到运行级别 0，这会使系统停止运行。
- **init 6**：将系统切换到运行级别 6，这会重启系统。
- **halt**：关闭系统。
- **reboot**：重启系统。

除了这些命令外，你还可以使用 **shutdown** 命令来关闭或重启系统。与前面的命令相比，它具有几个主要优势：

- 你可以指定系统在指定时间段后关闭。这给了用户时间在系统关闭前保存其工作并注销。即使你不在场，也可以让你在指定时间关闭系统。
- 它允许你向所有已登录的用户发送消息，警告他们即将关机。
- 它不允许其他用户在待执行的关机之前登录。

使用 shutdown 的语法是 `shutdown +m -h -r message`。`+m` 选项指定关闭系统前的时间量（以分钟计）。你也可以使用 `now` 选项代替 `+m` 以指定系统立即关闭。如果你需要在特定时间关闭系统，可以用时间（以 `hh:mm` 格式输入）替换 `+m`，该时间即为应执行关机的时间。`-h` 选项指定系统停止运行，而 `-r` 选项指定系统重启。shutdown 的一些使用示例如下所示：

`shutdown +10 -b Please save your work and log out.`

当你输入此命令时，其他所有已登录的用户将看到以下消息：

```text
tux@ws1:~/Desktop> 
Broadcast message from root@ws1 (pts/3) (Thu Feb 17 10:29:59 2011): 

Please save your work and log out.
The system is going DOWN for system halt in 10 minutes!
```

如果你使用 shutdown 命令计划了关机，但后来需要取消关机，请在 shell 提示符处输入 `shutdown -c`。

干得漂亮！你正在迈向 LPIC-1/CompTIA Linux+ 认证的路上！让我们回顾一下你在本章中学到的内容。

## 章节复习

在本章中，你学习了如何管理 Linux 启动过程。我在本章开始时回顾了 Linux 启动过程是如何工作的。我将启动过程分解为三个阶段：

- BIOS 阶段
- 引导加载程序阶段
- 内核阶段

在 BIOS 阶段，计算机的 BIOS 芯片控制着系统。它的主要任务是设置系统中的基本硬件，使用上电自检（POST）例程测试硬件，然后找到带有启动文件的设备。

在引导加载程序阶段，BIOS 将系统控制权交给引导加载程序。引导加载程序的关键任务是定位并加载你的操作系统内核。引导加载程序可以位于引导设备的主引导记录（MBR）中，也可以位于驱动器上的引导分区中。Linux 引导加载程序可以配置菜单，为最终用户提供几个引导操作系统的选项。甚至可以配置为加载非 Linux 操作系统，例如 Windows。

Linux 引导加载程序在你的系统 RAM 中创建一个虚拟硬盘（称为 ramdisk），并将基本根文件系统复制到其中。你的 Linux 内核可以使用这个虚拟文件系统来加载访问真实存储设备所需的软件，检查它们并挂载它们。这个虚拟文件系统称为 initrd 映像。

在内核阶段，引导加载程序从硬盘或其他引导设备将操作系统加载到你的系统 RAM 中。你的 Linux 内核位于文件系统中的 `/boot` 目录下，名为 `vmlinuz-version.gz`。在内核加载后，内核阶段会发生以下事件：

- 内核使用 BIOS 和 CMOS 芯片中的各种设置初始化系统中的基本硬件。
- 内核搜索并使用 initrd 文件系统运行 *linuxrc* 程序以设置系统。
- 当 *linuxrc* 执行完成后，initrd 文件系统被卸载，ramdisk 被销毁。
- 内核探测新硬件并加载适当的驱动程序模块。
- 真正的根（/）文件系统被挂载。
- 内核加载 init 进程。

然后我们将注意力转向配置 Linux 引导加载程序。我们查看的第一个 Linux 引导加载程序是 LILO 引导加载程序。LILO 曾经是最多 Linux 发行版使用的默认引导加载程序。最近，大多数发行版已经从 LILO 转向 GRUB 引导加载程序。如果你的系统当前使用 GRUB 并且你想切换到 LILO，你必须首先创建一个 `/etc/lilo.conf` 配置文件。然后在 shell 提示符处简单地输入 *lilo*。默认情况下，这会在引导设备的 MBR 中用 LILO 覆盖 GRUB。

你可以使用 *lilo* 命令的 *-b* 选项来指定 LILO 安装的位置。如果你指定一个存储设备，例如 */dev/hda*，则 LILO 将安装在指定设备的 MBR 中。如果你指定设备上的一个分区，例如 */dev/hda1*，则 LILO 将安装在该分区中。

一旦安装了 LILO，你可以使用 */etc/lilo.conf* 文件来自定义其工作方式。在此文件中做出任何配置更改后，必须在 shell 提示符处输入 *lilo* 重新安装 LILO。

某些类型的硬件将要求你使用 ELILO 代替 LILO。ELILO 是 LILO 的增强版本。ELILO 还与标准的 Intel x86 硬件向后兼容，因此你也可以在你的传统 Linux 系统上使用 ELILO 代替 LILO。

在讨论完 LILO 后，我接着讨论了 GRUB 引导加载程序。我指出，大多数当前的 Linux 发行版都使用 GRUB 引导加载程序。我指出，GRUB 分为几个阶段：

- **Stage 1**：通常存储在 MBR 中。它指向 Stage 1.5 或 Stage 2 的位置。
- **Stage 1.5**：存储在 MBR 之后的前 30KB 中。它指向 Stage 2 的位置。
- **Stage 2**：存储在磁盘分区内。向最终用户呈现一个菜单以选择要引导的操作系统。

我接着指出，用于配置 GRUB 的文件取决于你的发行版。一些发行版使用 */boot/grub/grub.conf*；其他使用 */boot/grub/menu.lst*。GRUB 将系统中的硬盘称为 `hdX`，其中 X 是系统中驱动器的编号。SCSI、SATA 和 IDE（PATA）驱动器以此方式引用。驱动器上的分区被称为 `hdX,Y`，其中 Y 是驱动器上分区的编号。

如果你在文件系统中为 /boot 目录创建了单独的分区，那么 GRUB 将使用此作为 GRUB 根，并在引用 /boot/grub 内的文件时不包含 /boot 路径。如果你的 /boot 目录没有自己的分区，那么 GRUB 将使用完整路径来引用 /boot/grub/ 文件。

