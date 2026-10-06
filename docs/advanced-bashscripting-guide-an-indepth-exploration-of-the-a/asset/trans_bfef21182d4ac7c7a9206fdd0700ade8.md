

# 高级 Bash 脚本指南

```bash
bash5 -n Linux osinfo.txt
2:这是一个包含 Linux 信息的文件。
6:GPL 规定了 Linux 系统的分发。
```

-v（或 --invert-match）选项会过滤掉匹配项。

```bash
grep pattern1 *.txt  grep pattern2

# 匹配 "*.txt" 中所有包含 "pattern1" 的行，
# 但***不包含*** "pattern2"。
```

-c (--count) 选项提供匹配项的数字计数，而不是实际列出匹配项。

```bash
grep -c txt *.sgml  # ("txt" 在 "*.sgml" 文件中出现的次数)

grep -cz ^ dot
# 意味着计数 (-c) 以零分隔 (-z) 分隔且匹配 " 的项，
# 即非空项（至少包含 1 个字符）。
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' grep -cz # 4
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' grep -cz '\$' # 5
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' grep -cz '^' # 5

printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' grep -c '$' # 9
# 默认情况下，换行符 \n 用作匹配项的分隔符。
```

```bash
# 注意 -z 选项是 GNU "grep" 特有的。
```

```bash
# 感谢，S.C.
```

当给出多个目标文件时，grep 会指定哪一个文件包含匹配项。

```bash
bash$ grep Linux osinfo.txt misc.txt
osinfo.txt:这是一个包含 Linux 信息的文件。
osinfo.txt:GPL 规定了 Linux 系统的分发。
misc.txt:Linux 操作系统正在稳流行。
```

> 若要强制 grep 在仅搜索单个目标文件时显示文件名，只需将 /dev/null 作为源即可。

```bash
bash$ grep Linux osinfo.txt /dev/null
osinfo.txt:这是一个包含 Linux 信息的文件。
osinfo.txt:GPL 规定了 Linux 系统的分发。
```

如果有成功匹配，grep 返回退出状态 0，这使得它在脚本的条件测试中非常有用，特别是配合使用 -q 选项抑制输出时。

```bash
SUCCESS=0 # 如果 grep 查找成功
word=Linux
```

## 12.4. 文本处理命令

# 高级 Bash 脚本指南

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

示例 30-5 展示了如何使用 grep 在系统日志文件中搜索单词模式。

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
        echo "$output    # sed -ne "/$1/|^|${file}:|p" 等于上述操作。
    fi
done

exit 0
```

# 练习：
# 1) 如果任何给定文件中有多个匹配项，则在输出中添加换行。
# 2) 添加功能。

egrep 等于 grep-E。它使用了一套稍不同的扩展正则表达式，可以使搜索更灵活。

fgrep 等于 grep-F。它执行字面字符串搜索（不使用正则表达式），据称

# 12.4. 文本处理命令

# 高级 Bash 脚本指南

可以稍微提高速度。

**agrep** 扩展了 **grep** 的功能以实现近似匹配。搜索字符串与结果匹配项之间允许指定数量的差异。该工具不是 Linux 发行版的核心。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_169_0.png)

要搜索压缩文件，使用 **zgrep**、**zegrep** 或 **zfgrep**。它们也可以用于非压缩文件，尽管速度比普通的 **grep**、**egrep**、**fgrep**慢。对于搜索混合文件非常方便。

要搜索 **bzipped** 文件，使用 **bgrep**。

**look** 命令的作用类似于 **grep**，但它对“字典”（排序后的列表）进行查找。默认情况下，**look** 在 /usr/dict/words 中搜索匹配，但可以指定不同的字典文件。

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
```

# 12.4. 文本处理命令

# 高级 Bash 脚本指南

```bash
do if [ "$word" != "end" ];
then
    echo "$word 是有效的的。"
else
    echo "$word 是无效的。"
fi
done
```

（注：OCR 文本在后半部分包含严重的损坏和碎片化的句子。我已根据标准的 Bash 使用法和提供的上下文片段重构了逻辑流。）

