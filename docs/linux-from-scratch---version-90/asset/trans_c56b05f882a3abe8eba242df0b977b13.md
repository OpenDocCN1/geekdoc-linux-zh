

## 6.22. Bzip2-1.0.8

Bzip2 软件包包含了用于压缩和解压缩文件的程序。使用 bzip2 压缩文件得到的压缩率比传统的 gzip 高得多。

**估算编译时间：** 少于 0.1 SBU

**所需的磁盘空间：** 7.7 MB

### 6.22.1. 安装 Bzip2

应用一个补丁，将其安装到此包的文档中：

```
patch -Np1 -i ../bzip2-1.0.8-install_docs-1.patch
```

以下命令确保符号链接的安装是相对路径：

```
sed -i 's@(ln -s -f \$(PREFIX)/bin/@@g' Makefile
```

确保手动页安装到正确的位置：

```
sed -i "s@ (PREFIX)/man@(PREFIX)/share/man@g" Makefile
```

准备 Bzip2 进行编译：

```
make -f Makefile-libbz2_so
make clean
```

`make` 参数的含义：

> -f Makefile-libbz2_so

这将导致 Bzip2 使用不同的 Makefile 文件进行构建，在此情况下为 Makefile-libbz2_so 文件，它会创建一个动态 libbz2.so 库，并将 Bzip2 工具链接到其上。

编译并测试包：

```
make
```

安装程序：

```
make PREFIX=/usr install
```

将共享的 bzip2 二进制文件安装到 /bin 目录，创建一些必要的符号链接并清理：

```
cp -av bzip2-shared /bin/bzip2
cp -sv ../lib/libbz2.so.1.0 /lib/libbz2.so
rm -v /usr/bin/(bzip2,bzcat,bzip22)
ln -sv bzip2 /bin/bzip2
ln -sv bzip2 /bin/bzcat
```

### 6.22.2. Bzip2 的内容

- **已安装的程序：** bzip2（链接到 bzip2）、bzcat（链接到 bzip2）、bzcmp（链接到 bdiff）、bdiff、bzegrep（链接到 bzegrep）、bzfgrep（链接到 bzegrep）、bzgrep、bzip2、bzip2recover、bless（链接到 bzmore）和 bzmore
- **已安装的库：** libbz2.[a,so]
- **已安装的目录：** /usr/share/doc/bzip2-1.0.8

# 简描述

| 程序 | 说明 |
| :--- | :--- |
| bunzip2 | 解压缩 bzipped 文件 |
| bzcat | 解压缩到标准输出 |
| bzcmp | 在 bzipped 文件上运行 **cmp** |
| bzldiff | 在 bzipped 文件上运行 **diff** |
| bzegrep | 在 bzipped 文件上运行 **egrep** |
| bzfgrep | 在 bzipped 文件上运行 **fgrep** |
| bzgrep | 在 bzipped 文件上运行 **grep** |
| bzip2 | 使用 Burrows-Wheeler 块文本压缩算法结合霍夫曼编码压缩文件；其压缩率优于使用“Lempel-Ziv”算法的更多压缩器，如 **gzip** |
| bzip2recover | 尝试从损坏的 bzipped 文件中恢复数据 |
| bzless | 在 bzipped 文件上运行 **less** |
| bzmore | 在 bzipped 文件上运行 **more** |
| libbz2 | 使用 Burrows-Wheeler 算法实现无损块排序数据压缩的库 |

## 6.23. Pkg-config-0.29.2

Pkg-config 软件包包含一个工具，用于执行 configure 和 make 文件期间将包含路径和/或库路径传递给构建工具。

**估算编译时间：** 0.4 SBU
**所需的磁盘空间：** 30 MB

### 6.23.1. 安装 Pkg-config

准备 Pkg-config 进行编译：

```
./configure --prefix=/usr \
    --with-internal-glib \
    --disable-host-tool \
    --docdir=/usr/share/doc/pkg-config-0.29.2
```

新的 configure 选项的含义：

- --with-internal-glib
这将允许 pkg-config 使用其内部版本的 Glib，因为 LFS 中没有可用的外部版本。
- --disable-host-tool
此选项禁用了对 pkg-config 程序创建不必要的硬链接。

编译包：

```
make
```

要测试结果，请执行：

```
make check
```

安装包：

```
make install
```

### 6.23.2. Pkg-config 的内容

- **已安装的程序：** pkg-config
- **已安装的目录：** /usr/share/doc/pkg-config-0.29.2

# 简描述

**pkg-config** 返回指定库或包的元信息

## 6.24. Nurses-6.1

Nurses 软件包包含了用于处理终端无关的字符屏幕的库。

估算编译时间：0.4 SBU
所需的磁盘空间：42 MB

### 6.24.1. 安装 Nurses

不要安装未由 configure 处理的静态库：

```
sed -i '/LIBTOOL_INSTALL/d' c++/Makefile.in
```

准备 Nurses 进行编译：

```
./configure --prefix=/usr \
    --mandir=/usr/share/man \
    --with-shared \
    --without-debug \
    --without-normal \
    --enable-pc-files \
    --enable-wide
```

新的 configure 选项的含义：

- --enable-wide
这将切换为构建宽字符库（例如 libncursesw.so.6.1）而不是普通库（例如 libncurses.so.6.1）。这些宽字符库可以在多字节和传统的 8 位本地化（locale）中使用，而普通库在 8 位本地化中可以正常工作。宽字符库和普通库在源码上是兼容的，但在二进制上是不兼容的。
- --enable-pc-files
此开关将为 pkg-config 生成并安装 .pc 文件。
- --without-normal
此开关将禁用的构建和安装大多数静态库。

编译包：

```
make
```

该包带一个测试套件，但它只能在包安装后才能运行。测试用例位于 `test/` 目录中。更多详细信息请参阅该目录下的 `README` 文件。

安装包：

```
make install
```

将共享库移动到 /lib 目录，它们被预期驻留那里：

```
mv -v /usr/lib/libncursesw.so.* /lib
```

由于库已被移动，有一个符号链接指向一个不存在的文件。重新创建它：

```
ln -sfv ../../lib/$(readlink /usr/lib/libncursesw.so) /usr/lib/libncurses.so
```

Linux From Scratch - Version 9.0

许多应用程序期望链接器能够找到非宽字符的 Ncurses 库。通过符号链接和链接器脚本欺骗此类应用程序链接到宽字符库：

```
for lib in ncurses menu ; do
  rm -vf /usr/lib/lib${lib}.so
  echo "INPUT-${lib}w" > /usr/lib/lib${lib}.so
  ln -sfn ${lib}w.pc /usr/lib/pkgconfig/${lib}.pc
done
```

最后，确保在构建时使用 -lcurses 的旧应用程序是可构建的：

```
rm -vf /usr/lib/libncurses.so
echo "INPUT-ncursesw" > /usr/lib/libncurses.so
ln -sfv libncursesw.so /usr/lib/libncurses.so
```

如果需要，安装 Ncurses 文档：

```
mkdir -p /usr/share/man
cp -rv doc/* /usr/share/man
```

### 6.24.2. Nurses 的内容

- **已安装的程序：** captoinfo（链接到 tic）、clear、infocmp、intofac（链接到 tic）、ncursesw6-reset（链接到 tset）、tabs、tic、toip 和 tost
- **已安装的库：** libcurses.so（指向 libncurses.so 的符号链接和链接脚本）、libform.so、libmenew.so
- tic：terminfo 条目描述编译器，将 terminfo 文件从源格式转换为 ncurses 库所需的二进制格式
- toe：列出所有可用的终端类型，给出每个类型的主要名称和描述
- **已安装的目录：** /usr/share/tabset, /usr/share/terminfo 和 /usr/share/doc/ncurses-6.1

