
# 注意：大多数 BASH 和 Kornshell 的安装都允许你
# 使用 '=' 或 '==' 来判断两个 字符串是否相同。
print "某些手册说明，在字符串比较中使用 '=' 是"
print "'已弃用'（不建议使用）。"
print "\n接下来的操作对周几的判断将执行两次，\n先使用 '=' 然后再使用 '=='\n"

# 第一次测试：if [ "$Day_of_week" == Sat || "$Day_of_week" == Sun ]; then
`Day_of_week`=$(date +Ka)
print "\nDay_of_week 为 $Day_of_week"
if [ "$Day_of_week" == 'Sat' || "$Day_of_week" == 'sun' ]; then
then print "\n是周末。\n"
else print "\n是工作日。\n"

# 第二次测试：if [ "$Day_of_week" == Sat || "$Day_of_week" == sun ]; then
`Day_of_week`=$(date +Ka)
print "\nDay_of_week 为 $Day_of_week"
if [ "$Day_of_week" == 'Sat' || "$Day_of_week" == 'sun' ]; then
then print "\n是周末。\n"
else print "\n是工作日。\n"

# 这种技术也可以用于启动应用程序，
# 并判断它是否成功启动。参见下文，
# "如何查看你的应用程序是否成功启动。\n"

printf "\n你的名字是什么?\n"
read first_name
printf "\n你的姓氏是什么?\n"
read last_name

printf "\n你输入了：first_name: $first_name last_name: $last_name\n"
echo "测试中：if [ -z "$first_name" ] 如果你的字符串包含零字节 ..."
if [ -z "$first_name" ]; then
then print "\n那么：你的字符串为空。first_name: $first_name\n"
else print "\n否则：你的字符串不空。first_name: $first_name\n"

echo "测试中：if [ -n "$first_name" ] 如果你的字符串不为空 ..."
if [ -n "$first_name" ]; then
then print "\n那么：你的字符串不空。first_name: $first_name\n"
else print "\n否则：你的字符串为空。first_name: $first_name\n"

```
# /home/larry -name -o -name "junk"* -ctime +7 -ok rm {} \
# /home/larry -name -o -name "junk"* -ctime +7 -is -l {} ; >/tmp/lar
# /home/larry -name -o -name "junk"* -ctime +7 -exec rm -rf {}
```

## 为什么我的命令不起作用？

`find` 极其强大且有用，除非（有时）它让你感到非常沮丧。

`find` 命令是那种“沉默而有实力”的男人——当被问到“你为什么不告诉我！”时，他会回答：“你你没说。”

## 尽管如此！命令可以非常长，

不要试图通过省略文件名来节省空间！

1. 你必须在反斜杠 `\` 后面加一个空格： `\ \`

2. 你必须在反斜杠 `\` 前后都加空格

3. 你必须在反斜杠 `\` 前后都加空格

4. 你必须在 `\\` 前后都加空格，它表示不是

5. 你必须在 `\\` 前后都加空格，但不要在内部加空格

6. 你必须对包含 `atime`（访问时间）的 `find` 命令使用引号，否则你无法获得你明明看到的那些。

为什么？因为在运行像 `find` 或 `grep` 的命令后，文件会被标记为已访问。

为了获得一致的结果，请使用 `cime` 代替 `atime`。

`cime` 中的 `c` 是一个有点愚蠢（但很有用）的记忆方法：想想它的含义：一个文件被命名为“奶奶的奶奶”是什么时候？你刚刚问：“距离我们上次检查它已经有一周了”。

- `-ctime +7` 表示列出一周内没有检查过的文件。

- `-mtime` 是文件创建或修改的时间。

- `-ctime` 使用 `cime` 代替 `mtime` 来获取“最后访问时间”。

- `-atime` 是文件被访问（或被 `grep` 搜索）但未被修改的时间。

7. 当你使用 `-ctime +30` 时，“意味着文件已经**超过** 30 天没有修改了。换句话说，当你看到加号 `+` 时，表示“大于”；当你看到减号 `-` 时，表示“小于”。

你可以将 `-daystart` 与 `-ctime` 和 `-mtime` 结合使用。

- `-mtime -1` 表示在过去 24 小时内创建的文件。

- `-daystart -1day` 表示文件自昨午夜以来创建。

注意：`/home/larry -type f -mtime +9 -print`

`find` 查找修改超过一周但少于一个月的文件。

8. 当你使用 `-exec 'ls'` 删除文件时，千万不要先测试命令。

测试命令的好方法是将 `ls` 替换为 `rm`：`-exec ls \`

你也可以使用 `-ok` 选项，这样每次删除都会经过你的确认，然后你回复 `y` 或 `n`（见下文示例）。

9. `'-a'` 表示“所有”。你不需要频繁使用 `'-a'`，因为它是默认假设的。

例如，让我们来看这个：`-type f -size +100000000 -ctime +30`。

你想找到文件 (`-type f`) 大小超过 1 亿个字符 (`+100000000`) 且超过 30 天未被访问的文件 (`-ctime +30`)。

换句话说，

类型是文件 且 大于 1MB 且 超过 1 个未访问

`find /home -type f -size +100000 -ctime +30 -print`

10. `'-o'` 表示“或”。

示例：`find -type f -atime +5 | -name "*.o" -o -name "junk" -print`

解释：`find` 从当前目录开始，查找所有 5 天未访问过的、要么以 `'.o'` 结尾要么以 `'junk'` 开头的文件。

11. 以下选项值得了解：

- `-mount`, `-xdev`, `-local`（见下文示例）

- `-user-larry` 列出由用户 id-larry 拥的文件

- `-empty` 列出为空（0字节）的文件

- `-user` 列出所有者在 `/etc/passwd` 中未列出的文件。

- `-perm` 列出具有特定权限集的文件。（见下文示例。）

## 怪癖/烦恼

某些系统上存在一个怪癖：如果你搜索的路径是一个链接，它将无法找到你正在寻找的内容。例如，`/u/xyz` 可能是同一个目录，因为有一个软链接（在 `/u/xyz` 中），但如果你要求系统查看软链接，它将找不到你的文件；`find /u/xyz -name myfile 'myfile'` 将找到。`find /u/xyz -name myfile 'myfile'` 将找不到。

## 初始化

`month_alpha`=$(date +b)

`mm`=$(date +m)

`dd`=$(date +d)

`h`=$(date +H)

`min`=$(date +M)

`today`=$month_alpha

`mmdd`=$mm

7 月 4 日是 04

错误示例：

`find /` 从根目录 (`/`) 开始搜索。

7. 当你使用 `-ctime +30` 时，“意味着文件已经**超过** 30 天没有修改了。换句话说，当你看到加号 `+` 时，表示“大于”；当你看到减号 `-` 时，表示“小于”。你可以将 `-daystart` 与 `-ctime` 和 `-mtime` 结合使用。

`-mtime -1` 表示在过去 24 小时内创建的文件。

`-daystart -1day` 表示文件自昨午夜以来创建。

错误示例：

`find /home` 从当前目录开始搜索。

`find /home/larry` 从当前目录开始搜索。

提示：如果你不确定文件的路径（后缀）是什么，请使用通配符：

`find /home/larry -name ".*"`

这是该命令的输出：

`find /home/larry -name ".*"`

提示：你可以通过使用 `'-type f'` 让你的 `find` 命令更快，不仅是文本文件，还有编译程序。

`find /home/larry -name ".*"`

这是该命令的输出：

`find /home/larry -name ".*"`

提示：`find` 还可以让你轻松识别在一天、一个月或六个月内创建或修改的文件。

`/home/larry/ROSETTA`

创建日期和时间："$day"

当前日期："$today"

`ls -v "Total"` 不打印 `"total"` 行。

这里是今天创建或修改的文件（过去 4 天内）：
