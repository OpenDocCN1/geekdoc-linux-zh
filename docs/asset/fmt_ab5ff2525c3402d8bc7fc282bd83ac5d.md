
((byte_counter++)) # 为 `byte_counter` 加 1

if [ $byte_counter -eq 9 ]; then 我们“切出”字符串的第 9 个字符：

  `one_byte=$(echo "$string" | cut -c $byte_counter)`

  `print number $byte_counter is ${one_byte}`

((length--)) # 从 `$length_of_string` 减 1

done

### #示例 2: 接下来，让我们读取一个较小的文件（两条记录）
`print "并按字节处理每个记录。"`

`IFS=''` # 将内部字段分隔符设为空。

```
while read -r
do
  length="$record"
  byte_counter=0
  print "current record: $record"
  while [$length -gt 0]
do
    ((byte_counter++)) # 为 byte_counter 加 1
    if [ $byte_counter -eq 9 ]; then “切出”记录的第 9 个字符：
    one_byte=$(echo "$record" | cut -c $byte_counter) # 切出一个字节
    print number $byte_counter is ${one_byte}"
  ((length--)) # 从 $length 减 1
done
done <$INPUT
```

`rm $INPUT` # （删除）临时/测试文件。
`IFS=$DEFAULT_IFS` # 恢复默认值。（在这里不是必须的，但这样做很好！）

`print "#DONE. process data byte-by-byte.ksh:$0\n"`

OUTPUT: `process data byte-by-byte.ksh`
脚本执行方式: `./process_data_byte-by-byte.ksh`
OUTPUT:

Comment: 这是脚本 `./process_data_byte-by-byte.ksh`。

PURPOSE: 按字节处理文件或字符串中的数据。
Reminder: 你可以使用 `'cut -c'` 来获取记录中
列（或多个列）中的信息。

EXAMPLE 1: 按字节处理字符串。

```
以下字符串正作为我们的输入: I love LINUX!

字节数 1 是 I

字节数 2 是

字节数 3 是 l

字节数 4 是 o

字节数 5 是 v

字节数 6 是 e

字节数 7 是 i

字节数 8 是 L

字节数 9 是 I

字节数 10 是 N

字节数 11 是 U

字节数 12 是 X

字节数 13 是 !
```

EXAMPLE 2: 接下来，让我们读取一个较小的文件（两条记录）
并按字节处理每个记录。

```
Current record: abcd

Byte number 1 is a

Byte number 2 is b

Byte number 3 is c

Byte number 4 is d
```

```
Current record: 1234

Byte number 1 is 1

Byte number 2 is 2

Byte number 3 is 3
```

# 397

```bash
if [ -d $filename ]; # 如果是一个目录，则
  print -n 'DIRECTORY: '
  ls -ld $filename
fi
```

```bash
print "####################################### 方法 3 #######################################"
print "方法 3 使用 'find' 命令。"
# 假设她拥有金牌大 Boss
# 当 "think" 认为名为 /tmp/projectxyz2 的目录中有一堆旧杂物时
# 当你想要对这些文件提供一些统计信息时，你可以
# 使用下面所示的 "find" 命令。
```

```bash
for filename in $home/larry/ROSETTA_TEMP/* do
  if [ -e $filename ]; # 如果未找到 filename（即不存在）...
    print "NOT FOUND: $filename"
  elif [ -s $filename ]; # 如果文件没有“大小”，则..
    print "EMPTY FILE: $filename"
  elif [ -f $filename ]; # 如果 filename 是普通文件，则..
    ls -l $filename
  elif [ -d $filename ]; # 如果是一个目录，则
    print -n 'DIRECTORY: '; ls -ld $filename
  fi
done
```

```bash
print "####################################### 方法 4 #######################################"
print "方法 #4 将 'for' 与 'ls' (list) 命令结合。"
cd /home/larry/ROSETTA_TEMP
for filename in $(ls); do
  if [ -e $filename ]; # 如果未找到 filename（即不存在）...
    # 这部分与 ls 冗的
    print "NOT FOUND: $filename"
  elif [ -s $filename ]; # 如果文件没有“大小”，则..
    print "EMPTY FILE: $filename"
  elif [ -f $filename ]; # 如果 filename 是普通文件，则..
    ls -l $filename
  elif [ -d $filename ]; # 如果是一个目录，则
    print -n 'DIRECTORY: '; ls -ld $filename
  fi
done
```

```bash
print "####################################### 方法 5 #######################################"
print "方法 #5 将 'for' 与星号结合。"
cd /home/larry/ROSETTA_TEMP
for filename in * do
  if [ -s $filename ]; # 如果文件没有“大小”，则..
    print "EMPTY FILE: $filename"
  elif [ -f $filename ]; # 如果 filename 是普通文件，则..
    ls -l $filename
  elif [ -d $filename ]; # 如果是一个目录，则
    print -n 'DIRECTORY: '; ls -ld $filename
  fi
done
```

```bash
print "\n完成. 脚本: $0\n"
```

输出：提供 `list.ksh` 中文件的统计信息。OUTPUT
脚本是如何执行的：在 `list.ksh` 中执行 `.provide_stats_about_files`
输出如下：

注释：这是 `list.ksh` 中的 `./provide_stats_about_files` 脚本。
目的：提供文件名列表中的文件信息。

## 方法 1：如果你想在脚本中复制并粘贴文件名列表，请使用此方法。

```
DIRECTORY: drwx-xr-x 2 larry 20480 Mar 16 14:24 /home/larry/ROSETTA/TEMP

NOT FOUND: /home/larry/tmp/empty_file.txt

NOT FOUND: /home/larry/tmp/junk

NOT FOUND: /home/larry/tmp/more.stuff.txt

NOT FOUND: /home/larry/tmp/thisFileNotExist

-rw-rw-r 1 larry 367 Mar 7 11:38 /home/larry/ROSETTA/TEMP/lar.ksh
```

## 方法 2
如果文件名保存在磁盘文件中，则使用此方法。

```
DIRECTORY: drwx-xr-x 2 larry 20480 Mar 16 14:24 /home/larry/ROSETTA/TEMP

NOT FOUND: /home/larry/tmp/empty_file.txt

NOT FOUND: /home/larry/tmp/junk
```
