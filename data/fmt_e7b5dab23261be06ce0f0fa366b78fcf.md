
- `uidduid` 显示用户 ID
- `uidparse` 解析 UID
- `wall` 向所有用户发送消息
- `wipes` 擦除磁盘
- `lscpu` 打印 CPU 架构信息
- `lsfd` 显示打开文件的信息；替换 `lsof`
- `lsipc` 打印系统当前使用的 IPC 设施信息
- `lsirq` 显示内核中断计数器信息
- `lslocks` 列出本地系统锁
- `lslogins` 列出关于用户、组和系统账户的信息
- `lsmem` 列出可用内存范围及其其在线状态
- `lsnsns` 列出命名空间（namespaces）
- `mcmookie` 为 xauth 生成魔法 Cookie（128 位十六进制数）
- `mesg` 控制其他用户是否能向用户的终端发送消息
- `mkfs` 在设备上（通常是硬盘分区）上构建文件系统
- `mkfs.bfs` 创建 Santa Cruz Operations (SCO) 文件系统
- `mkfs.cram` 创建 cram 文件系统
- `mkfs.minix` 创建 Minix 文件系统
- `mkswap` 将给定的设备或文件初始化为交换区域（swap area）
- `more` 用于逐页翻页查看内容的过滤器
- `mount` 将设备上的文件系统挂载到文件系统树中的指定目录
- `mountpoint` 检查目录是否为挂载点
- `namei` 显示给定路径中的符号链接
- `snenter` 在其他进程的命名空间中运行程序
- `partx` 告知内核磁盘上分区的存在和编号
- `pivot_root` 将给定的文件系统变为当前进程的新根文件系统
- `prlimit` 获取和设置进程的资源限制
- `readprofile` 读取内核分析信息
- `rename` 重命名给定文件，将指定的字符串替换为另一个
- `renice` 更改运行进程的优先级
- `resizepart` 请求 Linux 内核调整分区大小
- `rev` 反转给定文件的行
- `rfkill` 用于启用和禁用无线设备的工具
- `ricwake` 用于进入系统睡眠状态，直到指定的唤醒时间
- `script` 创建终端会话的类型脚本（typescript）
- `scriptlive` 使用时间信息重新运行会话脚本
- `scriptreplay` 使用时间信息回放脚本
- `set` 在新的程序环境中更改报告的架构，并设置特性标志（personality flags）
- `setsid` 在新会话中运行给定的程序
- `seterm` 设置终端属性

## sfdisk

磁盘分区表操作器

## slogin

允许 root 登录；通常在系统进入单用户模式时由 init 调用

## swaplabel

将内容更改为交换区域的 UUID 和标签

## swapoff

禁用用于分页和交换的设备和文件

## swapon

启用用于分页和交换的设备和文件，并列出当前使用的设备和文件

## switch_root

切换另一个文件系统作为挂载树的根

## taskset

获取或设置进程的 CPU 亲和性

## uclampset

操作系统或进程的利用率限制属性（utilization clamping）

## ul

一种用于将下划线转换为指示终端下划线的转义序列的过滤器

## umount

从系统文件树中断开文件

## uname26

指向 `setarch` 的符号链接

## unshare

在与父进程共享某些命名空间的情况下运行程序

## utmpdump

显示 uuid 库的内容，以安全且保证唯一的方式生成基于时间的 UUID

## uuidgen

创建新的 UUID。每个新 UUID 都是一个随机数，极高概率在本地系统及其他系统（过去和未来）创建的所有 UUID 之间是唯一的（可能产生 2^128 个 UUID）

## uididparse

用于解析唯一标识符的实用

## wall

在所有当前登录用户的终端上显示文件内容，或默认显示标准输入

## wdctl

显示硬件看门狗状态

## whereis

报告给定命令的二进制文件、源文件和帮助页的位置

## wipefs

从设备上擦除文件系统签名

## x86_64

指向 `setarch` 的符号链接

## zramctl

设置和控制 zram（压缩内存磁盘）设备的程序

## libblkid

包含设备识别和提取的程序

## libfdisk

包含操作分区表的程序

## libmount

包含块设备挂载和卸载的程序

## libsmartcols

包含辅助表格格式输出的程序

## libuuid

包含为对象生成唯一标识符的程序

## 8.79. E2fsprogs-1.47.0

E2fsprogs 包包含处理 ext2 文件系统的工具。它还支持 ext3 和 ext4 日志文件系统。

**近似构建时间：** 机械硬盘上 2.4 SBU，SSD 上 0.4 SBU

**所需磁盘空间：** 95 MB

### 8.79.1 安装 E2fsprogs

E2fsprogs 建议在源码树的子目录中进行构建：

```
mkdir -v build
cd build
```

准备编译 E2fsprogs：

```
./configure --prefix=/usr
  --sysconfdir=/etc
  --enable-elf-shlibs
  --disable-libblkid
  --disable-libuuid
  --disable-uuid
  --disable-fck
```

配置 的的含义：

```
--enable-elf-shlibs
```

创建此包中某些程序使用的共享库。

```
--disable-*
```

这些防止构建和安装 `libuuid` 和 `libblkid` 库、`uuid` 守护进程、`fck` 封装，util-linux 安装最新版本。

编译包：

```
make
```

要运行测试，执行：

```
make check
```

要运行测试，执行：

```
make check
```

要运行测试，执行：

```
make check
```

要运行测试，执行：

```
make check
```

要运行测试，执行：

```
make check
```

## 从零开始构建 Linux - 版本 12.1

- `logsave`: 将命令的输出输出保存到日志文件中
- `lsattr`: 列出第二个扩展文件系统上的文件属性
- `mk_cmds`: 将命令名和帮助信息的表转换为适用于 libs subsystem 库的 C 源文件
- `mke2fs`: 在给定设备上创建 ext{234} 文件系统
- `mkfs.ext2`: 默认创建 ext{3} 文件系统，是 `mke2fs` 的硬链接
- `mkfs.ext3`: 默认创建 ext{4} 文件系统，是 `mke2fs` 的硬链接
- `mkfs.ext4`: 在 ext{234} 文件系统上创建 lost+found 目录；它为该目录预先分配磁盘块，以减轻 e2fsck 的任务
- `mklost+found2fs`: 可用于扩展或缩小 ext{234} 文件系统
- `tune2fs`: 调整 ext{234} 文件系统上的可调文件系统参数
- `libcomm_err`: 通用错误显示例程
- `libe2p`: 被 `dumpe2fs`、`chattr` 和 `lsattr` 使用
- `libext2fs`: 包含允许用户级程序操作 ext{234} 文件系统的例程
- `libss`: 被 `debugfs` 使用

## 8.80. Syslogd-1.5.1

Syslogd 包包含用于记录系统消息的程序，例如当发生异常情况时内核发出的消息。

**预计编译时间：** 少于 0.1 SBU

**所需的磁盘空间：** 680 KB

### 8.80.1. 安装 Syslogd

首先，修复在某些条件下导致 klog 发生段错误的问题，并修复一个过时的程序结构：

```bash
sed -i '/Error loading kernel symbols/(n;n;d)' ksym_mod.c
sed -i '/union wait/int/' syslogd.c
```

编译该包：

```bash
make
```

该包不带测试套件。

安装该包：

```bash
BINDIR=/sbin install
```

### 8.80.2. 配置 Syslogd

运行以下命令创建一个新的 `/etc/syslog.conf` 文件：
