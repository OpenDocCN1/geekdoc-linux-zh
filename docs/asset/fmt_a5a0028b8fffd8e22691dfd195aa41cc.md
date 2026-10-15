
$ expr magazine | book

magazine

```
```

$ expr 5 | 0

5

```
```

$ expr 0 | 5

5

```
```

$ expr 5 | 6

5

```
# file

显示文件的分类

`file` `[option]` `file-list`

`file` 工具根据内容对文件进行分类。

参数 `file-list` 包含 `file` 分类的一个或多个文件的路径。你可以在 `file-list` 中指定任何类型的文件，包括普通文件、目录和特殊文件。

参数

- `-t` `file` 从文件中读取检查的文件名，而不是从命令行读取。文件名必须每行一个列在文件中。
- `-z` `zip` 尝试对压缩文件中的文件进行分类。

说明

`file` 工具可以分类超过 5000 种文件类型。GNU/Linux 系统上 `file` 显示的一些常见文件类型包括：

- archive（归档）
- ascii text（ASCII 文本）
- c program text（C 程序文本）
- commands text（命令文本）
- core file（核心文件）
- cpio archive（cpio 归档）
- data（数据）
- directory（目录）
- ELF 32-bit executable（ELF 32位可执行文件）
- empty（空）
- English text（英文文本）
- executable（可执行文件）

`file` 工具在尝试对文件进行分类时最多使用三种测试：文件大小、魔数和语言测试。当 `file` 识别出文件类型时，将停止测试。第一个测试文件系统测试检查 `stat` old的返回值，判断文件是否为空或特殊文件。魔数测试（第 178 页）查找文件开头附近特定固定格式的数据。如果需要，最后一个测试将确定文件是否为文本文件、使用什么编码以及用什么语言编写。请参阅 `file` 页面获取有关其工作原理的详细说明。`file` 的结果并不总是准确的。

以下是文件识别的示例：

```
/etc/a2ps.cfg: ASCII English text

/etc/aep: directory

/etc/aliases.db: 无法读取 '/etc/aliases.db'（权限拒绝）。

/etc/dmpdates: empty

/etc/grub.conf: 指向 ../boot/grub/grub.conf 的符号链接

/etc/mime-magic: ASCII C++ program text

/usr/bin/40db: a /usr/bin/python script text executable

/usr/bin/a2p: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (shared libs), stripped Bourne shell script text executable

/usr/bin/AbWord: per-l script text executable

/usr/bin/addrname.awk: awk script text executable

/usr/bin/authconfig: 指向 consolehelper 的符号链接

/usr/share/alocalcl-1.4/error.m4: ASCII M4 language pre-processor text

/usr/share/alocalcl-1.5/termios.m4: ASCII C program text

/usr/share/alocalcl/esd.m4: ASCII M4 language pre-processor text

/usr/share/apacheconf/apacheconf.glade: ASCII Java program text

/usr/share/apacheconf/ApacheConf.py: XML document text

/usr/share/apacheconf/ApacheConf.py: a /usr/bin/python script text executable

/usr/share/application-registry/gnome-vfs.applications: ASCII text, with very long lines

/usr/share/applications/apacheconf.desktop: UTF-8 English text

/usr/share/doc/w3c-libwww-5.4.0/48x.gif: GIF image data, version 89a, 48,

/usr/share/doc/w3c-libwww-5.4.0/COPYRIGHT.html: HTML document text

/usr/share/doc/xmltext-2000018/readme.txt: gzip compressed data, deflated, last modified: Wed Dec 31 16:00:00 199, max compression, os: Unix

/usr/share/doc/zlib-devel-1.4/c: ASCII program text
```

满足上述准则。如果在*表达式*中没有出现操作准则，默认假设为 `-print`。请参考下面的“讨论（Discussion）”和“注释（Notes）”部分。

`-exec` `command\;` 如果命令返回零（*true*）作为退出状态，则被评估的文件符合此准则。你必须用分号终止命令。命令中的一对大括号 `{}` 表示正在被评估的文件名。你可以在一组其他准则的末尾使用 `-exec` 操作准则，以便在满足上述准则时执行该命令。参见“讨论（Discussion）”。请参阅第 1377 页的 `xargs` 以获取一种实现此选项功能的更高效的方法。

`-ok` `command\;` 此操作与 `-exec` 相同，但会将每个要执行的命令包含在角括号内并显示，且只有在从标准输入接收到 y 或 Y 时才执行该命令。

`-depth` 被评估的文件符合此准则。它导致 `find` 在处理目录本身之前先处理该目录中的条目。当你使用 `find` 将文件发送给 `cpio` 实用程序时，`-depth` 准则使 `cpio` 能够保留目录的修改时间（假设你为 `cpio` 使用了 `--preserve-modification-time` 选项）。参见第 1126 页和 1127 页的“讨论（Discussion）”和“示例（Examples）”。

`-xdev` 被评估的文件符合此准则。它导致 `find` 不搜索工作目录（来自目录列表参数）所在文件系统以外的文件系统中的目录。类似于 `-mount`。

`-nouser` 如果被评估的文件不属于 `/etc/passwd` 文件中的用户，则该文件符合此准则（即与文件关联的用户 ID 不对应于系统中的已知用户）。

`-nogroup` 如果被评估的文件不属于 `/etc/group` 文件中列出的用户组，则该文件符合此准则。

`-follow` 当指定了此准则且 `find` 遇到指向目录文件的符号链接时，`find` 会追踪该链接。

# 讨论 (Discussion)

假设 `x` 和 `y` 是准则。如果准则 `y` 不满足准则 `x`，则以下命令行永远不会测试准则 `y`。因为准则之间用空格（逻辑与运算符 AND）分隔，所以如果发现准则 `x` 不满足，文件就不可能满足准则，因此 `find` 不再继续测试。你可以将该表达式读为“（测试）文件是否满足准则 `x` 以及（空格意味着与）准则 `y`”：

```
$ find dir x y
```

如果准则 `x` 不满足，则下一个命令行将测试文件是否满足准则 `y`。文件仍然可以满足准则，因此 `find` 继续评估。它被读为“（测试）是否满足准则 `x` 或 准则 `y`”。如果文件满足准则 `x`，则不会评估准则 `y`，因为没有必要：

```
$ find dir x -or y
```

某些“准则”并不选择文件，而是导致 `find` 采取操作。当 `find` 评估这些操作准则之一时，就会触发操作。因此，操作在命令行中的位置，而不是其评估的结果，决定了 `find` 是否采取该操作。

`-print` 操作准则导致 `find` 显示其正在测试的文件的路径名。以下命令行显示目录（及其所有子目录）中所有满足准则 `x` 的文件名：

```
$ find dir -print x
```

以下命令行仅显示目录中满足准则 `x` 的文件名：

```
$ find dir x -print
```

在测试准则后使用 `-print` 的这种常见用法是默认的操作准则。以下命令行的功能与前一个命令行相同：

```
$ find dir x
```
