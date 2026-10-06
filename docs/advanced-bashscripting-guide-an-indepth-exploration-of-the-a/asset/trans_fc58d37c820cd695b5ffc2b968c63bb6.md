

# 高级 Bash 脚本指南

- 3. -r 追加（文件到归档）
- 4. -t 列出（归档内容）
- 5. -u 更新归档
- 6. -x 提取（从归档提取文件）
- 7. -z gzip 归档

从损坏的 gzipped tar 归文件中恢复数据可能困难。在归档文件时，请制作多个备份。

shar

Shell 归档工具。shell 归档中的文件是在不压缩的情况下连接的，生成的归档本质上是一个 shell 脚本，包含 #!/bin/sh 头，并包含所有必要的解包命令。shar 归档出现在互联网新闻组中，但除此之外 shar 已经被 tar/gzip 充分取代。unshar 命令用于解 shar 归档。

ar

广泛用于二进制对象文件的归档创建和处理工具。

cpio

这种专门的归档复制命令（复制输入和输出）已经很少见到，因为它已被 tar/gzip 取代。它仍然有其用处，例如移动目录树。

# 示例 12–22. 使用 cpio 移动到目录树

```bash
#!/bin/bash

# 使用 cpio 复制目录树

ARGS=2
E_BADARGS=65

if [ $# -ne "$ARGS" ];
then
    echo "Usage: basename $0 destination"
    exit $E_BADARGS
fi

source=$1
destination=$2

find "$source" -depth | cpio -admv "$destination"
# 读取 man 页以解读这些 cpio 选项。

exit 0
```

# 示例 12–23. 解包 rpm 归档

```bash
#!/bin/bash
# de-rpm.sh: 解包一个 'rpm'
```

## 12.5. 文件与归档命令

```bash
E_NO_ARGS=65
TEMPFILE=$$.cpio # 带有“唯一”名称的临时文件。
                 # $$ 是脚本的进程 ID。

if [ -z "$1" ]
then
    echo "Usage: basename $0 filename"
    exit $E_NO_ARGS
fi

rpm2cpio < $1 $TEMPFILE # 将 rpm 归档转换为 cpio 归档。
cpio --make-directories -F $TEMPFILE -i # 解包 cpio 归档。
rm -f $TEMPFILE # 删除 cpio 归档。
```

### gzip

标准的 GNU/UNIX 压缩工具，取代了劣质且专有的 **compress**。相应的解压缩命令是 **gzip -d**。

**zcat** 将 gzipped 文件解压到 `stdout`，作为管道或重定向的可能输入。这实际上是一个作用于压缩文件的 cat 命令（包括用**旧版 compress** 工具处理的文件）。**zcat** 命令等于 **gzip -dc**。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_179_0.png)

> 在某些商业 UNIX 系统上，zcat 是 **uncompress -c** 的别名，将无法作用于 gzipped 文件。

另参阅 [示例 7–6](#)。

### bzip2

另一种压缩工具，通常比 **gzip** 更有效率，特别是在处理大文件时。相应的解压缩命令是 **bzip2**。

### compress, uncompress

这是在商业 UNIX 发行版中找到的旧专用压缩工具。更有效的 **gzip** 已在很大程度上取代了它。Linux 发行版通常包含一个兼容的 **compress** 模拟，尽管 **gunzip** 可以解包用 **compress** 处理的文件。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_179_1.png)

> **znew** 命令将 **compressed** 文件转换为 gzipped 文件。

### sq

另一种压缩工具，一个仅作用于排序后的 ASCII 单词列表的过滤器。它使用过滤器的标准调用语法 `sq < input-file > output-file`。速度快，但远没有 gzip 高效。相应的解压缩过滤器是 unsq，调用方式与 sq 一样。

sq 的输出可以管道到 gzip 进行进一步压缩。

跨平台文件归档和压缩工具，兼容 DOS PKZIP。“Zipped”归档在互联网上似乎比“tarballs”（tar 包）是更易接受的交换媒介。

# 文件信息

### file

一种用于识别文件类型的工具。命令 `file file-name` 将返回文件的文件的规格，例如 ascii 文本或数据。它引用 /usr/share/magic、/etc/magic 或 /usr/lib/magic 中的魔数数，取决于 Linux/Unix 发行版。

-f 选项导致 file 以批模式运行，读取一个文件名列表进行分析。-z 选项用于压缩目标文件，强制其分析解压缩后的文件类型。

```bash
$ bash file test.tar.gz
test.tar.gz: gzip compressed data, deflated, last modified: Sun Sep 16 13:34:51 2001, os:
$bash file -z test.tar.gz
test.tar.gz: GNU archive (gzip compressed data, deflated, last modified: Sun Sep 13
```

# 示例 12–24. 从 C 程序文件中剥离注释

```bash
#!/bin/bash
# strip-comment.sh: 去除 C 程序中的注释 (* COMMENT *)。

E_NOARGS=65
E_ERROR=66
E_WRONG_FILE_TYPE=67

if [ $# -eq "$E_NOARGS" ]
then
    echo "Usage: basename $0" >&2 # 错误消息。
    exit $E_ERROR
fi

# 检查文件类型。
type=$(file $1 | awk '{ print $2,3,4 }') # "file" 删除了这里的第一个字段...
# 然后将结果放入变量 "type"。
if [ "$type" != "ASCII" ]
then
    echo "此脚本仅作用于 ASCII 文件。"
    exit $E_WRONG_FILE_TYPE
fi

# 相当晦涩的 sed:
# 如果你花几个小时学习基础知识，就会很容易理解。
# 需要在 sed 中增加增加行来处理同一行后面紧跟注释的情况。
# 此外，上面的删除了带有“/*”的行。由于 'exit 0'，此行代码不会执行。
# Stephane Chazelas 建议了以下替代方案：

```bash
usage() {
    echo "Usage: $0" >&2
    exit 1
}
WEIRD=$(echo $1)
[[ $# -eq 1 ]] && usage
case "$WEIRD" in
    *)
        sed -e "s/\/\*///g;s/\*\///g" "$1"
        )
esac
```

```
# 这仍然内容欺骗：
# printf("/*");
# *
# 为了处理特殊情况（行中的注释）...
exit 0
```

which 提供 "command-xxx" 的完整路径。这有助于确定特定的命令或工具是否安装在系统中。

```bash
$bash which rm
/usr/bin/rm
```

### whereis

与 which ，whereis 提供 "command-xxx" 的完整路径，但也提供了其 man 页。

```bash
$bash whereis rm
/bin/rm /usr/share/man/man1/rm.bz2
```

### whatis

whatis 在 whatis 数据库中查找“file”。这有助于识别系统命令和重要的配置文件。将其视为简化的 man 命令。

```bash
$bash whatis whatis
whatis (1) search the whatis database for complete words
```

# 示例 12–25. 探索 /usr/X11R6/bin

```bash
#!/bin/bash

# /usr/X11R6/bin 中那些神秘的二进制文件是什么？
DIRECTORY="/usr/X11R6/bin"
# 尝试 "/bin", "/usr", "/local/bin" 等。

for file in $DIRECTORY
do
    whatis basename '$file' # 输出二进制信息。
done

exit 0
# 你可能希望重定向 whatis 的输出，如下：
# whatis.sh >>whatis.db
# 或者在标准输出上一页查看，
# whatis.sh | less
```

另参阅示例 10–3。

### vdir

显示详细的目录列表。效果类似于 ls -l。这是 GNU 文件工具之一。

```bash
$ vdir
total 10
-rw-r--r 1 bozo bozo 4034 Jul 18 22:04 datal.xrolo
-rw-r--r 1 bozo bozo 4602 May 25 13:58 datal.xrolo.bak
-rw-r--r 1 bozo bozo 877 Dec 17 2000 employment.xrolo
```

