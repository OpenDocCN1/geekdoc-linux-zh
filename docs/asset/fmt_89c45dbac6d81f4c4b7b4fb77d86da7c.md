
### 注意事项
# 在你列出文件后（使用 `-l *`），
# 几的数字并不总是显示两个数字。
# 例如：Feb 9
# `-rw-r--r-- 5535 Feb 9 15:42 testfile.txt`
# `-rw-xr-x 1698 Feb 10 11:16 test`
# 要用今天的日期进行 `grep (-l|grep $MMMM_DD)`，你必须
# 设置 `date` 命令以显示，否则系统将无法
# 检查每个月前九天（1-9）的文件：

### 关于 'sed' 命令的说明：
# `MMMM_DD=$(date +%Xd | sed -e 's/ /\2/g' 2>/dev/null)`
# `'sed'` 命令中的 `'s'` 代表 `'substitute'`替换）；换句话说，
# 如果 `'sed'` 在它的数据管道中找到 `0`，那么 `'0'` 就会被更改
# 从而移除前导零。这会创建一个如 `"Feb 09"` 这样的日期，
# `sed` 会将其更改为 `"Feb"`。
# 如果没有 `sed` 命令，下一行的 `grep` 将无法
# 在每个月的前九天找到匹配的日期：
# 是 `grep $MMMM_DD`
# 错误：`grep $MMMM_DD` # 因为 `$MMMM_DD` 包含空格。
# 正确：`grep "$MMMM_DD"` 你需要引号是因为 `$MMMM_DD` 包含空格。
# 如果这对你不清楚，执行以下两条命令：
# `date +%Xd`
# 注意结束。

`OUTPUT: grep for files_with_todays_date.OUTPUT`

脚本是如何执行的：`./grep_for_files_with_todays_date.ksh`

输出：

注释：这是脚本 `./grep_for_files_with_todays_date.ksh`。

目的：列出今天创建或修改的文件。

方法 1：

你当前目录的文件在过去 24 小时内修改过：

当前目录：`/home/larry`

`-rw-r-- 8019 Mar 2 17:16 ./table_of.txt`

`-rw-r-- 15436 Mar 3 09:07 ./List`

方法 2：

你当前目录的文件在 Mar 3 修改过：

当前目录：`/home/larry`

`-rw-r-- 2304 Mar 3 15:36 ./grep_for_files_with_todays_date.ksh`

`-rw-r-- 2768 Mar 3 15:36 ./grep_for_files_with_todays_date.OUTPUT`

完成。：`./grep_for_files_with_todays_date.ksh`

# 程序：`grep_for_items_in_list.ksh`

```bash
#!/bin/bash

# 程序：grep_for_items_in_list.ksh

# 目的：如何在列表中查找每一项。

# 程序员：Larry Smith。修订于 __date__。

# 难度：易

# 用法：./grep_for_items_in_list.ksh
```

### 注意：

### 注意结束。

```
clear 屏幕。
print "这是脚本 $0。"
print "如何在列表中查找每一项。"
```

### 初始化：
```bash
DIRECTORY=/home/larry/INPUT_FILES
number_of_files_examined=$(ls -1 $REGION/ | wc -l) # 查看 'wc.sh'
LIST_OF_STATES_TO_GREP=$(ls -1 $REGION/ # "ls 减一" (注意: "ls 1")
print "报告检查的文件数：$number_of_files_examined"
print "报告检查的文件名："
print "$DIRECTORY/$REGION (注意: "ls 1")
```

```bash
for STATE in $LIST_OF_STATES_TO_GREP; do
# -c 计算 grep 命令找到的匹配数量。
# $STATE 以 'with' 开头；'NEBR'记录开头。
# 因此，如果 $STATE 是 NEBR，那么 grep -c 命令将计算
# 以 'NEBR' 为开头的记录。
number_of_matches=$(cd $DIRECTORY/$REGION/ | grep -c "$STATE")
print "以 $STATE 开头的记录数：$number_of_matches"
done
```

```
print "DONE. script: $0\n"
```

输出：`grep_for_items_in_list.ksh.OUTPUT`
脚本是如何执行的：`./grep_for_items_in_list.ksh`
输出如下：

注释：这是脚本 `./grep_for_items_in_list.ksh`。

目的：如何在列表中查找每一项。

报告检查的文件数：3

报告检查的文件名：
home/larry/INPUT_FILES/REGION_CENT SALES
home/larry/INPUT_FILES/REGION_EAST SALES
home/larry/INPUT_FILES/REGION_WEST SALES

以 NEBR 开头的记录数：2
以 IOWA 开头的记录数：2
以 CALIF 开头的记录数：2

完成。脚本：`./grep for items in list.ksh`

`$ /home/larry/INPUT_FILES/REGION_CENT_Feb_SALES`

NEBR:TYPE:235419:P

NEBR:TYPE:43591:P

IOWA:TYPE:876119:P

IOWA:TYPE:876115:A

MICH:TYPE:5861995:Z

MICH:TYPE:5861995:S

`$ /home/larry/INPUT_FILES/REGION_EAST_Feb_SALES`

NYORK:TYPE:235419:P

NYORK:TYPE:43591:P

NJERS:TYPE:876119:P

NJERS:TYPE:876115:A

PENN:TYPE:5861995:Z

PENN:TYPE:5861995:S

`$ /home/larry/INPUT_FILES/REGION_WEST_Feb_SALES`

CALIF:TYPE:235419:P

CALIF:TYPE:43591:P

UTAH:TYPE:876119:P

UTAH:TYPE:876115:A

WASH:TYPE:5861995:Z

WASH:TYPE:5861995:S

有时你需要知道某段数据的格式是否正确，或者你可能想知道它是否包含任何无效字符。

假设一个名为 `'SSN'`（社会安全号码）的字段可以格式化为 `'123-45-6789'` 或 `'123456789'`。如果数据格式无效，我们就打印一条错误消息。

```bash
print "Example1a: (Expected not found.)"
ssn="123-45-6789"
# See (below) EXPLANATORY COMMENTS ABOUT THE PATTERN.
# echo "$ssn" | grep "[0-9]{3}\-[0-9]{2}\-[0-9]{4}" >/dev/null 2>&1
if [ $? -eq 0 ]; then if grep was successful, then
print "FOUND pattern in $ssn"
else print "Your pattern was not found in $ssn"
```

```bash
print "Example1b: (Expected found.)"
ssn="123-45-6789"
# echo "$ssn" | grep "[0-9]{3}\-[0-9]{2}\-[0-9]{4}" >/dev/null 2>&1
if [ $? -eq 0 ]; then if grep was successful, then
print "FOUND pattern in $ssn"
else print "Your pattern was not found in $ssn"
```

```bash
print "Example1c: (Expected not found.)"
ssn="123456789"
# echo "$ssn" | grep "[0-9]{3}\-[0-9]{2}\-[0-9]{4}" >/dev/null 2>&1
if [ $? -eq 0 ]; then if grep was successful, then
print "FOUND pattern in $ssn"
else print "Your pattern was not found in $ssn"
```
