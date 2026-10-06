

# 高级 Bash 脚本指南

```bash
for filename in * # 没有必要使用 basename，
  # 因为 "*" 不会返回包含 "/" 的文件
do=$(echo "$filename" | tr '[:upper:]' '[:lower:]')
  # POSIX 字符集表示法。
  # 添加末尾的斜杠是为了确保它们
  # 不被命令替换移除。
  # 变量替换：
  n=${filename%/} # 从 filename 中移除上面添加末尾斜杠。
  [[ $filename == $n ]] || mv "$filename" "$n"
  # 检查文件名是否已经是小写。
done

exit 0
```

# 示例 12-16. DOS 到 UNIX 文本文件转换。

```bash
#!/bin/bash
# du.sh: DOS 到 UNIX 文本文件转换

E_WRONGARGS=65

if [ -z "$1" ];
then
  echo "Usage: basename $0 filename-to-convert"
  exit $SE_WRONGARGS
fi

NEWFILENAME=$1.unx

CR=$'\x15' # 回车符。
# DOS 文本文件以 CR-LF 结尾。

tr -d $CR < $1 > NEWFILENAME
# 删除 CR 并写入新文件。

echo "Original DOS text file is \"$1\""
echo "Converted UNIX text file is \"$NEWFILENAME\""

exit 0
```

# 示例 12-17. rot13, rot13，极弱加密。

```bash
#!/bin/bash
# rot13.sh: 经典的 rot13 算法，足以欺骗 3 岁小孩的加密。

# 使用: ./rot13.sh filename
# 或 ./rot13.sh $filename
# 或 ./rot13.sh 并提供键盘输入 (stdin)

cat "$@" | tr 'a-zA-Z' 'n-za-MN-ZA-M' # "a" 变成 "n", "b" 变成 "o",以此此类推。
# "cat @@" 结构
# 允许从 stdin 或文件获取输入。

exit 0
```

# 示例 12-18. 生成“加密引言”谜题

```bash
#!/bin/bash
# crypto-quote.sh: 加密引言
```

## 12.4. 文本处理命令

```bash
# 将使用简单的单字母替换法加密引言。
# 结果类似于在日报评论版中
# 看到的“加密引言”谜题。
```

```bash
key=ETAOINSHRDULBCFGJMPVW2XYK
# "key" 仅仅是一个乱序的字母表。
# 改变 "key" 就会改变加密。

# 'cat @$' 结构从 stdin 或文件获取输入。
# 如果使用 stdin，用 Control-D 结束输入。
# 否则，指定文件名作为命令参数。
```

```bash
cat "$@"    tr "a-z"      tr "A-Z" "$key"
             |       to uppercase             encrypt
# 支持小写、大写或混合大小写的引言。
# 非字母字符保持不变通过。
```

> 尝试用这个脚本处理类似的内容：
> "其他人的习惯不需要改革。"
> 马克·吐温 (Mark Twain)

```bash
# 输出是：
# "CPHFRCS QF CIIQ MINFERCS EQ FPHIM GIFGUI'Q HETPQ."
# BEEML PZERC
```

```bash
# 要反转加密：
# cat "$@" | tr "A-Z"
```

这种简单的密码可以被平均水平的 12 岁孩子
++ 仅用铅笔和纸就能破解。

```bash
exit 0
```

## tr 变体

tr 工具有两个历史变体。BSD 版本不使用括号（tr a-z A-Z），但 SysV 版本使用 tr '[a-z]' '[A-Z]'。GNU 版本与 BSD 相似，因此括号内的范围是强制性的。

这种过滤器会将行文本折行到指定的宽度。配合 -s 选项使用时特别有用，它会在空格处折行（参见示例 12–19 和示例 A–2）。

这是一个简单的格式化器，用于在管道中“折行”长文本输出。

# 示例 12–19. 格式化列表。

```bash
#!/bin/bash
WIDTH=40                # 40 列宽。
```

## 12.4. 文本处理命令

```bash
b=`ls /local/bin`      # 获取文件列表...
echo $b | fmt -w       # 也可以通过 echo $b | fold -w 完成。
exit 0
```

**fmt** 的强大替代方案是 Kamil 的 **col** 工具，从 http://berkeley.edu/~kamil/col/ 获取。它输出文件的置换索引（交叉列表），在必要时可以在管道中进一步过滤和格式化。

欺骗性的过滤器从输入流中移除行。它还尝试用空格替换制表符。**col** 的主要功能是过滤某些文本处理工具的输出，例如 **groff** 和 **tbl**。

```bash
# 这是对 "column" 手页中文件的微调。
printf "%PERMISSIONS OWNER SIZE HH:MM PROG-NAME\n" \
# -t 选项删除了输出的第一行
ls -l | sed 1 | column -t) # 其中 "N" 是通过 "ls -l" 找到的文件数。
exit 0
```

列移除器。它从文件中移除列（字符），并将每行的第二到第四字符写回 **stdout**。

如果文件包含制表符或不可打印字符，可能会导致不可预测的行为。在这种情况下，考虑在 col 之前使用 expand 和 unexpand。

nl 将文件名列表到 stdout，但在每个非空行开头插入连续数字。默认情况下如此。

# 12–21. nl: 自动编号脚本。

```bash
#!/bin/bash
# 此脚本将自身回显到 stdout 并带有行号。
# 'nl' 将上述行视为第 3，因为它不列出空行。
# 'cat -n' 将上述行视为第 5。
nl 'basename $0'
# 注意 'nl -ba' 也会做到这一点。
exit 0
```

列格式化器。它将文件 (stdout) 分页，用于硬拷贝打印或在屏幕上查看。各种选项允许行和列的操作、合并行、添加页眉以及合并文件等。pr 命令结合了 nl、paste 和 expand 的许多功能。

```bash
pr -o 5 --widths=65 file | # 给出一个 5 和 65 列的精美分页输出。
```

一个特别用的选项是 -d，强制双倍间距（效果相当于 sed -G）。一个用于本地化并将程序输出翻译成外语的 GNU 工具。主要用于 C 程序，并在 shell 脚本中使用。一个将文件转换为不同编码（字符集）的工具。它的主要用途是本地化。考虑这个高级版本的 iconv。这个将文件转换为不同编码的通用工具不是标准 Linux 安装的一部分。

## TeX, gs

- **TeX 和 Postscript** 是用于准备打印或格式化视频显示的文本标记语言。

**TeX** 是 Donald Knuth 复杂的排版系统。通常编写一个 shell 脚本来封装给这些标记语言之一的所有选项和参数是非常方便的。

*Ghostscript (gs)* 是一个 GPL Postscript 解释器。

## groff, tbl, eqn

另一种文本标记和显示格式语言是 **groff**。它是古老的 UNIX roff/tbl 显示和排版包的增强 GNU 版本。Manpages* 使用 **groff**（参见示例 A–1）。

**tbl** 处理工具被认为是 **groff** 的一部分，其功能是将表格标记转换为 **groff** 命令。**eqn** 方程处理工具同样是 **groff** 的一部分，其功能是将方程标记转换为 **groff** 命令。

## lex, yacc

**lex** 词法分析器产生用于模式匹配的程序。在 Linux 系统上已被非专利的 **flex** 代替**yacc** 工具根据一组规范创建解析器。在 Linux 系统上已被非专利的 **bison** 代替。

## 12.5. 文件和归档命令

### 归档

### tar

标准的 UNIX 归档工具。最初是一个磁带归档（Tape Archiving）程序，它已发展成为一个通用软件包，可以处理所有类型的目标设备，从磁带驱动器到除 stdout 外的所有文件（参见示例 4–4）。GNU tar 早已修复以接受 **gzip** 压缩选项，如 `tar czvf archive-name.tar.gz *`，它递归地归档并压缩目录树中的所有文件，当前工作目录 ($PWD) 中的隐藏文件。

一些常用的 tar 选项：

- 1. -c（创建新归档）
- 2. --delete（从归档中删除文件）

