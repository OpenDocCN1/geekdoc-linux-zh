
```
# if [ $(ps -ef | grep -v grep) -eq 0 ]; then
# 以下操作具有相同的功能（使用反引号）：
# if [ `ps -ef | grep -v grep` -eq 0 ]; then
# ps 命令列出了服务器上运行的所有进程：
# 我们正在寻找一个名为 'applicationZZ' 的应用程序，这就是我们 grep 查找的；
# -c grep 选项允许我们统计包含 'applicationZZ' 的行数。
# 从命令行执行以下命令：
# ps -ef grep applicationZZ
# 在这里我发现的是：
# 但请注意进程 applicationZZ 本身就是 grep
# 换句话说，applicationZZ 目前没有在这台服务器上运行。
# 现在尝试此命令：grep -c --grep applicationZZ
# 我们看到的计数是 '1'；当 applicationZZ 实际上在服务器上运行时，
# 我们看到的计数是 2（1 是因为 grep，第二个是因为 applicationZZ 处于激活状态）。
# 我们通过使用 grep 的 -v 选项也解决了这个困惑：
# grep -c -v grep - 统计包含 'applicationZZ' 的行数
# 以忽略 (-v) 任何包含 'grep' 的行。
# 因此，这一行被忽略了：14:06/00 00:00:00 grep applicationZZ
# 当 applicationZZ 激活时，我期望看到计数为 1。
# 当 applicationZZ 未激活时，我期望看到计数为 0。
# 如果 applicationZZ 在服务器上运行的次数为 0；
# 并且 $PGM_should_be_y_or_n 为 'y'，则显示错误信息。
# END_DOES。
```

### 另参：`applicationZZ.ksh` 和 `bring_up_application.ksh`

```
清除用户的屏幕。
print "注释：这是脚本 $0"
print "目的：显示如何使用嵌套语句。"
```

```
### 初始化：
day_of_week=$(date +%u) # 周一=1; 周五=5; 周日=7
current_min=$(date +%M) # 当前分钟：00 到 59
current_hr=$(date +%H) # 当前小时：00 到 23；上早8点, 下午1点, 下午6点
PGM=applicationZZ
###
### 用于测试：你可以取消以下 4 行的注释：
# day_of_week='5'
# current_min='20'
# print "警告: hr, min, and day_of_week 已设置为测试.\\"
```

```
print "示例："
print "让我们假设情况是周一至周五，早上 8:00 到晚上 8:30 (20:30)。"
print "当前小时：$current_hr。当前分钟：$current_min。"
print "星期几：$day_of_week。 (1 是周一；7 是周日)。"
```

```
program_should_be_y_or_n='n'
if [[ $day_of_week -ge 0 && $day_of_week -lt 6 ]]; then PGM 在这一周几运行的是 M,T,Th, 或 F
if [[ $current_hr -lt 21 ]]; then
  if [ "$PGM" = "PGM 在此小时通常运行" ]; then
    if [ "$current_hr" -eq 20 ]; then 如果当前小时是晚上 8 点，那么
      then print "现在查看时间是否已过了晚上 8:30"
      fi
    fi
  fi
fi
if [[ $current_min -ge 0 && $current_min -lt 31 ]]; then
    program_should_be_y_or_n='y'
    # print "现在是晚上 8 点到 8:30 点之间。"
  fi
fi
```

`identify_unprintable_characters.bash`, `.ksh`, `.pl`。

注意：更多关于 `IFS`（内部字段分隔符）的信息，请参见 `IFS.ksh`, `IFS.bash`

建议：使用 `'od -a -b'` 或 `'od -c'`，因为输出结果易读。

更多建议：仅在必须时使用 `'od -b'`。

如果你想查看八进制值列表，请执行命令 `'man ascii'`

如果你想查看 `"Hi"` 的八进制值，请执行以下操作：

`echo 'Hi'|od -b`

结果：

`echo 'Hi'|od -b`

000000 H i ! nl

110 151 041 012

换句话说：

110 是 H。151 是 i。012 是换行符。

### 注释：如果你想知道 `$IFS` 的当前值，

请使用以下命令：

`echo "${IFS}"|od -b`

输出：

000000 137 040 011 012 137 012

000000

如果你不想看到输出的第二行（'000006'），

请执行此命令（在命令行）：`$ echo "${IFS}"|od -b |head -1`

让我们来看这两行输出：

000000 是起始偏移量（字节#1 是偏移量0；字节#2 是偏移量1）

后续的数字是：137 040 011 012 137 012

例如，空格可以表示为八进制符号 `\040`。

137 是下划线：

（下划线用于显示 IFS 的开始和结束）。

040 是空格。

012 是制表符 (t)。

012 是换行符 (\n)。

037（第二次出现）是下划线。

行末尾的 012 是换行符（由 `'echo'` 自动放置）。

000006 表示你到为止已打印了 6 个字节。

你可能在问：“既然我已经知道了这些，这意味着什么？！”

这意味着默认的 `IFS` 有三个值：空格 (SPACE)、制表符 (TAB) 和换行符 (NEWLINE)。

######################################################################

另一个有用命令是 `'cat -A filename'`：

`cat 'A'` 将行中的不可打印字符显示为制表符 (TAB) 和行尾 (END-OF-LINE)。

```
程序：or.ksh
#!/bin/ksh
# 程序：or.ksh
# 目的：显示“或” (( | )) 逻辑。
# 编写者：Larry Smith, __ 于 ____ 修订
# 难度：中等
# 用法：示例 "./or.ksh"
# 注意：
# 'grep -eg' 是扩展 grep，允许你使用 '|' 表示“或”。
# 2>/dev/null 表示将错误发送到与 STDOUT 相同的地方。
# /dev/null 是“垃圾桶”。
### 注释结束。
### 另请：eq_ne_gt_it_le_STRING.ksh
### 另请：grep_egrep_fgrep.ksh
### 初始化：
```

```
# Day_of_week=$(date +a) # 示例：Day_of_week 可能是 'Tue'（周二）

string='
stoge1='larry'
stoge2='moe'
stoge3='CURLY JOE';
```

```
# 这种也有效：if [[ "$Day_of_week" == "Sat" || "Day_of_week" == "Sun" ]]
print "示例 2：在这个例子中，我们使用 'or' 来判断字符串是否包含"
print "单词 'Larry'、或 'Moe'、或 'Curly Joe'："
string='Joe and Curly';

print "我们的第一次测试在哪里："
# 在接下来的行行中，竖线 '|' 是一个管道，允许数据向下流动；
# 它被用在 grep 'or' 内部。
echo "$string | grep (Larry|Moe|Curly Joe)" >/dev/null 2>&1
if [ $? -eq 0 ]; then # 如果 grep 找到了匹配项，则
print "你的字符串"
print "匹配：你的字符串包含 'Larry' 或 'Moe' 或 'Curly Joe'。"
else
print "你的字符串不包含 'Larry' 或 'Moe' 或 'Curly Joe'。"
fi
```
