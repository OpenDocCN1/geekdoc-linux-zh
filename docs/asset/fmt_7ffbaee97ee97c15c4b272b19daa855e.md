
### 6.46.2. Gzip 目录

- 安装的程序：`gzip`, `zxze`, `uncompress`, `zcat`, `zcmp`, `zdiff`, `zgrep`, `zfgrep`, `zforce`, `zgrep`, `zmore`, 和 `znew`

### 简说明

- `gzip`: 解压缩 gzipped 格式的文件
- `zxze`: 创建自解压的可执行文件
- `gzip`: 使用 Lempel-Ziv (`LZ77`) 编码压缩给定文件
- `uncompress`: 解压缩压缩的文件
- `zcat`: 将指定的 gzipped 文件解压缩到标准输出
- `zcmp`: 在 gzipped 文件上运行 `cmp`
- `zdiff`: 在 gzipped 文件上运行 `diff`
- `zgrep`: 在 gzipped 文件上运行 `egrep`
- `zfgrep`: 在 gzipped 文件上运行 `fgrep`
- `zforce`: 对所有给定的 gzipped 文件强制加上 `.gz` 扩展名，这样 `gzip` 不会再次对其压缩；这在文件传输过程中文件名被截断时非常有用
- `zgrep`: 在 gzipped 文件上运行 `grep`
- `ziess`: 在 gzipped 文件上运行 `less`
- `zmore`: 在 gzipped 文件上运行 `more`
- `znew`: 将文件从 `compress` 格式重新压缩为 `gzip` 格式---z 到 `.gz`

## 6.47. IPRoute2-3.2.0

`IPRoute2` 软件包包含基于 `IPV4` 的基础和高级网络程序。
预计编译时间：0.1 SBU
所需的磁盘空间：6.6 MB

### 6.47.1. 安装 IPRoute2

此软件包包含的 `arpd` 二进制文件依赖于 Berkeley DB。由于 `arpd` 不是 Linux 系统上的常见需求，请通过应用以下命令删除对 Berkeley DB 的依赖。如果在 BLFS 书籍 http://www.linuxfromscratch.org/lfs/view/server/databases.html#db 中找到 `arpd` 二进制文件。

```
sed -i '/TARGETS/s@arp@arpd@' misc/Makefile
```

```
sed -i /ARPD/d Makefile
```

```
rm man/man8/arpd.8
```

移除 `IPRoute2` 不需要需的 Libnl 头文件引用：

```
sed -i -e '/netlink\/d' ip/ipl2tp.c
```

编译软件包：

```
make DESTDIR=
```

该选项的含义是：

`DESTDIR=` 确保 `IPRoute2` 二进制文件将安装到正确的目录。默认情况下，`DESTDIR` 设置为 `/usr`。

此软件包带有一个测试套件，但由于其所做的假设，无法在 chroot 环境中可靠地运行这些测试。如果你希望在进入你的 LFS 系统后运行这些测试，请确保选择内核支持 `/proc/config.gz` `CONFIG IFCONFIG PROC` ("General setup") -> "Enable access to config through /proc/config.gz" 支持，然后从 `testsuite/` 子目录运行 `make all`。

安装软件包：

```
make DESTDIR=/usr/share/man /
DOCDIR=/usr/share/doc/iproute2-3.2.0 install
```

### 6.47.2. IPRoute2 目录

- 安装的程序：`ctstat`（链接至 Instat）, `genl`, `ifconfig`, `ifstat`, `ip`, `Instat`, `ntable`, `route`, `routel`, `rtatc et`, `rtmon`, `rtprist`（链接至 Instat）, `ss`, 和 `tc`

- 安装的目录：`/etc/iproute2`, `/lib/tc`, `/usr/share/doc/iproute2-3.2.0`, `/usr/lib/tc`

### 简说明

- `ctstat`: 连接状态工具
- `genl`

## 6.48. Kbd-1.15.2

`Kbd` 软件包包含键盘布局文件和键盘工具。
预计编译时间：少于 0.1 SBU
所需的磁盘空间：160 KB

### 6.48.1. 安装 Kbd

Backspace 和 Delete 键在 `Kbd` 软件包的布局图中是不一致的。以下补丁修复了 i386 的问题：

```
patch -N -i ..kbd-backspace.patch
```

打补丁后，Backspace 键生成代码 127，Delete 键生成一个转义序列。

为编译准备 `Kbd`：

```
./configure --prefix=/usr --datadir=/lib/kbd
```

`configure` 选项的含义是：

`--datadir=/lib/kbd` 将键盘布局数据放在根分区而不是 `/usr/share/kbd`。

编译软件包：

```
make
```

此软件包未带测试套件。

安装软件包：

```
make install
```

注意：对于某些语言（例如俄罗斯语），`Kbd` 软件包提供了 ISO-8859-5 布局，通常使用 CP1251 布局。此类语言的用户必须单独处理布局。LFS 脚本依赖于 `kbd_mode`, `loadkeys` 和 `setfont`。由于在启动早期 `/bin` 可能不可用，这些二进制文件需要放在根分区：

```
mv -v /bin/{kbd_mode,loadkeys,setfont} /bin
```

如果需要，安装文档：

```
mkdir -v /usr/share/doc/kbd
cp -R doc/* /usr/share/doc/kbd
```

### 6.48.2. Kbd 目录

安装的程序：`chvt`, `deallocvt`, `dumpkeys`, `fgconsole`, `getkeycodes`, `kbd_mode`, `kbdrate`, `loadkeys`, `loadunimap`, `mapsrc`, `openvt`, `psfaddtable`（链接至 `psftable`）, `psfgettable`（链接至 `psftable`）, `psfstriptable`（链接至 `psftable`）, `resizecons`, `setfont`, `metled`, `showconsolefont`, `showkey`, `unicode_start`, 和 `unicode_stop`

- `chvt`: 切换虚拟虚拟终端
- `deallocvt`: 释放未使用的虚拟终端
- `dumpkeys`: 转储键盘翻译表
- `fgconsole`: 打印活动虚拟终端的数量
- `getkeycodes`: 打印扫描码到键码的映射表
- `kbd_mode`: 报告或设置键盘模式
- `kbdrate`: 设置键盘重复和延迟速率
- `loadkeys`: 加载键盘翻译表
- `loadunimap`: 加载 unicode 到字体的映射表
- `mapsrc`: 一个过时的程序，用于将定义的输出字符表加载到控制台驱动；现在由 `setfont` 完成
- `openvt`: 在新的虚拟终端 (VT) 上启动程序
- `psfaddtable`: 链接至 `psftable`
- `psfgettable`: 链接至 `psftable`
- `psfstriptable`: 链接至 `psftable`
- `psftable`: 处理控制台字体表
- `resizecons`: 修改内核控制台的大小
- `setfont`: 修改控制台上的增强图形适配器 (EGA) 和视频图形阵 (VGA) 字体
- `setkeys`: 加载扫描码到键码的映射项；如果键盘上有异常键，这非常有用
- `setled`: 设置键盘标志和发光二极管 (LEDs)
- `metset`: 定义元键处理
- `showconsolefont`: 显示当前的 EGA/VGA 控制台字体
- `showkey`: 报告按下键的扫描码和 ASCII 代码
- `unicode_start`: 将键盘和控制台置于 UNICODE 模式
- `unicode_stop`: 将键盘和控制台从 Unicode 模式恢复
- `ip`: 主执行文件。它有多个功能：
- `ip link <device>`: 允许用户查看设备状态并更改
- `ip add`: 允许用户查看地址及其属性、添加新地址并删除旧地址
- `ip neighbor`: 允许用户查看邻居绑定及其属性、添加新条目并删除条目
- `ip rule`: 允许用户查看路由策略并更改
- `ip route`: 允许用户查看路由表并更改路由表
- `ip addr`: 允许用户查看并更改组地址
- `ip maddr`: 允许用户设置或删除组地址
- `ip monitor`: 持续监控设备、地址和路由的状态
- `ip tunnel`: 允许用户查看隧道及其属性
- `ip -o`: 允许用户估计进入网络的流量
- `route`: `ip` 的一个组件。用于清空路由表
- `route`: `ip` 的一个组件。用于列出表
- `ifcfg`: `ip` 命令的 shell 脚本封装
- `ifstat`: 显示接口统计，包括每个接口发送和接收的数据包数量
- `rtacct`: 显示 `/proc/net/acct` 的内容
- `rtmon`: 路由监控工具
- `rtpr`: 将 `ip -o` 的输出转换回可读格式
- `rtstat`: 提供 Linux 统计数据。它是旧 `netstat` 的通用且功能更完整的替代品
- `Route`: 路由状态工具
- `ss`:  `netstat` 命令；用于服务质量 (QOS) 和分类服务 (COS) 的实现
- `tc qdisc`: 允许用户设置队列规则
- `tc class`: 允许用户根据队列规则调度设置类
- `tc estimator`: 允许用户估计网络流量
- `tc filter`: 允许用户设置 QOS/COS 数据包过滤
- `tc policy`: 允许用户设置 QOS/COS 策略

## 6.49. Kmod-5

`Kmod` 软件包包含加载内核模块的库和实用程序

预计编译时间：少于 0.1 SBU
所需磁盘空间：16.0 MB

### 6.49.1. Kmod 的安装

为编译 `Kmod` 准备工作：

```
liblzma CFLAGS="-I/usr/include" \
llzma LIBS="-L/lib -lzma" \
zlib CFLAGS="-I/usr/include" \
zlib LIBS="-L/lib -lz" \
./configure --prefix=/usr --bindir=/bin --libdir=/lib --sysconfdir=/etc \
with-xz --with-zlib
```

`configure` 选项的含义：
`lib*` 和 `--with-z*`

这些选项允许 `Kmod` 加载压缩的内核模块。在缺少 `pkg-config` 的情况下，需要这些 变量以便找到 `xz` 和 `zlib` 的头文件和库。

编译软件包：

```
make
```

要测试结果，执行：

```
make check
```

安装软件包，并创建符号链接以兼容 Module-Linit-Tools（以前一个处理 Linux 内核模块的软件包）：

```
make pkgconfigdir=/usr/lib/pkgconfig install
for target in dep ../bin/kmod insmod modinfo modprobe rmmod; do
ln -sv $target /sbin/$target
done
ln -sv kmod /bin/lsmod
```

### 6.49.2. Kmod 的内容

- 安装的程序：`depmod`（链接到 `kmod`）、`insmod`（链接到 `kmod`）、`kmod`、`kmod-nolib`、`lmod`（链接到 `kmod`）、`modinfo`（链接到 `kmod`）、`modprobe`（链接到 `kmod`）和 `rmmod`（链接到 `kmod`）
`lib/kmod.so`

安装的库：

简要说明

- **depmod**: 根据在现有模块集中找到的符号创建依赖文件；该依赖文件用于 `modprobe` 自动加载所需的模块
- **insmod**: 在正在运行的内核中安装可加载模块
- **kmod**: 加载和卸载内核模块
- **libkmod**: 此库被其他程序用于加载和卸载内核模块
- **lsmod**: 列出当前加载的模块
- **modinfo**: 检查与内核模块相关的对象文件并显示它可以获取的任何信息
- **modprobe**: 使用 **depmod** 创建的依赖文件自动加载相关模块
- **rmmod**: 从正在运行的内核中卸载模块

## 6.50. Less-444

`Less` 软件包包含一个文本查看器。
预计编译时间：少于 0.1 SBU
所需磁盘空间：3.5 MB

### 6.50.1. Less 的安装

为编译 `Less` 准备工作：

```
./configure --prefix=/usr --sysconfdir=/etc
```

`configure` 选项的含义：
`--sysconfdir=/etc`
此选项告诉软件包创建的程序去 `/etc` 查找配置文件。

编译软件包：

```
make
```

此软件包不带测试套件。

安装软件包：

```
make install
```

### 6.50.2. Less 的内容

- 安装的程序：`less`、`lessecho` 和 `lesskey`

# 简要说明

- **less**: 文件查看器或分页器；它显示给定文件的内容，允许用户滚动、查找字符串并跳转到标记
- **lessecho**: 用于在 Unix 系统文件名中扩展元字符（如 * 和 ?）
- **lesskey**: 用于指定 less 的键绑定

## 6.51. Libpipeline-1.2.0

`Libpipeline` 软件包包含一个库，用于以灵活方便的方式操作子进程的管道。

**预计编译时间：** 0.1 SBU
**所需磁盘空间：** 8.0 MB

### 6.51.1. Libpipeline 的安装

为编译 `Libpipeline` 准备工作：

```
./configure CHECK_CFLAGS=-I/tools/include \
CHECK_LIBS="-L/tools/lib -lcheck" --prefix=/usr
```

`configure` 选项的含义：

```
CHECK_CFLAGS=, CHECK_LIBS=
这些环境变量指定了第 5.14 节“Check-0.9.8”中构建的测试库的位置。
```

编译软件包：

```
make
```

要测试结果，执行：

```
make check
```

安装软件包：

```
make install
```

### 6.51.2. Libpipeline 的内容

安装的库：`libpipeline.so`

# 简要说明

- **libpipeline**: 此库用于安全地构建子进程之间的管道

## 6.52. Make-3.82

`Make` 软件包包含一个用于编译软件包的程序。
预计编译时间：0.3 SBU
所需磁盘空间：9.7 MB

### 6.52.1. Make 的安装

为编译 `Make` 准备工作：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

要测试结果，执行：

```
make check
```

安装软件包：

```
make install
```

### 6.52.2. Make 的内容

- 安装的程序：`make`

# 简要说明

- **make**: 自动确定软件包的哪些部分需要（重新）编译，然后发布相关命令

## 6.53. Man-DB-2.6.1

`Man-DB` 软件包包含查找和查看 man 页的程序。
预计编译时间：0.4 SBU
所需磁盘空间：22 MB

### 6.53.1. Man-DB 的安装

为 `Man-DB` 编译准备工作：

```
PKG_CONFIG=/usr/bin/true \
CFLAGS='' \
LIBS='-libpipeline' \
./configure --prefix=/usr --lib-db-2.6.1 --execdir=/usr/lib \
--docdir=/usr/share/doc/man-db-2.6.1 --sysconfdir=/etc \
--disable-setuid \
--with-pager=/usr/bin --with-pager=/usr/bin
```

`configure` 选项的含义：

`PKG_CONFIG...` 这些环境变量允许配置过程在没有外部 `pkg-config` 程序的情况下完成。

`--disable-setuid` 禁用 man setuid 程序。

`--with...` 这三个参数用于设置默认程序。`lynx` 是一个基于文本的浏览器，`vgrind` 将转换为 Groff 输入， `grap` 用于 Groff 文档的排版。`vgrind` 和 `grap` 通常用于查看 man 页，但如果你需要，可以安装它们。

编译软件包：

```
make
```

要测试结果，执行：

```
make check
```

安装软件包：

```
make install
```
