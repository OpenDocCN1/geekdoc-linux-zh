
```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

将程序移动到最终预期位置。虽然在这个环境中并非必要，但我们必须这样做，因为某些程序硬编码了位置：

```bash
mv -v $LFS/usr/bin/chroot $LFS/sbin
mkdir -p $LFS/share/man/man8 $LFS/share/man/man8
mv -v $LFS/share/man/man1/chroot.1 $LFS/share/man/man1/
sed -i 's/"8"/'
```

关于此软件包的详情位于第 8.53 节，“Coreutils 的内容”。

## 6.6. Diffutils-3.8

Diffutils 软件包包含了显示文件或目录差异的程序。

预计编译时间：0.2 SBU

所需的磁盘空间：28 MB

### 6.6.1. 安装 Diffutils

为编译准备 Diffutils：

```bash
./configure --prefix=/usr --host=$LFS_T
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.55 节，“Diffutils 的内容”。

## 6.7. File-5.40

File 软件包包含了确定给定文件或文件类型的工具。

预计编译时间：0.2 SBU

所需的磁盘空间：31 MB

### 6.7.1. 安装 File

构建宿主机上的 file 命令需要与我们正在构建的版本相同。运行以下命令进行构建：

```bash
mkdir build
pushd build
  ./configure --disable-bzlib \
  --disable-libccomp \
  --disable-xzlib \
make
pop
```

新 configure 选项的含义：

- --disable-*

配置脚本尝试使用宿主机某些软件包。如果存在库文件但不存在相应的头文件，可能会导致编译失败。这些选项防止使用宿主机不需要的功能。

为编译准备 File：

```bash
./configure --prefix=/usr --host=$LFS_TGT --build=$(./config.guess)
```

编译软件包：

```bash
make FILE_COMPILE=$(pwd) /build/src/file
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.10 节，“File 的内容”。

## 6.8. Findutils-4.8.0

Findutils 软件包包含了查找文件的程序。这些程序用于递归搜索目录树以及创建、维护和搜索数据库（如果最近没有更新数据库，则不可靠）。

预计编译时间：0.2 SBU

所需的磁盘空间：40 MB

### 6.8.1. 安装 Findutils

为编译准备 Findutils：

```bash
./configure --prefix=/usr \
--localstatedir=/var/lib \
--host=$LFS_TGT \
--build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.57 节，“Findutils 的内容”。

## 6.9. Gawk-5.1.0

Gawk 软件包包含了处理文本文件的程序。

预计编译时间：0.2 SBU

所需的磁盘空间：43 MB

### 6.9.1. 安装 Gawk

```bash
sed -i 's/extras//*' Makefile.in
```

为编译准备 Gawk：

```bash
./configure --prefix=/usr \
--host=$LFS_TGT \
--build=$(./config.guess)
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.56 节，“Gawk 的内容”。

## 6.10. Grep-3.7

Grep 软件包包含了搜索文件内容的程序。

预计编译时间：0.2 SBU

所需的磁盘空间：25 MB

### 6.10.1. 安装 Grep

为编译准备 Grep：

```bash
./configure --prefix=/usr \
--host=$LFS_TGT
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.33 节，“Grep 的内容”。

## 6.11. Gzip-1.10

Gzip 软件包包含了压缩和解压缩文件的程序。

预计编译时间：0.1 SBU

所需的磁盘空间：10 MB

### 6.11.1. 安装 Gzip

为编译准备 Gzip：

```bash
./configure --prefix=/usr --host=$LFS_TGT
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.60 节，“Gzip 的内容”。

## 6.12. Make-4.3

Make 软件包包含一个程序，用于从源文件控制包的可执行文件和其他非源文件的生成。

预计编译时间：0.1 SBU

所需磁盘空间：15 MB

### 6.12.1. 安装 Make

为编译准备 Make：

```
./configure --prefix=/usr \
--without-guile \
--host=$LFS_TGT \
--build=$(build-aux/config.guess)
```

新 configure 选项的含义：

- --without-guile

  尽管尽管我们正在进行交叉编译，但如果 configure 在构建宿主机上找到 guise，它会尝试使用它。这会导致编译失败，因此此开关可以防止使用它。

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.64.2 节，“Make 的内容”。

## 6.13. Patch-2.7.6

Patch 软件包包含一个程序，用于通过应用通常由 diff 程序创建的“patch”文件来修改或创建文件。

预计编译时间：0.1 SBU

所需磁盘空间：12 MB

### 6.13.1. 安装 Patch

为编译准备 Patch：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.65.2 节，“Patch 的内容”。

## 6.14. Sed-4.8

Sed 软件包包含一个流编辑器。

预计编译时间：0.1 SBU

所需磁盘空间：20 MB

### 6.14.1. 安装 Sed

为编译准备 Sed：

```
./configure --prefix=/usr \
--host=$LFS_TGT
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.29.2 节，“Sed 的内容”。

## 6.15. Tar-1.34

Tar 软件包提供了创建 tar 存档以及执行各种归档操作的能力。Tar 可用于之前创建的归档以提取文件、存储额外文件，或者更新或列出已存储的文件。

**预计编译时间：** 0.2 SBU

**所需磁盘空间：** 38 MB

### 6.15.1. 安装 Tar

为编译准备 Tar：

```
./configure --prefix=/usr \
  --host=$LFS_TGT \
  --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.66.2 节，“Tar 的内容”。

## 6.16. Xz-5.2.5

Xz 软件包包含压缩和解压缩文件的程序。它提供了对 Lma 和较新的 xz 压缩格式的支持。使用 **xz** 压缩文件得到的压缩率比使用传统的 **gzip** 或 **bzip2** 命令更好。

**预计编译时间：** 0.1 SBU

**所需磁盘空间：** 15 MB

### 6.16.1. 安装 Xz

为编译准备 Xz：

```
./configure --prefix=/usr \
--host=$LFS_TGT \
--build=$(build-aux/config.guess) \
--disable-static \
--docdir=/usr/share/doc/xz-5.2.5
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.8.2 节，“Xz 的内容”。

## 6.17. Binutils-2.37 - Pass 2

Binutils 软件包包含一个链接器、一个汇编器以及处理其他文件的工具。

预计编译时间：1.3 SBU

所需磁盘空间：505 MB

### 6.17.1. 安装 Binutils

再次创建一个独立的构建目录：

```
mkdir -v build
cd build
```

为编译准备 Binutils：

```bash
../configure /\
--prefix=/usr \
--build=$(../config.guess) \
--host=$LFS_TGT \
--disable-nls \
--enable-shared \
--disable-werror \
--enable-64-bit-bfd /
```

新 configure 选项的含义：

- --enable-shared

  将 libbfd 构建为共享库。

- --enable-64-bit-bfd

  启用 64 位支持（在字长位较窄的宿主机上）。在 64 位系统上可能不需要，但并无害处。

编译软件包：

```
make
```

安装软件包，并解决导致 libc.so 链接到宿主机发行版 zlib 的问题：

```
make DESTDIR=$LFS install -j1
install -vm755 libctf./libs/libc.so.0.0.0 $LFS/usr/lib
```

关于该软件包的详细信息位于第 8.8.2 节，“Binutils 的内容”。

## 6.18. GCC-11.2.0 - Pass 2

GCC 软件包包含一个编译器、一个 C++ 编译器以及用于构建的其他工具。

预计编译时间：12 SBU

所需磁盘空间：3.3 GB

### 6.18.1. 安装 GCC

再次创建一个独立的构建目录：

```bash
mkdir -v build
cd build
```

为编译准备 GCC：

```bash
../configure /\
--prefix=/usr \
--build=$(../config.guess) \
--host=$LFS_TGT \
--disable-nls \
--enable-shared \
--disable-werror \
--enable-64-bit-bfd /
```

新 configure 选项的含义：

- --with-sysroot=$LFS

  确保编译器在 $LFS 中查找头文件和库。

- --enable-array

  在构建 GCC 时自动启用。

编译软件包：

```
make
```

安装软件包，并解决导致 libc.so 链接到宿主机发行版 zlib 的问题：

```
make DESTDIR=$LFS install -j1
install -vm755 libctf./libs/libc.so.0.0.0 $LFS/usr/lib
```

关于该软件包的详细信息位于第 8.2.2 节，“GCC 的内容”。

## 6.19. Glibc-2.36

Glibc 软件包包含 GNU C 库，它是 Linux 系统的核心组件。

预计编译时间：2.5 SBU

所需磁盘空间：500 MB

### 6.19.1. 安装 Glibc

为编译准备 Glibc：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.11.2 节，“Glibc 的内容”。

## 6.20. Libcrypt-4.2.3

Libcrypt 软件包包含用于加密和解密的库。

预计编译时间：0.5 SBU

所需磁盘空间：10 MB

### 6.20.1. 安装 Libcrypt

为编译准备 Libcrypt：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.13.2 节，“Libcrypt 的内容”。

## 6.21. Zlib-1.3.1

Zlib 软件包包含用于数据压缩的库。

预计编译时间：0.2 SBU

所需磁盘空间：5 MB

### 6.21.1. 安装 Zlib

为编译准备 Zlib：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.15.2 节，“Zlib 的内容”。

## 6.22. Readline-8.2

Readline 软件包包含用于编辑格式化输入行的库。

预计编译时间：0.3 SBU

所需磁盘空间：5 MB

### 6.22.1. 安装 Readline

为编译准备 Readline：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.17.2 节，“Readline 的内容”。

## 6.23. Ncurses-6.4

Ncurses 软件包包含用于创建终端界面的库。

预计编译时间：0.5 SBU

所需磁盘空间：15 MB

### 6.23.1. 安装 Ncurses

为编译准备 Ncurses：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.19.2 节，“Ncurses 的内容”。

## Chapter 7. Entering Chroot and Building Tools

### 7.1. Introduction

本章介绍了如何构建各个软件包所需的最后工具。现在所有循环依赖已经解决，我们可以使用一个“chroot”环境，除了运行的内核之外，它是完全隔离的。

为了隔离环境的正常运行，必须与运行的内核建立通信。这是通过所谓的内核文件系统实现的，它们在进入 chroot 环境时必须挂载。在第 7.4 节进入 chroot 环境之前，命令必须以 root 身份运行并设置 IFS 变量。进入 chroot 后，所有命令都以 root 身份运行，幸运的是无法访问你构建 LFS 的操作系统。尽管如此，错误的命令很容易破坏系统。

### 7.2. Changing Ownership

> 注意 本书剩余部分必须以 root 用户身份执行。此外，检查 root 环境中的 IFS。

目前，`$IFS` 中的整个目录层次结构由用户 root 所有，该用户仅存在于宿主机系统中。如果 `$IFS` 下的目录和文件夹保持原样，它们将由一个没有相应账户的用户 ID 所有。这是危险的，因为以后创建的用户账户可能会获得相同的用户 ID 并拥有 `$LFS` 下的所有文件。

为了解决这个问题，通过运行以下命令将 `$LFS/*` 目录的所有权更改为用户 root：

```bash
chown -R root:root $IFS/{usr,lib,var,etc,bin,sbin,tools}
case $(uname -m) in
x86_64) chown -R root:root $LFS/lib64 ;;
esac
```
