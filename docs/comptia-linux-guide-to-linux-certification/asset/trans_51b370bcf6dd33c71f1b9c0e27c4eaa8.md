

**Qt 工具包** 在 K 桌面环境中使用的软件工具包。

**restart 命令** 一个可以手动重启 upstart 守护进程的命令。

**runlevel（运行级别）** 一个 UNIX SysV 术语，用于定义 Linux 系统上特定类型和数量的守护进程。

**runlevel 命令** 用于显示当前及最近一次（上一次的）运行级别的命令。

**运行时配置 (rc) 脚本** 在系统初始化过程中使用，用于启动守护进程并提供系统功能的脚本。

**service 命令** 一个可以手动启动、停止和重启 UNIX SysV 守护进程的命令。

**service 单元** 一个 Systemd 术语，用于描述守护进程。

**start 命令** 一个可以手动启动 upstart 守护进程的命令。

**stop 命令** 一个可以手动停止 upstart 守护进程的命令。

**systemctl 命令** 一个可以手动启动、停止和重启 Systemd 守护进程，以及在系统初始化过程中配置 Systemd 守护进程启动的命令。

**system-config-keyboard 命令** 一个用于在 Fedora Linux 系统上配置键盘以供 X Windows 使用的命令。

**Systemd** 一种在 Linux 系统上使用的相对较新的软件框架，提供系统初始化过程和系统管理功能。

**系统初始化过程** 在启动期间执行提供系统服务的守护进程，并将系统带入可用状态的过程。

**target（目标）** 参见*目标单元*。

**目标单元** 一个 Systemd 术语，用于描述在 Linux 系统上运行的守护进程的数量和类型。它在功能上等同于 UNIX SysV 术语*runlevel（运行级别）*。

**telinit 命令** 一个 UNIX SysV 命令，用于将操作系统从一个运行级别更改为另一个运行级别。

**update-rc.d 命令** 一个可以在 Ubuntu Linux 系统上用于按运行级别配置 UNIX SysV 守护进程启动的命令。

**upstart** 现代 Linux 发行版中使用的 UNIX SysV 系统初始化过程的最近版本。

**UNIX SysV** 一个 UNIX 标准，用于提供 Linux 系统上系统初始化过程的结构。

**窗口管理器** 负责确定由 X Windows 在屏幕上绘制的窗口外观的 GUI 组件。

**X 客户端** X Windows 的一个组件，它请求从 X 服务器绘制图形并将其显示在终端屏幕上。

**X 显示管理器 (xdm)** 一个图形登录屏幕。

**XFree86** 在 Linux 发行版中使用的 X Windows 的一种常见实现。

**X.org** 在 Linux 发行版中使用的 X Windows 的一种常见实现。

**X 服务器** X Windows 的一个组件，它负责在终端屏幕上的窗口上绘制图形。

**xvidtune** 一个用于微调 X Windows 中使用的显卡 vsync（垂直同步）和 hsync（水平同步）设置程序。

**X Windows** Linux GUI 中负责在终端屏幕上的窗口上显示图形的组件。

## 复习题

1. 可以使用哪个命令来微调显卡的 vsync 和 hsync，以便在 X Windows 中使用？
   - a. `vidtune`
   - b. `synctune`
   - c. `xvidtune`
   - d. `vhtune`

2. 以下哪项陈述是正确的？
   - a. GRUB 引导加载器存储在 /usr/grub 目录中。
   - b. LILO 在修改后需要重新安装。
   - c. GRUB2 引导加载器常用于传统 Linux 系统。
   - d. GRUB 在修改后需要重新安装。

3. 哪个目录存储了大多数 UNIX SysV rc 脚本？
   - a. `/etc/rc5.d`
   - b. `/etc/rc.d`
   - c. `/etc/init.d`
   - d. `/usr/local/systemd`

4. 哪个运行级别会停止系统？
   - a. `1`
   - b. `6`
   - c. `0`
   - d. `5`

5. UNIX SysV init 守护进程在启动时参考哪个文件来确定默认运行级别？
   - a. `/etc/inistate`
   - b. `/inittab`
   - c. `/etc/init`
   - d. `/etc/inittab`

6. 可以使用哪个命令来启动 X Windows、窗口管理器和默认桌面环境？
   - a. startgui
   - b. startxdm
   - c. startx
   - d. gstart

7. 以下哪项陈述是正确的？
   - a. 引导加载器指向 MBR/GPT。
   - b. MBR/GPT 或活动分区都可以包含引导加载器。
   - c. MBR/GPT 和活动分区都指向引导加载器。
   - d. 引导加载器指向活动分区。

8. 对于 GRUB 来说，以下哪一项表示第三块硬盘驱动器上的第二个分区？
   - a. (hd3,2)
   - b. (hd4,3)
   - c. (hd2,3)
   - d. (hd2,1)

9. 在 Linux 中常用的两个 X Windows 实现是什么？（选择两个答案。）
   - a. X.org
   - b. Xfce
   - c. Xconfigurator
   - d. XFree86

10. 包含指向运行级别 2 的 UNIX SysV rc 脚本符号链接的目录名称是什么？
    - a. /etc/rc2.d
    - b. /etc/init.d/rc2.d
    - c. /etc/runlevel/2
    - d. /etc/inittab/rc2/d

11. GRUB2 引导加载器的第二阶段存储在哪个目录中？
    - a. /boot
    - b. /root
    - c. /bin
    - d. /

12. Linux 系统上加载的第一个守护进程是 ____________。
    - a. initstate
    - b. inittab
    - c. init
    - d. linux

13. 哪个命令会导致系统进入单用户模式？
    - a. init 0
    - b. init 1
    - c. init 6
    - d. initstate 5

14. GRUB 配置文件中的超时值是以什么为单位测量的？
    - a. 秒
    - b. 分钟的 1/10
    - c. 秒的 1/10
    - d. 秒的 1/100

15. 你最近修改了 /etc/default/grub 文件中的选项。接下来你可以使用什么命令来重建 GRUB2 配置文件？
    - a. grub2-install
    - b. grub-install
    - c. grubby
    - d. grub2-mkconfig

16. 你希望配置特定 upstart 守护进程被启动的运行级别。你应该怎么做？
    - a. 运行适当的 update-rc.d 命令。
    - b. 修改 /etc/rc[runlevel]d 目录的内容。
    - c. 修改 /etc/init 目录中的守护进程配置文件。
    - d. 运行适当的 systemctl 命令。

17. 以下哪个 Systemd 命令可用于停止名为 lala 的守护进程？
    - a. service stop lala
    - b. systemctl stop lala.service
    - c. chkconfig stop lala
    - d. stop lala

18. 以下哪个命令可用于在运行级别 1、2 和 3 中启动名为 lala 的 UNIX SysV 守护进程？
    - a. `chkconfig --level 123 lala on`
    - b. `update-rc.d lala defaults`
    - c. `systemctl enable lala 123`
    - d. `service enable lala 123`

19. 哪个 Systemd 目标对应运行级别 5？
    - a. `multi-user.target`
    - b. `graphical.target`
    - c. `system.target`
    - d. `runlevel5.target`

20. 可以在引导加载器中指定哪个关键字来强制系统以单用户模式启动？
    - a. `init`
    - b. `rescue`
    - c. `single`
    - d. `telinit`

## 动手项目

![](img/c27875544958897d817484d558c208c8_410_0.png)

这些项目应按给定的顺序完成。本章中的动手项目总共需要三小时完成。此实验的要求包括：

- 一台根据动手项目 2-1 安装了 Fedora Linux 并根据动手项目 6-1 安装了 Ubuntu Server Linux 的计算机。

### 项目 8-1

在这个动手项目中，你将在 Fedora 20 上使用并配置 GRUB2 引导加载器。

1. 启动你的 Fedora Linux 虚拟机。在你的 Linux 系统加载后，按下**Ctrl+Alt+F2**切换到命令行终端（tty2），并使用用户名*root*和密码 LNXrocks! 登录到终端。

2. 在命令提示符下，键入`less /boot/grub2/grub.cfg`并按 Enter。哪一行设置了在启动屏幕上用户交互的默认超时？检查 menuentry 段落。许多选项是否与原始 GRUB 引导加载器中的选项相匹配？

3. 在命令提示符下，键入`vi /etc/default/grub`并按 Enter 以编辑 GRUB2 配置文件。将`GRUB_TIMEOUT`的值更改为`30`。保存你的更改并退出 vi 编辑器。

