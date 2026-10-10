
# 附录 A：Bash 命令快速指南

内置命令的性能高于外部命令，但添加到 shell 中的内置命令越多，其占用的内存就越多，其中可能包含你从未使用过的命令。Bash shell 还包含提供扩展功能的外部命令。这些将在下一节中讨论。

## 查看常见的 Bash 命令

除了内置命令外，Bash shell 还利用外部命令，使你可以操作文件系统以及管理文件和目录。表 A.2 展示了你在 Bash shell 中工作时希望使用的常见外部命令。

### 表 A.2 Bash Shell 外部命令

| 命令 | 描述 |
| :--- | :--- |
| at | 在设定的未来时间执行指定的脚本或命令。 |
| atq | 显示 at 实用程序队列中的作业。 |
| atrm | 从 at 实用程序队列中移除指定的作业。 |
| bash | 从标准输入或文件解释命令，或使用 Bourne Again Shell 命令语言启动子 shell。 |
| bc | 通过其编程语言执行计算。 |
| bzip2 | 使用 Burrows-Wheeler 块排序文本压缩算法和霍夫曼编码进行压缩。 |
| cat | 列出指定文件的内容。 |
| chage | 更改指定系统用户账户的密码过期日期。 |
| chfn | 更改指定用户账户的当前信息。 |
| chgrp | 更改指定文件或目录的默认组。 |
| chmod | 更改指定文件或目录的系统安全权限。 |
| chown | 更改指定文件或目录的默认所有者。 |
| chpasswd | 读取登录名和密码对的文件并更新密码。 |
| chsh | 更改指定用户账户的默认 shell。 |
| clear | 从终端模拟器或虚拟控制台终端中移除文本。 |
| compress | 原始 UNIX 文件压缩实用程序。 |
| coproc | 在后台模式生成子 shell 并执行指定命令。 |
| cp | 将指定文件复制到另一个位置。 |
| crontab | 如果允许，则启动用户 cron 表文件的编辑器。 |
| cut | 移除每个指定文件行中指定的部分。 |
| date | 以各种格式显示日期。 |
| df | 显示所有已挂载设备的当前磁盘空间统计信息。 |
| dialog | 在文本环境中创建窗口对话框。 |
| du | 显示指定文件路径的磁盘使用统计信息。 |
| emacs | 调用 Emacs 文本编辑器。 |
| env | 在修改后的环境中执行指定程序或显示所有环境变量的值。 |
| exit | 对当前进程执行正常终止。 |
| expr | 计算指定表达式。 |
| fdisk | 组织并创建指定磁盘的分区表。 |
| file | 显示指定文件的文件类型。 |
| find | 对文件执行递归搜索。 |
| free | 检查系统中可用和已使用的内存。 |
| fsck | 检查并可选地修复指定的文件系统。 |
| gawk | 使用编程语言命令进行流编辑。 |
| grep | 在文件中搜索指定的模式。 |
| gedit | 调用 GNOME 桌面编辑器。 |
| getopt | 解析命令选项，包括长选项。 |
| gdialog | 为 GNOME Shell 创建窗口对话框。 |
| groups | 显示指定用户的组成员资格。 |
| groupadd | 创建一个新的系统组。 |
| groupmod | 修改现有的系统组。 |
| gunzip | 调用 GNU 项目使用 Lempel-Ziv 压缩的解压功能。 |
| zcat | 调用 GNU 项目用于使用 Lempel-Ziv 压缩显示压缩文件内容的实用程序。 |
| gzip | 调用 GNU 项目使用 Lempel-Ziv 压缩的压缩功能。 |
| head | 显示指定文件内容的前部分。 |
| help | 显示 Bash 内置命令的帮助页面。 |
| kdialog | 为 KDE 创建窗口对话框。 |
| killall | 根据进程名向运行中的进程发送系统信号。 |
| kwrite | 调用 KWrite 文本编辑器。 |
| less | 启用高级文件内容查看功能。 |
| link | 使用别名创建到文件的链接。 |
| ln | 创建到指定文件的符号链接或硬链接。 |
| ls | 列出目录内容和/或文件信息。 |
| lvcreate | 创建逻辑卷管理器 (LVM) 卷。 |
| lvdisplay | 显示 LVM 卷。 |
| lvextend | 增加 LVM 卷的大小。 |
| lvreduce | 减小 LVM 卷的大小。 |
| mandb | 创建允许 man 页关键字搜索的数据库。 |
| man | 显示指定命令或主题的 man 页面。 |
| mkdir | 创建指定的目录。 |
| mkfs | 使用指定的文件系统格式化分区。 |
| mktemp | 创建临时文件或目录。 |
| more | 列出指定文件的内容，并在每个屏幕数据后暂停。 |
| mount | 显示或挂载磁盘设备到虚拟文件系统。 |
| mv | 重命名文件或目录。 |
| nano | 调用 nano 文本编辑器。 |
| nice | 使用系统中不同的优先级级别运行命令。 |
| nohup | 忽略 **SIGHUP** 信号执行指定命令。 |
| passwd | 更改系统用户账户的密码。 |
| printenv | 显示指定环境变量的值或显示所有环境变量的值。 |
| ps | 显示关于系统中运行进程的信息。 |
| pvcreate | 创建物理 LVM 卷。 |
| pvdisplay | 显示物理 LVM 卷。 |
| pwd | 显示当前工作目录。 |
| renice | 更改系统中运行应用程序的优先级。 |
| rm | 删除指定的文件或目录。 |
| rmdir | 删除指定的空目录。 |
| sed | 使用编辑器命令进行流线编辑。 |
| setterm | 修改终端设置。 |
| sleep | 暂停 Bash shell 操作指定的一段时间。 |
| sort | 根据指定顺序组织数据文件中的数据。 |
| stat | 查看指定文件的文件统计信息。 |
| sudo | 以 root 用户账户身份运行应用程序。 |
| tail | 显示指定文件内容的最后部分。 |
| tar | 将数据和目录归档到单个文件中。 |
| tee | 将信息同时发送到 STDOUT 和 STDIN。 |
| top | 显示活动进程，显示关键系统统计信息。 |
| touch | 创建新的空文件或更新现有文件的时间戳。 |
| umount | 从虚拟文件系统中卸载已挂载的磁盘设备。 |
| uptime | 显示系统运行了多久的信息。 |
| useradd | 创建新的系统用户账户。 |
| userdel | 移除现有的系统用户账户。 |
| usermod | 修改现有的系统用户账户。 |
| vgchange | 激活或停用 LVM 卷组。 |
| vgcreate | 创建 LVM 卷组。 |
| vgdisplay | 显示 LVM 卷组。 |
| vgextend | 增加 LVM 卷组的大小。 |
| vgreduce | 减小 LVM 卷组的大小。 |
| vgremove | 删除 LVM 卷组。 |
| vi | 调用 vim 文本编辑器。 |
| vim | 调用 vim 文本编辑器。 |
| vmstat | 生成关于系统内存和 CPU 使用情况的详细报告。 |
| wc | 显示文本文件统计信息。 |
| whereis | 显示指定命令的文件，包括二进制文件、源代码和 man 页面。 |
| which | 查找可执行文件的位置。 |
| who | 显示当前登录到系统的用户。 |
| whoami | 显示当前用户的用户名。 |
| xargs | 从 STDIN 获取项目，构建命令并执行这些命令。 |
| xterm | 调用 xterm 终端模拟器。 |
| zenity | 为 GNOME Shell 创建窗口小部件。 |
| zip | 调用 Windows PKZIP 程序的 UNIX 版本。 |

