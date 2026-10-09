

- `/sbin/update` 由 inittab 执行，用于刷新脏缓冲区。
- `/etc/rc.d/rc*.d` 目录包含在启动和关机过程中由 init 执行的脚本。最常用的运行级别是 3 和 5。3 是默认的命令行运行级别，5 是默认的图形用户界面（GUI）运行级别。

共有七种不同的运行级别。

- 0 关机
- 1 单用户模式
- 2 未使用（可由用户定义）
- 3 完整多用户模式
- 4 未使用（可由用户定义）
- 5 基于 X 的登录屏幕（GUI）的完整多用户模式
- 6 重启

运行级别 2 到 5 具有虚拟控制台，可通过 Ctrl+Alt+F1-7 键组合访问。

关闭 Linux 系统可以确保文件被保存且文件系统被卸载。如果不执行关机操作直接断电，可能会导致文件损坏。

用户通过用户名进行标识，通过密码进行身份验证。可以使用 `useradd` 命令轻松添加用户，并使用 `passwd` 命令更改密码。用户还通过 UID 进行标识，UID 是一个唯一标识符，值大于或等于 500。也有 GUI 工具可以轻松地添加用户和组。

用户总是属于一个组。一个组可以包含一个或多个用户。组用于简化在处理文件权限时的管理问题。

Linux 中的文件分为可共享和不可共享、变量和静态文件。可共享文件可供多个用户使用，不可共享文件仅供一个用户使用。变量文件可以根据需要进行更改，而静态文件具有恒定值。

文件系统层次结构标准（FHS）为 Linux 系统定义了常用目录。文件系统层次结构以根（/）目录开始，包含许多常用目录和其他用户定义的目录。

文件权限分配给所有者、组和其他所有人。权限指示读取、写入和执行权限。在长文件列表中，每个文件列表开头的 10 个字符表示文件类型以及所有者、组和其他人的权限。使用 `chmod` 命令分配权限。

## 自我测试

1. _______ 程序包含控制键盘、显示器、磁盘驱动器及其他连接到计算机的设备所需的所有代码。
   a. BIOS
   b. PnP
   c. init
   d. PnP

2. 下列哪项是系统启动的正确顺序？
   a. 寻找可启动介质，POST，加载引导加载程序，加载内核，执行 init
   b. 寻找可启动介质，POST，加载内核，加载引导加载程序，执行 init
   c. POST，寻找可启动介质，加载引导加载程序，加载内核，执行 init
   d. POST，寻找可启动介质，加载内核，加载引导加载程序，执行 init

3. 下列哪项是 init 进程的正确启动顺序？
   a. 读取 /etc/inittab 文件，运行 /etc/rc.d/rc.sysinit 脚本，启动后台进程
   b. 读取 /etc/inittab 文件，启动后台进程，运行 /etc/rc.d/rc.sysinit 脚本
   c. 启动后台进程，运行 /etc/rc.d/rc.sysinit 脚本，读取 /etc/rc.d/rc.sysinit 文件
   d. 运行 /etc/rc.d/rc.sysinit 脚本，读取 /etc/inittab 文件，启动后台进程

4. **配置文件**由 Ctrl+Alt+Delete 键序列处理。
   a. /etc/inittab
   b. /etc/rc.d/rc.sysinit
   c. /etc/init
   d. /etc/lilo

5. 哪个运行级别提供完整的多用户模式和命令行接口？
   a. 0
   b. 1
   c. 3
   d. 5
   e. 6

6. 哪个配置文件包含默认运行级别信息？
   a. /etc/inittab
   b. /etc/rc.d/rc.sysinit
   c. /etc/init
   d. /etc/lilo

7. 哪个运行级别提供带有基于 X 的登录屏幕（GUI）的完整多用户模式？
   a. 0
   b. 1
   c. 3
   d. 5
   e. 6

8. 重启 Linux 操作系统的正确命令是 ________。
   a. /sbin/reboot -r now
   b. /sbin/reboot -h now
   c. /sbin/shutdown -r now
   d. /sbin/shutdown -h now

9. 下列哪些是强密码的特征？（选择三项。）
   a. 长度至少为 8 个字符。
   b. 包含单词序列以使其更易于记忆。
   c. 包含大写字母和小写字母。
   d. 包含特殊字符和数字。
   e. 应包含连续的数字或日期。

10. 使用 ______ 命令添加用户。
    a. su
    b. useradd
    c. groupadd
    d. usermod
    e. passwd

11. 使用 ______ 命令将用户添加到组中。
    a. su
    b. useradd
    c. groupadd
    d. usermod
    e. passwd

12. 权限由长文件列表中显示的十个字符标识。最后三个字符表示什么？
    a. 目录或文件
    b. 其他所有人
    c. 组
    d. 所有者

13. 要将文件 myfile 的权限更改为包含所有者的执行权限，请使用命令 ______。
    a. chmod o+x myfile
    b. chmod o+w myfile
    c. chmod u+x myfile
    d. chmod u+w myfile

14. 判断对错：强密码应每 30 到 90 天更改一次。

15. 命令 **chmod 754 myfile** 分配了下列哪种权限？
    a. 所有者、组和其他所有人的读/写/执行权限
    b. 所有者的读/写/执行权限，组的读/写权限，以及其他所有人的读/写权限
    c. 所有者的读/写/执行权限，组的读/执行权限，以及其他所有人的读/写权限
    d. 所有者的读/写/执行权限，组的读/执行权限，以及其他所有人的只读权限

16. 要删除 /home/jsmith/mydir 目录，请使用下列哪个命令？
    a. rmkdir /home/jsmith/mydir
    b. rm /home/jsmith/mydir
    c. rm -r /home/jsmith/mydir
    d. cd /home/jsmith/mydir

17. BIOS 程序存储在 ___________ 中。
    a. RAM
    b. CMOS
    c. ROM
    d. MBR

18. 判断对错：运行命令 **chmod 755 myfile** 后，myfile 被分配给所有者的读、写和执行权限。

19. BIOS 将什么加载到内存中？
    a. RAM
    b. CMOS
    c. ROM
    d. MBR

20. Linux 操作系统在启动期间所需的任何程序都由 ____________ 脚本启动。
    a. /etc/rc.d/rc.sysinit
    b. /sbin/update
    c. /etc/sysconfig
    d. /etc/rc.d/rc3.d

21. 判断对错：命令 **usermod -G jsmith -U dbrown** 将用户 dbrown 添加到组 jsmith。

22. 关于文件 /etc/rc3.d/$S5sshd，下列哪些说法是正确的？（选择两项。）
    a. 它是一个启动文件。
    b. 它在运行级别 3 中执行。
    c. 它是一个终止脚本。
    d. 它是第 55 个执行的脚本。

23. 哪些运行级别可由用户定义？（选择两项。）
    a. 1
    b. 2
    c. 3
    d. 4
    e. 5

24. 判断对错：通过将运行级别 5 设置为默认运行级别进入单用户模式。

25. 判断对错：用户名必须由用户的首名首字母和姓氏组合而成。

## Linux 命令行

第 5 章

### 章节目标

- 设置环境变量
- 描述并使用多用户环境的功能
- 使用常见的 shell 命令和表达式
- 使用 vi 创建、编辑和保存文件

### 使用命令行 Shell

绝大多数，甚至所有命令都可以通过 GUI 工具完成。然而，了解命令行界面（CLI）可以使大多数任务的 Linux 管理变得更快。有些命令只能通过命令行完成。使用 GUI 工具需要鼠标移动并通过迷宫般的菜单和工具栏寻找命令，这对大多数管理员来说是一个繁琐的过程。

经验丰富的用户还可以编写 shell 脚本。shell 脚本是存储在一个文件中的命令集合。该文件被授予执行权限，用于执行各种任务。脚本将在下一章中讨论。

最早的操作系统使用命令行解释器与用户交互。命令解释器通过键盘接受用户输入，解释每个单词（或解释这些单词），然后执行所需的动作。最早的命令解释器相当基础，提供的功能不多。为了提供更好的与操作系统交互的方式，开发了 shell（图 5–1）。第一个 shell 程序是 Bourne shell (sh)，由 S. R. Bourne 开发。此后，开发了其他 shell，包括 C shell (csh)、Korn shell (ksh) 和 bash shell (Bourne Again Shell)。

### 命令行基础

bash shell（参见 http://www.gnu.org/software/bash/bash.html）是自由软件基金会的产品，被大多数 Linux 操作系统使用。Linux 中通常提供几种 shell，但 bash shell 是用户的默认 shell。

如果你将系统启动到运行级别 3，你就处于命令行提示符下。如果你正在使用 X 窗口系统（GUI），你需要打开一个终端窗口。终端窗口是一个终端模拟器程序，它在窗口中打开并运行 shell 程序。有几种不同的终端程序：gnome-terminal、xterm 等。通常，在 GUI 中，你可以右键单击屏幕并从显示的弹出菜单中选择终端。

在第 2 章中讨论的虚拟终端也可以使用。按 Ctrl+Alt+F1 显示第一个虚拟终端，Ctrl+Alt+F2 显示第二个，等等。Linux 通常有六个虚拟终端，第七个显示 GUI。虚拟终端与 CLI 一起工作，但 GUI 仍然处于活动状态，可以通过按 Ctrl+Alt+F7 显示。当终端显示 **login:** 提示符时，输入有效 ID 然后输入密码以显示 bash shell。将显示 CLI 提示符。通常，提示符将是 $，

