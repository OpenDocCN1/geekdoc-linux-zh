
```
./configure --prefix=/tools --enable-install-hostname
```

`configure` 选项的含义：

```
--enable-install-hostname
```

这启用了 `hostname` 的构建和安装。

编译该包：

```
make
```

编译现在完成。如前所述，对于本章中的临时工具，并非强制运行测试套件。如果仍要运行 Coreutils 测试套件，请执行以下命令：

```
make EXPENSIVE_TESTS=yes
```

安装该包：

```
make install
```

此包的详情见第 6.54.2 节，“内容”。

## 5.20. Diffutils-3.7

Diffutils 包包含显示文件或目录差异的程序。

预计编译时间：0.2 SBU

所需磁盘空间：26 MB

### 5.20.1. 安装 Diffutils

为编译 Diffutils 准备：

```
./configure --prefix=/tools
```

编译该包：

```
make
```

要测试结果，执行：

```
make check
```

安装该包：

```
make install
```

此包的详情见第 6.56.2 节，“Diffutils 的内容”。

## 5.21. File-53

File 包包含一个确定给定文件或多个文件类型的工具。

预计编译时间：0.1 SBU

所需磁盘空间：19 MB

### 5.21.1. 安装 File

为编译 File 准备：

```
./configure --prefix=/tools
```

编译该包：

```
make
```

编译现在完成。如前所述，对于本章中的临时工具，并非强制运行测试套件。如果仍要运行 File 测试套件，请执行以下命令：

```
make check
```

安装该包：

```
make install
```

此包的详情见第 6.12.2 节，“File 的内容”。

## 5.22. Findutils-4.6.0

Findutils 包包含查找文件的程序。这些程序通过递归搜索目录树来创建、维护和搜索数据库（通常比递归的 find 快，但如果数据库没有最近更新，则不可靠）。

预计编译时间：0.3 SBU

所需磁盘空间：36 MB

### 5.22.1. 安装 Findutils

首先，进行 glibc-2.28 需要的一些修复：

```
sed -i '/s/O_ftrylockfile/IO_OF_SEEN/' gl/lib/*.c
sed -i '/unistd/s #include <sys/sysmacros.h>' gl/lib/mountlist.c
echo "#define IO_IN_BACKUP 0x100" >> gl/lib/stdio-impl.h
```

为编译 Findutils 准备：

```
./configure --prefix=/tools
```

编译该包：

```
make
```

编译现在完成。如前所述，对于本章中的临时工具，并非强制运行测试套件。如果仍要运行 Findutils 测试套件，请执行以下命令：

```
make check
```

安装该包：

```
make install
```

此包的详情见第 6.58.2 节，“Findutils 的内容”。

## 5.23. Gawk-5.0.1

Gawk 软件包包含了用于处理文本文件的程序。

预计编译时间：0.2 SBU

所需磁盘空间：46 MB

### 5.23.1. 安装 Gawk

为编译 Gawk 做准备：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现已完成。如前所述，对于本章中的临时工具来说，运行测试套件并非强制性的。如果仍要运行 Gawk 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息位于第 6.57.2 节，“Gawk 的内容”。

## 5.24. Gettext-0.20.1

Gettext 软件包包含了用于国际化和本地化的工具。这些工具允许程序在带有 NLS（原生语言支持）的情况下进行编译，使其能够以用户的母语言输出消息。

- 预计编译时间：1.8 SBU
- 所需磁盘空间：300 MB

### 5.24.1. 安装 Gettext

对于我们的临时工具集，我们只需要从 Gettext 中安装三个程序。

为编译 Gettext 做准备：

```
./configure --disable-shared
```

配置 选项的含义：

`--disable-shared`

我们目前不需要安装任何共享的 Gettext 库，因此没有必要构建它们。

编译软件包：

```
make
```

由于环境限制，不建议在此阶段运行测试套件。

安装 `msgfmt`、`msgmerge` 和 `xgettext` 程序：

```
cp -v gettext-tools/src/{msgfmt,msgmerge,xgettext} /tools/bin
```

关于该软件包的详细信息位于第 64.72 节，“Gettext 的内容”。

## 5.25. Grep-3.3

Grep 软件包包含了用于搜索搜索的程序。

预计编译时间：0.2 SBU

所需磁盘空间：24 MB

### 5.25.1. 安装 Grep

为编译 Grep 做准备：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现已完成。如前所述，对于本章中的临时工具来说，运行测试套件并非强制性的。如果仍要运行 Grep 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息位于第 6.33.2 节，“Grep 的内容”。

## 5.26. Gzip-1.10

Gzip 软件包包含了用于压缩和解压文件的程序。

预计编译时间：0.1 SBU

所需磁盘空间：10 MB

### 5.26.1. 安装 Gzip

为编译 Gzip 做准备：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现已完成。如前所述，对于本章中的临时工具来说，运行测试套件并非强制性的。如果仍要运行 Gzip 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息位于第 6.62.2 节，“Gzip 的内容”。

## 5.27. Make-4.2.1

Make 软件包包含了用于编译软件包的程序。

预计编译时间：0.1 SBU

所需磁盘空间：13 MB

### 5.27.1. 安装 Make

首先，解决由 glibc-2.27 及更高版本引起的错误：

```
sed -i '221,217 d; 219,229 d; 232 d' glob/glob.c
```

为编译 Make 做准备：

```
./configure --prefix=/tools --without-guile
```

`without` 选项的含义：

`--without-guile`

这确保 `Make-4.2.1` 不会链接 Guile 库，这些库可能存在于主机系统上，但在下一章的 chroot 环境中不可用。

编译软件包：

```
make
```

编译现已完成。如前所述，对于本章中的临时工具来说，运行测试套件并非强制性的。如果仍要运行 Make 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息位于第 66.66.2 节，“Make 的内容”。

## 5.28. Patch-2.7.6

Patch 软件包包含了通过应用通常由 diff 程序创建的“patch”文件来修改或创建文件的程序。

预计编译时间：0.2 SBU

所需磁盘空间：13 MB

### 5.28.1. 安装 Patch

为编译 Patch 做准备：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现已完成。如前所述，对于本章中的临时工具来说，运行测试套件并非强制性的。如果仍要运行 Patch 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息位于第 6.67.2 节，“Patch 的内容”。

## 5.29. Perl-5.30.0

Perl 软件包包含了“实用提取与报告语言”（Practical Extraction and Report Language）。

预计编译时间：1.6 SBU

所需磁盘空间：275 MB

### 5.29.1. 安装 Perl
