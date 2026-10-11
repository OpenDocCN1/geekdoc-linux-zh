
# 第 20 页

以下是目录 `/home/larry/ROSETTA` 下的子目录：

```
find /home/larry/ROSETTA -type d -print
```

`/home/larry/ROSETTA/TEST`

`/home/larry/ROSETTA/LOGS`

`/home/larry/ROSETTA/TEMP`

`/home/larry/ROSETTA/OUTPUT_FILES`

`/home/larry/ROSETTA/PAYROLL_ERR_DIR`

`/home/larry/ROSETTA/REPORTS`

`/home/larry/ROSETTA/ARCHIVES`

`/home/larry/ROSETTA/INPUT_FILES`

`/home/larry/ROSETTA/PROD`

`/home/larry/ROSETTA/PAYROLL`

`/home/larry/ROSETTA/INTRO`

`/home/larry/ROSETTA/SYS`

`/home/larry/ROSETTA/INT_TEST`

这里是 `/home/larry/ROSETTA` 下超过 90 天未被访问的子目录列表：

（提示：你什么也看不见，因为我错误地使用了 `-atime -ctime`）

```
find /home/larry/ROSETTA -type d -atime +90 -print
```

让我们再次运行该命令，使用 `-ctime`：

`/home/larry/ROSETTA/PAYROLL_ERR_DIR`

### 列出特定目录下的所有子目录

以下任命令均有效：

```
ls -1 /home/larry/ROSETTA | grep d
```

```
find /home/larry/ROSETTA -type d
```

### 列出所有文件

列出所有文件（包括子目录下的所有文件），以下任命令均有效：

```
ls -1 /home/larry/ROSETTA
```

```
find /home/larry/ROSETTA -print
```

```
find /home/larry/ROSETTA -type f -print
```

注意：如果你使用 `.`（表示当前目录），输出将不包含完整路径。

以下两个命令将显示相同的输出；这两个命令都应从命令行输入：

```
ls -1 /home/larry/SCRIPTS | grep "Jul 15"
```

```
find /home/larry/SCRIPTS | grep "Jul 15"
```

记住：你可以为搜索指定多个点。该命令能够搜索两个目录树 `/home/larry` 和 `/home/jane`，查找包含字符串 'Where are you'的文件。

```
find /home/larry/jane -type f -exec grep -l "Where are you" {} \;
```

### 如何使用 `-ctime +30 (-name "*" -name "junk*") -print`

解释：从当前目录开始，所有超过 30 天未被访问且以 `.o` 结尾或以 `junk` 开头的文件。

你很少需要使用 `-`（与），“与”逻辑是隐含的。例如，当你想查找 `-ctime +30 -size +1000000c` 时，你是在要求查找大小超过 1 MEG 且超过 30 天未被访问的文件（两个条件必须同时满足，而不仅仅是其一）。

感叹号 `!` 表示“非”；在配合 `-a !`（与非）使用时通常是合适的

```
find /home/larry -type f \( -name "*.ksh" -a ! -name "*.pl" ) -print
```

换句话说，从目录 `/home/larry` 开始，查找所有不 `!` 以 `.ksh` 结尾的文件，并且 `-a` 查找所有不以 `.pl` 结尾的文件。

使用 `ls` 列出文件有多种方法。尝试选择你最喜欢的一种。

注意：`'-ls'` 选项与 `'exec -l'` 提供相同的输出。

这些命令列出了所有超过 1 兆（100 万字节）的文件：

```
find /home/larry -type f -size +1000000c -ls >/tmp/output
```

```
find /home/larry -type f -size +1000000c -exec ls -l \; >/tmp/output
```

```
find /home/larry -type f -size +1000000c -ls >/tmp/output
```

永远在没有测试命令的情况下使用 `'exec rm'` 来删除文件。为什么？例如，当我要求 `'find'` 删除所有超过一周的文件时，这里是一些我想要删除的文件：

```
-rw-r-- 1 root group      181 Sep 18 InputStream.h
-rw-r-- 1 root group    135 Sep 18 Connection.h
-rw-r-- 1 root group      97 Sep 18 Handler.h
```

`find` 很好地定位了所有文件，但发现有几个没有包含 core 单词的文件：

所以，让我们再次强调这一点：

在没有先测试命令的情况下使用 `'exec rm'` 来删除文件。

另一种方法是用 `'exec ls -l'` 替换 `'exec rm'`。

这是一个如何将 `'find'` 与 `'rm'` 结合的示例：

```
find / -name core -name "*junk*" -time +7 -exec rm -f {}
```

删除所有名为 `'core'` 或 `'junk'` 且未被访问的文件

建议：先使用 `find` 命令获取将删除文件的日志：

```
find / -name core -name "*junk*" -time +7 -exec ls -l {} >/tmp/log
```

你也可以使用 `-ok` 选项，如果你想删除文件（系统会询问你），你必须回答 `'y'` 或 `'n'`。

```
find -name "*junk*" -time +7 -ok {}
```

处理大量文件（例如 10,000 个文件）时，`'x'` 是未知数量；`xargs` 命令告诉系统无论有多少参数，都处理所有

```
find -type f -print|xargs "$my_string"
```

然后 `"find"` 会搜索系统上的每个文件并列出包含 `"Hi, Larry!"` 的文件。

如果 `$my_string` 包含 `"HI, Larry!"`，如果你有访问远程服务器，可以将 `'rsh'` 命令（远程 shell）与 `find` 命令结合；例如：

```
rsh server -type f -size +900000c -print -ls 2>/dev/null
```

完成。`find.ksh`

## `find_file.ksh`

```bash
#!/bin/ksh

# 程序：find_file.ksh

# 目的：帮助查找文件。

# 作者：Larry Smith，审核：__

# 难度：中

# 用法：./find_file.ksh 将提示 (1) 起点 (2)文件名

# 或 ./find_file.ksh /home/larry/myfile.txt

# 或 ./find_file.ksh /home/larry/myfile*

# 或 ./find_file.ksh /home/larry/myfile* >/tmp/results

# 注意：

# 记住：'larry*' 将查找所有以 'larry' 开头的文件。

# 'larry.*' 将查找所有以 'larry' 开头的文件。

# 为什么？'*' 匹配前面的字符零个或多个。

# 详情：wildcards.txt

clear # 清空用户屏幕
```

注释：这是脚本 `$0`。

目的：帮助查找文件。

如果用户在命令行中提供了起始目录名和文件名，则使用它们；否则，提示用户输入。

```bash
if [ $# -eq 2 ]; then #命令行参数数量为 2，则
where_to_search=$1
filename=$2
if [ ! -d "$filename" ] || [ ! -x "$filename" ]; then # 如果不是目录或可读/执行，则
print "无效目录：$where_to_search"
exit
else # 提示用户输入 ($where_to_search 和文件名)
print "\请输入你想开始搜索的目录："
```

系统警告：这将花费很长时间！

你的当前目录搜索点为：`$home/larry`

默认值为 `/home/larry`

```
read dir_name
where_to_search=${dir_name:-/home/larry}
if [ ! -d "$where_to_search" ] || [ ! -x "$where_to_search" ]; then
print "无效目录：$where_to_search"
exit
print "\请输入你想查找的文件名。
示例 1：myfile.txt
示例 2：myfile.*
print "文件名："
read filename
if [ -z "$filename" ]; then # 如果用户只是按了回车，则退出
print "错误"
你必须指定文件名全部或部分。
重试。退出。
print "\n你的搜索将从目录 $where_to_search 开始
```
