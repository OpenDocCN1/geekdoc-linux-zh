

# 高级 Bash 脚本指南

```bash
if [ "$fname" != "$sn" ]  # 仅重命名尚未转换为小写的文件。
then
    mv $fname $sn
fi
done
exit 
```

```bash
# 此行以下代码将由于 "exit" 而不会执行。
# 如需运行它们，请删除上行的脚本。
# 上述脚本不适用于包含空格或换行符的文件。
# Stephanie Chazelas 建议采用以下替代方案：

for filename in *  # 没有必要使用 basename，
    do n=$(echo "$filename" | tr '[:upper:]' '[:lower:]') # 因为它不会返回任何包含 "/" 的文件
        # POSIX 集合符号。
        # 加上斜杠是为了防止末尾的换行符被
        # 命令替换移除。
        # 变量替换：
        n=${n*/} # 从文件名中移除上面添加的末尾斜杠。
        [ "$filename == "$n" ] || mv "$filename" "$n" # 检查文件名是否已经是小写。
done
exit 0
```

示例 16-23. du: 从 DOS 到 UNIX 的文本文件转换。

```bash
#!/bin/bash
# Du.sh: DOS 到 UNIX 的文本文件转换器。

E_WRONGARGS=85
if [ -z "$1" ]
then
    echo "Usage: `basename $0` filename-to-convert"
    exit $E_WRONGARGS
fi
NEWFILENAME=$1.unix

CR='\015'  # 回车。
# 015 是 CR 的八进制 ASCII 码。
# DOS 文本文件以 CR-LF 结尾。
# UNIX 文本文件仅以 LF 结尾。

tr -d $CR < $1 > $NEWFILENAME
# 删除 CR 并写入新文件。

echo "Original DOS text file is \"$1\""
echo "Converted UNIX text file is \"$NEWFILENAME\""

exit 0

# 练习：
```

第 16 章 外部过滤器、程序和命令

# 高级 Bash 脚本指南

```bash
# -------
# 修改上述脚本以实现从 UNIX 转换为 DOS。
```

# 示例 16-24. rot13: 弱加密。

```bash
#!/bin/bash
# rot13.sh: 经典的 rot13 算法，
#                 足以欺骗 3 岁小孩
#                 大约 10 分钟的加密。

# 使用方法: ./rot13.sh filename
# 或    ./rot13.sh <filename>
# 或    ./rot13.sh 并提供键盘输入 (stdin)

cat "$@" | tr "a-zA-Z" "n-za-ZA-M" # "a" 变为 "n", "b" 变为 "o..."
# cat "$@" 结构
# 允许从标准输入或文件输入。

exit 0
```

# 示例 16-25. 生成“加密引言”谜题

```bash
#!/bin/bash
# crypto-quote.sh: 加密引言

# 将使用简单的单字母替换来加密引言。
# 结果类似于周日报社论版页面中
# 常见的“加密引言”谜题。
```

```bash
key=ETAINOQHSRDLUBFCGMQPVWZYXK
# “key”只是一个乱序的字母表。
# 更改“key”会改变加密结果。

# cat "$@" | tr "a-zA-z" "A-Z" "$key"
# | 大写加密
# 适用于小写、大写或混合大小写的引言。
# 让非字母字符原样通过。
```

```bash
# 尝试用以下内容运行脚本：
# "Nothing needs reforming as other people's habits."
# --Mark Twain

# 输出为：
# #CFPHCS Q CIQOI MINBRCS EQ FPHIM GIFUI'Q HETRQP.
# --BEML FEERC
```

```bash
# 要反转加密
# cat "$0" | tr "$key" "A-Z"

# 这种简单的密码可以被普通的 12 岁小孩
# 仅用纸笔就能破解。

exit 0
```

第 16 章 外部过滤器、程序和命令

```bash
# 练习：
# 修改脚本，使其根据命令行参数
# 执行加密或解密。
# tr 非常适合用于代码混淆。
```

```bash
#!/bin/bash
# jabsh.sh

x="wftedskaebjgdbstbdsmmnjgz"
echo $x | tr "a-z" "oh, turtleneck Prase!"

# 基于维基百科文章“Just another Perl hacker”。
```

# tr 变体

tr 有两个历史悠久的变体。BSD 版本不使用括号 (tr a-z A-Z)，SysV 版本使用 (tr '[a-z]' '[A-Z]')。GNU 版本的 tr 与 BSD 版本相似。

一个用于将输入行包装到 fmt 格式的过滤器是 Kamil Tomar 的 fmt 工具，可以从 http://www.cs.berkeley.edu/~amc/ 获取。参见示例 16-26 和示例 A-1。

简单的文件格式化工具，用于折叠行。

示例 16-26. 格式化列表。

```bash
#!/bin/bash
WIDTH=40
# 输出被折叠为 $WIDTH 个字符。
pr -s $WIDTH < input.txt
```

`pr` 命令用于为打印格式化文本，添加页眉、页脚和页码。它还可以将文本分列显示。

```bash
# -w 设置宽度
# -s 添加自定义后缀
# -h 添加标题
pr -w 80 -s " Page " -h "My Report" input.txt
```

`fold` 命令用于将行折叠为指定的宽度。

```bash
# -w 指定每行的最大宽度
# -s 只在空格处折行
fold -w 80 -s input.txt > wraped_output.txt
```

`column` 命令用于将多列格式。

```bash
# -t 将输入视为表格并对齐列
column -t < input.txt
```

`paste` 命令将文件的行合并。默认情况下合并列。

```bash
# 使用逗号分隔符合并两个文件
paste -d ',' file1.txt file2.txt
```

`sort` 命令用于对文件行排序。

```bash
# 数字反序排序
sort -nr numbers.txt
```

`uniq` 命令用于过滤或排序文件中相邻行。它要求输入先进行排序。

```bash
# 过滤掉重复行
sort file.txt | uniq
```

`grep` 命令用于在文件中搜索匹配正则表达式的行。

```bash
# 搜索包含 "error" 的行
grep "error" log.txt
```

`sed` 命令是一种流编辑器，用于过滤和转换文本。

```bash
# 全局替换第一个出现的 "old" 为 "new"
sed 's/old/new/g' file.txt
```

`awk` 命令是一种用于文本和数据的强大模式处理语言。

```bash
# 打印文件的第一和第三列
awk '{print $1, $3}' data.txt
```

