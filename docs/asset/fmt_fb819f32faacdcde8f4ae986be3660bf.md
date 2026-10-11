
### 64.4.2. Sysvinit 包含内容

**已安装的程序：** `bootlogd`, `fstab-decode`, `halt`, `init`, `killall5`, `poweroff`（链接到 `halt`）, `reboot`（链接到 `halt`）, `runlevel`, `shutdown`, 以及 `telinit`（链接到 `init`）

#### 简述

- `bootlogd` 将启动日志记录到日志文件
- `fstab-decode` 使用 `fstab` 编码的参数运行命令
- `halt` 通常情况下带 `-h` 选项调用 `shutdown`，除非已处于运行级别 0，在那种情况下，它会通知内核停止系统；它会在文件 `/var/log/tmp` 中记下系统已关机
- `init` 内核初始化硬件时启动的第一个进程，它接管启动过程并启动其配置文件中指定的所有进程
- `killall5` 向所有进程发送信号，但你当前会话中的进程除外，因此它不会杀死其父 shell
- `power` 告诉内核停止系统并关闭计算机（`halt`）
- `reboot` 告诉内核重启系统（`halt`）
- `runlevel` 报告之前的和当前的运行级别，如 `/var/run/utmp` 中最后一次运行级别记录所示
- `shutdown` 以安全的方式关闭系统，向所有进程发送信号并通知所有登录用户
- `telinit` 告诉 `init` 切换到哪个运行级别

## 6.65. Eudev-3.2.1

`Eudev` 软件包包含了动态创建设备节点的程序
预计编译时间：0.2 SBU
所需磁盘空间：78 MB

### 6.65.1. 安装测试脚本

首先，修复测试脚本：

```
sed -r -i 's|/usr/(bin/test)|\1|g' test/udev-test.pl
```

接下来，移除一行导致编译失败的用行：

```
sed -i '/keyboard_lookup_key/' src/udev/udev-builtin-keyboard.c
```

接下来，添加一个变通方案，以防止 `/tools` 目录被硬编码到 Eudev 二进制文件路径中：

```
cat > config.cache << "EOF"

HAVE_BLKID=1

BLKID_LIBS="-lblkid"

BLKID_CFLAGS="-I/tools/include"

EOF
```

为编译 Eudev 准备工作：

```
./configure --prefix=/usr \
  --bindir=/sbin \
  --sbindir=/sbin \
  --libdir=/usr/lib \
  --sysconfdir=/etc \
  --libexecdir=/lib \
  --with-rootprefix \
  --with-rootlibdir=/lib \
  --enable-manpages \
  --disable-static \
  --config-cache
```

编译该包：

```
LIBRARY_PATH=/tools/lib make
```

现在创建测试需要的、也将作为安装一部分的目录：

```
mkdir -pv /lib/udev/rules.d
mkdir -pv /etc/udev/rules.d
```

要测试结果，执行：

```
make LD_LIBRARY_PATH=/tools/lib check
```

安装该包：

```
make LD_LIBRARY_PATH=/tools/lib install
```

安装一些在 LFS 环境中实用的自定义规则和设置文件：

```
tar -xvf ../udev-lfs-20140408.tar.bz2
make -f udev-lfs-20140408/Makefile.lfs install
```

### 6.65.2. 配置 Udev

硬件设备的信息维护在 `/etc/udev/hwdb.d` 和 `/usr/lib/udev.d` 目录下。`udev` 需要将信息编译成二进制数据库 `/etc/udev/hwdb.bin`。创建初始数据库：

```
LD_LIBRARY_PATH=/tools/lib udevadm hwdb --update
```

此命令在每次硬件信息更新时都需要运行。

### 6.65.3. Udev 包含内容

- 安装的程序：`udevadm` 和 `udevd`
- 安装的库：`libudev.so`
- 安装的目录：`/etc/udev`, `/lib/udev`, 以及 `/usr/share/doc/udev-20140408`

#### 简述

- `udevadm`: 通用 `udev` 管理工具：控制 `udev` 守护进程，提供来自 `udev` 数据库的信息，监控 `uevents`，等待 `uevents` 完成，并为给定设备触发 `uevents`
- `udevd`: 监听 `netlink` 套接字 `uevents` 的守护进程，创建设备并响应这些事件运行外部程序
- `libudev`: `udev` 的库接口
- `/etc/udev`: 包含设备命名的 `udev` 配置、权限和规则

## Util-linux-2.29.1

`Util-linux` 软件包包含了各种杂用程序。其中包含处理文件系统、控制台、分区和消息的工具。

预计编译时间：1.0 SBU
所需磁盘空间：6 MB

### FHS 合规性

FHS 建议使用 `/var/lib/hwclock` 代替通常的 `/etc` 目录作为 `adjtime` 位置。为存储 `hwclock` 创建目录：

```
mkdir -pv /var/lib/hwclock
```

### 6.65.2. 安装 Util-linux

为编译 `Util-linux` 准备工作：

```
./configure ADJTIME_PATH=/var/lib/hwclock/adjtime \
  --docdir=/share/doc/util-linux \
  --disable-chsh \
  --disable-login \
  --disable-ologin
```

编译该包：

```
make
```

如果需要，以 root 用户运行测试套件：

```
make
```

**注意**：在重启后可以安全地运行，LFS 目录：

```bash
=$PWD
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
=$PATH"
```

**注意**：在重启后可以安全地运行，LFS 目录：

```chown -Rv nobody
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
=$PWD
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
,mkfs, mkfs.min
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
,make
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
,mkfs.cramfs, mkfs.min, mkswap
```

安装该包：

```
make install
```
