
`typeset -x DISPLAY`
`typeset -x EDITOR`
`typeset -x GDMESSION`

注意：如果你知道想查看哪个变量，请使用 `'env' | 'grep'` 来获取信息。
例如：`'env' | grep PATH`
`PATH=/usr/kerberos:/bin:/usr/local/bin:/usr/bin:/bin:/usr/X11R/sbin`
或者，执行此操作：`echo $PATH`
`/usr/kerberos:/bin:/usr/local/bin:/usr/bin:/bin:/usr/X11R/sbin`

注释：
命令 `'set'` 列出的变量数量：47
命令 `'env'` 列出的变量数：35

已完成。脚本：`./show_env_environment.ksh`

### 程序：`show_file_modification_date.ksh`
``` 
#!/bin/ksh
# 程序：显示文件最后修改的日期和时间。
# 目的：Larry Smith。由 __ 在 __date__ 修订
# 难度：中等。
# 用法：./
# ###
# 从 UNIX-LINUX 命令行：
# 如果 -lt 按修改日期排序。（-t 按时间排序，从新到旧）
# 如果 -lrt 按修改日期排序。（-r 反转排序顺序）
# 如果 -lt 保持相同，但不打印所有者或组信息。
###### 注释结束。
### 另见：show_minus_1.ksh, grep_for_files_with_days.ksh
```

`clear clear` 清空用户的屏幕。
`print "\n注释：这是脚本 $0"`
`print "目的：显示文件最后修改的日期和时间。"`

`print "\n按日期排序的文件（从新到旧）："`
`-lgt t!*.txt` # 参见注释（见上文）。"

`print "\n按日期排序的文件（从旧到新）："`
`-lrtgo t!*.txt` # 参见注释（见上文）。"

`print "\n已完成。脚本：$0"`

输出：`show_file_modification_date.ksh.OUTPUT`
输出：`show_file_modification_date.ksh`
脚本的执行方式：`./show_file_modification_date.ksh`
输出如下：

注释：这是脚本. `./show_file_modification_date.ksh`
目的：显示文件最后修改的日期和时间。

按日期排序的文件（从新到旧）：
`-rw-rw-r-- 1 213222 Apr 16 17:21 testing and debugging_tips.txt`
`-rw-rw-r-- 1 7034 Mar 23 16:49 tips and tricks.txt`

按日期排序的文件（从旧到新）：
`-rw-rw-r-- 1 7034 Mar 23 16:49 tips and tricks.txt`
`-rw-rw-r-- 1 213222 Apr 16 17:21 testing and debugging_tips.txt`

已完成。脚本：`./show_file_modification_date.ksh`

### 程序：`show_number_in_decimal_hex_octal.ksh`
``` 
#!/bin/ksh
# 程序：show_number_in_decimal_hex_octal.ksh
# 目的：显示如何进行数字转换。
# 程序员：Larry Smith。由 __ 在 __date__ 修订
# 难度等级：简单
# 用法，示例：./decimal_hex_octal_number_conversions.ksh
```

`print "\n当使用 printf 时，数字转换非常简单："`
`i=10`
`print "$i 在十进制中是 %d，在十六进制中是 %x，在八进制中是 %o\n" $i $i $i`

`print "\n已完成。脚本：$0"`

输出：`show number in decimal hex octal.ksh,OUTPUT`
脚本的执行方式：`./show_number in decimal hex octal.ksh`
输出如下：

注释：这是脚本 `./show_number in decimal hex octal.ksh.`
目的：显示如何进行数字转换。

当使用 `printf` 时，数字转换非常简单：
`is` 在十进制中是 10，在十六进制中是 a，在八进制中是 12

已完成。脚本：`./show_number in decimal hex octal.ksh`

### 程序：`show_os_operating_system.ksh`
``` 
#!/bin/ksh
# 程序员：show_os_operating_system.ksh
# 目的：显示你正在使用的操作系统。
# 程序员：Larry Smith。由 __ 在 __date__ 修订
# 难度等级：简单
# 用法，示例：./show_os_operating_system.ksh
### 注释

# UNIX-LINUX 命令 "uname -o" 显示 OS/操作系统。
# "uname -a" 提供额外信息；（a=全部）
# "uname -s" 提供的与 "hostname" 命令相同的信息。
### 注释结束
```

`print "你的操作系统：$(uname -o)"`
`print "\n已完成。脚本：$0"`

输出：`show_os_operating_system.ksh,OUTPUT`
脚本的执行方式：`./show_os_operating_system.ksh`
输出如下：

注释：这是脚本 `./show_os_operating_system.ksh.`
目的：显示你正在使用的操作系统。

你的操作系统：GNU/Linux

已完成。脚本：`./show_os_operating_system.ksh`

### 程序：`show_start_and_end_times.ksh`
``` 
#!/bin/ksh
# 程序员：show_start_and_end_times.ksh
# 目的：显示脚本的开始时间和结束时间。
# 程序员：Larry Smith。由 __ 在 __date__ 修订
# 难度等级：简单
# 用法，示例：./show_start_and_end_times.ksh
### 注释：
### 注释结束。
```

`clear` # 清空用户的屏幕。
`print "\n注释：这是脚本 $0。"`
`print "目的：显示脚本的开始时间和结束时间。\n"`

### 初始化：
`start_time=$(date)`
`end_time=0`
`start_stopwatch=$(date +%s)`
`end_stopwatch=0`
###
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
`end_time=$(date)`
`end_stopwatch=$(date +%s)`

`print "开始时间：$start_time"`
`print "结束时间：$end_time"`

`print "执行此脚本需要："`
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
# 正常情况下，有几行逻辑：
`print "所需秒数：$((end_stopwatch - start_stopwatch))"`

`print "\n已完成。脚本：$0"`

输出：`show_start_and_end_times.ksh.OUTPUT`
脚本的执行方式：`./show_start_and_end_times.ksh`
输出如下：

注释：这是脚本 `./show_start_and_end_times.ksh。`
目的：显示脚本的开始时间和结束时间。

开始时间：Fri Apr 16 17:21 2024
结束时间：Fri Apr 16 17:22 2024

执行此脚本需要：
所需秒数：1

已完成。脚本：`./show_start_and_end_times.ksh`

### 程序：`show_version.ksh`
``` 
#!/bin/ksh
# 程序：show_version.ksh
# 目的：显示内核版本。
# 程序员：Larry Smith。由 __ 在 __date__ 修订
# 难度：简单
# 用法，示例：./show_version.ksh
### 注释

# UNIX-LINUX 命令 "uname -v" 显示内核版本。
# "uname -a" 提供额外信息；（a=全部）
# "uname -r" 提供的与 "内核版本" 命令相同的信息。
### 注释结束
```

`print "内核版本：$(uname -v)"`
`print "\n已完成。脚本：$0"`

输出：`show_version.ksh,OUTPUT`
脚本的执行方式：`./show_version.ksh`
输出如下：

注释：这是脚本 `./show_version.ksh。`
目的：显示内核版本。

内核版本：#1 5.15.0-76-generic #Wed May 17 14:22:12 UTC 2023

已完成。脚本：`./show_version.ksh`

# 470

####################################
将重复行存入单独的文件：
`'uniq -d'` 命令将重复行放入一个单独的文件：
`sort myfile uniq -d > /tmp/duplicates`
####################################

####################################
`-t` (用于指定字段分隔符)。
####################################
示例记录如下：
`CENT:OMAHAEMP-1750:YOH, HELEN Z:87222:20051201:`
例如，如果你指定 `'-t '`，上一行的记录包含 6 个字段；
如果你指定 `'-t ':'`，则同一条记录仅包含 2 个字段。
示例：
`sort -t ':' -k 4 $INPUT $OUTPUT_sorted`
字段由冒号 (`':'`) 分隔。
记录中的第 5 个字段将按数字升序排序（从低到高）。
在第 4 个字段上有一个次要字母数字排序 (`-k 4`)。
####################################

####################################
`-r` 选项（反转，REVERSE）：
（按降序排序，从高到低）。
示例：
`sort -t ':'nr -k 4 $INPUT $OUTPUT_sorted`
字段由冒号 (`':'`) 分隔。
记录中的第 5 个字段按数字降序排序。
在第 4 个字段上有一个次要字母数字排序 (`-k 4`)。
####################################

####################################
`-k` (用于指定键 key)。
####################################
`'k 1'` 指记录中的第一个字段；
（不需要考虑偏移量，第一个字段偏移为 0）。
示例 1：
`sort -t ' ' -k 4 $INPUT $OUTPUT_sorted`
字段由空格 (`' '`) 分隔。
记录中的第 5 个字段按数字降序排序。
在第 4 个字段上有一个次要字母数字排序 (`-k 4`)。

示例 2：
`sort -t ':' -k 5,6 -k 4,5 $INPUT $OUTPUT`
字段由冒号 (`':'`) 分隔。
主排序：从第 5 个字段开始排序；
当从第 6 个字段开始时停止。
第 5 个字段按数字降序排序。
次要排序：从第 4 个字段开始排序；
当从第 5 个字段开始时停止排序。

####################################
使用 `+` 和 来指定偏移量 OFFSETS：
####################################
个人而言，我更倾向于使用 `-k`。
有些人习惯用偏移量思考（0 是第一个字段）；
如果你是其中一员，请尝试这种方法。

（由于没有更好的词，我将第一个字段称为 `'offset0'`；
第二个字段是 `'offset1'`；第三个字段是 `'offset2'`）。

示例 1：
```
