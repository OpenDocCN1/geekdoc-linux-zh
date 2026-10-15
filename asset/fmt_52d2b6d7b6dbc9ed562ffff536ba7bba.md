
从上一个输出可以看出，`LANG`变量被设置为`en_US.UTF-8`。同样注意，其他特定格式的区域变量被设置为使用`LANG`的值。这允许用户覆盖特定格式类型（如测量单位）的默认设置。例如，为了确保操作系统组件使用加拿大公制单位进行测量，你可以在 shell 环境中添加行`export LC_MEASUREMENT="en_CA.UTF-8"`；这将会使用带有 UTF-8 字符集的加拿大英语进行测量，而对所有其他类型使用美国英语。或者，为了确保所有类型都使用该区域设置，你可以设置`LC_ALL`变量的值，它会覆盖`LANG`和所有其他`LC`变量。要查看可以运行的所有区域设置的列表，可以运行`locale -a`命令。

> 注意
> `C`是所有 UNIX 和 Linux 系统都使用的标准区域。许多 Linux 管理员会在 shell 脚本的开头（哈希行下方）添加`export LANG=C`，以确保脚本中任何命令的标准输出（stdout）不依赖于执行它的系统的的区域设置。

你可以使用`localectl`命令更改系统上的区域设置。在不带参数的情况下，`localectl`显示当前区域设置。要查看可用区域列表，请运行`localectl list-locales`；要将默认值设置为`en_CA.UTF-8`，请运行`localectl set-lang=en_CA.UTF-8`。

### 总结

- GRUB引导程序通常由标准 BIOS 从存储设备的 MBR 或 GPT 加载，或者由 UEFI BIOS 从 UEFI 系统分区加载。GRUB Legacy 支持带有标准 BIOS 和 MBR 存储设备的系统，而 GRUB2 同时支持标准系统和 UEFI 系统，以及 MBR 和 GPT 存储设备。

- 引导程序加载 Linux 内核后，系统初始化过程将加载守护进程，以使系统处于可用状态。

- 有两种常见的初始化过程：UNIX Sysv 和 Systemd。
- UNIX Sysv 根据内存中加载的守护进程数量使用运行级别（runlevels）。Systemd 使用对应七个 UNIX 运行级别的五个标准。
- `init`守护进程负责切换运行级别时加载和卸载守护进程，以及启动和关机。
- 守护进程在系统初始化期间通过 UNIX Sysv 脚本或系统单元（units）执行。`/etc/init.d`目录包含 init 脚本，`/lib/systemd/system`和`/system`目录包含大多数系统单元。
- 除了使用单元和服务单元管理系统初始化外，Systemd 还可以使用 socket 单元管理网络守护进程、timer 单元调度程序以及挂载点文件。

- 你可以使用多种不同的命令在系统初始化后启动、停止和重启守护进程。`service`命令用于启动、停止和重启 UNIX Sysv 守护进程，而`systemctl`命令用于启动、停止和重启 Systemd 守护进程。
- 你可以使用`chconfig`或`update-rc`命令在启动时配置 UNIX Sysv 守护进程，并使用`systemctl`命令在启动时配置 Systemd 守护进程。
- Linux 具有可交换的环境，包括 X、客户端窗口管理器以及可选的桌面环境管理器，使用户能够更方便地使用桌面环境。
- X 是 Linux GUI 的核心组件，用于在屏幕上绘制图形。它有两个开源实现版本：X 和 Wayland。X 需要的硬件信息是自动检测的，但可以使用几种工具进行修改。
- 你可以通过命令行提示符从运行级别 3 启动 Linux GUI，也可以通过显示管理器（如 GDM）从运行级别 5 启动。
- Linux 有许多特定区域的设置，包括时间、日期和区域设置。

### 关键术语

- active（激活）
- ASCII
- assistive（辅助的）
- boot（启动）
- chconfig
- Desktop（桌面）
- de-
- dracut
- epoch（时期）
- init
- ISO
- kernel（内核）
- locale（区域设置）
- --
- mount（挂载）
- multi
- net
- partition（分区）
- root（根）
- runlevel（运行级别）
- runtime（运行时）
- service（服务）
- shell
- system
- target（目标）
- tzselect
- UTF-8
- window manager（窗口管理器）
- Wayland

### 复习题

1. 哪个命令可以修改默认区域设置？
a. tzselect
b. cmdline
c. locale
d. export LANG=C

2. 下列哪个说法正确？
a. GRUB Legacy 可以用于 MBR 或 GPT。
b. 修改 /etc/grub 后，必须运行 grub2-mkconfig。
c. GRUB 只能从 UEFI 系统分区加载。
d. 修改后需要重新安装 GRUB。

3. 哪个运行级别启动显示管理器 GDM？
a. 1
b. 6
c. 0
d. 5

4. 哪个 System 功能等于运行级别？
a. service
b. target
c. timer
d. mount

5. 哪个可以启动 Windows、窗口管理器和默认桌面环境？
a. startgui
b. startxd
c. startx
d.

6. 下列哪个说法正确？
a. Unicode 为不同语言提供了本地化支持。
b. ASCII 是目前最常用的字符集。
c. UTF-8 用于提供 Unicode 字符集。
d. ASCII 是 IEEE-8859 标准的扩展。

7. 下列哪个标识了驱动第三块硬盘上的第二个 MBR 分区？
a. hd2,msdos2
b. hd4,mbr3
c. hd3,mbr1
d. hd2,msdos1

8. 哪些 X 实现通常用于 Linux？（选择两个答案）
a. Xorg
b. XFCE
c. winX
d. Wayland

9. 哪个目录包含指向运行级别 2 的 Unix SysV rc 脚本的符号链接？
a. /etc/rc2
b. /etc/init.d/rc2
c. /etc/runlevel/2
d. /etc/initab/rc2

10. GRUB引导程序的第二阶段存储在何处？
a. /boot
b. /bin
d. /

## 第 8 章 系统初始化、X 和 Windows

11. 哪条命令指示 UNIX SysV init 或 Systemd 守护重启系统？

+ - init 0
- telinit 1
- init 6
- telinit 5

12. 哪种辅助技术会使低视力人士更容易访问桌面环境？

+ - 高对比度 (High Contrast)
- 视觉警报 (Visual Alerts)
- 重复键 (Repeat Keys)
- 鼠标辅助 (Click Assist)

13. 你已使用 `date` 命令修改了系统时间。运行什么命令可以确保系统 BIOS 也更新了相同的时间？

+ - timatectl --update
- tzclock
- hwclock -w
- date --set

14. 你想配置运行级别（runlevels）以便启动某个特定的启动守护进程。你应该怎么做？

+ - 运行 `update-rc.d` 命令
- 修改 /etc/init/ 目录的内容。
- 使用 /etc/init 目录修改配置文件。
- 运行 `systemctl` 命令。

15. 下列哪个系统命令可以用于停止守护进程调用？

+ - service stop la
- systemctl stop la.service
- chkconfig stop la
- stop la

16. 下列哪个命令可以用于在运行级别 1 和 2 中启动 UNIX SysV 守护进程调用？

+ - chkconfig --level 123 la
- update-rc.d la defaults
- systemctl enable la 123
- service enable la 123

17. 你创建了一个 System 单元，在进入多用户目标（target）时挂载文件系统。但是：

+ - 验证单元文件中是否使用 UUID 指定了文件系统。
- 检查 /etc/fstab 中文件系统的条目。
- 确保使用 `systemctl` 命令激活了 root。
- 运行 `update-rc.d` 命令重新加载单元文件。

18. 在引导加载程序中可以指定什么顺序，使系统进入单用户模式（Single Mode）？

+ - init
- rescue
- single
- telinit

19. 在 shell 脚本开头设置哪个变量来选择特定的区域设置（locale）？

+ - LC
- LANG
- LOCALE
- CMDLINE

20. 哪种桌面环境最可能安装在 Linux 服务器上？

+ - XFCE
- XDM
- KDE
- GN

这些项目应该按照给出的顺序完成。本章介绍的实践项目总共有三小时完成时间。实验的要求包括：

+ - 一台安装了 Linux 的计算机，用于实践项目 2-1。

## 项目 8-1

预计耗时：35 分钟
目标：使用 GRUB2。
描述：在这一实践项目中，你将在 Fedora 上配置 GRUB2 引导加载程序。

+ 1. 启动你的 Linux 虚拟机。在 Linux 系统启动后，使用 Ctrl+Alt+F5 切换到命令行终端 (tty)，并使用用户 root 和密码 LINUXroot 登录。

# CompTIA Linux+ 和 LPCIC-1: Linux 认证指南

+ 2. 如果你的虚拟机启用了 UEFI BIOS，输入 `cat /boot/efi/fedora/grub.cfg` 并按回车。注意文件中的 "set prefix" 和 "configfile" 指的是 /boot/grub2/grub.cfg 的内容。

+ 3. 在命令提示符下，输入 `less /boot/grub2/grub.cfg` 并按回车。哪一行设置了启动屏幕上用户交互的超时？是否存在许多段落？完成后按 q 。

+ 4. 在命令提示符下，输入 `ls -l /boot/loader/entries/*64.conf` 并按回车。这些文件代表什么？注意 Linux 内核初始化的内联。

+ 5. 在命令提示符下，输入 `vi /etc/default/timeout` 并按回车以编辑 GRUB2 配置文件。将 `GRUB_TIMEOUT` 的值改为 30。保存更改并退出 vi 编辑。

+ 6. 在命令提示符下，输入 `grub2-mkconfig -o /boot/grub2/grub.cfg` 并按回车，使用你的更改重构 GRUB2 配置文件。

+ 7. 输入 `reboot` 并按回车重启系统。在 GRUB 启动界面上，查看可用选项。在 POST 之后、默认操作系统启动之前，你如何与 GRUB 引导加载程序交互？接下来，按 c 获取命令提示符。

+ 8. 在 GRUB 提示符下，输入 `help` 并按回车查看可用命令列表，按空格键循环到下一个项目。输入 `lsmod` 并按回车查看 GRUB2 加载的模块列表。是否加载了 isbf 模块？之后，应该有一个名为 GRUB2 的变量（存储在 /boot/grub2/grubenv 中的上一个操作系统）。输入 `reboot` 并按回车重启系统。

+ 9. 在 GRUB 启动界面上，按 e 编辑配置。找到第一个以 "linux" 单词开头的行并导航到该行的末尾（该行的最后两个单词应该是 quiet）。在 quiet 单词之后添加 `single` 单词并按 F10 启动你修改后的配置。这种修改对引导加载程序有什么什么影响？

+ 10. 输入你的 root 密码 LINUXRocks!

+ 12. 在命令提示符下，输入 `systemctl status` 并按回车。当前状态是什么？

## 项目 8-2

预计耗时：35 分钟
目标：SysV。
描述：在这一实践项目中，你将探索 SysV 初始化。

+ 1. 按 Ctrl+Alt+F5 切换到命令行终端，并使用用户 root 和密码 LINUXroot 登录。

+ 2. 在命令提示符下，输入 `runlevel` 并按回车。当前运行级别是多少？

+ 3. 在命令提示符下，输入 `cat /etc/fstab` 并按回车。列出了哪些文件系统？

+ 4. 在命令提示符下，输入 `ls /etc/init.d/` 并按回车。哪些脚本？

+ 5. 在命令提示符下，输入 `chkconfig --list` 并按回车。哪些服务已启用？

+ 6. 在命令提示符下，输入 `ls /etc/runlevel.d/` 并按回车。哪些符号链接？

+ 7. 在命令提示符下，输入 `init 3` 并按回车。当前运行级别是多少？

+ 8. 在命令提示符下，输入 `init 5` 并按回车。当前运行级别是多少？

+ 9. 在命令提示符下，输入 `service status cron` 并按回车。cron 服务正在运行吗？

+ 10. 在命令提示符下，输入 `service restart cron` 并按回车。cron 服务重启了吗？

+ 11. 在命令提示符下，输入 `service stop cron` 并按回车。cron 服务停止了吗？

+ 12. 在命令提示符下，输入 `service start cron` 并按回车。cron 服务启动了吗？

+ 13. 在命令提示符下，输入 `chkconfig disable` 并按回车。cron 服务被禁用了吗？

+ 14. 在命令提示符下，输入 `chkconfig enable` 并按回车。cron 服务已启用吗？

+ 15. 在命令提示符下，输入 `systemctl list-units` 并按回车。哪些单元是激活的？

## 项目 8-3

预计耗时：40 分钟
目标：配置单元服务。
描述：在实践项目中，配置一个单元文件用于在 Fedora Linux 系统初始化过程中执行 shell 脚本 (/bootstrap)。

+ 1. 按 Ctrl+Alt+F5 切换到命令行终端，并使用用户 root 和密码 LINUXroot 登录。

+ 2. 在命令提示符下，输入 `vi /bootstrap.sh` 并按回车。按照以下行：找到、保存并退出编辑器。

```
#!/bin/bash

echo "Boot started" >>/tmp/bootstrap.txt
```

+ 3. 在命令提示符下，输入 `chmod +x /bootstrap.sh` 并按回车，确保新创建的脚本可以执行。

+ 4. 在命令提示符下，输入 `vi /etc/systemd/system/bootstrap.service` 并按回车。创建以下单元文件：

```
[Unit]

Description=Bootstrap Script

[Service]

Type=oneshot

ExecStart=/bootstrap.sh

[Install]

WantedBy=multi-user.target
```

+ 5. 在命令提示符下，输入 `systemctl daemon-reload` 并按回车，让 systemd 知晓新的单元文件。

+ 6. 在命令提示符下，输入 `systemctl start bootstrap.service` 并按回车。执行了吗？

+ 7. 在命令提示符下，输入 `cat /tmp/bootstrap.txt` 并按回车。输出是什么？

+ 8. 在命令提示符下，输入 `systemctl enable bootstrap.service` 并按回车，启用该服务以便下次启动时运行。

+ 9. 重启系统并检查脚本是否再次执行。

# CompTIA Linux+ 与 LPIC-1：Linux 认证指南

4. 在命令提示符下，输入 `vi /etc/systemd/system/bootscript.service` 并按回。添加以下行。完成后，保存并退出 vi 编辑器。

```
[Unit]

Description=boot script

[Service]

ExecStart=+bootscript.sh

[Install]

WantedBy=multi-user.target
```
