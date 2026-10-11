
安装包：

```bash
make install
```

删除无用的静态库：

```bash
rm -fv /usr/lib/libcomm_rer,lib2p,libext2fs,libss.a
```

此包安装了一个经过 gzip 的 `.info` 文件，但不会更新系统级的 dir 文件。使用以下命令解压此文件并更新 dir 文件：

```bash
gunzip -v /usr/share/info/libext2fs.gz
install-info --dir-file=/usr/share/info /usr/share/info/libext2fs.info
```

如果需要，可以通过以下命令创建并安装额外的文档：

```bash
makeinfo -o doc/com_err.texinfo /lib/etc/com_err.texinfo
install -v -m644 doc/com_err.info /usr/share/info/
install-info --dir-file=/usr/share/info/dir /usr/share/info/com_err.info
```

## 8.74. 配置 E2fsprogs

`/etc/mke2fs.conf` 包含了 `mke2fs` 命令行选项的默认值。你可以编辑该文件使默认值适用于你的需求。例如，某些实用程序（在 LFS 或 BLFS 中）无法识别启用了 `metadata_csum_seed` 的 ext4 文件系统。如果你需要此类实用程序，可以使用以下命令从默认 ext4 特性列表中移除该功能：

```bash
sed 's/metadata_csum_seed,///' -i /etc/mke2fs.conf
```

详情请参阅手册页 `mke2fs.conf(5)`。

## 8.74.3. E2fsprogs 的内容

- `已安装的程序：` badblocks, chattr, charm_et, debugfs, dumpefs, e2freefrag, e2fsck, e2image, e2label, e2mpstat, e2scrub, e2scrub_all, e2undo, e4crypt, e4defrag, filefrag, fskext.ext2, fskext.ext3, fskext.ext4, logsave, inattr, mk_mdcs, mke2fs, mkefts.2, mkefts.3, mkefts.4, mkplusfind, resize 以及 tune2fs

- `已安装的库：` libcom_err, lib2bp.so, libext2fs.so, 以及 libss

- `已安装的目录：` `/usr/include`, `/usr/include/`, `/usr/include/ext2fs`, `/usr/include/ss`, `/usr/lib/e2fsprogs`, `/usr/share` 以及 `/usr/share/ss`

## 简要描述

- `badblocks` 设备（通常是磁盘分区）中的坏块

- `chattr` 修改 ext(2) 文件系统上的文件属性

- `charm_et` 一个错误表编译器；它将错误代码名称和消息表转换为适用于 com_err 库的 C 源码

- `debugfs` 一个文件系统调试器；用于检查和更改 ext(2) 文件系统的状态

- `dumpefs` 打印设备上文件系统的超级块和块组信息

- `e2freefrag` 报告空空间碎片信息

- `e2fsck` 用于检查并可选地修复 ext(2) 文件系统

- `e2image` 用于将 ext(2) 文件系统数据保存到文件中

- `e2label` 显示或更改给定设备上 ext(2) 文件系统的标签

- `e2mpstat` 检查 ext4 文件系统的 MPP（多点挂载保护）状态

- `e2scrub` 检查 ext(2) 文件系统的内容

- `e2scrub_all` 检查所有挂载的 ext(2) 文件系统的错误

- `e2undo` 重放设备上 ext(2) 文件系统的撤销日志。[这可以用于撤销由 E2fsprogs 执行失败的操作。]

- `e4crypt` Ext4 文件系统加密

- `e4defrag` ext4 在线碎片整理

- `filefrag` 报告文件可能碎片化的程度

- `fskext.ext2` 默认检查 ext2 文件系统

- `fskext.ext3` 默认检查 ext3 文件系统

- `fskext.ext4` 默认检查 ext4 文件系统

- `logsave` 将命令的输出保存到文件

- `inattr` 节点属性

- `mk_mdcs` 创建 mdisk 设备

- `mke2fs` 创建新的 ext2 Linux 文件系统

- `mkefts.2, mkefts.3, mkefts.4` 创建文件系统表

- `mkplusfind` 在磁盘上查找加块

- `resize` 调整文件系统大小

- `tune2fs` 调整 ext2 文件系统参数

## 8.77. 关于调试符号

大多数程序和库默认情况下在编译时都包含了调试符号（使用 `gcc -g` 选项）。这意味着，当你调试一个编译了调试信息的程序或库时，调试器不仅可以提供内存地址，还可以提供例和变量的名称。

包含这些调试符号会显著增大程序或库的大小。以下是它们所占空间两个两个示例：

- 包含调试符号的 bash 二进制文件：1200 KB

- 不包含调试符号的 bash 二进制文件：480 KB（减小了 60%）

- 包含调试符号的 Glibc 和 GCC 文件（位于 `/lib` 和 `/usr/lib`）：87 MB

- 不包含调试符号符号的 Glibc 和 GCC 文件：16 MB（减小了 82%）

大小取决于使用了哪个编译器和 C 库，差异巨大。剥离了调试符号（stripped）的程序通常比其未剥离的版本小 50% 到 80%。由于大多数用户永远不会在系统软件上使用调试器，通过删除这些符号可以恢复大量的磁盘空间。下一节将展示如何从程序和库中剥离所有调试符号。

## 8.78. 剥离 (Stripping)

本节是可选的。如果目标用户不是程序员且不计划对系统进行任何调试，可以通过从二进制文件和库中移除调试符号以及某些符号表项，将系统大小减少约 2 GB。这对于典型的 Linux 用户不会造成任何实际不便。

大多数使用下述命令的人并不会遇到任何困难。然而，很容易出错并导致系统无法使用。在运行 `strip` 命令之前，最好对当前状态下的 LFS 系统进行备份。

带有 `--strip-needed` 选项的 `strip` 命令会从二进制文件或库中移除所有调试符号。它还会移除链接器（对于静态库）或动态链接器（对于动态链接的二进制文件和共享库）不需要的符号表项。

所选库的调试符号被保留在单独的文件中。在 BLFS 中，使用 `valgrind` 或 `gdb` 进行回归测试时需要调试信息。

注意，`strip` 会覆盖它正在处理的二进制文件或库文件。这可能会导致使用该文件代码或数据的进程崩溃。如果运行 `strip` 的进程处于活动状态，正在剥离的二进制文件或库可能会被破坏；为了避免这个问题，我们将某些库和二进制文件拷贝到 `/tmp`，在那里进行剥离，然后使用此处的 `install` 命令重新安装。（第 8.2.1 节中“升级问题”的相关条目提供了在此处使用 `install` 命令的理由。）

> ELF 加载器在64 位系统上名为 `ld-linux-x86-64.so`，32 位系统名为 `ld-linux.so`。该构造根据当前架构选择正确的名称，排除任何以 "g" 结尾的内容，以防命令已经运行过。

## 重要

如果任何包的版本与书籍指定的版本不同（为了遵循安全公告或满足个人偏好），可能需要更新 `save_usrlib` 或 `online_usrlib` 中的库文件名。未这样做可能会导致系统完全无法使用。

```
save_usrlib=$(cd /usr/lib; ls ld-linux*[*]) nlibc.so.6
libthread-db.so
libquadmath.so.0.0.0
libstdc++.so.6.0.30
libmrt.so.1.0.0
libdatomic.so.1.2.0
```

```
cd /usr/lib
for LIB in $save_usrlib; do
objcopy --only-keep-debug $LIB $LIB.dbg
cp $LIB /tmp/$LIB
strip --strip-unneeded /tmp/$LIB
objcopy --add-gnu-debuglinks $LIB.DBG /tmp/$LIB
install -vm755 /tmp/$LIB /usr/lib
rm /tmp/$LIB
done
```
