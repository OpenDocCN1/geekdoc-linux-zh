
- 安装的库：`filesource.so`, `fnmatch.so`, `fork.so`, `inplace.so`, `intdiv.so`, `ordchr.so`, `readdir.so`, `readfile.so`, `revoutput.so`, `rewtway.so`, `rrway.so` 以及 `time.so`（均位于 `/usr/lib/gawk`）

- `/usr/lib/libexec/awk`, `/usr/share/awk`, `/usr/share/doc` 以及 `/usr/share/doc/gawk-5.2.1`

### 概要说明

- `awk`：指向 `gawk` 的链接

- `gawk`：一个用于处理文本文件的程序；它是 `awk` 的 GNU 实现

- `gawk-5.2.1`：指向 `gawk` 的硬链接

## 8.58. Findutils-4.9.0

`Findutils` 包包含查找文件的程序。提供的程序用于搜索目录树中的所有文件，并创建、维护和搜索数据库（通常比递归 `find` 更快，但除非数据库已更新，否则不可靠）。`Findutils` 还提供了 `xargs` 程序，可用于对搜索选的每个文件运行指定的命令。

预计编译时间：0.4 SBU

所需磁盘空间：51 MB

### 8.58.1. 安装 Findutils

为编译准备 `Findutils`：

```
case ($uname -m) in
  i686) TIME_32_BIT_OK=yes ./configure --prefix=/usr --localstatedir=/var/lib/locate;
  x86_64) ./configure --prefix=/usr --localstatedir=/var/lib/locate;
esac
```

`configure` 选项的含义：

`TIME_32_BIT_OK=yes`

在 32 位系统上编译需要此设置。

`--localstatedir`

此选项将 `locate` 数据库移动到 `/var/lib/locate`，这是符合 FHS 标准的位置。

编译该包：

```
make
```

如需测试结果，请执行：

```
chown -R tester
su tester -c "PATH=$PATH make check"
```

安装该包：

```
make install
```

### 8.58.2. Findutils 的内容

- 安装的程序：`find`, `locate`, `updatedb` 和 `xargs`

- 安装的目录：`/var/lib/locate`

### 概要说明

`find` `find`

在目录树中搜索符合特定标准的文件

- `locate`

搜索文件名数据库并报告包含给定字符串或匹配给定模式的名称

- `updatedb`

更新 `locate` 数据库；它扫描整个文件系统（包括当前挂载的其他文件系统，除非指示不要扫描）并将每个文件名放入数据库

- `xargs`

可用于对文件列表应用给定的命令

## 59. Groff-1.22.4

`Groff` 包包含用于处理和格式化文本及图片的程序。

预计编译时间：0.2 SBU

所需磁盘空间：89 MB

### 59.1. 安装 Groff

`Groff` 环境变量 `PAGE` 包含默认纸张。对于美国用户，`PAGE=letter` 是合适的。在其他地方，`PAGE=A4` 可能更合适。虽然默认纸张是在编译期间配置的，但之后可以通过向 `/etc/papersize` 文件回显 "A4" 或 "letter" 来重写。

为编译准备 `Groff`：

```
PAGE=<paper_size> ./configure --prefix=/usr
```

构建该包：

```
make
```

此包不带测试套件。

安装该包：

```
make install
```

### 59.2. Groff 的内容

- 安装的程序：`adddtinfo`, `afmotid`, `chem`, `eqn`, `eqn2graph`, `giddmfk`, `glylipond`, `gperl`, `gpinyin`, `graph2graph`, `grn`, `godvi`, `groff`, `groffer`, `grogl`, `globp`, `groj4`, `gropdf`, `grops`, `grotty`, `hptft`

- 安装的目录：`/usr/lib/groff`, `/usr/share/doc/groff-1.22.4`

### 概要说明

- `adddtinfo`：用于 `groff -T4` 的文件

- `afmotid`：用于 `groff -T4` 的文件

- `chem`：产生化学结构的预处理器

- `eqn`：编译 `troff` 输入中嵌入的描述

- `eqn2graph`：将方程转换为图片

- `giddmfk`：用于 `groff -T4` 的文件

- `glylipond`：将乐谱转换为 `groff`

- `gperl`：允许 `perl` 代码的 `groff` 预处理器

- `gpinyin`：允许普通的 `groff` 预处理器

- `graph2graph`：将图转换为图片

- `grn`：用于创建图表的 Unix 语言

- `godvi`：将 `groff` 的输出转换为 `dvi`

- `groff`：通常是 `troff` 的前端，它运行 `troff` 程序

- `groffer`：在终端上显示 `groff` 页面

- `grogl`：LBP4 的驱动程序

- `globp`：LBP-4 的驱动程序

- `groj4`：是 `groff -Tlj4` 的驱动程序

- `gropdf`：将 `troff` 输出转换为 PDF

- `grops`：将 GNU `troff` 输出转换为 PostScript

- `grotty`：将 GNU `troff` 输出转换为打字机设备格式

- `hptft`：从 HP 标记字体度创建用于 `groff -Tlj4` 的文件

`Linux From Scratch - 版本 11.3`

`roff2dvi` 将 `roff` 文件转换为 DVI 格式

`roff2html` 将 `roff` 文件转换为 HTML 格式

`roff2pdf` 将 `roff` 文件转换为 PDF

`roff2ps` 将 `roff` 文件转换为 ps 文件

`roff2text` 将 `roff` 文件转换为文本文件

`roff2x` 将 `roff` 文件转换为其他格式

`soelim` 读取文件并将形如 `.so file` 的行替换为所提文件的内容

`tbl` 将嵌入在 `troff` 输入文件中的表格描述编译为 `troff` 可识别的命令

`tfmtodit` 为创建一个供 `groff -Tdvi` 使用的字体文件

`troff` 与 Unix `troff` 具有高度兼容性；通常应使用 `groff` 命令调用它，该命令将以适当的顺序和相应的选项运行预处理器和后处理器

## 60. GRUB-2.06

`GRUB` 软件包包含 Grand 统一引导加载程序（GRand Unified Bootloader）。

估计编译时间：0.3 SBU

所需的磁盘空间：161 MB

### 8.60.1. 安装 GRUB

> 注意

如果你的系统支持 UEFI 且希望通过 UEFI 启动 LFS，你可以跳过 LFS 中的此软件包，并按照 BLFS 页面上的说明安装带有 UEFI 支持的 `GRUB`（及其依赖项）。

> 警告

取消可能影响以下的环境变量：

```bash
unset (C, CPP, CXX, LD)FLAGS
```

不要尝试使用自定义编译标志进行“调优”。此软件包是一个引导加载程序。源代码中的低级操作可能会被过度优化所破坏。

修复当 `/boot` 分区（或如果 `/boot` 不是独立分区则为根分区）由 `e2progs-1.4.70` 或更高版本创建时导致 `grub-install` 失败的问题：

```bash
patch -p1 -i ../grub-2.06-upstream-fixes-1.patch
```

为编译 `GRUB` 准备：

```bash
./configure --prefix=/usr
--sysconfdir=/etc
--disable-efisym
--disable-werror
```

新配置选项的含义：

`--disable-werror`

这允许构建在较新版本的 Flex 引入的警告的情况下完成。

`--disable-efisym`

此选项通过禁用某些功能并消除 LFS 不需要的一些测试程序，最大限度地减少构建内容。

编译软件包：

```bash
make
```

不建议运行此软件包的测试套件。大多数测试依赖于受限 LFS 环境中不可用的软件包。如果仍运行测试，请执行 `make check`。

安装软件包：

```bash
make install
mv -v /etc/bash_completion.d/grub /usr/share/bash_completion/completions
```

如何使用 `GRUB` 使你的 LFS 系统可引导，将在第 10.4 节“使用 `GRUB` 设置启动过程”中进行讨论。

## 8.60.2. GRUB 的内容
