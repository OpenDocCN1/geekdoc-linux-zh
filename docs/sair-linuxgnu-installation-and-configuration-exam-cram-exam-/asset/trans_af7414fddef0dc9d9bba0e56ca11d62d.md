
## nroff

nroff 是一个 Linux 格式化工具，其中命令嵌入在文本文件中。Linux 手册（man）页面就是用此工具创建的。

## of

输出过滤器。与 /etc/printcap 打印机配置文件相关。指定在一系列打印作业中第一个使用的过滤器。

## open source

一种发布软件的方法和许可。开源软件可自由重新分发并包含源代码。对开源软件的修改必须通过“补丁”进行，以保持原始软件的完整性。开源许可不针对任何特定产品。

## Open Source Initiative (OSI)

一个由 Eric Raymond 于 1998 年发起的团体，用以捍卫“自由软件”。OSI 有自己的许可，其限制比 GPL 稍微宽松。另见 open source。

## other

在 /etc/lilo.conf 文件中发现的一个参数，指定非 Linux 操作系统。

## partition

硬盘的逻辑分区。

## password

用于特定用户名的字母和数字组合。强烈建议使用数字和大小写字母组合的密码。

## PATH

Linux 变量，指定 Linux 自动查找命令的目录。如果某个目录不在你的 $PATH 变量中，你需要指定绝对路径才能运行该目录中的程序或脚本。

## PCI

外围组件互连。可安装在计算机内部的外设标准。

## PCL

参见 Printer Control Language。

## pico

Pine 编辑器。Linux 的文本编辑器。

## PID

进程标识符。如果要终止一个程序，需要其 PID。你可以用适当的 ps 命令找到 PID。

## pine

互联网新闻和邮件程序。由华盛顿大学开发的 Linux 邮件阅读器。

## pipe

Linux 命令构造，使用 |，其中一个命令的标准输出被定向为第二个命令的标准输入。

## Plug-and-Play

计算机 BIOS 和/或操作系统能够自动分配或配置与各种组件和外设的通信通道。

## PostScript

Adobe 为与打印机通信而开发的打印机语言。

## primary partition

可包含主引导记录的分区。你可以设置 Linux 目录挂载到主分区上。每个硬盘最多可配置四个主分区。

## Printer Control Language (PCL)

Hewlett Packard 为与打印机通信而开发的语言。

## printtool

Red Hat 的打印机配置实用程序。

## private IP addresses

不能在互联网上分配的 IP 地址范围。私有 IP 地址用于连接到互联网的私有局域网。

## ps

进程状态命令，显示当前正在运行的程序和实用程序。诸如 ps aux 之类的命令会返回 Linux 计算机上当前运行的所有程序和守护进程。它还会输出 PID，你可以用它来识别和终止选择的程序。

## pseudoterminal

可通过网络连接从远程计算机访问的虚拟控制台。

## pwd

返回当前工作目录的 Linux 命令。

## RAM

随机存取存储器。计算机内部的主存储器。

## rawrite

基于 MS-DOS 的 Linux 实用程序。rawrite 实用程序主要用于将 Linux 映像（如 boot.img）中的文件解包到软盘上。

## Raymond, Eric

开放源代码倡议的创始人，该组织是开源许可背后的团体。

## rc.d

包含在不同运行级别加载的各种文件和脚本的目录。这些脚本通常按运行级别划分，并链接到 init.d 目录中的实际脚本。

## read error

与不良介质相关的错误，例如有缺陷的软盘。

## reboot

reboot 命令在重启计算机之前停止当前程序。通常与运行级别 6 相关联。运行 reboot 命令时，Linux 会在重新启动计算机之前初始化 halt 运行级别（0）。

## Red Hat

也许是最广为人知的 Linux 发行版。

## refresh rate

每秒向显示器重新发送信息的次数。

## relative path

相对于当前工作目录的 Linux 文件或目录的路径。

## renice

允许你提高或降低当前正在运行程序相关优先级的命令。

## rescue disk

磁盘，通常是 1.44MB 软盘，可用于将计算机启动到 Linux。常在 LILO 或主引导记录出现问题时使用。

## restoreb.exe

可用于从存储在 rootboot.00x 文件（x 通常为 0 到 9 之间的数字）中的备份恢复主引导记录的实用程序。

## rm

删除文件的 Linux remove 命令。根据使用的开关，此命令还可以删除目录。在 /etc/printcap 打印机配置文件中，rm 是一个参数，指定具有远程打印机的计算机的主机名或 IP 地址。

## rmdir

删除目录命令。如果要删除的目录不为空，此命令不起作用。

## rmmod

移除当前加载在系统上的驱动程序的命令。

## rootboot.00x

主引导记录（MBR）的备份文件，其中 x 为 0 到 9 之间的数字。你可以设置 fips 从 MBR 的信息创建此文件。如果出于任何原因需要恢复 MBR，则可以使用 restoreb.exe 命令。

## run level

在 /etc/inittab 文件中定义的参数，定义不同的进程和守护进程。不同的运行级别与 Linux 中的不同条件相关联，例如单用户或多用户模式。

## Samba

允许运行 Linux 的计算机与运行 Microsoft Windows 的计算机通信的网络程序。

## Sax

S.u.S.E. 的 GUI 配置工具。

## ScanDisk

用于检查硬盘错误的 Microsoft Windows 实用程序。

## SCSI

小型计算机系统接口。用于磁盘驱动器和其他外设的一种连接器。

## sd

Spool 目录。指定打印机处理前的 spool 文件位置。与 /etc/printcap 打印机配置文件相关。

## sendmail

基于 Linux 的邮件传输代理，允许你设置邮件服务器。

## setleds

为不同虚拟终端设置键盘默认值（如 Num Lock）的命令。

## shadow

/etc/shadow 文件是加密的密码文件。

## shell

命令解释器。最常见的 Linux shell 称为 *bash*，它是从原始 Unix Bourne shell 开发而来的。

## shell variable

可能随 shell 而变化的变量。

## shutdown

关闭 Linux 的命令。根据使用的开关，此命令可以停止或重启计算机。

## single sequential user system

仅允许一次一个用户登录的操作系统。系统仅限于单个终端。

## single user

仅允许一个用户在 Linux 中运行程序的运行级别。通常与运行级别 1 或 S 相关联。如果启动到单用户模式，则无需登录，并且具有 root 权限。

## Slackware

具有 ZipSlack 包选项用于 Zip 驱动器的 Linux 发行版。

## srm.conf

定义浏览你网站的人使用的子目录的 Apache 配置文件。

## Stallman, Richard

自由软件基金会和 GNU 通用公共许可证（也称为 *copyleft*）的创始人。

## Stampede

专注于易用性和最新处理器硬件的 Linux 发行版。

## Star Office

Sun Microsystems 拥有的办公软件套件。可免费下载用于 Linux。

## startx

启动 Linux 图形用户界面（GUI）的命令；也称为 *X Window*。

## stderr

标准错误，通常输出到显示器。

## stdin

标准输入，通常来自键盘。

## stdout

标准输出，通常输出到显示器。

## stty

标准 Linux 终端线路设置。

## subnet mask

参见 network mask。

## sudo

参见 superuser。

## SuperProbe

检测视频控制器关键部件的命令。

## superuser

当普通用户想要在 Linux 计算机上获得 root 权限时，他或她可以用 root 用户密码登录为 superuser。也称为 *sudo*。
