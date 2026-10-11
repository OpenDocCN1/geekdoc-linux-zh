
环境变量和配置选项的含义：

`--root-prefix=""` 和 `--bindir=/bin`
程序（如 `efsck` 程序）被视为基本程序。例如，当 `/usr` 未挂载时，这些程序仍然可用。它们属于 `/lib` 和 `/sbin` 目录。如果没有将此选项传递给 E2fsprogs 的 `configure`，程序将安装到 `/usr` 目录。

`--enable-elf-shlibs`
这会创建该包中某些程序使用的共享库。

`--disable-*`
这可以防止 E2fsprogs 构建和安装 `libuuid` 和 `libblkid` 库、`uuid` 守护进程以及 `fsck` 包装器，因为 Util-Linux 安装了最新版本。

编译包：

```
make
```

运行测试，执行：

```bash
make check
```

E2fsprogs 的测试之一将尝试分配 256 MB 内存。如果你的内存没有明显多于此，请确保为测试启用足够的交换空间。详细信息请参阅第 2.5 节“在分区上创建文件系统”和第 2.7 节“挂载新分区”。

安装二进制文件、文档和共享库：

```
make install
```

## 从头开始安装 - 版本 9.0

安装静态库头文件：

```
make install-libs
```

使已安装的静态库变为可写，以便以后删除调试符号：

```
chmod -v u /usr/lib/libcom_err,lib2p,lib2fs,lib2ss.a
```

此包经过了 `gzip` 压缩。`info` 文件不会更新系统目录文件。解压此文件，然后使用以下命令更新系统目录：

```
gunzip -v /usr/share/info/libext2fs.info.gz
install-info --dir-file=/usr/share/info/dir /usr/share/info/libext2fs.info
```

如果需要，可以通过执行以下命令创建额外的文档：

```
make-info -o doc/com_err.info ./lib/et/com_err.texinfo
install -v -m644 doc/com_err.info /usr/share/info
install-info --dir-file=/usr/share/info/dir /usr/share/info/com_err.info
```

## 74.2. E2fsprogs 的内容

安装的库：

`libcom_err,lib2p,lib2fs,lib2ss.a`

安装的目录：

`/usr/include`, `/lib`, `/share/info`

简短描述：

- `badblocks`: 搜索坏块
- `champ`: [unknown]
- `patle`: [unknown]
- `debugfs`: 一个系统调试器
- `dump2fs`: 打印超级块信息
- `e2freefrag`: 报告剩余空间
- `e2ck`: 检查文件系统
- `eimage`: 用于创建镜像
- `label`: 修改文件系统的标签
- `e2mpstatus`: 检查 e2mp 状态
- `e2scrub`: 检查 ext2 文件系统
- `e2scrub_all`: 检查所有 ext2 文件系统
- `eundo`: 重放还原
- `e4crypt`: Ext4 加密
- `e4defrag`: 在线碎片整理
- `filefrag`: 报告文件碎片
- `fsck2`: [unknown]
- `fsck3`: [unknown]
- `fsext4`: [unknown]
- `logsate`: 保存命令输出
- `mkfs_2fs`: 创建 ext2 文件系统
- `mkfs_ext4`: 创建 ext4 文件系统
- `resize2fs`: 可以增大或缩小文件系统
- `tune2fs`: 调整系统参数

## 6.75. Syslog-1.5

Syslog 包包含用于记录系统消息程序，例如内核在发生异常时提供的信息。

预计构建时间：0.1 SBU
所需磁盘空间：0.6 MB

### 6.75.1. Syslog 的安装

首先，修复 `klog` 在某些情况下导致段错误的问题并修复过时的程序结构：

```
sed -i '/Error loading kernel symbols/{n;n;d}' kysm_mod.c
sed -i '/s/union wait/int/' syslog.c
```

编译包：

```
make
```

此包未自带测试套件。

安装包：

```
make BINDIR=/sbin install
```

### 6.75.2. 配置 Syslog

通过运行以下命令新的 `/etc/syslog.conf` 文件：

```
cat > /etc/syslog.conf << "EOF"
# Begin /etc/syslog.conf
auth,authpriv.* - /var/log/auth.log
*.,;authpriv.none -/var/log/sys.log
daemon.* - /var/log/daemon.log
kern.* - /var/log/kern.log
mail.* - /var/log/mail.log
user.* - /var/log/user.log
* .emerg *
# End /etc/syslog.conf
EOF
```

### 6.75.3. Syslog 的内容

安装的程序：`klogd` 和 `syslog`

简短描述：

- `klogd`: 用于拦截和记录内核消息的系统守护进程

`syslog` 记录了系统程序提供的日志消息。[每条被记录的消息至少包含一个日期时间戳和一个主机名，通常还包含程序名称，但这取决于对日志守护进程信任的信任信度设置。]

## 7.6. Sysunit-2.95

Sysunit 软件包包含了控制系统启动、运行和关闭的程序。

预计编译时间：少于 0.1 SBU
所需磁盘空间：1.3 MB

### 6.76.1. 安装 Sysunit

首先，应用补丁以移除其他软件包安装的程序，澄清一条消息，并修复编译器警告：

```
patch -Np1 -i ../sysunit-2.95-consolidated-1.patch
```

编译软件包：

```
make
```

此软件包不带测试套件。

安装软件包：

```
make install
```

### 6.76.2. Sysunit 的内容

已安装的程序：`bootlogd`, `fstab-decode`, `halt`, `init`, `killall5`, `poweroff`（链接到 `halt`）, `reboot`（链接到 `halt`）, `runlevel`, `shutdown`, 以及 `telinit`（链接到 `init`）

简述

- `bootlogd`: 将启动消息记录到日志文件
- `fstab-decode`: 使用 fstab 编码算法运行命令
- `halt`: 通常带 `-h` 选项调用 `shutdown`，但在运行级别为 0 时除外，此时它通知内核停止系统；它会在 `/var/log/wt.tmp` 文件中记录系统已关机
- `init`: 内核接管启动过程时启动的第一个进程，它会启动其配置文件中指定的所有进程
- `killall5`: 向所有进程发送信号，运行会话中的进程除外，因此它不会杀死其父 shell
- `poweroff`: 通知内核停止系统并关闭计算机（`halt`）
- `reboot`: 通知内核重启系统（`halt`）
- `runlevel`: 报告上一个运行级别和当前运行级别，如 `/var/run/ut.mp` 中最后的运行级别记录所示
- `shutdown`: 以安全的方式关机系统，向所有进程发送信号并通知所有登录用户
- `telinit`: 告诉 `init` 要切换到哪个运行级别

## 6.77. Eudev-3.2.8

Eudev 软件包包含了动态创建设备节点的程序。
预计编译时间：0.2 SBU
所需磁盘空间：22 MB

### 6.77.1. 安装 Eudev

为编译 Eudev 做准备：

```
./configure --prefix=/usr \
--bindir=/sbin \
--sbindir=/sbin \
--libdir=/usr/lib \
--sysconfdir=/etc \
--libexecdir=/lib \
--with-rootlibprefix= \
--with-rootlibdir=/lib \
--enable-manpages \
--disable-static
```

编译软件包：

```
make
```

现在创建测试所需但也将作为安装一部分使用的目录：

```
mkdir -pv /lib/udev/rules.d
mkdir -pv /etc/udev/rules.d
```

执行以测试结果：

```
make check
```

安装软件包：
