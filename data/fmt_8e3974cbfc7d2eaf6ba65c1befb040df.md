
```bash
root:bzip2-1.0# mv $LFS/usr/bin/ $LFS/bin
root:bzip2-1.0# cd /
root:bzip2-1.0# ./configure --prefix=/usr --disable-nls
root:bzip2-1.0# make LDFLAGS=$--static
root:bzip2-1.0# make prefix=$LFS/usr install
root:bzip2-1.0# cd $LFS/usr/bin
root:bin# mv bcat bunzip2 bzip2 $LFS/bin
```

### 内容

`Bzip2` 软件包包含 `bzip2`, `bunzip2`, `bzcat` 和 `bziprecover`。

### 描述

`bzip2` 使用 Burrows-Wheeler 排序算法和 Huffman 编码压缩文件。其压缩率通常比更多的 LZ7/LZ8 压缩器更好。

### Bunzip2

`Bunzip2` 解压缩 `Bzip2` 压缩的文件。

### bzcat

`bzcat`（或 `bzip2`）将所有文件解压缩到标准输出。

### bziprecover

`bziprecover` 从损坏的 `bzip2` 中恢复数据。

### cp

`cp` 将文件从一个地方复制到另一个地方。

### dd

`dd` 复制文件（默认从标准输入到标准输出），可以使用用户可选的块大小，并可选地对其进行转换。

### df

`df` 显示包含每个文件名参数的文件系统上可用的磁盘空间。如果没有提供文件名，则显示所有当前挂载文件系统的可用空间。

### ls, dir and vdir

`dir` 和 `vdir` 是 `ls`的不同版本，具有不同的默认输出格式。这些程序列每个文件或目录名称。目录内容按字母排序。对于 `ls`，如果标准输出是终端，文件默认按列列出并垂直排序；否则每行显示一个。对于 `dir`，文件默认按列列出并垂直排序。对于 `vdir`，文件默认以长格式列出。

### dircolors

`dircolors` 输出设置 `LS_COLOR` 环境变量的命令。`LS_COLOR` 变量用于更改 `ls` 及相关工具使用的默认颜色方案。

### du

`du` 显示每个参数以及目录参数的每个子目录使用的磁盘空间。

### install

`install` 复制文件并设置它们的权限模式，如果可能，还会设置它们的所有者和组。

### ln

`ln` 在文件之间创建硬链接或软链接（符号链接）。

### mkdir

`mkdir` 创建给定名称的目录。

### mkfifo

`mkfifo` 为每个给定名称创建 FIFO（先进先出文件）。

### mknod

`mknod` 用指定的文件名创建 FIFO、字符设备文件或块设备文件。

### mv

`mv` 根据给 `mv` 的参数将文件从一个目录移动到另一个目录或重命名文件。

### rm

`rm` 删除文件或目录。

### rmdir

`rmdir` 删除空空目录。

### sync

`sync` 强制将更改的块写入磁盘并更新超级块。

### touch

`touch` 将每个给定文件的访问和修改时间更改为当前时间。不存在的文件将创建空文件。

### 如果必要在普通系统上安装 GCC

为了稍后编译 `Glibc-2.1.3`，你需要安装 `gcc-2.95.2`。虽然 2.8 以上的任何 `GCC` 版本都可以，但 2.95.2 是强烈推荐的版本。`egcs-2.91.x` 也是已知的。如果你没有 `gcc-2.95.x` 或 `egcs-2.95.x`，你需要在编译本章中的 `Glibc` 之前在你的普通系统上安装 `gcc-2.95.2`。

要查找你的系统具有哪个编译器版本，运行以下命令：

```
root:~# gcc --version
```

如果你的 Linux 系统没有安装 `gcc-2.95.x` 或 `egcs-2.91.x`，你现在需要安装。我们不会替换你系统上的当前编译器，但我们将在单独目录 (`/usr/local/gcc2952`) 中安装 `gcc`。这样就不会替换二进制文件或头文件。

在解压 `gcc-2.95.2` 存档后，不要进入新创建的 `gcc-2.95.2` 目录，而是留在 `LFS/usr/src` 目录。运行以下命令安装 `GCC`：

```
root:src# mkdir $LFS/usr/src/gcc-build
root:src# cd $LFS/usr/src/gcc-build
root:gcc-build# ../gcc-2.95.2/configure \
    > --with-local-prefix=dir/usr/local/gcc2952 \
    > --with-gxx-include-dir=/usr/local/gcc2952/include/g++ \
    > --enable-shared --enable-languages=c,c++
root:gcc-build# make bootstrap
root:gcc-build# make install
```

### 内容

`GCC` 软件包包含编译器、预处理器和 GNU C++ 库。

### 描述

如果必要在普通系统上安装 `GCC`

### 编译器

编译器将文本格式的源代码转换为计算机能理解的格式。在源代码被编译成对象文件后，链接器将从一个或多个这些编译器生成的对象文件创建一个可执行文件。

### 预处理器

预处理器对源文件进行预处理，例如将头文件的内容包含到源文件中。你通常不需要自己手动这样做，以节省大量时间。你只需插入一行 `#include <filename>`。预处理器会将该文件的内容插入到源文件中。这是预处理器做的事情之一。

### C++ 库

`C++` 库被 `C++` 程序使用。`C++` 库包含了在 `C++` 程序中频繁使用的函数。这样一来，程序员在每次创建程序时，就不需要从零开始编写某些函数（例如向屏幕写入一段文本）。

### 在 LFS 系统上安装 GCC

在 `LFS` 系统上安装 `GCC`

在解压 `gcc-2.95.2` 存档后，没有进入新创建的 `gcc-2.95.2` 目录，而是留在 `$LFS/usr/src` 目录。运行以下命令安装 `GCC`：

```
root:src# mkdir $LFS/usr/src/gcc-build
root:src# cd $LFS/usr/src/gcc-build
root:gcc-build# ../gcc-2.95.2/configure --prefix=$usr \
    > --with-gxx-include-dir=/usr/local/gcc2952/include/g++ \
    > --enable-shared --enable-languages=c,c++
root:gcc-build# make bootstrap
root:gcc-build# make install
```

### 内容

`GCC` 软件包包含编译器、预处理器和 GNU C++ 库。

### 描述

如果必要在普通系统上安装 `GCC`

### 编译器

编译器将文本格式的源代码转换为计算机能理解的格式。在源代码被编译成对象文件后，链接器将从一个或多个这些编译器生成的对象文件创建一个可执行文件。

### 预处理器

预处理器对源文件进行预处理，例如将头文件的内容包含到源文件中。你通常不需要自己手动这样做，以节省大量时间。你只需插入一行 `#include <filename>`。预处理器会将该文件的内容插入到源文件中。这是预处理器做的事情之一。

### C++ 库

`C++` 库被 `C++` 程序使用。`C++` 库包含了在 `C++` 程序中频繁使用的函数。这样一来，程序员在每次创建程序时，就不需要从零开始编写某些函数（例如向屏幕写入一段文本）。

### 在 LFS 系统上安装 GCC

在 `LFS` 系统上安装 `GCC`

在解压 `gcc-2.95.2` 存档后，没有进入新创建的 `gcc-2.95.2` 目录，而是留在 `$LFS/usr/src` 目录。运行以下命令安装 `GCC`：

```
root:src# mkdir $LFS/usr/src/gcc-build
root:src# cd $LFS/usr/src/gcc-build
root:gcc-build# ../gcc-2.95.2/configure --prefix=$usr
    > --with-gxx-include-dir=/usr/local/gcc2952/include/g++
    > --enable-shared --enable-languages=c,c++
root:gcc-build# make bootstrap
root:gcc-build# make install
```

### 内容

`GCC` 软件包包含编译器、预处理器和 GNU C++ 库。

### 描述

如果必要在普通系统上安装 `GCC`

### 编译器

编译器将文本格式的源代码转换为计算机能理解的格式。在源代码被编译成对象文件后，链接器将从一个或多个这些编译器生成的对象文件创建一个可执行文件。

### 预处理器
