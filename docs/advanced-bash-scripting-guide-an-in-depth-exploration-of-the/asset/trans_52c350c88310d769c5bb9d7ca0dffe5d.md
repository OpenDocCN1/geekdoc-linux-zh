

# 高级 Bash 脚本指南

例如，执行 `encrypt filename.txt -p filename.ps` 会生成 PostScript 输出文件 `filename.ps`。
groff, tbl, eqn

另一种标记和显示格式语言是 groff。它是经典的 UNIX roff/roff 显示和排版包的增强型 GNU 版本。帮助页（manpages）使用了 groff。

`tbl` 表格处理工具被 groff 的一部分，其功能是将表格标记转换为 groff 命令。

`eqn` 处理工具同样是 groff 的一部分，其功能是将公式标记转换为 groff 命令。

## 示例 16-29. manview: 查看格式化后的帮助页

```bash
#!/bin/bash
# manview.sh: 对帮助页源码进行格式化以供查看。

# 此脚本在编写帮助页源码时非常有用。
# 它可以让你在处理源码时即时查看中间结果。
E_WRONGANGS=85

if [ -z "$1" ]
then
    echo "Usage: `basename $0` filename"
    exit $E_WRONGANGS
fi
# -Tascii -man $1 | less
# 参考 groff 的帮助页。

# 如果帮助页包含表格和/或公式，
# 那么上面的代码会报错。
# 下面的行可以处理这种情况。
# gtbl < "$1" | weqn -Tlatlin | groff -Tlatlin -mtty-char -man
# 感谢 S.C.

    # 另见 "maned.sh" 脚本。
```

exit? 参见示例 A-39。

lex, yacc

`lex` 词法分析器生成用于模式匹配的程序。在 Linux 系统上，它已被非专利 `flex` 取代。

`yacc` 工具根据一组规范创建解析器。在 Linux 系统上，它已被非专利 `bison` 取代。

## 16.5 文件与存档命令

### 存档

### tar

标准的 UNIX 归档工具。[75] 最初是一个磁带归档程序（Tape ARchiving），现在已发展成为一个通用软件包，可以处理各种设备的各种归档，范围从磁带驱动到使用 `stdout` 的普通文件（参见示例 3-4）。GNU tar 经过补丁后接受各种压缩过滤器，例如：`tar czvf archive_name.tar.gz`，它会递归归档并 `gzips` 目录树中的所有文件，但当前工作目录（PWD）下的 `dofiles` 除外。[]

一些 tar 选项：

- 1. -c create（创建一个新归档）
- 2. -x extract（从现有归档提取文件）
- 3. --delete delete（从现有归档删除文件）
> 此选项在磁带设备上不起作用。

- 4. -r append（将文件添加到现有归档）
- 5. -A append（将 tar 到现有归档）
- 6. -t list（列出现有归档的内容）
- 7. -u update 更新归档
- 8. -d 归档与指定的文件系统
- 9. --after-date 仅处理时间戳在指定日期之后的文件
- 10. -z zip 归档（压缩或解压缩，取决于与 -c 或 -x 选项结合）
- 11. -j bzip2 归档

> 从损坏的压缩归档中恢复数据可能很困难。导入文件时，请进行多次备份。

### shar

Shell 存档工具。shell 存档中的文本和/或二进制文件在不压缩的情况下进行合并，结果归档本质上是一个 shell 脚本，带有 #/bin/sh 头，包含了所有必要的归档命令以及文件本身。目标文件中的不可打印二进制字符将转换为输出 shar 中的 ASCII 字符。Shar 存档曾出现在 Usenet 组中，而 shar 已被 tar/gzip 取代。`unshar` 命令解压 shar 存档。

`mailshar` 命令是一个 Bash 脚本，使用 shar 将多个文件合并为一个文件以发送邮件。该脚本支持压缩和 u编码。

### ar

用于归档的创建和操作工具，主要用于二进制对象文件库。

### rpm

红帽软件包管理器（Red Hat Package Manager）或 rpm 工具为源码或二进制归档提供了封装。它包含了安装软件包和检查软件包完整性等命令。

简单的 `rpm -i package_name` 通常足够安装软件包，尽管还有更多可用选项。

`rpm -qf` 识别文件自哪个包。

```bash
bash$ rpm -qf /bin/ls
```

> `rpm -qa` 列出系统中所有安装的 rpm 软件包。`rpm -qa package_name` 列出对应于 package_name 的包。

```bash
bash$ rpm -qa
```

### cpio

这种特殊的归档复制命令（cpio 输入和输出）已很少见到，已被 tar/gzip 取代。它仍有用途，如移动目录树。在指定适当块大小（用于复制）的情况下，它可以比 tar 快得多。

## 示例 16-30. 使用 cpio 移动目录树

```bash
#!/bin/bash

# 使用 cpio 复制目录：
# 使用 cpio 的优势：
# 复制速度。在管道操作中比 tar 快。
# 非常适合复制特殊文件（如命名管道），
# 这些文件 'cp' 可能会出错。

ARGS=2
E_BADARGS=65
```

```bash
if [ "$#" -ne "$ARGS" ]
then
    echo "Usage: `basename $0` source destination"
    exit $E_BADARGS
fi

source="$1"
destination="$2"

################################################################
find "$source" -depth 1 cpio -admv "$destination"
# 读取 'find' 和 'cpio' 的帮助页以解析这些选项。
# 上述仅相对于 $PWD（当前目录）有效，除非指定完整路径。
################################################################

# 练习：
# ----

# 添加代码检查 'find | cpio' 管道的退出状态 ($?)
# 并在出错时输出相应的错误信息。
```

### rpm2cpio

此命令从 rpm 中提取 cpio 存档。

```bash
#!/bin/bash
# de-rpm.sh: 解压 'rpm' 存档

echo "Usage: `basename $0` target-file"
# 必须将 'rpm' 存档名称作为参数。

TEMPFILE=$$.cpio                # 具有“唯一”命名的临时文件。
                                # $$ 是脚本的进程 ID。

rpm2cpio < $1 > $TEMPFILE         # 将归档转换为
                                cpio 存档。
cpio --make-directories -F $TEMPFILE -i # 解压 cpio 存档。
rm -f $TEMPFILE                  # 删除 cpio 存档。
```

```bash
练习：
# 添加检查：1) "target-file" 是否存在以及
# 2) 是否是一个 rpm 存档。
# 提示：解析 'file' 命令的输出。
```

### pax

pax 可移植存档交换促进了定期文件备份，并在不同的 Unix 版本之间具有兼容性。它被设计用于取代 tar 和 cpio。

```bash
pax -wf daily_backup.pax ~/linux-server/files
# 创建目标目录下所有文件的 tar 存档。
```

```bash
# 注意 pax 选项必须处于正确的顺序 --
# pax -fw 有完全不同的效果。

pax -f daily_backup.p
# 列出存档中的文件。

pax -rf daily_backup.p /bsd-server/files
# 将备份的文件从 Linux 机器
恢复到 bsd 机器上。
```

注意 pax 处理了许多标准的存档命令。

## 压缩

### gzip

标准的 GNU/UNIX 压缩工具，取代了低劣且专有的 compress。相应的解压缩命令是 gzip，等同于 -d。

- -c 选项将 gzip 的输出选择到 stdout。这在管道到其他命令时非常有用。

类似于 zcat 命令，bcat 将 gzipped 文件解压到 stdout。它本质上是一个压缩文件的 cat 命令（包括用 compress 处理的文件）。

- 在某些常见的 UNIX 系统上，zcat 是 uncompress -c 的同义词，且无法处理 gzipped 文件。
另见示例 7-7。

### zip2

另一种压缩工具，通常比 gzip 更高效（但更慢），特别是处理大文件时。解压缩命令是 bunzip2。

类似于 zcat 命令，bcat 将 bzipped2 文件解压到 stdout。

- 较新版本的 tar 已经修复了支持 zip2。

### compress, uncompress

这是商业 UNIX 发行版中发现的旧专有压缩工具。更高效的 gzip 已取代取代它。Linux 发行版通常包含一个兼容性的 compress 代品，尽管 gzip 可以解压缩 compress 处理的文件。

- znew 命令将压缩文件转换为 gzipped 文件。

### sq

另一种压缩（压缩）工具，一个仅适用于排序后的 ASCII 列表的过滤器。它使用过滤器的标准语法 `sq < input-file > output-file`。但不如 gzip 快。

- sq 的输出可以管道到 gzip 进行进一步压缩。

### zip, unzip

跨平台文件存档工具，与 DOS pkzip.exe 兼容，“压缩存档似乎是互联网上使用 tar 包（tarballs）更常见的文件交换媒介。”

