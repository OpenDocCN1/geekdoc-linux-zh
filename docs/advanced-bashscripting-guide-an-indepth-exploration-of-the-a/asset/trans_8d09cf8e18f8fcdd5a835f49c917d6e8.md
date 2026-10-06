

# 高级 Bash 脚本指南

◆ column 3 = 两者共有的行。

这些选项允许隐藏一或多列的输出。

- ◆ -1 隐藏第 1 列
- ◆ -2 隐藏第 2 列
- ◆ -3 隐藏第 3 列
- ◆ -12 隐藏第 1 列和第 2 列，以此此类推

## uniq
此过滤器从排序后的文件中删除重复行。它通常与 sort 配合管道使用。

```bash
cat list-1 list-2 list-3 | sort | uniq > final.list
# 合并列表文件，
# 对它们进行排序，
# 移除重复行，
# 最后将结果写入输出文件。
```

有用的 -c 选项会在输入文件的每行前加上该行出现的次数。

```bash
bash cat testfile
这一行只出现一次。
这一行出现了两次。
这一行出现了两次。
这一行出现了三次。
这一行出现了三次。
这一行出现了三次。
```

```bash
bash$ uniq -c testfile
1 这一行只出现一次。
2 这一行出现了两次。
3 这一行出现了三次。
```

```bash
bash sort testfile | uniq -c | sort -nr
3 这一行出现了三次。
2 这一行出现了两次。
1 这一行只出现一次。
```

`sort INPUTFILE | uniq -c | sort -nr` 命令会生成 INPUTFILE 文件的出现频率列表（-nr 选项导致反向数值排序）。该模板用于日志文件和字典列表的分析，适用于任何需要检查文档词法结构的地方。

## 示例 12–9. 词频分析

```bash
#!/bin/bash
# wf.sh: 对文本文件进行粗略词频分析。

# 检查命令行是否存在输入文件。
ARGS=$1
E_BADARGS=65
```

## 12.4 文本处理命令

```bash
E_NOFILE=66

if [ $# -ne "$ARGS" ]; then # 传递脚本的参数数量是否正确？
then
    echo "用法: `basename $0 filename`"
    exit $E_BADARGS
fi

if [ ! -f "$1" ]; then # 检查文件是否存在。
then
    echo "文件 \$1 不存在。\n
    exit $E_NOFILE
fi
```

```bash
############################################################
# main ()
sed -e 's/\.'//g' -e s/ | -c/g "$1" | tr 'A-Z-a-z' | sort | uniq | sort -nr
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

### expand, unexpand

expand 过滤器将制表符转换为空格。它通常用于管道中。

## 12.4 文本处理命令

unexpand 过滤器将空格转换为制表符。这与 expand 的效果相反。

### cut

一个用于从文件中提取字段的工具。它类似于 awk 中的 `print $N` 命令，但功能更具局限。在脚本中使用 cut 可能会比使用 awk 更简单。特别重要的是 -d（分隔符）和 -f（字段指定符）选项。

使用 cut 获取已挂载的文件系统列表：

```bash
cat /etc/mtab | cut -d ' ' -f1,2
```

使用 cut 列出操作系统和内核版本：

```bash
uname -a | cut -d" " -f1,3,11,12
```

使用 cut 从邮件文件夹中提取标题头：

```bash
bash grep '^Subject:' messages | cut -c10-80
Subject: Linux for mission-critical apps
Subject: Spam
```

使用 cut 解析文件：

```bash
# 列出 /etc/passwd 中的所有用户
FILENAME=/etc/passwd

for user in $(cut -d: -f1 $FILENAME)
do
    echo $user
done
# 感谢提供这个建议。
```
`cut -d ' ' -f2,3` 等同于 `awk -F' ' '{print $2,3}'。

### join

将不同文件合并为单个多列文件的工具。与 cut 结合使用时，适用于创建系统文件。将其视为 paste 的特殊用途亲戚。这个强大的工具允许以意义的方式合并两个文件，创建一个关系数据库的简单版本。join 命令精确地在两个文件上操作，它将具有共同标记字段（通常是数值）的行拼接在一起，并将结果写入标准输出。

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

