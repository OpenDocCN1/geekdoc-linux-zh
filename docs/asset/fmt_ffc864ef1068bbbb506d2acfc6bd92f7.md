
构建主机上的 `file` 命令需要与我们正在构建的版本相同，以便创建签名文件。运行以下命令来制作 `file` 命令的临时副本：

```
mkdir build
pushd build
./configure --disable-zlib \
               --disable-libseccomp \
               --disable-zlib \
               --disable-zlib \

make
popd
```

新 configure 选项的含义含义：

```
--disable-zlib*
```

配置脚本尝试使用宿主机上的某些文件。如果存在这些文件，会导致编译失败。为了这些宿主机上的文件。

为编译准备 File：

```
./configure --prefix=/usr --host=$LFS
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS
```

关于此软件包的详情位于第 8.28.2 节，“File 的内容”。

## 6.8. Findutils-4.9

Findutils 软件包包含在构建机器上运行的新构建 tic 程序的路径，这样就可以无错误地创建终端数据库。搜索文件。

预计构建时间：0.2 SBU

所需磁盘空间：42 MB

### 6.8.1. 安装 Findutils

为编译准备 Findutils：

```
./configure --prefix=/usr \
--host=$LFS \
--build=$(config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

## 6.9. Gawk-5.2

Gawk 软件包包含处理文本。

预计构建时间：0.1 SBU

所需磁盘空间：47 MB

### 6.9.1. 安装 Gawk

首先，修复一个上游发现的问题：

```
sed -e '/$ldef SIGPIPE,+2 d' \
-e '/$undef FATAL_SIG/i FATAL_SIG(SIGPIPE);' \
-i src/main.c
```

为编译准备 Gawk：

```
./configure --prefix=/usr \
--without-guile \
--host=$LFS_TGT \
--build=$(config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

## 6.10. Grep-3.8

Grep 软件包包含搜索文件内容的程序。

预计构建时间：0.2 SBU

所需磁盘空间：25 MB

### 6.10.1. 安装 Grep

为编译准备 Grep：

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

## 6.11. Gzip-1.12

G 软件包包含压缩和解压缩文件的程序。

预计构建时间：0.1 SBU

所需磁盘空间：11 MB

### 6.11.1. 安装 Gzip

为编译准备 Gzip：

```
./configure --prefix=/usr --host=$LFS_TGT
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

## 6.12. Make-4.4

Make 软件包包含一个从源文件生成可执行文件和其他源文件的程序。

预计构建时间：少于0.1 SBU

所需磁盘空间：15 MB

### 6.12.1. 安装 Make

尽管我们正在交叉编译，但 `configure` 会尝试在发现宿主机 `guile` 时使用它。这会导致编译失败，因此此开关防止使用它。

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

## 6.13. Patch-2.7.6

Patch 包包含一个通过应用“patch”文件（通常由 `diff` 程序创建）来修改或创建文件的程序。

近似编译时间：0.1 SBU

所需的磁盘空间：12 MB

### 6.13.1. 安装 Patch

为编译准备 Patch --prefix=/usr：

```
./.configure --prefix=/usr \
--host=$TGT \
--build=$(build-aux/config/config.guess)
```

编译该包：

```
make
```

安装该包：

```
make DESTDIR=$LFS install
```

关于此包的详尽信息请参见第 8.66.2 节，“Patch 的内容”。

## 6.14. Sed-4.9

Sed 包包含一个流编辑器。

近似编译时间：0.2 SBU

所需的磁盘空间：19 MB

### 6.14.1. 安装 Sed

为编译准备 Sed：

```
./configure --prefix=/usr \
--host=$LFS_TGT
```

编译该包：

```
make
```

安装该包：

```
make DESTDIR=$LFS install
```

关于此包的详尽信息请参见第 8.29.2 节，“Sed 的内容”。

## 6.15. Tar-1.34

Tar 包提供了创建 tar 归包以及执行其他各种归档操作的能力。Tar 可用于之前创建的归包以提取文件、存储额外文件，或者更新或列出已存储的文件。

近似编译时间：0.1 SBU

所需的磁盘空间：38 MB

### 6.15.1. 安装 Tar

为编译准备 Tar：

```
./configure --prefix=/usr \
  --host=$LFS_TGT \
  --build=$(build-aux/config.guess)
```

编译该包：

```
make
```

安装该包：

```
make DESTDIR=$LFS install
```

关于此包的详尽信息请参见第 8.67.2 节，“Tar 的内容”。

## 6.16. Xz-5.4.1

Xz 包包含用于压缩和解压缩文件的程序。它提供了对 lzma 和更新的 xz 压缩格式的支持。使用 xz 压缩文本文件的压缩率比使用传统的 gzip 或 bzip2 命令更高。

近似编译时间：0.1 SBU

所需的磁盘空间：20 MB

### 6.16.1. 安装 Xz

为编译准备 Xz：

```
./configure --prefix=/usr \
  --host=$LFS_TGT \
  --build=$(build-aux/config.guess) \
  --disable-static \
  --docdir=/usr/share/doc/xz-5.4.1
```

编译该包：

```
make
```

安装该包：

```
make DESTDIR=$LFS install
```

删除 libtool 存档文件，因为它对交叉编译是有害的：

```
rm -v $LFS/usr/lib/liblzma.la
```

关于此包的详尽信息请参见第 8.8.2 节，“Xz 的内容”。

## 6.17. Binutils-2.40 - 第二轮编译

Binutils 包包含链接器、汇编器以及其他处理对象文件的工具。

近似编译时间：0.4 SBU

所需的磁盘空间：525 MB

### 6.17.1. 安装 Binutils

Binutils 的 tar 包中包含一个过时的 libtool 副本。它缺少 sysroot 支持，因此生成的二进制文件将错误地链接到来自主机发行版的库。解决此问题：

```
sed '609s/$add_dir///' -i lmain.sh
```

创建一个单独构建目录：

```
mkdir -v build
cd build
```

为编译准备 Binutils：

```
./configure \
  --prefix=$(../config.guess) \
  --build=$LFS_TLS \
  --host=$LFS_TLS \
  --disable-nls \
  --enable-shared \
  --enable-gocf=no \
  --disable-werror \
  --enable-64-bit-bfd
```

新配置选项的含义：

- `--enable-libbfd`: 将 libbfd 构建为共享库。
- `--enable-64-bit-bfd`: 启用 64 位支持（针对字长较小的主机）。这在 64 位系统上可能不需要，但并无大碍。

编译该包：

```
make
```

安装该包：

```
make DESTDIR=$LFS install
```
