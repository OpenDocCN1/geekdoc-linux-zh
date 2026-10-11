
# 用法

`./for.ksh` `argument1` `argument2` `argument3` `more`

`./for.ksh/larry/ROSETTA/INPUT_FILES/REGION*` `more`

```bash
for arg in $*; do print "ARGUMENT FROM COMMAND LINE: $arg";done
```

### 示例 6B

`print` `"显示 $* 或 @@ 包含命令行中的参数。"`

```bash
if [ $# -gt 0 ]; then
  print "你在命令行上输入了 $ arguments 个参数。"
else
  print "你没有在命令行上输入任何参数。"
fi
```

```bash
for arg in $@;do print "ARGUMENT FROM COMMAND LINE: $arg";
```

### 示例 7

`print` `"你可以使用 'for' 将以 txt 结尾的文件中的 ALL 更改为 THAT"`
`print` `"注意：详情在脚本中提供。"`

另请参：`substitute_THIS_when_you_FIND_THAT.ksh`

```bash
for filename_ending_with_txt in *.txt; do
  print "正在处理 $filename_ending_with_txt"
  sed -e 's/this/that/gi' -e 's/Ms Woe/Ms Yu/g' <$filename_ending_with_txt >/tmp/$filename_ending_with_txt
done
```

这里是另一个示例，展示了如何轻松更改拼写错误：

另请参：`change_ALL_THIS_TO_THAT.method1.ksh`

```bash
for file in $$
do
  cp $file $E_O_F
  sed %s/thier/the/g %s/writable/g <$E_O_F >$file
done
```

### 示例 8

`print` `"'find' 可以用于更改文件名。"`
`print` `"注意：详情在脚本中提供。"`

另请参：`script change_all_filenames.ksh`

目标：将所有以 `.text` 结尾的文件名更改为 `.txt`

```bash
for file in $(find -type f -name *) do 
  # 查找所有文件（忽略目录）。
  newname=$(echo $file | sed -e "s/\.text$$/.txt")
  mv file $newname 2>/dev/null
done
```

```bash
# "示例 9：结合 'for' 与 'grep' 使用。"
# print "note：详情在脚本中提供。"
# for=$(print "SCRIPT analyze_peak_traffic.ksh"
HOURS_OF_THE_DAY_BEING_ANALYZED=08 09 16 # 上午8点，上午9点，下午4点
for hr in $HOURS_OF_THE_DAY_BEING_ANALYZED
do
  # num_matching_recs=$(grep -c "$HR.*" $transactions_log)
  # print "小时 HR 处理的交易数: $num_matching_recs"
done
```

```bash
# "示例 10：向列表中的所有人发送邮件。"
# list_of_emails=$(cat<<EOF
larrythree.stooges.com
moe@three.stooges.com
curly_joe@three.stooges.com
EOF)
# agenda=/tmp/agenda
# subject="Meeting at 9AM"
# for person in $list_of_addresses
do
  # print "正在向 $person 发送邮件"
  # /bin/mail -s $subject $person < $agenda
```

```bash
# "示例 11：检查所有必需文件是否到达。"
# mmdd=$(date +%B%d) # 示例：7月4日
# cd /home/larry/ROSETTA/
# required_files="NEW_$mmdd"
# for filename in $required_files
do
  # 如果是普通文件 或者不为空 或者 可读，则
  if [ ! -f "$filename" ] || [ ! -s "$filename" ] || [ ! -r "$filename" ]; then
    print "必需文件已收到: $filename"
# 示例12：查看 PATH 中的目录
IFS=$OLD # 保存旧值以便恢复。
IFS=: # 设置内部分隔符为冒号。（默认是空格）。
for directory in $PATH
do
  # 第一个查找 PATH 中的 ":"，如果长度为0：
  if [ -z "$directory" ]; then
    printf "\nPATH 包含 ':'\n"
  elif [ ! -d "$directory" ]; # 不是目录
    printf "\n不是有效的目录: $directory\n"
  elif [ ! -e "$directory" ]; # 不存在
    printf "\n不存在: $directory\n"
  fi
  ls -ld "$directory"
done
IFS=$IFS_OLD
```
