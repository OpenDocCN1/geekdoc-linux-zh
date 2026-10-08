

# 高级 Bash 脚本编写指南

```
#!/bin/bash
# dict-lookup.sh
```

# 此脚本用于在 1913 版韦伯士字典中查找定义。
# 这本公共领域字典可以从多个网站下载，包括
# 古籍登堡项目 (http://www.gutenberg.org/etextet/247)。

# 在使用此脚本之前，请将其从 DOS 格式转换为 UNIX 格式（行尾保留 LF）。
# 将文件存储为纯文本、未压缩的 ASCII 格式。
# 在下方设置 DEFAULT_DICTFILE 变量为路径/文件名。

```
E_BADARGS=85
MAXCONTEXTLINES=50 # 显示的最大行数。
DEFAULT_DICTFILE="/usr/share/dict/webster1913-dict.txt"
# 默认字典文件名。
# 根据需要修改此项。
```

# 注意：
# 1913 版韦伯士字典的这一特定版本
# 每个条目都以大写字母开头
# （其余字符为小写）。
# 只有条目的“第一行”是这样开头的
# 搜索算法正是这样工作的。

```
if [[ -z "$1" ]]; then sed -n '/[^A-Z]//p'
# 必须至少指定要查找的单词，
# 且它必须以大写字母开头。
then
echo "Usage: basename $0 Word-to-define [dictionary-file]"
echo
echo "Note: Word to look up必须以大写字母开头，
单词其余部分为小写。"
echo "------------------------------------------------"
echo "Examples: Abandon, Dictionary, Marking, etc."
    exit $E_BADARGS
fi
```

```
if [ -z "$2" ]; then
dictfile=$DEFAULT_DICTFILE
else
dictfile="$2"
fi
```

```
Definition=$(grep -A $MAXCONTEXTLINES "$1" "" "$dictfile")
    # 格式为 "Word..." 的定义
```

# 而且，是的，“grep" 的速度足够搜索
# 即使是非常大的文本文件。

```
# 现在，截取出定义块。
echo "$Definition" |
sed -n '/^\[A-Z\]]/p'
# 从输出的第一行开始打印
+# 到下一个条目的第一行。
sed '$d' | sed 'd'
# 删除输出的最后两行
+# （空行和下一个条目的第一行）。
#
```

exit $?

# 练习题：

+   # 1) 修改脚本以接受任何类型的字母输入
+# （大写、小写、混合大小写），并将其转换为
+# 可处理的格式。

+   # 2) 将脚本转换为 GUI 应用程序，
+# 使用类似 'dialog' 或 'zenith' 的工具
# 脚本将不再从命令行
+# 获取其参数。

+   # 3) 修改脚本以解析其他可用的
+# 公共字典，例如美国人口普查局地名索引。

> 参见示例 A-41，获取在大文件上进行快速 fgrep 查找的示例。

agrep (近似 grep) 扩展了 grep 的功能用于近似匹配。搜索字符串与匹配结果之间存在指定数量的差异。此工具不是 Linux 核心发行版的一部分。

> 要搜索压缩文件，请使用 zgrep、zegrep 或 zgrep。这些也适用于非压缩文件，尽管比纯 grep、egrep、fgrep 慢。它们对于搜索混合了部分压缩和未压缩的文件集非常方便。

要搜索 bzipped 文件，请使用 bgrep。

该命令的工作原理类似于 grep，但会对“字典”（一个排序后的列表）进行查找。默认情况下，look 在 /usr/dict/words 中搜索匹配，也可以指定不同的字典文件。

示例 16-20. 检查列表中单词的有效性

```
#!/bin/bash
# lookup: 对数据文件中的每个单词进行字典查找。
file=words.data # 从其中读取测试单词的数据文件。
echo
echo "Testing file $file"
echo

while [ "$word" != "end" ];
do
  # 数据文件中的最后一个单词。
read word # 从数据文件读取，因为循环末尾有重定向。
look $word > /dev/null # 不需要显示字典文件中的行。
# 在文件 /usr/share/dict/words 中搜索单词
+# （通常是 linux.words 的软链接）？
# look 命令的退出状态。
```
if [ "$lookup" -eq 0 ];
then
    echo "$word" 是有效的。"
else
    echo "$word" 是无效的。"
fi

done <"$file" # 重定向 stdin 到 $file，因此读取内容来自该文件。

```

echo

```
exit 0

#
# 下方的代码将不会执行，因为上面有 "exit" 命令。

# Stephane Chazelas 提了以下更简洁的替代方案：
while read word && [[ "$word" != "end" ]];
do
    if look "$word" > /dev/null
    then echo "$word" 是有效的。"
    else echo "$word" 是无效的。"
    fi
done <"$file"
```
exit 0

```sed

适用于解析文件和命令输出的脚本语言。可以单独使用或嵌入 shell 脚本中。

awk

非交互式“流编辑器”，允许在批量处理中使用许多 awk 命令。它在 shell 脚本中有许多用途。

wc

编程的文件提取器和格式化工具，用于处理和提取结构化文本文件的字段（列）。其语法与 C 语言相似。

对文件或 I/O 流给出“单词计数”：

```bash
bash $ wc /usr/share/doc/sed-4.1.2/README
13 70 447 README
[13 行 70 个单词 447 个字符]
```

+   wc -l 只显示行数。
wc -c 只显示字节数。
wc -m 只显示字符数。
wc -L 只显示最长行的长度。
```

