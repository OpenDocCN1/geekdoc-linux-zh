
仔细考虑为远程 SUSE Linux 安装选择的协议非常重要。许多组织使用网络防火墙和安全设备来保护网络免受未经授权的使用。因此，如今只有某些协议允许跨网络使用。

在本节中，你使用 `NFS` 执行了网络安装。使用 Internet 上的文档（`http://www.novell.com`）或你的 SUSE Linux 系统（`/usr/share/doc`）将你的计算机启用为 `FTP`、`HTTP` 或 `SMB/CIFS` 安装服务器，并从你的安装服务器执行另一次网络安装。

## Using Disk-Imaging Software to Deploy SUSE Linux

在本节中，你学习了如何使用 `AutoYaST` 和 SUSE Linux 安装程序自动化 SUSE Linux Enterprise Desktop 的安装。作为此方法的替代方案，许多大型组织使用磁盘映像软件创建已安装 SUSE Linux Enterprise Desktop 的硬盘的克隆副本。使用 Internet 研究可用于 SUSE Linux Enterprise Desktop 的磁盘映像实用程序及其功能。准备一份简短备忘录，比较磁盘映像与 `AutoYaST` 安装。如果可能，对你当前的 SUSE Linux 安装执行磁盘映像。

在本节中，您将找到重要命令、程序和目录的概述，以及列出 DOS/Windows 命令和对应的 Linux 命令的表格。

- 重要命令概述
- Windows—Linux：可比命令

## 重要命令概述

在本部分，列出了重要命令。有关单个命令的详细信息可以通过输入

```
man command
```

获得

命令按以下任务排序：

- 处理文件和目录
- 查找文件和文件内容
- 显示和修改文件内容
- 恢复数据、压缩和归档文件
- 管理用户和组
- 管理权限
- 管理系统
- 管理进程、启动和停止系统
- 监控系统
- 安装软件
- 管理硬盘和文件系统
- 自动化任务
- 修复系统
- 使用在线帮助
- 处理内核和模块
- 打印（CUPS）
- 管理 X Window 系统
- 处理 MS-DOS 软盘
- 使用网络
- 使用 vi

### 处理文件和目录

- `cd`—更改到另一个目录
- `cp`—复制文件
- `ln`—创建链接
- `ls`—列出目录的内容
- `mkdir`—创建一个或多个目录
- `mkfifo`—生成 FIFO 文件
- `mknod`—在目录 `/dev` 中设置新的设备文件
- `mv`—将文件移动到不同目录或重命名文件
- `rm`—删除一个或多个文件
- `rmdir`—删除一个或多个空目录
- `split`—将文件拆分为几个较小的文件
- `tee`—将输出分支到 stdout 并同时写入一个或多个文件
- `touch`—更改文件的时间戳或创建大小为 0 字节的新文件

### 查找文件和文件内容

- `file`—确定文件类型，例如文本文件或 HTML 文档
- `find`—搜索文件
- `grep`—在一个或多个文件中搜索字符串并显示匹配的行
- `locate`—在先前创建的数据库中搜索文件
- `updatedb`—更新 `locate` 的 `/var/lib/locatedb` 数据库
- `whereis`—定位命令的二进制、源代码和手册页文件
- `which`—显示（shell）命令的完整路径

### 显示和修改文件内容

- `cat`—在标准输出上显示文件的内容
- `cut`—从文件的所有行中剪切特定字段并显示所选区域
- `echo`—将给定字符串输出到标准输出
- `expand`—将制表符转换为空格
- `fmt`—是一个简单的文本格式化程序，按段落格式化文本文件或标准输入的内容
- `head`—向 stdout 显示文件的开头（默认 10 行）
- `less`—逐页向 stdout 显示文件，也可显示压缩文件的内容
- `more`—逐页向 stdout 显示文件。功能不如 `less` 多
- `sort`—按字段对文本文件的行进行字母排序。排序后的文件也可以合并为一个文件
- `strings`—显示文件中可打印字符的字符串。该命令主要用于确定二进制文件的内容
- `tac`—显示文件，从最后一个字段开始（`cat` 的反向）
- `tail`—向 stdout 显示文件的末尾（默认 10 行）
- `tr`—从标准输入替换或删除字符并写入标准输出
- `unexpand`—将空格转换为制表符
- `uniq`—从已排序的文件中删除重复行
- `wc`—显示字符、单词和行的数量

### 恢复数据、压缩和归档文件

- `ar`—创建、修改和从归档中提取
- `bunzip2`—解压缩用 `bzip2` 压缩的文件
- `bzip2`—压缩和解压缩文件
- `cpio`—将文件复制到归档和从归档复制（`cpio` 或 `tar` 归档）
- `dd`—在不同存储介质（软盘、硬盘等）之间传输数据块
- `dump`—创建 ext2 和 ext3 文件系统备份
- `gunzip`—解压缩用 `gzip` 压缩的文件
- `gzip`—压缩或解压缩文件
- `mt`—用于处理磁带
- `restore`—从用 `dump` 制作的备份中恢复文件或文件系统
- `rsync`—在不同主机上创建整个目录的副本或在本地镜像目录
- `sync`—将内存中缓冲的任何数据写入磁盘
- `tar`—生成或解包由多个文件和目录组成的归档
- `zcat`—在标准输出上显示用 `gzip` 压缩的文件的解压缩内容
- `zip`—打包和压缩（归档）文件

### 管理用户和组

- `chage`—列出并更改用户的密码过期信息
- `chfn`—更改 `/etc/passwd` 文件中 GECOS 字段中的用户信息
- `chsh`—更改用户的登录 shell
- `faillog`—显示格式化的 `/var/log/faillog` 文件
- `finger`—显示本地和远程系统用户的信息
- `gpasswd`—删除组密码（选项 `-r`）
- `groupadd`—创建新组
- `groupmod`—修改组
- `groups`—为用户提供其组成员身份的信息
- `id`—为用户提供其 UID 和其组成员身份的信息
- `last`—显示 `/var/log/wtmp` 文件的内容（最后登录的用户列表）
- `lastlog`—显示 `/var/log/lastlog` 文件的内容
- `newgrp`—更改用户的有效组 GID
- `passwd`—为用户分配密码或更改密码
- `pwck`—检查 `/etc/passwd` 和 `etc/shadow` 文件中数据完整性
- `sg`—更改用户的有效组 GID
- `su`—允许您更改为另一个用户的 UID
- `sudo`—允许普通用户执行 root 命令
- `useradd`—创建新用户
- `userdel`—删除用户
- `usermod`—更改用户账户
- `visudo`—用于修改 `/etc/sudoers` 文件
- `w`—显示当前在机器上的用户及其进程的信息
- `who`—显示当前登录到系统的人员以及上次登录时间等信息
- `whoami`—显示您当前在系统上以哪个用户登录

### 管理权限

- `chattr`—设置和删除 ext2 文件系统的文件属性；更改文件的版本号
- `chgrp`—更改文件的组归属
- `chmod`—更改文件的访问权限
- `chown`—更改文件的拥有者
- `lsattr`—显示 ext2 文件系统的文件属性和文件的版本号
- `umask`—对新创建的文件和目录的访问模式设置限制

### 管理系统

- `alias`—定义新的别名
- `clear`—删除屏幕或文本控制台的内容
- `date`—打印或设置系统日期和时间
- `ethtool`—显示或更改以太网卡设置
- `export`—将 shell 变量转换为环境变量。因此，它在子 shell 中也可用
- `fdformat`—对软盘进行低级格式化，然后可以在其上安装文件系统（使用 `mformat` 或 `mkfs`）
- `grub`—在系统运行时启动 GRUB shell；重新安装引导管理器 GRUB
- `grub-install`—安装引导管理器 GRUB
- `history`—列出最后执行的命令
- `ip`—显示和更改网络接口配置
- `iptables`—在 Linux 内核 2.4.0 或更新版本中设置、维护和检查 IP 数据包过滤规则表
- `lilo`—读取在 LILO 配置 `/etc/lilo.conf` 文件中进行的更改
- `pwd`—指定当前目录的路径
- `set`—显示 shell 已知的全部变量
- `SuSEconfig`—将 `/etc/sysconfig/` 目录中的文件更改传输到各个程序特定的配置文件
- `swapoff`—禁用用于分页和交换的设备和文件
- `swapon`—启用用于分页和交换的设备和文件
- `tune2fs`—调整 ext2 文件系统上的可调文件系统参数

### 管理进程，启动和停止系统

- `unalias`—移除别名
- `uname`—显示操作系统的名称（Linux）
- `unset`—删除 shell 变量
- `bg`—在后台继续中断的进程
- `chkconfig`—启用或禁用系统服务
- `fg`—将后台运行的进程移到前台
- `fuser`—显示使用指定文件或文件系统的进程的 PID
- `halt`—结束当前正在运行的所有进程（关机）
