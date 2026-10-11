
`aclocal` 程序会根据 `configure.in` 的内容自动生成 `aclocal.m4` 文件。这提供了一种获取 `Automake` 提供的宏的方便方法，无需四处寻找。此外，`aclocal` 机制是可的，可供其他包使用。

## automake

要为包创建所有的 `Makefile.in`，在顶目录下运行 `automake` 程序。不带任何参数时，`automake` 将自动找到每个合适的 `Makefile.am`（通过扫描 `configure.in`）并生成相应的 `Makefile.in`。

## 安装 Bash

### Bash 的安装

运行以下命令安装 Bash：

```
root:bash-2.04# ./configure --prefix=/usr --with-ncurses
root:bash-2.04# make
root:bash-2.04# make install
root:bash-2.04# logout
root:lfs# mv $LFS/usr/bin/bash $LFS/bin
root:lfs# chroot $LFS env -i HOME=/root bash --login
```

### 目录

Bash 软件包包含 `bash` 程序

### 描述

Bourne-Again Shell 是 Unix 系统上广泛使用的命令解释器。`Bash` 是一个从标准输入（键盘）读取的程序。你输入内容，程序将评估你输入的内容并对其进行处理，例如运行一个程序。

## 安装 Flex

### Flex 的安装

运行以下命令安装 Flex：

```
root:flex-2.34# ./configure --prefix=/usr
root:flex-2.34# make
root:flex-2.34# make install
```

### 目录

Flex 软件包包含 `flex`

### 描述

#### flex

Flex 是一个词法分析器生成器。用于识别文本中的模式。

## 安装 File

### File 的安装

运行以下命令安装 File：

```
root:file-3.31# ./configure --prefix=/usr
root:file-3.31# make
root:file-3.31# make install
```

### 目录

File 软件包包含 `file` 程序

### 描述

#### file

File 对文件进行分类。有三组测试，执行顺序为：文件系统、魔数、语言。

## 安装 Libtool

### Libtool 的安装

运行以下命令安装 Libtool：

```
root:libtool-2.4# ./configure --prefix=/usr
root:libtool-2.4# make
root:libtool-2.4# make install
```

### 目录

Libtool 软件包包含 `libtool` 和 `toolize` 程序。它包含 `ldl`。

### 描述

#### libtool

Libtool 提供通用的库构建服务。

#### toolize

toolize 提供了一种标准方法为你的包添加 libtool 支持。

#### ldl

Libtool 提供了一个名为 `libtool` 的小型库，旨在解决用户的各种困难。

## 安装 Bin86

### Bin86 的安装

运行以下命令安装 Bin86：

```
root:bin86# make
root:bin86# PREFIX=/usr
```

### 目录

Bin86 包含 `as86`, `as86_encap`, `ld86`, `objdump86`, `nm86` 和 `size86` 程序。

### 描述

#### as86

`as86` 是适用于 886-386 处理器的汇编器。

#### as86_encap

`as86_encap` 是一个 shell 脚本，调用 `as86` 将生成的二进制转换为 C 文件，以便包含或与其他程序链接。

#### ld86

`ld86` 仅理解 `as86` 汇编器产生的文件，它可以将其链接成非纯或独立的执行文件。

#### objdump86

无描述。

#### nm86

无描述。

#### size86

无描述。

## 安装 Binutils

### Binutils 的安装

运行以下命令安装 Binutils：

```
root:binutils-2.10# ./configure --prefix=/usr --enable-shared
root:binutils-2.10# make -e tooldir=/usr
root:binutils-2.10# make -e tooldir=/usr install
```

### 描述

Binutils 软件包包含 `ld`, `ar`, `nm`, `objcopy`, `objdump`, `ranlib`, `size`, `strings`, `strip`, `c++fitt`, `addr2line` 和 `nlmconv` 程序

#### ld

`ld` 连接多个对象文件和归档，重定位它们的数据并连接符号引用。

#### as

`as` 主要用于汇编 GNU C 编译器 `gcc` 的输出，供链接器 `ld` 使用。

#### ar

`ar` 程序创建、修改和提取归档。归档是一个包含其他文件的单个文件，其结构使得能够检索原始单个文件（称为归档成员）。

#### nm

`nm` 列出对象文件中的符号。

#### objcopy

`objcopy` 工具将一个对象文件的内容复制到另一个文件中。`objcopy` 使用 GNU BFD 库来读取和写入对象文件。它可以以不同于源对象文件的格式写入目标对象文件。

#### objdump

`objdump` 显示一个或多个对象文件的信息。选项用于控制显示哪些特定信息。这些信息对于正在编写编译工具的程序员来说最有用，而对于只想让自己的程序编译并运行的程序员来说则不然。

#### ranlib

`ranlib` 生成归文件内容的索引并将其存储在归文件中。该索引列出了归文件中每个作为可重定位对象文件的成员所定义的每个符号。

#### size

`size` 列出其列表中每个对象文件（objfile）的节段大小以及总大小。默认情况下，每个对象文件或归档中的每个模块都会生成一行输出。

#### strings

对于每个文件，`strings` 会打印长度至少为 4 个字符（或程序选项指定的数字）且后跟一个不可打印字符的可打印字符序列。默认情况下，它只打印对象文件中已初始化和加载段的字符串；对于其他类型的文件，它会打印整个文件的字符串。

`strings` 主要用于确定非文本文件的内容。

#### strip

`strip` 从对象文件中丢弃所有或特定的符号。对象文件列表可能包含归文件。必须至少给出一个对象文件。`strip` 修改参数中指定的文件，而不是以不同的名称写入修改后的副本。

#### C++filt

C++ 语言提供了函数重载，这意味着你可以编写同名的函数（只需每个函数带有不同类型的参数）。所有 C++ 函数名都被编码为低级汇编标签（此过程称为修饰/mangling）。`c++filt` 程序执行反向映射：它将低级名称解码（去修饰）为用户级名称，以便链接器防止这些重载函数发生冲突。

#### addr2line

`addr2line` 将程序地址转换为文件名和行号。给定一个地址和一个可执行文件，它使用可执行文件中的调试信息确定与给定地址相关的文件和行号。

#### nlmconv

`nlmconv` 将可重定位对象文件转换为 NetWare 可加载模块（NLM）文件，可选地读取头文件以获取 NLM 头信息。

## 安装 Bzip2

### 安装 Bzip2

运行以下命令安装 Bzip2：

```
root:bzip2-1.0.1# make -f Makefile-libbzz2_so
root:bzip2-1.0.1# make bzip2recover libbz2.a
root:bzip2-1.0.1# cp bzip2-shared /bin/bzip2
root:bzip2-1.0.1# cp bzip2recover /bin
root:bzip2-1.0.1# cp bzip2.1 /usr/share/man/man1
root:bzip2-1.0.1# cp bzlib.h /usr/include
root:bzip2-1.0.1# cp -a libbz2.so* libbz2.a /lib
root:bzip2-1.0.1# rm /usr/lib/libbz2.a
root:bzip2-1.0.1# cd /bin
root# rm bunzip2 && ln -s bzip2 bunzip2
root# rm bzcat && ln -s bzip2 bzcat
root# cd /usr/share/man/man1
man1# ln -s bzip2.1 bzip2.1
man1# ln -s bzip2.1 bzcat.1
man1# ln -s bzip2.1 bzip2-recover
```
