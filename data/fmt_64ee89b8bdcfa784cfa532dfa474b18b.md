
# while read -r record
# do
# ((counter++)) # 计数加 1。
# print "这是记录编号: $counter"
# done

还有其他读取文件的方法，但它们更慢；一个例外是：你可以使用“文件描述符”来读取。

### read_cut_to_format.ksh

# 此脚本中读取数据的方法比
# “文件描述符”技术更简单，且速度相同。
# 结束。

清除用户屏幕。

注释: 这是一个脚本。

目的: 展示如何读取 `field1`, `field2` 以及记录的剩余部分。

### 声明与初始化

`INPUT`=`/home/larry/INPUT_files/rest_of_record.txt`

`DEFAULT_IFS`=`$IFS`

`IFS`="" # 保存默认字段分隔符（空格）。

# 首先，创建一个小文件作为输入：

`print` "这是 `$field1` 这里的 `$field2` 记录的剩余部分。" > `$INPUT`

`print` "一_二_三_四_五!" >>`INPUT`

这展示了如何解析 `field1`, `field2` 以及记录的剩余部分。

`IFS` 是分隔符，在每个记录中的

`cat` `$INPUT`

`print` "我们的两行"

`is_space_test.ksh` (等等，这里断开了，但逻辑从 END_TEST 继续)

```bash
# 如果你想“压缩”多个制表符和空格，请取消行的注释：
cat $INPUT | tr -s "[[:space:]]" " " $INPUT
# 注意：tr 有一个压缩选项 (-s) 可以将
# 多个制表符替换为单个空格，记录中的每个字段由空格隔开。
counter=0
IFS='' # IFS，字段分隔符已设为空。
while read -r field1 field2 rest_of_record
do
  ((counter++)) # 计数加 1。
  print "\n处理记录编号: $counter"
  print "field1: $field1"
  print "field2: $field2"
  # 如果 $rest_of_record 不包含空字节，则打印它：
  if [ -z "$rest_of_record" ]; then
    print "rest_of_record: $rest_of_record"
  fi
done < INPUT_squeezeed

print 重要：
IFS，内部字段分隔符很重要。
默认的 IFS 是空白（空格、制表符、换行）。
当你将 IFS 设置为空（IFS=''），记录的剩余部分 field1 field2 rest_of_record 不会给你预期的结果；就像你编写了 'record' 一样。
以下示例展示了这一事实。

counter=0
IFS='' # 字段分隔符已设为空。
while read -r field1 field2 rest_of_record
do
  ((counter++)) # 计数加 1。
  print "\n处理记录编号: $counter"
  print "field1: $field1"
  print "field2: $field2"
  # 如果 $rest_of_record 不包含空字节，则打印它：
  if [ -z "$rest_of_record" ]; then
    print "rest_of_record: $rest_of_record"
  fi
done < INPUT_sezed

# 恢复系统默认值（这里没必要，但是个好习惯！）
IFS="NONE. 脚本: $0\n"
```

# 程序：read_inside_read.ksh

# 目的：此脚本允许你在 'read' 内部执行另一个 'read'。

# 比较两个文件；；两个文件均已预先排序；

# 记录数相同；且字节数相同。

# 另见：compare_files.ksh，它不需要两个文件包含

# 相同的记录数（或要求记录预先排序）。

# 程序员：Larry Smith。由 _________ 修订。

# 难度：挑战性（使用了“文件描述符”和“read -u”）。

# 用法：./read_inside_read.ksh

# 注意：

# 'read -u' 允许我们从“文件描述符”读取（read -u A4.rec）。

# "read_and_cut_to_format_rec.ksh" 也使用了文件描述符。

# UNIX 'diff' 和 'comm' 工具均能比较 2 个文件。

#（要比较两个二进制文件，请使用 'cksum'）。

#

# 由于总页数的原因，此脚本

# 未包含在 Rosetta Stone 系列中。

# 结束备注。

`print` "注释：此脚本是 `$0`。"

`print` "目的：此脚本允许你在 'read' 内部执行 'read'。"

`print` "比较两个文件；；两个文件均已预先排序；记录数相同"

`print` "，且字节数相同。"

`print` "另见：compare_files.ksh，它不需要两个文件包含"

"相同的记录数（或要求记录预先排序）。"

### 初始化：

`integer` `counter` `recs_IN_FILE_A`=0

`integer` `recs_IN_FILE_B`=0

`integer` `make_counter`=0

`integer` `buffer_counter`=0

`REPORT`=`/tmp/report_file_comparison.results.txt`

`IN_FILE_A`=`/tmp/IN_FILE_A`

`IN_FILE_B`=`/tmp/IN_FILE_B`

###

# >REPORT 删除 REPORT 中的所有记录（如果已存在）。

# 创建两个小型测试文件：

`print` "1111111" >> `$IN_FILE_A`

`print` "2222222" >> `$IN_FILE_B`

`print` "3 3 3" >> `$IN_FILE_A`

`print` "4444444" >> `$IN_FILE_A`

####

`print` "1111111" >> `$IN_FILE_B`

`print` "2222222" >> `$IN_FILE_B`

`print` "3333333" >> `$IN_FILE_B`

`print` "4444444" >> `$IN_FILE_B`

############################################################

# 验证两个输入文件是否存在，然后...

# 如果是普通文件且有大小（不为空）并且是读的，\
if [[ -f "$IN_FILE_A" && -s "$IN_FILE_A" && -r "$IN_FILE_A" ]];
then : # 什么都不做；我们看起来很不错！
else print "$IN_FILE_A 无效或为空。正在退出。"
exit 1
fi

if [[ -f "$IN_FILE_B" && -s "$IN_FILE_B" && -r "$IN_FILE_B" ]];
then : # 什么都不做；我们看起来很不错！
else print "\n$IN_FILE_B 无效或为空。正在退出。"
exit 1
fi

# 414
fi

# 你必须使用 exec 来打开两个不同的文件描述符来读取
# 这两个输入文件。简单的“read-嵌套-read”逻辑将无法正常工作。
# 'fd' 选项允许我们从文件描述符读取。

exec 5<SIN_FILE_A
exec 5<SIN_FILE_B

# 处理中...

# 主处理：

FILE_A_EOF_y_or='n' # 'EOF' 意味着文件结束
FILE_B_EOF_y_or='n'

print "正在比较以下两个文件：" >>REPORT
print "IN_FILE_A: $IN_FILE_A" >>REPORT
print "IN_FILE_B: $IN_FILE_B" >>REPORT

while [[ $FILE_A_EOF_y_or == 'n' && $FILE_B_EOF_y_or == 'n' ]]; do
  read -u A_rec
  # 'read -u' 选项允许我们从“文件描述符”读取 (-u4)。
  if [[ $? -eq 0 ]]; # 如果读取成功，说明我们还没到达文件末尾。
    then((counter_rec_in_IN_FILE_A++)) # 计数器加1
    FILE_A_EOF_y_or='y'
    break
  fi
  # 跳出 while 循环（但不退出脚本）。
done

read -u B_rec
# 'read -u' 选项允许我们从“文件描述符”读取 (-u5)。
if [[ $? -eq 0 ]]; # 如果读取成功，说明我们还没到达文件末尾。
  then((counter_rec_in_IN_FILE_B++)) # 计数器加1
  FILE_B_EOF_y_or='y'
  break
fi
# 跳出 while 循环（但不退出脚本）。
fi
