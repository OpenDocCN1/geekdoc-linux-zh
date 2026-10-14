

## 管理进程，启动和停止系统

- unalias—移除别名
- uname—显示操作系统的名称（Linux）
- unset—删除 shell 变量
- bg—在后台继续中断的进程
- chkconfig—启用或禁用系统服务
- fg—将后台运行的进程移到前台
- fuser—显示使用指定文件或文件系统的进程的 PID
- halt—结束当前正在运行的所有进程（关机）
- init—允许切换到另一个运行级别或重新加载 /etc/inittab 文件而不改变运行级别
- insserv—在 /etc/init.d/rcrunlevel.d 目录中创建符号链接
- jobs—列出从 shell 启动并在后台运行的所有进程
- kill—向进程传递信号（指定 PID）
- killall—向进程传递信号（指定进程的命令名）
- lsof—列出打开的文件
- netstat—显示哪些网络端口提供服务以及建立了哪些连接
- nice—在进程启动时设置其 nice 值
- nohup—启动一个进程或程序，该进程或程序在注销后继续运行
- poweroff—确保立即、受控的系统关机
- ps—列出进程
- pstree—以进程树的形式显示当前正在运行的进程
- reboot—结束所有正在运行的进程然后重新启动计算机
- renice—更改正在运行进程的 nice 值（需要 PID）
- shutdown—关闭 Linux 系统
- top—根据计算机使用时间列出进程

## 监控系统

- df—指定硬盘及其分区或其他驱动器在文件系统中的挂载位置，以及它们占用的空间
- dmesg—显示内核环形缓冲区的內容
- du—提供文件和目录占用的空间信息
- hdparm—让您查看有关硬盘的信息并管理某些硬盘参数
- hwinfo—生成并显示有关安装在 Linux 系统上的设备的特定信息的列表
- iostat—显示设备和分区的 CPU 和输入/输出（I/O）统计信息
- logrotate—监控日志文件的大小和年龄
- lspci—显示 Linux 系统中所有 PCI 总线及其连接的所有设备的信息
- rpcinfo—显示有关 portmapper 的信息
- showmount—显示 NFS 服务器上导出的目录的信息
- siga—收集有关系统的各种信息并以 HTML 或 ASCII 格式输出
- uptime—显示当前时间、系统运行时间、系统上的用户数量以及过去 1、5 和 15 分钟内运行队列中作业的平均数量

## 安装软件

- configure—创建并自定义 makefile
- ldconfig—更新 /etc/ld.so.cache 文件
- ldd—提供程序所需的库的信息、它们的位置以及缺少的库
- make—编译程序
- rpm—以 RPM Package Manager 格式管理软件包
- rpmbuild—构建 RPM Packet Manager 软件包

## 管理硬盘和文件系统

- fdisk—分区硬盘
- mke2fs—创建 ext2 或 ext3 文件系统
- mkfs—在存储介质上创建文件系统
- mkreiserfs—创建 Reiser 文件系统格式的文件系统
- mount—将设备文件挂载到文件系统
- reiserfstune—调整 Reiser 文件系统上的可调文件系统参数
- resize_reiserfs—缩小或扩大 Reiser 文件系统
- resize2fs—缩小或扩大 ext2 或 ext3 文件系统
- tune2fs—调整 ext2 和 ext3 文件系统上的可调文件系统参数
- umount—从文件系统移除设备文件

## 自动化任务

- `at`—在指定时间执行命令
- `atq`—列出 at 作业
- `atrm`—删除 at 作业，以作业编号标识
- `crontab`—维护单个用户的 crontab 文件

## 修复系统

- `badblocks`—在分区上搜索坏块
- `chroot`—创建新的根目录
- `debugfs`—是 ext2 文件系统调试器
- `debugreiserfs`—是 Reiser 文件系统的调试工具
- `dumpe2fs`—提供有关文件系统状态的信息
- `e2fsck`—检查并修复 ext2 或 ext3 文件系统
- `fsck`—检查文件系统的一致性并在必要时进行修复
- `reiserfsck`—检查并修复 Reiser 文件系统

## 使用在线帮助

- `apropos`—搜索手册页的名称和描述
- `info`—以相同名称启动在线帮助系统
- `man`—显示给定命令的在线信息
- `whatis`—显示手册页描述

## 与内核和模块协作

- `partprobe`—使内核使用新的分区表
- `depmod`—生成各个模块的依赖关系
- `insmod`—将模块加载到内核
- `lsmod`—列出内核模块
- `modinfo`—显示有关内核模块的信息
- `modprobe`—将模块加载到内核，同时考虑模块依赖关系
- `rmmod`—从内核中移除模块

## 打印（CUPS）

- `accept`—在用 reject 设置为拒绝打印作业后，将队列设置为接受打印作业
- `cancel`—从队列中移除打印作业
- `disable`—停止队列
- enable—启用已禁用的队列
- lp—发送打印作业
- lpadmin—管理打印队列
- lpoptions—配置打印队列
- lpq—显示打印作业
- lpr—发送打印作业
- lprm—从队列中移除打印作业
- lpstat—显示打印作业
- mpage—将 ASCII 转换为 PostScript 并启用在一张纸上打印多页
- pr—格式化文本文件以便打印并使用页眉（日期、时间、文件名、页数）打印页面
- reject—将队列设置为拒绝打印作业

## 管理 X Window 系统

- sax2—配置 X 服务器
- startx—启动 X 服务器（从图形环境注销以再次停止 X 服务器）
- xinit—启动 X 服务器
- xvidtune—配置屏幕尺寸（宽度、高度）

## 与 MS-DOS 软盘协作

- mcd—更改到 MS-DOS 软盘上的目录
- mcopy—从 MS-DOS 软盘复制文件或向 MS-DOS 软盘复制文件
- mdel—删除 MS-DOS 软盘上的文件
- mdir—显示 MS-DOS 软盘的内容
- mformat—以 MS-DOS 格式格式化软盘
- mlabel—显示 MS-DOS 软盘的名称并提供更改名称的选项
- mmd—在 MS-DOS 软盘上创建新目录
- mmove—将 MS-DOS 软盘上的文件移动到另一个目录，或重命名 MS-DOS 软盘上的文件或目录
- mrd—从 MS-DOS 软盘删除空目录
- mren—将 MS-DOS 软盘上的文件移动到另一个目录或重命名 MS-DOS 软盘上的文件或目录
- mtype—在屏幕上显示 MS-DOS 软盘的文本文件（参见 cat）

## 使用网络

- ping—检查两台主机之间的网络连接
- scp—使用 SSH 在两台计算机之间安全复制文件
- sftp—是交互式文件传输程序，类似于 FTP
- ssh—连接到远程机器并登录
- ssh-add—将 RSA 或 DSA 身份添加到身份验证代理（ssh-agent）
- ssh-agent—保存用于公钥身份验证的私钥（RSA、DSA）
- ssh-copy-id—将您的 identity.pub 安装到远程机器的 authorized_keys 中
- ssh-keygen—生成、管理和交谈身份验证密钥
- ssh-keyscan—收集 SSH 公钥
- nmblookup—用于 NetBIOS 名称解析和测试
- smbclient—提供对 SMB 文件和打印服务的访问

## 使用 vi

- ESC—返回到普通模式

## 普通模式

- i—切换到插入模式以便插入文本
- dd—复制行。10dd 复制 10 行
- p—在光标下方或之后插入复制的文本
- v—允许您使用上、下、左、右箭头键选择文本
- y—复制突出显示的文本，或如果未突出显示文本，则复制光标所在的行
- /searchterm—搜索文本中的 searchterm；使用 n 跳转到 searchterm 的下一个出现位置
- ZZ—保存并退出

## 命令行模式

- :w—将文件写入磁盘
- :w filename—将文件写入 filename；您继续编辑原始文件，而不是 filename
- :e filename—打开 filename 进行编辑
- :syntax on—打开语法高亮
- :q—退出 vi
- :wq—保存更改后退出 vi
- :q!—丢弃更改后退出 vi
- :x—保存并退出

