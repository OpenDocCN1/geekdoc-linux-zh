
# 10 Linux 启动过程与运行级别

那么，如何找到安装特定文件的软件包？例如，如果 `/etc/krb.conf` 文件以某种方式损坏，你可以用此命令找到它来自哪个软件包：

```
rpm -qf /etc/krb.conf
```

这返回以下输出：

```
krbafs-1.1.1-1
```

**警报**

使用 `-f` 选项需要被查询文件的完整路径和文件名。这就是它在从数据库查询的软件包信息中的列表方式。如果在回答填空题时未包含被查询文件的完整路径，答案将被判为错误。

## 构建 RPMs

对于考试过程而言，构建 RPMs 只需要理解一套步骤。实际的构建 RPMs 过程可能比这里看到的要复杂得多。

系统管理员使用源代码 RPM 并构建自定义 RPM，以获得更好的性能、保证 RPM 文件中的内容、环境的安全性、机器的完整性以及许多其他原因。

一个目录树构成了构建环境，可以在 `/usr/src/redhat` 目录中作为子目录找到。这些包括：

- `BUILD` -- 这是软件包的源代码解压缩并构建软件的地方。
- `RPMs` -- 由构建过程创建的二进制软件包文件将写入此目录。
- `SOURCES` -- 这里包含源代码软件包、任何补丁和修复。
- `SPECS` -- 这里是保存 `.spec` 文件（本质上是美化的 `Makefile`）并从此启动构建的地方。
- `SRPMS` -- 这是存储由构建过程生成的任何源代码软件包的地方。

### 构建中发生了什么？

第一步是下载源代码 `.rpm` 或压缩代码的 tarball。两者的步骤相同，除了源代码 tarball 必须构建一个 `.spec` 文件，而源代码 `.rpm` 包含了所有这些。

如果是源代码 `.rpm`，你安装 `.rpm` 文件（`rpm -i source_pkg.rpm`），这将把源文件放置在 `/usr/src/redhat/SOURCES` 目录中，把 spec 文件放置在 `/usr/src/redhat/SPECS` 目录中。

然后你编辑 `/usr/src/redhat/SPECS/somepkg.spec` 文件以进行所需的任何更改。`.spec` 文件由一组信息和宏、要包含的文件的路径以及软件包作为 `.rpm` 文件安装时的安装说明组成。

这里有一个 `.spec` 文件的示例：

```
############### Preamble of spec file
Summary: a special program to do something.
Name: blah-woof
Version: 0.99
Release: 33
Copyright: GPL
Group: Applications/Special
Source: ftp://ftp.brunson.org/blahwoof.tar.gz
BuildRoot: /var/tmp/blahwoof-root

description
Blah-woof is the greatest program it does everything and nothing

prep
rm -rf $RPM_BUILD_DIR/blah-woof-1.0
tar xzf $RPM_SOURCE_DIR/blah-woof-1.0.tar.gz

build
make

install
rm -rf $RPM_BUILD_ROOT
mkdir -p $RPM_BUILD_ROOT/usr/{bin,man/man1}
make DESTDIR=$RPM_BUILD_ROOT install

clean
rm -rf $RPM_BUILD_ROOT

files

doc README
/usr/bin/blah-woof
/usr/bin/blah.inc
/usr/man/man1/blah-woof

changelog
* Wed 10th of Nov. Some developer <some@uy.int>
- fixed tendency to crash unexpectedly
```

对于用于安装软件包的文件，它必须包含以下部分：

- `Preamble`—摘要和其他显示在软件包信息页查询中的信息。
- `description`—这只是一个描述。
- `prep`—这是源代码 tarball 被解包并处理到构建目录的地方（包括应用的任何补丁）。
- `build`—这是实际构建软件的地方，通常使用 `make` 命令，就像普通软件一样。
- `install`—构成源文件安装的说明，通常是 `make install`。

## 需要理解的关键术语

- 启动过程
- 主引导记录
- 运行级别
- 扇区
- 信号
- 系统初始化

## 需要掌握的技巧

- 理解启动过程
- 启动进入不同的运行级别
- 理解运行级别
- 配置运行级别
- 关闭系统
- 制作启动盘

> 这是 117-102 考试资料的正式开始。

在本章中，我们将讨论 Linux 启动过程、运行级别，以及如何配置系统以正确的级别启动并运行正确的服务。

### Linux 启动过程

Linux 系统的启动步骤在大多数发行版中是相似的，可能只有 Slackware 和 BSD 变体有些不同。在下面的列表中，我将带你了解启动步骤，并提供一些你在该过程中可以使用的考试技巧：

1. 打开系统电源。
2. 基本输入/输出系统 (BIOS) 代码加载，并寻找有效的引导扇区。
3. BIOS 根据查找顺序从软盘、硬盘 (HD) 或 CD-ROM 加载引导扇区。
4. 读取主引导记录 (MBR)；它位于第一个或活动硬盘的第一个扇区的前 512 字节中。
5. 执行任何找到的引导加载程序代码。
6. 如果使用 LILO (Linux Loader)，则显示菜单代码（通常位于 `/boot/boot.b`）。LILO 的提示符在文本模式下为 `lilo:`，或是一个图形菜单选项。
7. 用户选择或输入一个选项，或者引导加载程序超时并开始加载默认条目。
8. 如果你选择了 Linux 映像，则读取加载 Linux 内核的路径，并执行压缩的内核。

   > 如果选择了另一种映像类型，例如双启动 Windows，则读取该分区的前 512 字节以获取 NTLDR 或该操作系统用于启动系统的任何程序。
9. 当 Linux 内核加载时，它初始化设备，加载必要的模块，查找初始 RAM 磁盘 (initrd)，并加载

## 备考题

1. 在从源 tarball 安装软件时，以下哪一步最可能需要用户为 root？（选择最佳答案。）

   - A. `make dep`
   - B. `make clean`
   - C. `make install`
   - D. `make mrproper`

   答案 C 正确，因为 `make install` 操作通常尝试将软件写入仅 root 用户可写的目录。答案 A、B 和 D 是编译软件的正确步骤，但仅访问本地目录，且可由任何用户执行。

2. 在下面的空白处，输入当包在默认的 Red Hat Linux 机器上通过 `rpm -b` 进程构建后，该包放置目录的完整路径：

   正确答案是 `/usr/src/redhat/RPMS/i386`。没有其他替代答案。

3. 以下哪个命令显示了磁盘上软件安装包文件的修订历史？

   - A. `rpm --revision tree-1.2-7.i386.rpm`
   - B. `rpm -qp tree-1.2-7.i386.rpm --changelog`
   - C. `rpm -qc tree-1.2-7.i386.rpm`
   - D. `rpm -qlp tree-1.2-7.i386.rpm --showrev`

   答案 B 正确，因为 `-qp` 和 `--changelog` 选项的组合显示了磁盘上包的变更日志或修订历史。答案 A 错误，因为 `rpm` 命令没有 `--revision` 选项。答案 C 错误，因为没有 `-p` 选项来查询磁盘上的包，而且 `-qc` 也不显示所需的信息。答案 D 错误，因为 `-qlp` 选项显示包中的文件，而不是修订历史，并且 `rpm` 命令没有 `--showrev` 选项。

4. 在下面的空白处，输入由 lccnf 程序在运行并处理机器上所有库文件后生成的文件的完整路径和文件名：

   正确答案是 `/etc/ld.so.cache`。没有其他替代答案。

5. 运行 `ldd` 程序的目的是什么？

   - A. 重建库文件的链接
   - B. 创建库文件的链接
   - C. 显示程序所需的库
   - D. 读取程序的库功能
