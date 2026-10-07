
`./configure --enable-arch --enable-partx --enable-write`

配置选项的含义：

- `--enable-arch`: 启用构建 arch 程序
- `--enable-partx`: 启用构建 addpart、delpart 和 parts 程序
- `--enable-write`: 启用构建 write 程序

编译软件包：

```bash
make
```

此软件包不带测试套件。

安装软件包：

```bash
make install
```

### 6.21.3. Util-linux 的内容

已安装的程序：addpart, agetty, arch, bl, blockdev, cal, cfdisk, chkdupe, chr, col, coerc, colm, column, ctrlaltdel, cytune, delpart, desmq, fallocate, fdformat, fdisk, findfs, findmnt, flock, fsck-ramfs, fsck-linux, fsfree, fstrim, hwclock, i386, ioctl, ipcmk, ipenc, ipocs, isdatch, linux32, linux64, logger, lookup, islbk, isblk, meocrie, mkfs, mkfs.bfs, mkfs.kamfs, mkfs-linux, mkswap, more, mount, mountpoint, name, partx, pg, pivot_root, rename, renice, renic, rtcwake, scriptreplay, setarch, setcdid, setterm, sdisk, swappable, spoflik (link to spawn), switch root, tail, tasket, tunelp, ul, unshare, uidd, uuidigen, wall, whereis, wipes, and write

已安装的库：`libblkid.{a,so}`, `libmount.{a,so}`, `libuuid.{a,so}`

已安装的目录：`/usr/include/blkid`, `/usr/include/libmount`, `/usr/include/uuid`, `/usr/share/getopt`, `/var/lib/hwclock`

## 要描述

- `addpart`: 通知 Linux 内核新分区
- `agetty`: 打开 tty 端口，提示登录名，然后调用登录程序
- `arch`: 报告机器架构
- `blkid`: 用于定位和打印块设备属性的命令行实用程序
- `blockdev`: 允许用户从命令行调用块设备 ioctl
- `cal`: 显示简单的日历
- `cfdisk`: 操作给定设备的分区表
- `chkdupe`: 查找重复的可执行文件
- `chrt`: 操作进程的实时属性
- `col`: 过滤掉反向行
- `colct`: 为缺少某些功能（如重叠和半行）的终端过滤非 col 内容
- `colrm`: 过滤掉指定的列
- `column`: 将给定文件格式化为多列
- `ctrlaltdel`: 将 Cylades 卡上串行驱动程序的 Ctrl+Alt+Del 键组合功能设为硬重置或软重置
- `cytune`: 调整 Cylades 卡串行驱动程序的参数
- `delpart`: 请求 Linux 内核删除分区
- `dmesg`: 倾储内核启动消息
- `fallocate`: 为文件预分配空间
- `fdformat`: 低级格式化软磁盘
- `fdisk`: 操作给定设备的分区表
- `findfs`: 通过标签或通用唯一标识符 (UUID) 查找文件系统
- `findmnt`: libmount 库的命令行接口，用于处理 mountinfo、fstab 和 mtab 文件
- `flock`: 获取文件锁并在持有锁的情况下执行命令
- `fsck`: 用于检查并可选地修复文件系统
- `fsck.cams`: 对给定设备上的 Cramfs 文件系统进行一致性检查
- `fsck.minix`: 对给定设备上的 Minix 文件系统进行一致性检查
- `fsrefree`: 对 FREEZE/FITHAW ioctl 内核驱动操作的非常简单的封装
- `fstrim`: 丢弃挂载文件系统上的未使用块
- `getopt`: 解析给定命令行中的选项
- `hexdump`: 以十六进制或另一个给定格式倾储给定文件
- `hwclock`: 读取或设置系统硬件时，也称为实时钟 (RTC) 或 BIOS 钟
- `i386`: 指 setarch 的符号链接
- `ionice`: 获取或设置程序的 io 调度类和优先级
- `ipcmk`: 创建各种 IPC 资源
- `iperm`: 移除指定的进程间通信 (IPC) 资源
- `ipcs`: 提供 IPC 状态信息
- `isize`: 报告 iso960 文件系统的尺寸
- `lddatch`: 挂载设备
- `linux32`: 指 setarch 的符号链接
- `linux64`: 指 setarch 的符号链接
- `logger`: 将消息输入系统日志
- `lookup`: 显示以特定行头的行
- `iscpu`: 生成关于 CPU 的信息
- `isblk`: 列出所有块设备的信息
- `meocrie`: 生成 128 位随机数
- `mkfs`: 构建文件系统
- `mkfs.bfs`: 创建 bfs 文件系统
- `mkfs.ramfs`: 创建 ramfs 系统
- `mkswap`: 初始化设备作为交换分区
- `more`: 分页显示文本
- `mount`: 挂载文件系统
- `mountpoint`: 检查目录是否为挂载点
- `namei`: 显示路径中的符号链接
- `partx`: 通知内核分区的存在和编号
- `pivot_root`: 将给定文件系统变为当前进程的根
- `rename`: 通过替换字符串重命名文件
- `renice`: 更改运行进程的优先级
- `rev`: 反转给定文件的行
- `rtcwake`: 用于指定时间唤醒系统睡眠
- `script`: 终端录制
- `scriptreplay`: 使用计时回放录制
- `setarch`: 在新环境中更改架构并设置性标记
- `setid`:在新会话中运行程序
- `setterm`: 设置终端属性
- `sdisk`: 磁盘分区操作器
- `swaplabel`: 允许更改交换区域 UUID
- `swap`: 列出设备和文件
- `switch_root`: 切换文件系统作为根
- `tail`: 跟踪日志文件的增长。显示最后 10 行，然后继续显示创建的新条目
- `taskset`: 获取或设置进程的 CPU 亲和性
- `tunelp`: 调整打印机参数
- `ul`: 将下划线转换为指示终端下线的转义序列的过滤器
- `umount`: 从系统树中卸载文件系统
- `unshare`: 与父进程分离某些命名空间运行程序
- `uuidgen`: UUID 库用于生成安全且保证唯一的 UUID 的守护进程
- `wall`: 将文件内容（默认其标准输入）显示在所有当前登录用户的终端上
- `whereis`: 报告给定命令的二进制文件、源码和手册页的位置
- `wipes`: 擦除设备上的文件系统签名
- `write`: 向指定用户发送消息，如果该用户未禁用接收此类消息

## 6.22. Psmisc-22.15

Psmisc 软件包包含了用于显示运行进程信息的程序。

**估算编译时间：** 少于 0.1 SBU
**所需的磁盘空间：** 3.6 MB

### 6.22.1. 安装 Psmisc

为编译 Psmisc 准备：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

此软件包不附带测试套件。

安装软件包：

```
make install
```

最后，将 killall 和 fuser 程序移动到 FHS 指定的位置：

```bash
mv -v /usr/bin/fuser /bin
mv -v /usr/bin/killall /bin
```

### 6.22.2. Psmisc 的内容

**已安装的程序：** fuser, killall, peekfd, prstat, pstree 和 pstreex11（链接到 pstree）

**简要描述**

- **fuser** 报告使用给定文件或文件系统的进程 ID (PID)
- **killall** 通过名称杀死进程；向所有运行任何给定命令的进程发送信号
- **peekfd** 给给定的 PID 查看文件描述符打印
- **prstat** 打印关于进程的信息
- **pstree** 以树的形式显示运行中的进程
- **pstreex11** 与 **pstree** 相同，不同在于它退出前会等待确认

## 6.23. E2fsprogs-1.42

E2fsprogs 软件包包含了处理 ext:2 文件系统的工具。它还支持 ext:3 和 ext:4 日志文件系统。

估算编译时间：0.5 SBU
所需的磁盘空间：45 MB

### 6.23.1. 安装 E2fsprogs

E2fsprogs 文档建议在源码树的子目录中构建软件包：

```bash
mkdir -v build
cd build
```

为编译 E2fsprogs 准备：

```bash
PKG_CONFIG=/tools/bin/true LDFLAGS="-lblklid -luuid" \
../configure --prefix=/usr --with-root-prefix="\
  --enable-elf-shlibs --disable-libklid --disable-luuid \
  --disable-uuuid --disable-fsck
```

配置选项的含义：

```
PKG_CONFIG...
```

这使得 E2fsprogs 可以在不需要先构建和安装 Pkg-config 的情况下构建。

```
--with-root-prefix=""
```

某些程序（例如 efsck 程序）被认为是基本程序。例如，当 /usr 未挂载时，这些程序仍然需要安装。它们属于 /lib 和 /sbin 等目录。如果未在 E2fsprogs 的配置中设置此选项，程序将安装到 /usr 目录。

```
--enable-elf-shlibs
```

这创建了该软件包中某些程序使用的共享库。

```
--disable-*
```

这防止了 E2fsprogs 构建并安装 libuuid 和 libklid 库、uuid 守护进程以及 fsck 包装器，因为 Ut-Linux 已经安装了它们所有内容。

编译软件包：

```
make
```

要测试结果，请执行：

```
make check
```

E2fsprogs 的测试之一将尝试分配 256 MB 内存。如果你的内存没有明显多于此，建议为测试启用足够的交换空间。详情请参见第 2.3 节“在分区上创建文件系统”和第 2.4 节“挂载新分区”有关创建和启用交换空间的说明。

安装二进制文件、文档和共享库：

```
make install
```

# Linux From Scratch - 版本 7.1

安装 install-libs 头文件：

```
make install-libs
```

为了调试目的，可以将已安装的静态库设置为可写，以后可以删除：

```bash
chmod -v uw /usr/lib/{libcom_err,libext2fs,libss}.a
```

此软件包安装一个压缩的 .info 文件但不会更新系统文件。解压此文件并使用以下命令更新系统文件：

```bash
gunzip -v /usr/share/info/libext2fs.info.gz
install-info --dir-file=/usr/share/info/ \
    /usr/share/info/libext2fs.info
```

如果需要，可以使用以下命令创建并安装一些文档：

```bash
makeinfo -o err.info ../lib/etc/com err.texinfo
install -v -m644 doc/com err.info /usr/share/info
--dir-file=/usr/share/info/dir \
    /usr/share/info/com err.info
```

### 6.23. E2fsprogs 的内容

- **已安装的程序：** badblocks, chattr, compile, debugs, dumpe2fs, e2freefrag, e2ck, e2image, e2nitrd_helper, e2label, e2undo, e4cfrag, filefrag, fckext2, fckext3, fckext4, fsckext4dev, lsave, lsatt, mkcd, mkfs, resize2fs, mkfsext2, mkfsext3, mkfsext4, mkfs+root, tune2fs
- **已安装的库：** libcom,[a.so], lib2p:[a.so], libext2fs:[a.so], libiquota.a 和 libss,[a.so], /usr/include/2cp, /usr/include/ct, /usr/include/ext2fs, /usr/include/quota, /usr/include/ss, /usr/share/ct, /usr/share/ss
- **已安装的目录：**

### 简要描述

- **badblocks**: 在设备（通常是磁盘分区）中搜索坏块
- **chattr**: 修改 ext2 文件系统上文件的属性；它也会更改 ext3 文件系统（即 ext2 文件系统的日志版本）
- **compile_et**: 错误编译器；在 C 源文件中创建错误代码名称和消息表，适用于 com err 库使用
- **debugs**: 系统调试器；可用于检查和更改 ext2 文件系统的状态
- **dumpe2fs**: 打印给定设备上文件系统的超级块和组组信息
- **e2freefrag**: 报告空空间碎片信息
- **e2ck**: 用于检查并可选地修复 ext2 文件系统
- **e2image**: 根据给定的 PID 查看文件描述符
- **e2nitrd_helper**: 查看 ext2 文件系统的类型
- **e2label**: 修改 ext2 文件系统的标签
- **e2undo**: 撤销 ext2 文件系统的操作
- **e4cfrag**: ext4 在线碎片整理
- **filefrag**: 报告文件碎片情况
- **fckext2**: 检查 ext2 文件系统
- **fckext3**: 检查 ext3 文件系统
- **fckext4**: 检查 ext4 文件系统
- **fsckext4dev**: 检查 ext4 开发文件系统
- **lsave**: 保存日志到文件
- **lsatt**: 列出文件的属性
- **mkcd**: 创建目录
- **mkfs**: 创建文件系统
- **resize2fs**: 调整 ext2 文件系统分区大小
- **mkfsext2**: 创建 ext2 文件系统
- **mkfsext3**: 创建 ext3 文件系统
- **mkfsext4**: 创建 ext4 文件系统
- **mkfs+root**: 创建带根目录的文件系统
- **tune2fs**: 调整 ext2 系统参数

## 6.24. Coreutils-8.15

Coreutils 软件包包含了显示和设置基本系统特征的工具。

估算编译时间：3.2 SBU
所需的空间：99 MB

### 6.24.1. 安装 Coreutils

此软件包中的 *uname* 程序有一个已知问题，即 -p 始终返回 unknown。以下补丁修复了 Intel 架构的问题：

```bash
case 'uname' -m in
i386 x864) patch -Npl -i ../coreutils-8.15-uname-1.patch ;;
esesac
```

POSIX Coreutils 无法正确识别字符边界。以下补丁修复了不符合标准的问题和其他国际化 bug：

```bash
patch -Npl -i ../coreutils-8.15-i18n-1.patch
```

> 注意
在 patch 中发现了许多 bug。在向 Coreutils 维护者报告新 bug 时，请检查在没有此补丁的情况下是否可以复现。

现在为编译 Coreutils 准备：

```bash
./configure --prefix=/usr \
    --libdir=/usr/lib \
    --enable-no-install-program=kill,uptime
```

配置选项的含义：

```
--enable-no-install-program=kill,uptime
```

此开关的目的是防止 Coreutils 安装稍后会被其他软件包安装的二进制文件。

编译软件包：

```
make
```

如果不运行测试，请跳到“安装软件包”。
现在测试套件已准备就绪。首先，运行要在 root 用户身份运行的测试：

```bash
make NON_ROOT_USERNAME=nobody check-root
```

我们将以 nobody 用户运行剩余测试。然而，某些测试需要用户属于多个组。因此，我们不会跳过这些测试，我们将创建一个临时组并让 nobody 用户成为该组的一部分：

```bash
echo "dummy:x:1000:nobody" >> /etc/group
```

# Linux 实验性 - 版本 7.1

修复部分权限以便非 root 用户可以编译并运行测试：

```bash
chown -R v nobody .
```

现在运行测试：
