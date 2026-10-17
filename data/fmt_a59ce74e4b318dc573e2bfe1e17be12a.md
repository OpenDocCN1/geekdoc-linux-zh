
## 在时间限制内运行命令

- `touch`

  更改文件时间戳，将给定文件的访问和修改时间设置为当前时间；文件不存在则创建零长度文件

- `tr`

  从标准输入翻译、压缩或删除给定的字符

- `true`

  什么都不做，执行成功；它始终以表示成功的状态码退出

- `truncate`

  缩小或扩展文件

- `tsort`

  执行拓扑排序；写出一个完全有序的列表

- `tty`

  报告连接到标准输入的终端

- `uname`

  报告系统信息

- `unexpand`

  将空格转换为制表符

- `uniq`

  删除所有连续相同行中仅保留的一个

- `unlink`

  删除给定文件的名称

- `users`

  报告登录用户的名称

- `vdir`

  与 `-l` 相同

- `wc`

  报告每个给定文件的行数、单词和字节数，当给定多个文件时计算总计

- `who`

  报告谁正在登录

- `whoami`

  报告与当前用户 ID 关联的用户名

- `yes`

  反复输出 y 或给定的字符串，直到被杀死

- `libdbuf`

  `stdbuf` 使用的库

## 80.60. Gawk-5.3.0

`Gawk` 软件包包含处理文本文件的程序。

近似编译时间：0.1 SBU

所需磁盘空间：42 MB

### 80.60.1. 安装 Gawk

首先，确保没有安装某些未使用的文件：

```
sed -i 's/ /extras//' Makefile.in
```

为编译 `Gawk` 准备工作：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

如需测试结果，请执行：

```
chown -R tester .
su tester -c "PATH=$PATH make check"
```

安装软件包：

```
rm -f /usr/bin/gawk-5.3.0
make install
```

该命令的含义：

```
rm -f /usr/bin/gawk-5.3.0
```

如果硬链接 `gawk-5.3.0` 已经存在，构建系统将不会重新创建。删除它以确保更新第 6.9 节“Gawk-5.3.0”中安装的之前的硬链接。

安装过程已经创建了 `awk` 指向 `gawk` 的符号链接，也为其新页面创建一个符号链接：

```
ln -sv gawk.1 /usr/share/man/man1/awk.1
```

如果需要，可以重新安装该命令：

```
mkdir -pv /usr/share/doc/gawk-5.3.0
cp -v doc/awkforai.txt.* {eps,pdf,jpg} /usr/share/doc/gawk-5.3.0
```

### 80.60.2. Gawk 的内容

- 安装的程序：

  - `awk`（指向 `gawk` 的链接）、`gawk` 和 `gawk-5.3.0`

  - `filefuncs.so`, `fnmatch.so`, `fork.so`, `inplace.so`, `intdiv.so`, `ordch.so`, `readdir.so`, `readfile.so`, `revoutput.so`, `rewtway.so`, `rarray.so` 和 `time.so`（均位于 `/usr/lib/gawk`）

- 安装的目录：

  - `/usr/lib/gawk`, `/usr/lib/execawk`, `/usr/share/awk` 和 `/usr/share/doc/gawk-5.3.0`

#### 简述

- `awk`：指向 `gawk` 的链接

- `gawk`：一个处理文本文件的程序；它是 `awk` 的 GNU 实现

- `gawk-5.3.0`：指向 `gawk` 的硬链接

## 8.61. Findutils-4.9.0

`Findutils` 软件包包含用于查找文件的程序。提供的程序可以搜索目录树中的所有文件，并进行创建、维护和搜索（通常比递归查找 `find` 快，但除非数据库已更新，否则结果不可靠）。`Findutils` 还提供了 `xargs` 程序，它可以对搜索选定的每个文件运行指定的命令。

近似编译时间：0.4 SBU

所需磁盘空间：51 MB

### 8.61.1. 安装 Findutils

为编译 `Findutils` 准备工作：

```
./configure --prefix=/usr --localstatedir=/var/lib/locate
```

`configure` 选项的含义：

```
--localstatedir
此选项将 `locate` 数据库移动到 `/var/lib/locate`，这是符合 FHS 标准的位置。
```

编译软件包：

```
make
```

如需测试结果，请执行：

```
chown -R tester .
su tester -c "PATH=$PATH make check"
```

安装软件包：

```
make install
```

### 8.61.2. Findutils 的内容

- 安装的程序：`find`, `locate`, `updatedb` 和 `xargs`

- 安装的目录：`/var/lib/locate`

#### 简述

- `find`：在给定的目录树中搜索符合标准的文件

- `locate`：通过文件名数据库搜索并报告包含给定字符串或匹配给定模式的名称

- `updatedb`：更新 `locate` 数据库；它扫描整个文件系统（包括当前挂载的其他文件系统，除非指示不扫描），并将找到的每个文件名放入数据库中

- `xargs`：可将指定的命令应用于文件列表

## 8.62. Groff-1.23.0

`Groff` 软件包包含处理和格式化文本及图片的程序。

近似编译时间：0.2 SBU

所需磁盘空间：107 MB

### 8.62.1. 安装 Groff

`Groff` 期望环境变量 `PAGE` 包含默认纸张大小。对于美国用户，`PAGE=letter` 是合适的。在其他地方，`PAGE=A4` 可能合适。虽然默认纸张大小是在编译期间配置的，但稍可以通过 `/etc/papersize` 文件通过“A4”或“letter”进行覆盖。

为编译 `Groff` 准备工作：

```
PAGE=<paper_size> ./configure --prefix=/usr
```

构建软件包：

```
make
```

如需测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

### 8.62.2. Groff 的内容

- 安装的程序：`adftninfo`, `afmotid`, `chem`, `eqn`, `eqn2graph`, `giffmk`, `glylipond`, `gperl`, `gpinyin`, `graph2n`, `gram`, `godvi`, `groff`, `grol`, `gropl`, `gropdf`, `gro j`, `grotty`, `hpdit`, `hpfoot`, `indbib`, `lkbib`, `lookbib`, `mmroff`, `neqn`, `pdfmon`, `pdfroff`, `pic`, `pic2graph`, `post-grohtml`, `preconv`, `pre-grohtml`, `refer`, `soelim`, `tm`

- 安装的目录：`/usr/lib/groff`, `/usr/share/doc/groff-1.23.0`

#### 简述

- `addftninfo`：添加字体信息

- `afmotid`：搜索额外的字体信息

- `chem`：使用 `groff` 处理化学结构

- `eqn`：编译嵌入 `troff` 或 `TeX` 中的方程

- `eqn2graph`：将方程转换为图片

- `giffmk`：标记 `groff` 和 `lilypond` 之间的差异

- `glylipond`：将谱转换为 `lilypond`

- `gperl`：在 `groff` 中插入 `perl` 代码

- `gpinyin`：在 `groff` 中插入拼音（中文）

- `graph2n`：将图转换为图片

- `gram`：无描述

- `godvi`：无描述

- `groff`：一种文档格式化系统

- `grol`：无描述

- `grol`：无描述

- `gropl`：无描述

- `gropdf`：从 `groff` 生成 PDF

- `gro j`：产生 PCL5 输出

- `grotty`：为打字机类设备转换输出

- `hpdit`：从 HP 字体度量文件为 `groff` 创建文件

- `hpfoot`：处理脚注

- `indbib`：为参考文献数据库创建倒排索引

- `lkbib`：根据指定键搜索参考文献数据库

- `lookbib`：根据关键词搜索参考文献数据库

- `mmroff`：`groff` 的简单预处理器

- `neqn`：格式化输出为 ASCII

- `pdfmon`：用于生成 PDF 文的 `groff` 封装

- `pdfroff`：使用 `groff` 创建 PDF 文

- `pic`：编译 `troff` 或 `TeX` 中的图片描述

- `pic2graph`：将 PIC 图表转换为图片

- `post-grohtml`：将 GNU `troff` 的输出转换为 HTML

- `preconv`：将文件的编码转换为 GNU `troff` 可理解的格式

- `pre-grohtml`：将 GNU `troff` 的输出转换为 HTML
