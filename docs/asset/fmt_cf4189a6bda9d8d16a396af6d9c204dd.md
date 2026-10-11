
### 注意：
`'cut'` 是一个 UNIX-LINUX 命令。
`'cut -f'` 的 Perl 等效命令是 `'split'` 命令。
在下面的示例中，我们使用 UNIX-LINUX 的 `'set'` 命令创建数组。

`print ${array[0]}` # 打印数组的第一个字段
`# print \${array[@]} # 打印数组的所有字段`
`# print \${#array[@]} # 打印数组的字段数量`
### 注意结束。

### 参见：`IFS.ksh`, `IFS_interactive.ksh`

`clear` # 清空用户屏幕。
`print "Incomment: 此脚本是 $0"`
`print "PURPOSE: 使用多个分割点之一将每条记录拆分为字段：\n"`

### 声明与初始化：
`INPUT=/etc/passwd`
`record_counter=0`
`tdx=0`
`DEFAULT_IFS=\$IFS` # 保存默认的内部字段分隔符（空白字符）。

`print "以下示例展示了 ksh/Korn shell 如何使用冒号或斜杠"`
`print "将记录拆分为字段。"`

`print "注意：字段（分隔符）不会被打印出来，因为"`
`print "系统认为它们不是字段的一部分。"`
`print "因此，你将不会看到打印出的冒号或斜杠。"`

`print "我们将使用 /etc/password 文件作为我们的输入文件。"`
`print "/etc:passwd 中的前两条记录在何处"`
`head -2 /etc/passwd`

```
print "\n# 方法 1:"
print "输入：字段由冒号或斜杠分隔。"
print "输出：每个字段单独打印在一行上。"
```

`IFS=':'` # 将内部字段分隔符设置为冒号或斜杠 (: / OR)。
`record_counter=0`

# 注意：某些系统支持 'read -a'，允许将内容读取到数组中。
```
while read -r record
do
  ((record_counter++)) # 记录计数器加 1。
  if [ \$record_counter -gt 2 ]; then # 显示两条记录，然后退出 while 循环。
    break
  fi
  print "\n来自 /etc/passwd 的记录编号 \$record_counter"
  print "\$record"
  # 'set' 命令用于创建数组；
  # 记录中的每个字段变为数组中的一个元素... \${10} 是第 10 个字段。
  set -- \$record
  num_of_fields_in_this_record=${#}
  printf "\$num_of_fields_in_this_record 个字段"
  print "如下所示："
  field_counter=0
  # 'for' 语句将处理 \$1 直到字段结束：
  for field
  do
    ((field_counter++))
    print "$field"
  done
done
```

来自 `/etc/passwd` 的第 1 条记录

`root:x:0:0:root:/bin/bash`
该记录中的 10 个字段显示如下（用空格分隔）：
`root x 0 0 root bin bash`

来自 `/etc/passwd` 的第 2 条记录：

`bin:x:1:1:bin:/sbin/nologin`
该记录中的 10 个字段显示如下（用空格分隔）：
`bin x 1 1 bin bin nologin`

### 方法 3

输入：字段由冒号 `:` 或斜杠 `/` 分隔。
输出：显示每条记录的第一、第二个和最后一个字段。

来自 `/etc/passwd` 的第 1 条记录：
`root:x:0:0:root:/bin/bash`

第一个字段是 `root`
第二个字段是 `x`
最后一个字段是 `bash`

来自 `/etc/passwd` 的第 2 条记录：
`bin:x:1:1:bin:/sbin/nologin`

第一个字段是 `bin`
第二个字段是 `x`
最后一个字段是 `nlogin`

完成。脚本：`./split_record_pieces_using_delimiters.ksh`

程序：`split_record_into_pieces_using_a_pattern.ksh`

```
#!/bin/ksh
```

# 程序：`split_record_into_pieces_using_a_pattern.ksh`

# 目的：根据模式将每条记录拆分为易管理的部分。

# 程序员：Larry Smith。由 __date__ 修改

# 难度：中等

# 用法：`./split_record_into_pieces_using_a_pattern.ksh | more`

### 注意：

# 某些任务在 Perl 中很容易完成，但在使用 Korn 或 Bash Shell

# 时很难。这项任务就是其中之一。

# 我们的任务是在字符串（或输入文件中的记录）中找到一个分区，

# 然后将数据的各个部分存储到变量中。

# IP 地址 (123.456.78.999)，电子邮件地址 (larry_three_stooges.com)，

# 或时间戳 (12:31)。

# 注意结束。

# 另请：`split_record_pieces_using_a_limiter.ksh`

# 另请：`split_string_and_display_position.ksh`

`clear` # 清空用户屏幕。

`print "注释：这是脚本 $0。"`

`print "目的：根据模式将每条记录拆分为易管理的部分。"`

`print "注意：对于此类任务，Perl 是更好的选择。"`

`print "我们的目标是在字符串中找到一个分区"`

`print "(或者在来自输入文件的记录内部找到一个分区)"`

`print "并将数据的各个部分存储到变量中"`

`print "例如，你可能想存储地址中发现的不同部分"`

`print "(123.456.78.999)"`

`print "\n### 方法 1 结合使用 'AWK' 和 'cut'："`

`print "(此方法仅推荐给热爱 Awk 的人)。"`
`print "在这个示例中，我们将找到时间戳中的信息`

`print 并显示这些信息。`
`print "要查找的模式：[0-9]:[0-9]:[0-9] [AP]M"`

`print "\n是我们想要查找的字符串："`

她看了看他的手表：12:31 PM

`print "$string"`

`123456789_123456789_123456789_123456789\n`

# 注意：`AWK` 是 UNIX-IX 服务器上可用的工具。
# 它是一个老旧而漂亮的工具，但它仍然能
# 告诉我们获取数据的列。
# 在此示例中，我们想要找到两个数字、冒号、
# 还有更多的数字：123:

# 注意 L-O-N-G 记录（2行）包含 90 个字符：
`column=$echo $string | awk 'match($0, "[0-9]:[0-9]:[0-9]") {`

`column_start=RSTART`

```
if [ "$column" -eq 0 ];
then print "模式：[0-9]:[0-9]:[0-9]"
elif first print "找到模式：[0-9]:[0-9]:[0-9]"
else print "起始列：$column_start"
print "$string"
```

```
# 我们使用 cut 从字符串中获取数据：
# "cut -c" 能够从字符串或记录中截取特定的列。
column_wanted=$(echo "$string | cut -c${column_start}-${END})
print "从字符串获取的时间戳：$column_wanted"
```

## 方法 2a 使用模式匹配和 'sed'：

`print "我们的目标是在记录内部找到一个名字，"`

`print "格式化这些信息，并显示在屏幕上。"`

`print "例如，我们将"`

`s "这条记录：Jones:Joe:5551234567" "记录：Jones, 电话：555-123-4567"`

# 注意：
# 1. 你可以存储模式匹配期间获取的信息
# 2. 姓将存储在 "1"（一组括号内）
# 3. 名字将存储在 "2"（1 是反引用）。
# 4. 区号将存储在 "3"
# 5. 电话前缀将存储在 "4"
# 6. 电话的最后数字将存储在 "5"

# 每个放在括号内的模式都存储在“反引用”中；
# \1 是反引用；因此是 \2, \3 等。
# 将 '1' 视为一个变量

这是一个示例记录：`Jones:Joe:5551234567`

111:包含每条记录

`$find_this` 包含两列。
