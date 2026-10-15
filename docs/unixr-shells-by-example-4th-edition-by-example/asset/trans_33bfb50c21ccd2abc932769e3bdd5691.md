

# 示例 6.171（续）

```
% cat form.letter
```

格式信函 `form.letter` 如下所示：

**************************************************
主题：项目“#1”状态报告
收件人：#2
发件人：#3
日期：@date
这封信是要告诉你，#2，项目“#1”目前进展正常。
我们预计一切将按计划于 #4 完成并准备发货。

谨致敬意！

#3
**************************************************

文件 `data.form` 是 awk 的输入文件，其中包含将替换 `form.letter` 中 #1-4 和 @date 的数据。

```
% cat data.form
```

Dynamo:John Stevens:Dana Smith, Mgr:4/12/2004
Callactius:Guy Sterling:Dana Smith, Mgr:5/18/2004

（命令行）

```
% nawk -f form.awk data.form
```

**************************************************
主题：项目“Dynamo”状态报告
收件人：John Stevens
发件人：Dana Smith, Mgr
日期：2004 年 3 月 2 日
这封信是要告诉你，John Stevens，项目“Dynamo”目前进展正常。
我们预计一切将按计划于 4/12/2001 完成并准备发货。
谨致敬意！

Dana Smith, Mgr
主题：项目“Callactius”状态报告
收件人：Guy Sterling
发件人：Dana Smith, Mgr
日期：2004 年 3 月 2 日
这封信是要告诉你，Guy Sterling，项目“Callactius”目前进展正常。
我们预计一切将按计划于 5/18/2004 完成并准备发货。

谨致敬意！

Dana Smith, Mgr

# 说明

- 1. 在 BEGIN 块中，字段分隔符（FS）被赋值为冒号，用户定义变量 n 被赋值为 1。
- 2. 在 while 循环中，getline 函数从名为 `form.letter` 的文件中一次读取一行。如果 getline 找不到该文件，则返回 -1。当到达文件末尾时，它返回 0。因此，通过测试返回值是否大于 1，我们可以知道该函数是否已从输入文件中读入一行。
- 3. `form.letter` 中的每一行都被赋给一个名为 `form` 的数组。
- 4. UNIX/Linux 的 `date` 命令的输出通过管道传递给 getline 函数，并赋给用户定义变量 d。然后，split 函数使用空白字符分割变量 d，创建一个名为 `today` 的数组。
- 5. 用户定义变量 `thisday` 被赋值为月份、日期和年份。
- 6. BEGIN 块结束。
- 7. for 循环将循环 n 次。
- 8. 用户定义变量 `temp` 被赋值为 `form` 数组中的一行。
- 9. 嵌套的 for 循环会遍历输入文件 `data.form` 中的一行，共循环 NF 次。`temp` 变量中存储的每一行都会检查字符串 `@date`。如果匹配到 `@date`，gsub 函数会将其替换为今天的日期（存储在 `thisday` 中的值）。
- 10. 如果存储在 `temp` 中的行包含 `#` 和一个数字，gsub 函数会将该 `#` 和数字替换为输入文件 `data.form` 中对应字段的值。例如，如果正在测试存储的第一行，则 `#1` 会被替换为 Dynamo，`#2` 会被替换为 John Stevens，`#3` 会被替换为 Dana Smith，`#4` 会被替换为 4/12/2004，依此类推。
- 11. 替换完成后，打印存储在 `temp` 中的行。

## 6.25.4 与 Shell 的交互

现在你已经了解了 awk 的工作方式，你会发现，在编写 shell 脚本时，awk 是一个非常强大的实用工具。你可以将单行 awk 命令或 awk 脚本嵌入 shell 脚本中。下面是一个嵌入了 awk 命令的 Korn shell 程序示例。

# 示例 6.172

```
#!/bin/ksh
# This korn shell script will collect data for awk to use in
# generating form letter(s). See above.
print "Hello $LOGNAME."
print "This report is for the month and year:"
1 cal | nawk 'NR==1{print $0}'

if [[ -f data.form || -f formletter? ]]
then
  rm data.form formletter? 2> /dev/null
fi
integer num=1
while true
do
  print "Form letter #$num:"
  read project?"What is the name of the project? "
  read sender?"Who is the status report from? "
  read recipient?"Who is the status report to? "
  read due_date?"What is the completion date scheduled? "
  echo $project:$recipient:$sender:$due_date >> data.form
  print -n "Do you wish to generate another form letter? "
  read answer
  if [[ "$answer" != [Yy]* ]]
  then
    break
  else
2   nawk -f form.awk data.form > formletter$num
  fi
  (( num+=1 ))
done
nawk -f form.awk data.form > formletter$num
```

# 说明

- 1 UNIX 的 `cal` 命令通过管道传递给 `nawk`。其中包含当前月份和年份的第一行会被打印出来。
- 2 `nawk` 脚本 `form.awk` 会生成格式信函，并将其重定向到 UNIX 文件中。

