
### 6.73.3. Util-linux 的内容

已安装的程序：`addpart`, `agetty`, `blkiscard`, `blkid`, `blkzone`, `blockdev`, `cal`, `cfdsk`, `cpchu`, `chmem`, `choom`, `chrt`, `col`, `colct`, `colrm`, `colmn`, `cltrldel`, `delpart`, `dmesg`, `eject`, `fallocate`, `fdism`, `fdisk`, `fin cwd`, `findinds`, `findfmt`, `fsk`, `fckramfs`, `fckminix`, `fsfreeze`, `ftrim`, `getopt`, `hexdump`, `hexclock`, `i1386`, `ibionic`, `ipemc`, `ipcs`, `isozize`, `kill`, `last`, `lastib` (链接到 `last`), `lddatch`, `linux32`, `linux64`, `logger`, `look`, `letup`, `islbk`, `isisc`, `isproc`, `islogins`, `lsmen`, `lmsnoct`, `colleague`, `meskg`, `mksbfs`, `mksdev`, `mksminix`, `mksnix`, `mkwap`, `mount`, `mountpoint`, `namei`, `nserter`, `part`, `pivot_root`, `primit`, `raw`, `readline`, `rename`, `renice`, `rezerv`, `rfkill`, `rtcwake`, `script`, `scriptreplay`, `setarch`, `setid`, `sfdird`, `sfdluk`, `sulogin`, `swallow`, `swapoff` (`swap` 链接), `spawn`, `swap_rost`, `taskset`, `ul`, `unmount`, `uname26`, `ushr`, `utmpdump`, `uuid`, `uigen`, `usidparse`, `wall`, `wcdtl`, `wepefs`, `x86_64`, 和 `zramctl`

已安装的目录：`/usr/include/blkid`, `/usr/include/libdisk`, `/usr/include/libmount`, `/usr/include/`, `/usr/include/linux/uapi`, `/usr/share/doc/util-linux-2.34`, 以及 `/var/lib/hwclock`

- `addpart` 添加分区
- `agetty` 打开一个 ty 端口，提示登录名称
- `blkiscard` 创建登录设备
- `blid` 查找分区
- `blkzone` 调制块设备
- `blockdev` 挂载文件
- `cal` 显示日历
- `cfdsk` 过滤掉
- `cpchu` 修改
- `chmem` 配置内存
- `choom` 优先级
- `chrt` 调制实时
- `col` 过滤掉
- `colct` 过滤掉
- `colrm` 过滤掉
- `colmn` 过滤掉
- `cltrldel` 终端是
- `delpart` 删除分区
- `dmesg` 打印内核消息
- `eject` 弹出移除介质
- `fallocate` 分配空间
- `fdism` 文件系统
- `fdisk` 磁盘分区表
- `fin cwd` 查找根目录
- `findinds` 查找用户
- `findfmt` 格式
- `fsk` 执行一致性检查
- `fckramfs` 修复 cramfs
- `fckminix` 修复 Minix 系统
- `fsfreeze` 冻结系统
- `ftrim` 丢弃块
- `getopt` 获取命令行
- `hexdump` 打印十六进制
- `hexclock` 实时时钟
- `i1386` 架构
- `ibionic` 进程间通信
- `ipemc` 报告 IPC
- `ipcs` 提供 IPC 状态
- `isozize` 尺寸
- `kill` 向进程发送信号
- `last` 显示登录的用户
- `lastib` (链接到 `last`)
- `lddatch` 挂载行
- `linux32` 架构
- `linux64` 架构
- `logger` 将消息记录到系统
- `look` 查找
- `letup` 文件系统
- `islbk` 设置循环设备
- `isisc` 系统类
- `isproc` 报告进程信息
- `islogins` 显示用户
- `lsmen` 关于用户的信息
- `lmsnoct` 显示系统
- `colleague` 工具
- `meskg` 控制用户是否可以发送消息
- `mksbfs` 构建文件系统
- `mksdev` 挂载设备
- `mksminix` 初始化 Minix 系统
- `mksnix` 创建文件系统
- `mkwap` 生成 magic cookies
- `mount` 挂载文件系统
- `mountpoint` 检查目录是否为挂载点
- `namei` 显示符号链接
- `nserter`
- `partx` 告知内核关于
- `pivot_root` 使文件系统成为根目录
- `primit`
- `raw` 绑定 Linux 字符设备
- `readline` 读取配置信息
- `rename` 重命名文件
- `renice` 修改运行进程的优先级
- `rezerv` 留内存
- `rfkill` 启用和禁用无线设备的工具
- `rtcwake` 进入系统睡眠状态
- `script` 终端会话的脚本
- `scriptreplay` 回放脚本
- `setarch` 更改报告的架构
- `setid` 设置会话
- `sfdird`
- `sfdluk`
- `sulogin` 允许 root 登录
- `swallow` 禁用分页和交换设备及文件
- `spawn` 启动新进程
- `swap_rost` 系统
- `taskset` 设置运行进程的亲和性
- `ul`
- `unmount` 卸载文件系统
- `uname26` 架构
- `ushr` 系统
- `utmpdump` 显示 wtmp 文件
- `uuid` 唯一标识符
- `uigen` 生成
- `usidparse` 系统
- `wall` 向当前用户发送消息
- `wcdtl`
- `wepefs`
- `x86_64` 架构
- `zramctl` 压缩 zram

#### switch_root

将另一个文件系统切换为挂载树的根

#### tailf

跟踪日志文件的增长；显示日志文件的最后 10 行，然后在日志文件新条目被创建时继续显示它们

#### taskset

获取或设置进程的 CPU 亲和性

#### ul

一种过滤器，用于将下划线转换为转义序列，以便在当前终端中显示下划线效果

#### unameount

从系统文件树中断开文件

#### uname26

一个指向 search 的符号链接

#### unshare

在某些命名空间与父进程分离（unshare）的情况下运行程序

#### utmpmpd

以更用户友好的格式显示给定日志文件的内容

#### uuidd

由 UUID 库提供的守护进程，用于以安全且保证唯一的方式生成基于时间的 UUID

#### uigen

创建新的 UUID。每个新生成的 UUID 在本地系统及其他系统（过去和未来）创建的所有 UUID 之间，都可以被合理地认为是唯一的

#### uipparse

用于解析唯一标识符的工具

#### wall

在所有当前登录用户的终端上显示文件内容，或默认显示标准输入

#### wdctl

显示硬件看门狗状态

#### whereis

报告给定命令的二进制文件、源码和帮助页的位置

#### wipes

从设备擦擦文件系统签名

#### x86_64

一个指向 setup 的符号链接

#### zramctl

用于设置和控制 zram（压缩内存磁盘）设备的程序

#### libblk

包含设备识别和令牌提取的例程

#### libfsdisk

包含操作分区表的例程

#### libmount

包含块设备挂载和卸载的例程

#### libsmartcols

包含辅助表格形式屏幕输出的例程

#### libuuid

包含为超出本地系统访问的对象生成唯一标识符的例程

## 74. E2fsprogs-1.45.3

E2fsprogs 包包含处理 ext2 文件系统的实用程序。它还支持 ext3 和 ext4 日志文件系统。

预计构建时间：3.1 SBU
所需磁盘空间：108 MB

### 6.74.1. E2fsprogs 的安装

E2fsprogs 文档建议将包在源码树的子目录中构建：

```
mkdir -v build
cd build
```

为编译 E2fsprogs 做好准备：

```
../configure --prefix=/usr
    --bindir=/bin
    --root-prefix=""
    --enable-elf-shlibs
    --disable-libblkid
    --disable-libuuid
    --disable-uuid
    --disable-fsck
```
