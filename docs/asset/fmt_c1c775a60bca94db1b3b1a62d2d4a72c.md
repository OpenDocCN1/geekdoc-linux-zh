
d. 无法做到，因为元字符至关重要。

e. 在其前面加 `\`

### 13. 你知道一个 Linux 命令可以为你执行功能，但你忘记了命令的完整名称。你记得哪个命令变量提示符显示可能包含你所需命令的列表？

a. `man -k flush`

b. `man -k find all`

c. `man`

d. `man -key`

### 14. 哪个命令显示当前登录 Linux 系统的用户？

a. `finger`

b. `who`

c. `id`

d. `date`

### 15. root 用户登录系统时接收到什么提示符？

a. `$`

b. `@`

c. `#`

d. `!`

### 16. 普通用户登录系统时接收到什么提示符？

a. `$`

b. `@`

c. `#`

d. `!`

# 第 2 章 Linux 的安装与使用 85

+ 17. 下列哪项指的是 Linux 中第二块 SAS 硬盘上的第三主分区？

aa. `hdb2`

b. `sda3`

c. `hdb3`

d. `ddb3`

+ 19. 如果你从 Linux 现场介质启动计算机，你可以在安装到持久性存储设备之前使用功能完备的 Linux 系统。

正确或错误？

+ 18. 在安装 Fedora Linux 时，你通常最少需要哪两个分区？（选择两个）

a. `/`

b. `/boot`

c. `swap`

d. `/home`

+ 20. 下列哪项不是用于在另一个操作系统中安装 Linux 的虚拟化软件示例？

a. Oracle VirtualBox

b. Microsoft Hyper-V

c. Spicewarks

d. VMWare

# 动手实践项目

这些项目应按照给出的顺序完成，总计需要三个小时来完成。这些项目对软件和硬件的要求包括：

* 一台 64 位计算机，至少配备 8GB 内存、120GB 持久性磁盘存储和一个 DVD 驱动器

* 一个包含虚拟化软件产品、Web 浏览器和互联网连接的 操作系统

* Fedora 28 现场介质的 ISO 镜像（`Fedora-Workstation-Live-x86_64-28-1.1.iso`）

### 项目 2-1

在这个动手项目中，你将在 Windows 计算机的虚拟机上安装 Fedora 28 Linux。

+ 1. 在你的虚拟化软件中，创建一个名为 Fedora Linux 的新虚拟机，并具有以下特征：

* 4GB 内存

* 通过电脑的网卡连接互联网（优选使用外部虚拟交换器或桥接模式）

* 一个 50GB 的 SATA/SCSI/SAS 虚拟硬盘（动态分配）

* 将虚拟机的 DVD 挂载到 Fedora 28 现场介质的 ISO 文件（`Fedora-Workstation-Live-x86_64-28-1.1.iso`）

+ 1. 使用你的虚拟化软件启动并连接到 Fedora 虚拟机。

+ 2. 在 Fedora-Workstation-Live 28 界面上，按 Enter 键测试你的安装介质并启动 Fedora Live。

+ 3. 在图形桌面和“欢迎 Fedora”屏幕加载后，选择安装到硬盘（Install to Hard Drive）选项启动 Fedora 安装程序。

+ 4. 在“欢迎 Fedora 28”界面上，选择英语（美国）并点击继续（Continue）。在安装摘要页面上，点击时间与日期（Time & Date），选择你的时区（如有必要），并点击完成（Done）。

+ 5. 在安装摘要页面上，点击安装目标（Installation Destination）。你应该看到你的 50GB 磁盘已被选中且为 `sda`。在存储配置上选择自定义（Custom），完成后点击完成（Done）。

+ 6. 在手动分区界面，从列表框中选择标准分区（Standard Partition）分区方案，并选择点击此处自动创建（Click here to create it automatically）链接。这将创建分区。

+ a. 突出显示 `/` (`sda3`) 分区，将容量（Capacity）减至 35GB (35GB)，并点击更新设置（Update Settings）。这将会在第一个磁盘上释放出一些未分区的空间供后续练习使用。

+ b. 点击完成（Done），然后在提示时接受更改（Accept Changes）。

+ 7. 在安装摘要页面上，点击开始安装（Begin Installation）。

+ 8. 当安装完成后，点击退出（Quit）。这将返回你的 Fedora 现场桌面。

+ 9. 点击右上角的电源图标，选择出现的电源图标，并点击关机（Power Off）关闭你的 Fedora Live 镜像。

+ 10. 在你的虚拟化软件的虚拟机设置中，确保 DVD 不再挂载到 Fedora ISO 镜像。

+ 11. 最后，使用你的虚拟化软件启动 Linux 虚拟机以进入你新的 Linux 操作系统。

+ 12. 在欢迎向导中，按下一步（Next）。

+ a. 在隐私页面，使用滑动条禁用地理位置服务（Location Services）和自动问题报告（Automatic Problem Reporting），并按下一步（Next）。

+ b. 在在线账户页面，按跳过（Skip）。

+ c. 在关于（About）页面上，在全名（Full Name）文本框中指定你的全名，在用户名（Username）文本框中指定用户名 `user1`，然后按下一步（Next）。

+ d. 在密码页面，指定密码为 `LINUXrocks` 并点击下一步（Next），然后点击使用 Fedora（Using Fedora）。

### 项目 2-2

在这个动手项目中，你为 root 用户设置密码，探索 Linux 系统上的某些命令行终端，并在 BASH shell 中输入一些命令。

+ 1. 在 Linux 系统完成安装加载并完成欢迎向导后，你将处于一个图形终端 (`tty1`)。不要登录此图形终端，按 `Ctrl+Alt+F3` 切换到命令行终端 (`tty3`)，并使用用户名 `user1` 和密码 `LinuxRocks!` 登录终端。你收到了什么提示符？为什么？

+ 2. 在提示符处，输入 `sudo password root` 并按 Enter 设置 root 用户密码。在提示时，输入密码 `LinuxRocks!`, 然后两次输入所需的 root 密码 `LinuxRocks!` 来设置 root 用户密码。

+ 3. 在提示符处，输入 `date` 并按 Enter 查看当前日期时间。现在，输入 `Date` 并按 Enter。为什么你会收到错误信息？你能判断是哪个 shell 给你的这条信息吗？

+ 4. 切换到不同的命令行终端 (`tty3`) 到命令行终端 (`tty3`)，并使用用户名 `user1` 和密码 `LinuxRocks!` 登录终端。你收到了什么提示符？为什么？

+ 5. 在提示符处，输入 `sudo password root` 并按 Enter 设置 root 用户密码。在提示时，输入密码 `LinuxRocks!`, 然后两次输入所需的 root 密码 `LinuxRocks!` 来设置 root 用户密码。

+ 6. 在提示符处，输入 `date` 并按 Enter 查看当前日期时间。现在，输入 `Date` 并按 Enter。为什么你会收到错误信息？你能判断是哪个 shell 给你的这条信息吗？

+ 7. 切换到不同的命令行终端 (`tty3`) 到命令行终端 (`tty3`)，并使用用户名 `user1` 和密码 `LinuxRocks!` 登录终端。你收到了什么提示符？为什么？

+ 8. 在提示符处，输入 `sudo password root` 并按 Enter 设置 root 用户密码。在提示时，输入密码 `LinuxRocks!`, 然后两次输入所需的 root 密码 `LinuxRocks!` 来设置 root 用户密码。

+ 9. 在提示符处，输入 `date` 并按 Enter 查看当前日期时间。现在，输入 `Date` 并按 Enter。为什么你会收到错误信息？你能判断是哪个 shell 给你的这条信息吗？

+ 10. 切换到不同的命令行终端 (`tty3`) 到命令行终端 (`tty3`)，并使用用户名 `user1` 和密码 `LinuxRocks!` 登录终端。你收到了什么提示符？为什么？

### 项目 2-3

在这个动手项目中，你为 root 用户设置密码，探索 Linux 系统上的某些命令行终端，并在 BASH shell 中输入一些命令。

+ 1. 在 Linux 系统完成安装加载并完成欢迎向导后，你将处于一个图形终端 (`tty1`)。不要登录此图形终端，按 `Ctrl+Alt+F3` 切换到命令行终端 (`tty3`)，并使用用户名 `user1` 和密码 `LinuxRocks!` 登录终端。你收到了什么提示符？为什么？

+ 2. 在提示符处，输入 `sudo password root` 并按 Enter 设置 root 用户密码。在提示时，输入密码 `LinuxRocks!`, 然后两次输入所需的 root 密码 `LinuxRocks!` 来设置 root 用户密码。
