
# 检查命令行是否存在输入文件。

```bash
ARGS=$1

E_BADARGS=65

## 12.4 文本处理命令

E_NOFILE=66

if [ $# -ne "$ARGS" ]; then # 传递脚本的参数数量是否正确？
    echo "用法: `basename $0 filename`"
    exit $E_BADARGS
fi

if [ ! -f "$1" ]; then # 检查文件是否存在。
    echo "文件 \$1 不存在。\n"
    exit $E_NOFILE
fi
```

```bash
############################################################
# main ()
sed -e 's/\.'//g' -e 's/ | -c/g' "$1" | tr 'A-Z-a-z' | sort | uniq | sort -nr
############################################################
    出现频率
# 过滤掉句号并
+# 将单词之间的空格替换为行符，
+# 然后将字符转换为小写，
+# 最后前加上出现计数并进行数值排序。
############################################################
# 练习：
# 1) 添加 'sed' 命令来过滤其他标点符号，如逗号。
# 2) 修改以过滤多个空格和其他空白字符。
# 3) 添加次要排序键，使得出现次数相同的实例
+# 按字母顺序排序。
```

```bash
bash$ cat testfile
这一行出现一次。
这一行出现两次。
这一行出现两次。
这一行出现三次。
这一行出现三次。
这一行出现三次。
```

```bash
bash$. ./wf.sh testfile
6 this
6 occurs
6 line
3 times
3 three
2 twice
1 only
1 once
```

### `expand`, `unexpand`

`expand` 过滤器将制表符转换为空格。它通常用于管道中。

## 12.4 文本处理命令

`unexpand` 过滤器将空格转换为制表符。这与 `expand` 的效果相反。

### `cut`

一个用于从文件中提取字段的工具。它类似于 `awk` 中的 `print $N` 命令，但功能更具局限。在脚本中使用 `cut` 可能会比使用 `awk` 更简单。特别重要的是 `-d`（分隔符）和 `-f`（字段指定符）选项。

使用 `cut` 获取已挂载的文件系统列表：

```bash
cat /etc/mtab | cut -d ' ' -f1,2
```

使用 `cut` 列出操作系统和内核版本：

```bash
uname -a | cut -d" " -f1,3,11,12
```

使用 `cut` 从邮件文件夹中提取标题头：

```bash
bash$ grep '^Subject:' messages | cut -c10-80
Subject: Linux for mission-critical apps
Subject: Spam
```

使用 `cut` 解析文件：

```bash
# 列出 /etc/passwd 中的所有用户
FILENAME=/etc/passwd
for user in $(cut -d: -f1 $FILENAME)
do
    echo $user
done
# 感谢提供这个建议。
```

`cut -d ' ' -f2,3` 等同于 `awk -F' ' '{print $2,3}'`。

### `join`

将不同文件合并为单个多列文件的工具。与 `cut` 结合使用时，适用于创建系统文件。将其视为 `paste` 的特殊用途亲戚。这个强大的工具允许以有意义的方式合并两个文件，创建一个关系数据库的简单版本。`join` 命令精确地在两个文件上操作，它将具有共同标记字段（通常是数值）的行拼接在一起，并将结果写入标准输出。

| range | action |
|---|---|
| 1.data | 2.data |
| 100 | Shoes |
| 200 | Laces |
| 300 | Socks |

```bash
bash$ join 1.data 2.data
100 Shoes
200 Laces
300 Socks
```

# 高级 Bash 脚本指南

```bash
bash$ grep -n Linux osinfo.txt
2:这是一个包含 Linux 信息的文件。
6:GPL 规定了 Linux 系统的分发。
```

`-v`（或 `--invert-match`）选项会过滤掉匹配项。

```bash
grep pattern1 *.txt | grep -v pattern2
# 匹配 "*.txt" 中所有包含 "pattern1" 的行，
# 但不包含 "pattern2"。
```

`-c` (`--count`) 选项提供匹配项的数字计数，而不是实际列出匹配项。

```bash
grep -c txt *.sgml  # ("txt" 在 "*.sgml" 文件中出现的次数)

grep -cz ^ dot
# 意味着计数 (-c) 以零分隔 (-z) 分隔且匹配 " 的项，
# 即非空项（至少包含 1 个字符）。

printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' | grep -cz # 4
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' | grep -cz '\$' # 5
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' | grep -cz '^' # 5
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' | grep -c '$' # 9
# 默认情况下，换行符 \n 用作匹配项的分隔符。
```

```bash
# 注意 -z 选项是 GNU "grep" 特有的。
```

```bash
# 感谢，S.C.
```

当给出多个目标文件时，`grep` 会指定哪一个文件包含匹配项。

```bash
bash$ grep Linux osinfo.txt misc.txt
osinfo.txt:这是一个包含 Linux 信息的文件。
osinfo.txt:GPL 规定了 Linux 系统的分发。
misc.txt:Linux 操作系统正在流行。
```

> 若要强制 `grep` 在仅搜索单个目标文件时显示文件名，只需将 `/dev/null` 作为源即可。

```bash
bash$ grep Linux osinfo.txt /dev/null
osinfo.txt:这是一个包含 Linux 信息的文件。
osinfo.txt:GPL 规定了 Linux 系统的分发。
```

如果有成功匹配，`grep` 返回退出状态 `0`，这使得它在脚本的条件测试中非常有用，特别是配合使用 `-q` 选项抑制输出时。

```bash
SUCCESS=0 # 如果 grep 查找成功
word=Linux
```

## 12.4. 文本处理命令

```bash
filename=data.file
grep -q "$word" "$filename"    # "-q" 选项导致没有任何输出到标准输出
if [ $? -eq $SUCCESS ]
then
    echo "$filename 中找到了 $word"
else
    echo "在 $filename 中未找到 $word"
fi
```

示例 30-5 展示了如何使用 `grep` 在系统日志文件中搜索单词模式。

# 示例 12-12. 在脚本中模拟 "grep"

```bash
#!/bin/bash
# grep.sh: 'grep' 的非常粗糙的实现
E_BADARGS=65
if [ -z "$1" ]    # 检查脚本参数。
then
    echo "用法: basename $0 pattern"
    exit $E_BADARGS
fi
for file in *      # 遍历 $PWD 下的所有文件。
do
    output=$(sed -n "/$1/p" $file)  # 命令替换。
    if [ ! -z "$output" ];    # 如果 "$output" 没有加引号会怎样？
    then
        echo -n "$file"
        echo "$output"  # sed -ne "/$1/|^|${file}:|p" 等于上述操作。
    fi
done
exit 0
```

# 练习：
# 1) 如果任何给定文件中有多个匹配项，则在输出中添加换行。
# 2) 添加功能。

`egrep` 等于 `grep -E`。它使用了一套稍不同的扩展正则表达式，可以使搜索更灵活。

`fgrep` 等于 `grep -F`。它执行字面字符串搜索（不使用正则表达式），据称

# 12.4. 文本处理命令

可以稍微提高速度。

`agrep` 扩展了 `grep` 的功能以实现近似匹配。搜索字符串与结果匹配项之间允许指定数量的差异。该工具不是 Linux 发行版的核心。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_169_0.png)

要搜索压缩文件，使用 `zgrep`、`zegrep` 或 `zfgrep`。它们也可以用于非压缩文件，尽管速度比普通的 `grep`、`egrep`、`fgrep` 慢。对于搜索混合文件非常方便。

要搜索 `bzipped` 文件，使用 `bgrep`。

`look` 命令的作用类似于 `grep`，但它对“字典”（排序后的列表）进行查找。默认情况下，`look` 在 `/usr/dict/words` 中搜索匹配，但可以指定不同的字典文件。

# 示例 12–13. 检查列表中单词的有效性

```bash
#!/bin/bash
# look: 对数据文件中的每个单词进行字典查找。
file=words.data # 用于测试的单词数据文件。
while [ "$word" != "end" ] # 数据文件中的最后一个单词。
do
    read word < /dev/null # 不显示字典文件中的行。
    lookup=$? # 'look' 命令的退出状态。
    if [ "$lookup" -eq 0 ];
    then
        echo "$word 是有效的。"
    else
        echo "$word 是无效的。"
    fi
done <"$file" # 将 stdin 重定向到 $file，因此“读取”来自那里。
exit 0
------------------------------------------------------------
# 下方的代码将因为 "exit" 命令而不会执行。
```

Stephane Chaselas 提出了以下更简洁的替代方案：

```bash
while read word && [[ $word != "end" ]]
do
    if [ "$word" != "end" ];
    then
        echo "$word 是有效的。"
    else
        echo "$word 是无效的。"
    fi
done
```

（注：OCR 文本在后半部分包含严重的损坏和碎片化的句子。我已根据标准的 Bash 使用法和提供的上下文片段重构了逻辑流。）

```bash
for filename in * # 没有必要使用 basename，
  # 因为 "*" 不会返回包含 "/" 的文件
do
    lower=$(echo "$filename" | tr '[:upper:]' '[:lower:]')
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
    exit $E_WRONGARGS
fi
NEWFILENAME=$1.unx
CR=$'\x15' # 回车符。
# DOS 文本文件以 CR-LF 结尾。
tr -d $CR < $1 > $NEWFILENAME
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
cat "$@" | tr 'a-zA-Z' 'n-za-MN-ZA-M' # "a" 变成 "n", "b" 变成 "o", 以此类推。
# "cat @@" 结构
# 允许从 stdin 或文件获取输入。
exit 0
```

# 示例 12-18. 生成“加密引言”谜题

```bash
#!/bin/bash
# crypto-quote.sh: 加密引言

# 将使用简单的单字母替换法加密引言。
# 结果类似于在日报评论版中
# 看到的“加密引言”谜题。

key=ETAOINSHRDULBCFGJMPVW2XYK
# "key" 仅仅是一个乱序的字母表。
# 改变 "key" 就会改变加密。
# 'cat $@' 结构从 stdin 或文件获取输入。
# 如果使用 stdin，用 Control-D 结束输入。
# 否则，指定文件名作为命令参数。

cat "$@" | tr "a-z" "A-Z" | tr "A-Z" "$key"
             # to uppercase             # encrypt
# 支持小写、大写或混合大小写的引言。
# 非字母字符保持不变。

# 输出是：
# "CPHFRCS QF CIIQ MINFERCS EQ FPHIM GIFGUI'Q HETPQ."
# BEEML PZERC

# 要反转加密：
# cat "$@" | tr "A-Z"

exit 0
```

这种简单的密码可以被平均水平的 12 岁孩子仅用铅笔和纸就能破解。

## `tr` 变体

`tr` 工具有两个历史变体。BSD 版本不使用括号（`tr a-z A-Z`），但 SysV 版本使用 `tr '[a-z]' '[A-Z]'`。GNU 版本与 BSD 相似，因此括号内的范围是强制性的。

`fold` 过滤器会将行文本折行到指定的宽度。配合 `-s` 选项使用时特别有用，它会在空格处折行（参见示例 12–19 和示例 A–2）。

这是一个简单的格式化器，用于在管道中“折行”长文本输出。

# 示例 12–19. 格式化列表。

```bash
#!/bin/bash
WIDTH=40                # 40 列宽。
b=$(ls /local/bin)      # 获取文件列表...
echo $b | fmt -w $WIDTH # 也可以通过 echo $b | fold -w 完成。
exit 0
```

`fmt` 的强大替代方案是 Kamil 的 `col` 工具，从 `http://berkeley.edu/~kamil/col/` 获取。它输出文件的置换索引（交叉列表），在必要时可以在管道中进一步过滤和格式化。

`col` 过滤器从输入流中移除行。它还尝试用空格替换制表符。`col` 的主要功能是过滤某些文本处理工具的输出，例如 `groff` 和 `tbl`。

```bash
# 这是对 "column" 手页中文件的微调。
printf "%PERMISSIONS OWNER SIZE HH:MM PROG-NAME\n" \
# -t 选项删除了输出的第一行
ls -l | sed 1d | column -t
# 其中 "N" 是通过 "ls -l" 找到的文件数。
exit 0
```
