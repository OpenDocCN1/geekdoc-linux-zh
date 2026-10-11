
通常情况下，在使用 `cut` 命令之前没有必要使用 `tr` 命令来转换数据，但 `ls` 命令的输出带给我们了一点挑战：它的字段是用空格和制表符分隔的。

关于示例 5 的注意：

示例 5 在 `bash` 上有效但在某些版本的 `cut` 中无效。如果你使用 `cut` 运行它，通常看到的错误消息是“bad substitution”。注释：你也可以用一个命令切割多个列：

```
cut -c 24-26,38-36,51-54 -$INPUT | sort -u >OUTPUT
```

### 注意

### 另参：`format_telephone_numbers.ksh`

### 另参：`read_and_cut_to_reformat_rec.ksh`

### 另参：`change_record_if_column9_is_b.ksh`

```
清除用户屏幕
print "增量：这是脚本 0.n\n"
print "目的：演示如何使用 'cut' 和 'substring'；换句话说，演示如何查看记录或文件中的任何列或多个列。"
```

### 初始化：
`INPUT=/home/larry/ROSETTA/INPUT_FILES/substr.testfile.txt`
`DEFAULT_IFS="$IFS"` # 保存默认文件（空格）。

```
## 首先，创建一个测试文件：
print "abcdefghi junk and more junk." >$INPUT
print "ABCDEFGHIJ junk and more junk!" >>$INPUT
print "123456789_123456789_123456789" >>$INPUT
```

######

# 在示例 1 中，我们展示如何在“read”内部使用 'cut'：

print "注意：如果输入记录的第 9 列等于 '9$，我们将把 '9' 改为 '2'。因为我们想展示重新格式化数据有多容易。\n\n"

```
counter=0
IFS="$IFS" # 设置内部字段分隔符为空；默认是空格
print "\n这里是我们的三行输入文件:"
cat -n $INPUT

# 循环开始：
while read -r line
do
```

(( `counter = counter + 1` ))

print "n###"

print "Here's Input record number $counter: $line"

`cols_9=$(echo "$line | cut -c 9)`

`cols_13_thru=$(echo "$line | cut -c 13-16)`

`cols_25_thru_end_of_line=$(echo "$line | cut -c 25-)`

print "col19 is $col9"

print "cols_13_thru_16 are $cols_13_thru_16"

`cols_25_thru_end_of_line=$cols_25_thru_end_of_line`

if [ "$col9" -ne 9 ]; then

then print "FOUND column 9 equal to 9 in record number $counter"

print "Now counting 9 to '2'"

`col_8=$(echo "$line | cut -c 1-8)`

`col_10="$col9"`

`cols_10_thru_end_of_line=$(echo "$line | cut -c 10-)`

print "Here's the reformatted record:"

print "${col_8}${col_9}${cols_10_thru_end_of_line}\n"

fi

done < $INPUT

## EXAMPLE 2

print "\n\nEXAMPLE 2 shows how to use cut:"

print "\nhere's our three-line INPUT FILE:"

cat $INPUT

print "\nhere are column 9 on each of our input records"

cut -c 9 $INPUT

print "\nhere are columns 13-16"

cut -c 13-16 $INPUT

print "\nhere are columns 25 through the end of each record"

cut -c 25-$INPUT

## EXAMPLE 3

print "\n\nEXAMPLE 3:"

print "\n\nhere's how to SUB-STRING using the incredibly awkward AWK:"

counter=0

IFS=''

# Set the entire Internal Field Separator to null; default is whitespace

while read -r line; do

  (( counter = counter + 1 ))

  print "\nHere's Input record number $counter: $line"

  print "\n###"

  # Notes: "$0" is the entire record that is sent down the pipe; awk to process.

  `cols_13=$(echo "$line" | awk '{partofline=substr($0, 9, 1); print partofline}')`

  `cols_13_thru_16=$(echo "$line" | awk '{partofline=substr($0, 13, 4); print partofline}')`

  # The following L-O-N-G (on 2 lines) contains 93 characters:

  `cols_25_thru_end_of_line=$(echo "$line" | awk '{partofline=substr($0, 25, 25); print partofline}')`

  print "col19 is $col9"

  print "cols_13_thru_16 are $cols_13_thru_16"

  cols_25_thru_end_of_line=$cols_25_thru_end_of_line

  if [ "$col9" -ne 9 ]; then

  then print "FOUND column 9 equal to 9 in record number $counter"

  fi

done < $INPUT

## EXAMPLE 4

print "\n\nEXAMPLE 4 shows how to use 'cut -f' to obtain fields from a record."

print "\HERE IS HOW TO PRINT SELECTED FIELDS AFTER AN ls COMMAND:"

```
print "first, here are a few files shown after an ls:"
ls -rtgo | tail -3
```

```
print "now let's use 'cut -f' to show selected fields from the 'ls -l':"
print "SIZE FILENAME"
ls -rtgo | tail -3 | tr "*" "[" " " | tr -s " " | cut -d ' ' -f 3-5,7
# Note: "NOTES ABOUT EXAMPLE"
# ordinally, it is not necessary to use the (cut transform)
# data prior to using the cut, but the output from the ls commands presents
# us with a bit of a challenge: its fields are separated by both spaces AND tabs.
```
