
- `cat`: 将文件连接到标准输出

- `chcon`: 更改文件和目录的安全上下文

- `chgrp`: 更改文件和目录的组所有

- `chmod`: 将每个文件的权限更改为指定的模式；该模式可以是要更改的权限的符号表示，也可以表示新权限的八进制

- `chown`: 更改文件和目录的用户和组所有

- `chroot`: 使用指定的目录作为 `/` 目录运行命令

- `cksum`: 打印每个指定文件的循环冗余检查 (CRC) 校验和和字节数

- `comm`: 比较两个排序后的文件，以三列输出唯一的行和公共行

- `cp`: 复制文件

- `split`: 将文件分成若干个新文件，根据给定的模式或行号分离，并输出每个新文件的字节数

- `cut`: 打印行的部分，根据给定的字段或位置选择部分

- `date`: 以指定的格式显示当前时间，或设置系统日期

- `dd`: 使用块大小和计数复制文件，同时对其进行优化的转换

- `df`: 报告所有挂载文件系统可用（及已用）的磁盘空间量，或仅报告持有所选文件的文件系统的空间

- `dir`: 列出每个目录的内容（同 `ls` 命令）

- `dircolors`: 输出设置 `LS_COLOR` 环境变量的命令，以更改 `ls` 使用的颜色方案

- `dirname`: 从文件名中删除非目录后缀

- `du`: 报告当前目录、每个给定的目录（包括所有子目录）或每个给定的文件使用的磁盘空间

- `echo`: 显示给定的字符串

- `env`: 在修改的环境中运行命令

- `expand`: 将制表符转换为空格

- `expr`: 计算表达式

- `factor`: 打印所有整数的质因数

- `false`: 什么都不做，失败；它始终以表示失败的状态码退出

- `fmt`: 重新格式化给定文件中的段

- `fold`: 折叠给定文件中的行

- `groups`: 报告用户的组组成

- `head`: 打印每个给定文件的前十行（或指定的行数）

- `hostid`: 报告主机的数字标识（十六进制）

- `id`: 报告当前用户或指定用户的有效 ID、组 ID 和组组成

- `install`: 在复制文件的同时设置其权限模式，如果可能，还设置所有者和组

- `join`: 合并具有相同字段的行

- `link`: 创建指定文件的硬链接

- `logname`: 报告用户名

- `md5sum`: 计算并打印 MD5 校验和

- `mkdir`: 创建目录

- `mknod`: 创建特殊文件

- `mv`: 移动或重命名文件

- `nice`: 以修改的优先级运行程序

- `nl`: 为行编号

- `noproc`: 报告进程数

- `numfmt`: 以人类可读格式打印数字

- `od`: 以八进制转储文件

- `paste`: 并排合并文件

- `patch`: 对文件应用补丁

- `paint`: (原文可能有错误)

- `printenv`: 打印环境变量

- `printf`: 打印格式化字符串

- `pwd`: 报告当前工作目录

- `readlink`: 打印符号链接的值

- `realpath`: 输出解析后的路径

- `rm`: 删除文件

- `rmdir`: 删除目录

- `runcon`: 使用安全上下文运行命令

- `seq`: 生成数字序列

- `sha1sum`: 计算并打印 SHA1 校验和

- `sha224sum`: 计算并打印 SHA224 校验和

- `sha256sum`: 计算并打印 SHA256 校验和

- `sha384sum`: 计算并打印 SHA384 校验和

- `sha512sum`: 计算并打印 SHA512 校验和

- `shred`: 重复覆盖文件

- `sheuf`: (原文可能有错误)

- `sleep`: 暂停指定的时间

- `sort`: 排序行

- `stat`: 显示文件状态

- `stdbuf`: 以更改缓冲的方式运行命令

- `stty`: 设置或报告终端行设置

- `sync`: 刷新系统缓冲区

- `tac`: 反序连接文件

- `tail`: 打印文件的最后几行

- `tee`: 从输入读取并写入多个输出

- `test`: 比较比较值并检查文件类型

- `timeout`: 带时间限制运行命令

- `touch`: 修改文件时间戳

- `tr`: 翻译字符

- `truncate`: 将文件缩小到指定大小

- `tty`: 报告终端名称

- `uname`: 报告系统信息

- `unexpand`: 将空格转换为制表符

- `uniq`: 丢弃重复行

- `unlink`: 删除文件

- `users`: 报告登录用户的名称

- `vdir`: 详细目录列表

- `wc`: 报告行、字和字节

- `who`: 报告谁登录

- `whoami`: 输出当前用户名

# 6.57. Check-0.12.0

Check 是一个 C 语言的单元测试框架。

近似编译时间：0.1 SBU（包含测试时约 3.8 SBU）

所需磁盘空间：12 MB

## 6.57.1. 安装 Check

为编译准备 Check：

```
/configure --prefix=/usr
```

构建软件包包：

```
make
```

编译现已完成。要运行 Check 测试套件，请执行以下命令：

```
make check
```

请注意，Check 测试套件可能需要较长时间（长达 4 SBU）。

安装软件包包：

```
make install
```

## 6.57.2. Check 的内容

安装的程序：`checkmk`

安装的库：`libcheck.{a,so}`

### 简要描述

- `checkmk`: 用于为配合 Check 单元测试框架生成 C 单元测试的 Awk 脚本

- `libcheck.{a,so}`: 包含允许从测试程序中调用 Check 的函数

# 6.58. Diffutils-3.6

Diffutils 软件包包含显示文件或目录之间差异的程序。

近似编译时间：0.4 SBU

所需磁盘空间：31 MB

## 6.58.1. 安装 Diffutils

为编译准备 Diffutils：

```
./.configure --prefix=/usr
```

编译软件包包：

```
make
```

要测试结果，请执行：

```
make check
```

安装软件包包：

```
make install
```

## 6.58.2. Diffutils 的内容

安装的程序：`cmp`, `diff`, `diff3`, 和 `sdiff`

### 简要描述

- `cmp`: 比较两个文件并报告它们是否存在差异

- `diff`: 比较两个文件或目录，并报告哪些行不同

- `diff3`: 逐行比较三个文件

- `sdiff`: 合并两个文件并交互式输出结果

# 59. Gawk-4.2.0

Gawk 软件包包含处理文本文件的程序。

近似编译时间：0.4 SBU

所需磁盘空间：42 MB

## 59.1. 安装 Gawk

首先，确保某些未使用的文件没有被安装：

```
sed -i 's/extras//' Makefile.in
```

为编译准备 Gawk：

```
./configure --prefix=/usr
```

编译软件包包：

```
make
```

要测试结果，请执行：

```
make check
```

安装软件包包：

```
make install
```

如果需要，请安装文档：

```
mkdir -v /usr/share/doc/gawk
cp -v doc/{awk.txt,*.pdf,*.jpg} /usr/share/doc/gawk
```

## 59.2. Gawk 的内容

安装的程序：`awk`（指向 `gawk` 的链接），`gawk`, 和 `awk`

安装的库：`filefuncs.so`, `fnmatch.so`, `fork.so`, `inplace.so`, `readdir.so`, `readfile.so`, `revoutput.so`, `rearray.so`, `testext.so`, `time.so`

安装的目录：`/usr/lib/gawk`, `/libexec/awk`, `/usr/share/doc/gawk`

### 简要描述

- `awk`: 指向 `gawk` 的链接

- `gawk`: 处理文本文件的程序；`awk` 的 GNU 实现

- `gawk`: 指向 `gawk` 的硬链接

- `igawk`: 使 `gawk` 包含文件的能力

# 60. Findutils-4.6.0

Findutils 软件包包含查找文件的程序。这些程序通过递归搜索目录来创建、维护和搜索数据库（通常比递归 `find` 更快，但如果数据库没有最近更新，则不可靠）。

近似编译时间：0.7 SBU

所需磁盘空间：49 MB

## 60.1. 安装 Findutils

首先，在可能会无限循环的机器上抑制测试：

```
sed -i 's/test//' tests/Makefile.in
```

为编译准备 Findutils：

```
./configure --prefix=/usr --localstatedir=/var/lib/locate
```

`configure` 选项的含义：

`--localstatedir` 将 `locate` 数据库的位置更改为 `/var/lib/locate`，这符合 FHS 标准。
