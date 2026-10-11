
你从树的底部开始，遇到数字 2 和 3，它们由乘法符号连接，因此计算机将 2 乘以 3。该乘法的结果被记录下来，计算机看到的下一个内容是 `2*3` 的结果和数字 1，它们由加号符号连接。在之前的结果基础上加上 1 得到 7。在计算时，最复杂的计算可以拆分为这种树状格式，计算机只需从底部开始逐向上工作，即可得到正确答案。当然，Bison 不仅用于计算器。

## 安装 Mawk

Mawk 的安装

运行以下命令安装 Mawk：

```
root:mawk-1.3.3# ./configure
root:mawk-1.3.3# make
root:mawk-1.3.3# make BINDIR=/usr/bin \
> MANDIR=/usr/share/man/man1 install
root:mawk-1.3.3# cd /usr/bin
root:bin# ln -s mawk awk
```

### 目录

Mawk 软件包包含 `mawk` 程序。

### 描述

`gawk`

Mawk 是 AWK 编程语言的解释器。AWK 语言用于数据文件的操作、文本检索与处理，以及算法的原型设计和实验。

## 安装 Patch

Patch 的安装

运行以下命令安装 Patch：

```
root:patch-2.5.4# ./configure --prefix=/usr
root:patch-2.5.4# make
root:patch-2.5.4# make install
```

### 目录

Patch 软件包包含 `patch` 程序。

### 描述

`patch` 程序根据补文件修改文件。补文件通常由 `diff` 程序创建的列表，包含了关于如何修改原始文件的指令。Patch 经常用于源码补丁，因为它节省了时间和空间。假设你有一个 1MB 大小的软件包包。该包的下一个版本仅对第一个版本中的两个文件进行了更改。你可以发送一个全新的 1MB 软件包，也可以提供一个 1KB 的补丁文件，它会将第一个版本更新为与第二个版本完全相同。因此，如果你已经下载了第一个版本，补丁文件可以节省你第二次下载的时间。

## 安装 Findutils

安装 Findutils

众所该软件包会导致编译问题。如果你在编译此软件包时也遇到问题，该软件包已知会导致编译问题。通过运行以下命令应用此补丁：

```
root:findutils-4.1# patch -N ../terminfo
```

运行以下命令安装 Findutils：

```
root:findutils-4.1# ./configure --prefix=/usr
root:findutils-4.1# make
root:findutils-4.1# make install
```

### 目录

Findutils 软件包包含 `find`, `locate`, `updatedb` 和 `xargs` 程序。

### 描述

#### Find

`find` 程序在目录中搜索符合标准的文件。如果没有给出任何标准，它将列出所有文件和子目录。

#### Locate

`Locate` 扫描包含所有文件和目录的数据库。该程序告诉你文件所在的位置。只有当你的 locate 数据库是最新的时，这才有意义。

#### Updatedb

`updatedb` 程序更新 locate 数据库。它扫描整个文件系统（包括当前挂载的文件系统），并将找到的每个文件放入 locate 程序使用的数据库中。每天更新一次数据库是一个好习惯，可以确保你获得最新的信息。

#### Xargs

`xargs` 命令将命令应用于文件列表。如果你需要对多个文件执行相同的命令，可以创建一个包含这些文件的文件（每行一个），并使用 `xargs` 执行该命令。

## 安装 Ncurses

Ncurses 的安装

运行以下命令安装 Ncurses：

```
root:ncurses-5.1# ./configure --prefix=/usr --libdir=/lib \
> --with-shared --disable-termcap
root:ncurses-5.1# make
root:ncurses-5.1# make install
```

### 目录

Ncurses 软件包包含 `ncurses`, `panel`, `menu` 和 `form` 库。它包含 `tic`, `infocmp`, `clear`, `tput`, `toe` 和 `tset` 程序。

### 描述

#### 库

构成 Ncurses 库的库用于在屏幕上显示文本（通常以华丽的方式）。使用 ncurses 的示例是内核的 `"make menuconfig"` 过程。库包含了创建面板、菜单、表单和通用文本显示的程序。

#### Tic

`Tic` 是 `terminfo` 编译器。该程序将源格式的 `terminfo` 文件转换为二进制格式供 ncurses 库程序使用。终端 文件包含有关终端能力的信息。

#### Infocmp

`infocmp` 程序用于比较二进制 `terminfo` 条与其他 `terminfo` 条目。

#### clear

`clear` 程序在可能的情况下清除屏幕。它查看环境变量中的终端类型，然后查询 `terminfo` 数据库确定如何清屏。

#### tput

`tput` 程序使用 `terminfo` 数据库将终端相关的能力和信息提供给 shell，初始化或重置终端，或返回请求的终端类型的全名。

#### toe

`toe` 程序按主名称列出所有可用终端类型及其描述。

#### tset

`Tset` 程序初始化终端以便使用，但它不再被广泛使用。它是为了 4.4BSD 的兼容性而提供的。

## 安装 Less

Less 的安装

运行以下命令安装 Less：

```
root:less-358# ./configure --prefix=/usr
root:less-358# make
root:less-358# make install
root:less-358# mv /usr/bin/less /bin
```

### 目录

Less 软件包包含 `less` 程序

### 描述

`less` 程序是一个文件分页器（或文本查看器）。它能够显示文件内容并支持滚动。Less 是对名为“more”的常用分页器的改进。Less 还具有反向滚动文件的能力，并且在启动时不需要读取整个文件，这使得在阅读大文件时速度更快。

## 安装 Groff

Groff 的安装

运行以下命令安装 Groff：

```
root:groff-1.16# ./configure --prefix=/usr
root:groff-1.16# make
root:groff-1.16# make install
```

### 目录

Groff 软件包包含 `addftinfo`, `afmtodit`, `eqn`, `grodvi`, `groff`, `grog`, `grohtml`, `grolj4`, `grops`, `grotty`, `hpftotid`, `indxbib`, `lkbib`, `lookbib`, `neqn`, `nroff`, `pfbtops`, `pic`, `psbb`, `refer`, `soelim`, `tbl`, `tfmtodit` 和 `troff` 程序。

### 描述

#### addftinfo

`addftinfo` 读取 `troff` 字体文件，并添加 `groff` 系统使用的某些额外字体度量信息。

#### afmtodit

`afmtodit` 创建一个供 `groff` 和 `grops` 使用的字体文件。

#### eqn

`eqn` 将嵌入 `troff` 输入文件中的方程描述编译为 `troff` 可理解的命令。

#### grodvi

`grodvi` 是 `groff` 的驱动程序，产生 TeX `dvi` 格式。

#### groff

`groff` 是 `groff` 文档格式化系统的前端。通常它会运行 `troff` 程序以及适用于所选设备的后处理器。

#### grog

`grog` 读取文件并猜测打印文件所需的 `groff` 选项（`-e`, `-man`, `-me`, `-mm`, `-ms`, `-p`, `-s` 和 `-t`），并将包含这些选项的 `groff` 命令打印到标准输出。

#### grohtml

`grohtml` 将 GNU `troff` 的输出转换为 `html`。

#### grolj4

`grolj4` 是 `groff` 的驱动程序，产生适用于 HP Laserjet 4 打印机的 PCL5 格式输出。

#### grops

`grops` 将 GNU `troff` 的输出转换为 PostScript。

#### grotty

`grotty` 将 GNU `troff` 的输出转换为适用于打字机类设备的格式。

#### hpftodit

`hpftodit` 从 HP 标记字体度量文件中创建一个供 `groff -Tlj4` 使用的字体文件。

#### indxbib

`indxbib` 为参考文献数据库创建一个倒索引，供 `refer`, `lookbib` 和 `Ikbib` 使用。

# Linux From Scratch

#### lkbib

`lkbib` 在参考文献数据库中搜索包含指定的引用，并将找到的所有引用打印到标准输出。

#### lookbib
