
# NIS（黄页服务）（第 213 页）

NIS 代码在使用之前必须进行修复。你可以在第 10 章找到如何执行此修复的详细说明，以及关于设置 IPX 服务器的信息。

尽管作者知道很多东西，但这并不其中。抱歉。你可以尝试阅读在线文档，或者找一个知道自己在做什么什么的朋友。

# RAID（第 218 页）

通过以下网址查看实验性的 RAID 软件：

```
ftp://ftp.readhat.com/pub/contrib/RPMS
```

该包名为 `ms-<version>.rpm`。

# 第 11 章

## MS-DOS 软盘（第 222 页）

许多 Linux 命令与处理 DOS 磁盘的 MS-DOS “标准”相似。（注意：你不需要挂载磁盘）
以下是与标准 MS-DOS 命令类似的命令列表：

| LINUX | MS-DOS |
| --- | --- |
| mattrib | ATTRIB |
| mcd | CD |
| mcheck | CHDSK / SCANDISK |
| mcopy | COPY |
| mdel | DEL |
| mdeltree | DELTREE |
| mdir | DIR |
| mformat | FORMAT |
| mlabel | LABEL |
| mmd | MD |
| mmove | RENAME |
| mrd | RD |
| mren | RENAME |
| mtype | TYPE |

## EOL 问题（第 224 页）

MS-DOS 使用 `<回车><换行符>` 作为行结束符。Linux 使用`<换行符>`。从 MS-DOS 将文件传输到 Linux 可能会导致文本文件的每行末尾都有一个 ^M（回车符）。

## 将 DOS 文件转换为 Linux 格式（第 225 页）

使用以下命令将名为 `in_file` 的输入文件转换为名为 `out_file` 的 Linux 文件：

```
[user@pc user]$ tr --delete '\r' <in_file> <out_file>
```

## 将 Linux 文件转换为 DOS 格式（第 225 页）

使用以下命令向文件添加`<回车>` 字符，从而创建 DOS 格式的文件：

```
[user@pc user]$ sed -e 's/$/r/' <in_file> <out_file>
```

## DOS 模拟器（第 225 页）

此功能不起作用。如果你真的需要 DOS，请启动 DOS。毕竟，MS-DOS 是目前最好的 MS-DOS 模拟器。

# 第 12 章

## 图像处理工具（第 231 页）

Linux 提供了以下图像处理工具：

| 工具 | 注释 |
| --- | --- |
| ImageMagick | 交互式效果非常好，但不要尝试从命令行使用它。 |
| Bitmap Toolset | 一组好用的实用。你可以用这个工具包做任何事情，但只能从命令行操作——一次只能做一件事。 |

## 绘图程序（第 47 页）

| 程序 | 注释 |
| --- | --- |
| xfig | 绘图程序 |
| xpaint | 类似 Microsoft Paint 的程序 |

## 杂项图形工具（第 48 页）

| 程序 | 注释 |
| --- | --- |
| mxp | Mandelbrot 生成器 |

## 音频（第 49 页）

| 程序 | 注释 |
| --- | --- |
| cd | 基于屏幕的 CD 播放器 |
| xplaycd | X Window CD 播放器 |
| xmixer | 音频混合器 |
| maplay | 播放 MPEG 格式文件 |
| play | 播放声音 (.wav, .au 等) |
| tracker, analyzer, randomizer | 播放 Amiga MOD 文件 |

## 动画（第 251 页）

| 程序 | 注释 |
| --- | --- |
| xanim | 程序。源代码可用，但有些涉及专有格式。 |

# 第 13 章

## 程序员工具（第 256 页）

GNU C 和 C++ 编译器是我见过最好的。它们高质量、健壮，并且包含了大量的扩展但也支持标准。如果你在使用容器，可能想使用 GNU 扩展，因为它们比标准灵活得多。

编程工具包括：

| 程序 | 注释 |
| --- | --- |
| gcc | GNU C 编译器 |
| g++ | GNU C++ 编译器 |
| gdb | 调试器 |
| xdbdb | Window 调试器 |
| make | 编译管理器（GNU 版本带了很多技巧。） 编辑器可以使用它来快速查找内容。 |
| RCS | 文件的版本控制 |
| CVS | 项目的版本控制 |
| proto | 生成函数原型 |
| patch | 修复 C/C++ 程序 |
| Threads | POSIX 线程库 |
| dist | 远程发行程序 |

以下是其他命令及其语言：

| 命令 | 语言 |
| --- | --- |
| fc | FORTRAN |
| f7 | FORTRAN |
| pp | PASCAL |
| basic | 请避免这个 |
| flex | lex 命令的更好版本 |
| bison | yacc 命令的更好版本 |
| java | 包含 JDK |
| python | X Window 系统的脚本语言 |

# 第 14 章

Linux 启动过程如下：

1. 启动程序 `LILO`。
2. Linux 启动并运行 `init` 程序。
3. `Init` 读取 `/etc/init` 文件并决定运行哪些程序。大部分是 `/etc/rc.d` 目录下的脚本，用于进入所需的运行级别。

在 `/etc/init` 文件中，将行：
`default:`
改为：
`default:`

要进入单用户模式进行系统维护，在 LILO 提示符输入：
`linux single`

# 第 15 章

## 构建新内核（第 281 页）

要配置新内核，执行以下命令：

```
[root@pc root]# cd /usr/src/linux
[root@pc linux]# make xconfig
```

现在填写表单。编译你的新内核，执行以下命令：

```
[root@pc linux]# make clean
[root@pc linux]# make dep
[root@pc linux]# make
```

另外，如果你有模块，执行以下命令：

```
[root@pc linux]# make modules
[root@pc linux]# make modules_install
```

## 创建启动软盘（第 300 页）

要创建启动软盘，执行以下命令：

```
[root@pc linux]# make disk
[root@pc linux]# /usr/sbin/rdev /dev/fd0 1
[root@pc linux]# /usr/sbin/rdev -s /dev/fd0 <partition>
```

在此处，`<partition>` 是你的根分区名称。

## 在磁盘上创建测试内核（第 301 页）

要在磁盘上创建测试内核，使用以下命令：

```
[root@pc linux]# cd /boot
[root@pc boot]# cp vmlinuz vmlinuz.ok
[root@pc linux]# cd /usr/src/linux
[root@pc linux]# make zImage
[root@pc linux]# cd arch/i86/boot
[root@pc boot]# cp zImage /boot/vmlinuz.ok
```

现在编辑 `/etc/lilo.conf` 文件，使其看起来如下：

```
boot=/dev/fd0
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
other=/dev/hda
label=dos
table=/dev/hda
image=/boot/vmlinuz
label=linux
root=/dev/hdb2
read-only
image=/boot/vmlinuz.ok
label=ok
root=/dev/hdc1
read-only
image=/boot/vmlinuz.new
label=new
root=/dev/hdc1
read-only
```

然后重新配置 LILO：
```
[root@pc linux]# lilo
```

你现在可以启动 linux（旧内核）、ok（安全内核）、（实验性内核）。

## 最终安装（第 302 页）

在确认一切运行正常后，您可以使用以下命令正式安装系统：

```
[user@pc linux]# cd arch/i86/boot
[user@pc boot]# cpImage /boot/vmlinuz
```
