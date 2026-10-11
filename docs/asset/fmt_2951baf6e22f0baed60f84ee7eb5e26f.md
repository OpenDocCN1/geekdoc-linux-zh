
### 6.65.3. Util-linux 包含内容

- 安装的程序：`addpart`, `aget`, `biskard`, `blkid`, `blockdev`, `cal`, `cfdisk`, `chcpu`, `chrt`, `col`, `colert`, `colm`, `column`, `crtalldel`, `delpart`, `dmesg`, `fstrim`, `fallocate`, `fdisk`, `finds`, `findmd`, `flock`, `fsk`, `fsk.cramfs`, `mkfs`, `mkfs.minix`, `mkswap`, `mount`, `mountpoint`, `name`, `parts`, `script`, `pivot_root`, `prlimit`, `profile`, `rename`, `resize`, `reswarp`, `rtwck`, `retretay`, `setsid`, `setter`, `sfdisk`, `ulogin`, `swagen`, `swappart`（链接到 `swap`）, `switch`, `switch_root`, `tailset`, `ul`, `umount`, `uname`, `unshare`, `utmpdd`, `uidd`, `ualigen`, `wall`, `wetird`, `weipes`, `x86`, `x64`
- 安装的库：`libblkid.so`, `libdisk.so`, `libmount.so`, `libsmartcols.so`, `libuuid`
- 安装的目录：`/usr/include`, `/usr/share/doc/util-linux-2.29.1`, `/var/lib/hwclock`

## 简述

- `addpart` 通知内核有新分区
- `agety` 打开 tty 端口，提示登录名，然后调用登录程序
- `biskard` 丢弃设备上的扇区
- `blkid` 用于定位和打印块设备属性的命令行工具
- `blockdev` 允许从命令行调用块设备 ioctls
- `cal` 显示简单的日历
- `cfdisk` 操作给定设备的分区表
- `chcpu` 修改 CPU 状态
- `chrt` 修改进程的实时属性
- `col` 过滤掉重复换行符
- `colert` 为缺少某些功能（如叠加和半行）的终端过滤输出
- `colm` 过滤掉指定的列
- `column` 将文件格式化为多列
- `crtalldel` 将 Ctrl+Alt+Del 键组合设置为硬重启或软重置
- `delpart` 请求内核删除分区
- `dmesg` 倾储内核启动消息
- `fstrim` 整理磁盘空间
- `fallocate` 分配文件空间
- `fdisk` 分区工具
- `finds` 查找节点
- `findmd` 查找挂点
- `flock` 锁
- `fsk` 检查文件系统
- `fsk.cramfs` 检查 cramfs 文件系统
- `mkfs` 创建文件系统
- `mkfs.minix` 创建 minix 文件系统
- `mkswap` 创建交换空间
- `mount` 挂载
- `mountpoint` 检查挂载点
- `name` 命名
- `parts` 查看分区信息
- `script` 脚本工具
- `pivot_root` 切换根目录
- `prlimit` 进程资源限制
- `profile` 进程配置文件
- `rename` 重命名
- `resize` 调整大小
- `reswarp` 调整重写
- `rtwck` 检查
- `retretay` 返回
- `setsid` 设置会话 ID
- `setter` 设置器
- `sfdisk` 磁盘分区工具
- `ulogin` 用户登录
- `swagen` 交换
- `swappart`（链接到 `swap`）
- `switch` 切换
- `switch_root` 切换根目录
- `tailset` 跟踪集
- `ul` 用户工具
- `umount` 卸载
- `uname` 输出内核信息
- `unshare` 共享命名空间
- `utmpdd` 登录记录
- `uidd` 唯一 ID
- `ualigen` 生成 ID
- `wall` 广播消息
- `wetird` 写入擦写
- `weipes` 擦除
- `x86` x86 架构
- `x64` 64 位架构

# 从零构建 Linux (Linux) - 版本 8.0

- `fallocate`
为文件预分配空间

- `fdformat`
低级格式化软磁盘

- `fdisk`
操作给定设备的分区表

- `findfs`
通过标签 (`label`) 或全局唯一标识符 (`UUID`) 查找文件系统

- `findmtnt`
是 `libmount` 的命令行接口，包含 `mountinfo`、`fstab` 和 `mtab` 文件的处理

- `flock`
获取文件锁并在持有锁的情况下执行命令

- `fsck`
用于检查并（可选）修复文件系统

- `fsck.cranfs`
对给定设备上的 Cramfs 文件系统进行一致性检查

- `fsck.minix`
是 MIFFREEZE/FITHAW ioctl 内核驱动操作的非常简单的封装器

- `fsfreez`
丢弃已挂载文件系统中未使用的块

- `getopt`
解析给定命令行中的选项

- `hexdump`
以十六进制或其他格式转储文件系统

- `hwclock`
读取或设置系统硬件时钟，也称为实时时钟 (`RTC`) 或基本输入输出系统 (`BIOS`) 时钟

- `i386`
指向 `setarch` 的符号链接

- `ionice`
获取或设置程序的调度类和优先级

- `ipcmk`
创建 IPC 资源

- `ipcrm`
删除给定的进程间通信 (`IPC`) 资源

- `ipcs`
提供 iso9660 文件系统的大小

- `isize`
报告 iso9660 文件系统的大小

- `kill`
向进程发送信号

- `last`
显示哪些用户已登录（登录和登出），回溯搜索 `/var/log/wtmp` 文件；它显示了系统启动、关机和运行级别的更改

- `lastb`
显示记录在 `/var/log/btmp` 中的失败登录尝试

- `ldattach`
在串行线上附加行规律 (`line discipline`)

- `linux32`
指向 `setarch` 的符号链接

- `linux64`
指向 `setarch` 的符号链接

- `logger`
将给定消息输入系统日志。显示以给定字符串开头的行

- `look`
显示以给定字符串开头的行

- `losesetup`
设置并控制循环设备

- `lsblk`
以树状格式列出所有或选定块设备的信息

- `cpu`
打印 CPU 架构信息

- `lsipc`
打印系统当前使用的 IPC 设施信息

- `islocks`
列出本地系统锁

- `lslogins`
列出用户、组和系统账户的信息

- `cookie` | 为 `xauth` 生成魔法 쿠기（128 位随机十六进制数）

- `mesg` | 控制其他用户是否可以向当前用户的终端发送消息

- `mkfs` | 在设备上（通常是硬盘分区）上构建文件系统

- `mkfs.bfs` | 创建 Santa Cruz Operations (SCO) bfs 文件系统

- `mkfs.ramfs` | 创建 cramfs 文件系统

- `mkfs.minix` | 创建 Minix 文件系统

- `mkswap` | 初始化给定的设备或文件以作为交换区域 (`swap area`)

- `more` | 一页一页翻页文本的过滤器

- `mount` | 将给定设备上的文件系统挂载到文件系统树中的指定目录

- `mountpoint` | 检查目录是否为挂载点

- `namei` | 显示给定路径中的符号链接

- `nsenter` | 使用其他进程的命名空间运行程序

- `partx` | 告知内核磁盘上分区的存在和数量

- `pg` | 一页一页显示文本文件

- `pivot_root` | 将给定的文件系统设置为当前进程的新根文件系统

- `prlimit` | 获取并设置进程资源限制

- `raw` | 将原始字符设备绑定到块设备

- `readfile` | 读取内核分析信息

- `rename` | 重命名给定文件，用一个字符串替换为另一个

- `renice` | 更改运行进程的优先级

- `resizepart` | 请求内核调整分区大小

- `rev` | 反转给定文件的行

- `rwake` | 用于进入系统睡眠状态，直到指定的唤醒时间

- `script` | 创建终端会话类型

- `scriptreplay` | 使用计时信息回放脚本

- `setarch` | 在新的程序环境中更改报告的架构并设置特性标志

- `setid` | 在新会话中运行给定程序

- `seterm` | 设置终端属性

- `sfdisk` | 磁盘分区器

- `sologin` | 允许 root 登录；通常系统进入单用户模式时由 `init` 调用

- `swapable` | 允许更改交换区的 UUID 和标签

- `swapoff` | 禁用分页和交换的设备和文件，并列出当前使用的设备和文件

- `swapon` | 切换到另一个文件系统作为挂载树的根

- `tail` | 跟踪日志文件的增长；显示日志文件的最后 10 行，然后在日志文件创建新条目时继续显示

- `taskset`
检索或设置进程的 CPU 亲和性

- `ul`
将下划线转换为指示中使用终端下划线序列的过滤器

- `umount`
从系统文件树中断开文件系统

- `uname26`
指向 `setarch` 的符号链接

- `unshare` | 在某些命名空间与父进程分离的情况下运行程序

- `utmpdump`
以用户友好的格式显示 uuid 登录文件的内容

- `uuididd`
UUID 库使用的守护进程，以安全且保证唯一的方式生成基于时间的 UUID

- `uuidigen`
创建新的 UUID。每个新 UUID 在本地系统和其他系统上创建的所有 UUID 之间都可以被认为是唯一的

- `wall` | 显示所有当前登录终端的文件内容或其标准输入，在过去和未来

- `wdctl`
显示看门狗状态

- `whereis`
报告给定命令的位置、源和 man 页

- `wipefs`
擦除设备上的文件系统签名

- `x86_64`
指向 `setarch` 的符号链接

- `zramctl`
设置并控制 `zram`（内存磁盘）设备的程序

- `libblkid`
包含设备识别例程

- `libdisk`
包含操作分区表的例程

- `libmount`
包含块设备挂载和卸载的例程

- `libsmartcols`
包含表格形式输出的例程

- `libuuid`
包含生成超出本地系统的唯一标识符的例程

# 6.7. Man-DB

- `fsck.cranfs`
对给定设备上的 Cramfs 文件系统进行一致性检查

- `fsck.minix`
是 MIFFREEZE/FITHAW ioctl 内核驱动操作的非常简单的封装器

- `fsfreez`
丢弃已挂载文件系统中未使用的块

- `getopt`
解析给定命令行中的选项

- `hexdump`
以十六进制或其他格式转储文件系统

- `hwclock`
读取或设置硬件时钟，也称为实时时钟 (`RTC`) 或基本输入输出系统 (`BIOS`) 时钟

- `i386`
指向 `setarch` 的符号链接

- `ionice`
获取或设置程序的调度类和优先级

- `ipcmk`
创建 IPC 资源

- `ipcrm`
删除给定的进程间通信 (`IPC`) 资源

- `ipcs`
提供 iso9660 文件系统的大小

- `isize`
报告 iso9660 文件系统的大小

- `kill`
向进程发送信号

- `last`
显示哪些用户已登录（登录和登出），回溯搜索 `/var/log/wtmp` 文件；它显示了系统启动、关机和运行级别的更改

- `lastb`
显示记录在 `/var/log/btmp` 中的失败登录尝试

- `ldattach`
在串行线上附加行规律

- `linux32`
指向 `setarch` 的符号链接

- `linux64`
指向 `setarch` 的符号链接

- `logger`
将给定消息输入系统日志。显示以给定字符串开头的行

- `look`
显示以给定字符串开头的行

- `losesetup`
设置并控制循环设备

- `lsblk`
以树状格式列出所有或选定块设备的信息

- `iscpu`
打印 CPU 架构信息

- `lsipc`
打印系统当前使用的 IPC 设施信息

- `islocks`
列出本地系统锁

- `lslogins`
列出用户、组和系统账户的信息

- `cookie` | 为 `xauth` 生成魔法 쿠기（128 位随机十六进制数）

- `mesg` | 控制其他用户是否可以向当前用户的终端发送消息

- `mkfs` | 在设备上（通常是硬盘分区）上构建文件系统

- `mkfs.bfs` | 创建 Santa Cruz Operations (SCO) bfs 文件系统

- `mkfs.ramfs` | 创建 cramfs 文件系统

- `mkfs.minix` | 创建 Minix 文件系统

- `mkswap` | 初始化给定的设备或文件以作为交换区域

- `more` | 一页一页翻页文本的过滤器

- `mount` | 将给定设备上的文件系统挂载到文件系统树中的指定目录

- `mountpoint` | 检查目录是否为挂载点

- `namei` | 显示给定路径中的符号链接

- `nsenter` | 使用其他进程的命名空间运行程序

- `partx` | 告知内核磁盘上分区的存在和数量

- `pg` | 一页一页显示文本文件

- `pivot_root` | 将给定的文件系统设置为当前进程的新根文件系统

- `prlimit` | 获取并设置进程资源限制

- `raw` | 将原始字符设备绑定到块设备

- `readfile` | 读取内核分析信息

- `rename` | 重命名给定文件，用一个字符串替换为另一个

- `renice` | 更改运行进程的优先级

- `resizepart` | 请求内核调整分区大小

- `rev` | 反转给定文件的行

- `rwake` | 用于进入系统睡眠状态，直到指定的唤醒时间

- `script` | 创建终端会话类型

- `scriptreplay` | 使用计时信息回放脚本

- `setarch` | 在新的程序环境中更改报告的架构并设置特性标志

- `setid` | 在新会话中运行给定程序

- `seterm` | 设置终端属性

- `sfdisk` | 磁盘分区器

- `sologin` | 允许 root 登录；通常系统进入单用户模式时由 `init` 调用

- `swapable` | 允许更改交换区的 UUID 和标签

- `swapoff` | 禁用分页和交换的设备和文件，并列出当前使用的设备和文件

- `swapon` | 切换到另一个文件系统作为挂载树的根

- `tail` | 跟踪日志文件的增长；显示日志文件的最后 10 行，然后在日志文件创建新条目时继续显示

- `taskset`
检索或设置进程的 CPU 亲和性

- `ul`
将下划线转换为指示中使用终端下划线序列的过滤器

- `umount`
从系统文件树中断开文件系统

- `uname26`
指向 `setarch` 的符号链接

- `unshare` | 在某些命名空间与父进程分离的情况下运行程序

- `utmpdump`
以用户友好的格式显示 uuid 登录文件的内容

- `uuididd`
UUID 库使用的守护进程，以安全且保证唯一的方式生成基于时间的 UUID

- `uuidigen`
创建新的 UUID。每个新 UUID 在本地系统和其他系统上创建的所有 UUID 之间都可以被认为是唯一的

- `wall` | 显示所有当前登录终端的文件内容或其标准输入，在过去和未来

- `wdctl`
显示看门狗状态

- `whereis`
报告给定命令的位置、源和 man 页

- `wipefs`
擦除设备上的文件系统签名

- `x86_64`
指向 `setarch` 的符号链接

- `zramctl`
设置并控制 `zram`（内存磁盘）设备的程序

- `libblkid`
包含设备识别例程

- `libdisk`
包含操作分区表的例程

- `libmount`
包含块设备挂载和卸载的例程

- `libsmartcols`
包含表格形式输出的例程

- `libuuid`
包含生成超出本地系统的唯一标识符的例程

# 6.7. Man-DB

| Language (code) | Encoding | Language (code) | Encoding |
| --- | --- | --- | --- |
| Danish (da) | ISO-8859-1 | Croatian (hr) | ISO-8859-2 |
| German (de) | ISO-8859-1 | Hungarian (hu) | ISO-8859-2 |
| English (en) | ISO-8859-1 | Japanese (ja) | EUC-JP |
| Spanish (es) | ISO-8859-1 | Korean (ko) | EUC-KR |
| Estonian (et) | ISO-8859-1 | Lithuanian (lt) | ISO-8859 |
| Finnish (fi) | ISO-8859-1 | Latvian (lv) | ISO-8859-1 |
| French (fr) | ISO-8859-1 | Macedonian (mk) | ISO-8859-5 |
| Irish (ga) | ISO-8859-1 | Polish (pl) | ISO-8859-2 |
| Galician (gl) | ISO-8859-1 | Romanian (ro) | ISO-8859-2 |
| Indonesian (id) | ISO-8859-1 | Russian (ru) | KOI8-R |
| Icelandic (is) | ISO-8859-1 | Slovak (sk) | ISO-8859-2 |
| Italian (it) | ISO-8859-1 | Slovenian (sl) | ISO-8859-2 |
| Norwegian Bokmål (nb) | ISO-8859-1 | Serbian Latin (sr@cat) | ISO-8859-2 |
| Norwegian Nynorsk (nn) | ISO-8859-1 | Serbian (sr) | ISO-8859-5 |
| Norwegian (no) | ISO-8859-1 | Turkish (tr) | ISO-8859-9 |
| Portuguese (pt) | ISO-8859-1 | Ukrainian (uk) | KOI8-U |
| Swedish (sw) | ISO-8859-1 | Vietnamese (vi) | TCVN5712-1 |
| Belarus (be) | CP1251 | Simplified Chinese (zh_CN) | GBK |
| Bulgarian (bg) | CP1251 | Simplified Chinese, Singapore (zh_SG) | |
| Czech (cs) | ISO-8859-2 | Traditional Chinese, Hong Kong (zh_HK) | BIG5HKSCS |
| Greek (el) | ISO-8859-7 | Traditional Chinese (zh_TW) | BIG5 |

## 简述

`accessdb` 以人类可读的形式导出 `whatis` 数据库的内容

`apropos` 搜索 `whatis` 数据库并显示包含给定字符串的系统命令的短描述

`catman` 创建或更新预格式化的帮助页

`lexgrog` 显示给定帮助页的单行摘要信息

`man` 格式化并显示所请求的帮助页

`mandb` 创建或更新 `whatis` 数据库

`manpath` 显示 `$MANPATH` 的内容，或者（如果未设置 `$MANPATH`）显示基于 `man.conf` 设置和用户环境的合适搜索路径

`whatis` 搜索 `whatis` 数据库并显示包含给定关键词（作为独立单词）的系统命令的短描述

`libman` 包含 `man` 的运行时支持

`libmandb` 包含 `man` 的运行时支持

# 68. Tar-1.29

Tar 软件包包含一个归档程序。
预计编译时间：3.2 SBU
所需磁盘空间：40 MB

## 6.68.1. 安装 Tar

为编译准备 Tar：

```
