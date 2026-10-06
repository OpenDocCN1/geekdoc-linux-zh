

# 第 3 章 工具

若要根据第三个冒号分隔的字段（该字段包含你的用户 ID）对文件进行排序，你需要使用算术排序，指定第三字段 (-k3)，并指定冒号作为字段分隔符 (-t :):

```bash
$ sort -k3 -t : /etc/passwd
root:x:0:The Super User:/usr/bin/ksh
cron::1:1:Cron Daemon for periodic tasks::/
bin::3:3:The system of files::/
uucp::5:5:/usr/spool/uucpublic:/lib/uucp/uucico
as*:6:6:The Owner of Assignable Devices::/
sysinfo*:10:10:Access to System Information::/usr/bin/sh
george*:75:75:/users/george:/usr/bin/sh
steve*:203:300:/users/steve:/usr/bin/ksh
mail*:301::/usr/mail::
```

在这里，我们对每一行的第三个字段进行了加粗，这样你就可以轻松验证文件是否已根据用户 ID 正确排序。

# 其他选项

排序的其他选项允许你跳过字段中的某些字符、指定排序结束的字段、合并输入文件，并使用“字典序”（比较时仅使用字母、数字和空格）。关于这些选项的更多详细信息，请参阅 Unix 用户手册中的 sort 部分。

# uniq

当你需要查找或删除文件中的重复行时，就会使用 uniq 命令。
命令的基本格式为：

```bash
uniq in_file out_file
```

在此格式中，uniq 将 `in_file` 复制到 `out_file`，并在此过程中删除任何重复行。uniq 对重复行的定义是：完全匹配的连续行。

如果未指定 `out_file`，结果将写入标准输出。如果也未指定 `in_file`，uniq 将作为一个过滤器，并从标准输入读取输入。

以下是一些示例，向你展示 uniq 是如何工作的。假设你有一个名为 `names` 的文件，内容如下：

```bash
$ cat names
Charlie
Tony
Emanuel
Lucy
Ralph
Fred
Tony
$
```

你可以看到名字 Tony 在文件中出现了两次。你可以使用 uniq 来删除删除项：

```bash
$ uniq names # 打印唯一的行
Charlie
Tony
Emanuel
Lucy
Ralph
Fred
Tony
$
```

哎！Tony 在前面的输出中仍然出现了两次，因为这些多次出现在文件中并不是连续的，且不满足 uniq 对重复的定义。为了解决这种情况，通常会使用 sort 让重复行彼此相邻，正如本章前面提到的那样。然后将 sort 的结果传递给 uniq 处理：

```bash
$ sort names | uniq
Charlie
Emanuel
Fred
Lucy
Ralph
Tony
$
```

sort 将两行 Tony 移动到一起，然后 uniq 过滤掉重复行（但请记住，带有 `-u` 选项的 sort 正好可以执行此功能）。

# # -d 选项

通常，你会对查找文件中的重复项感兴趣。uniq 的 `-d` 选项可以用于此类目的：它告诉 uniq 只将重复行输出到 out_file（或标准输出）。无论出现多少次，行都只写入一次。

```bash
$ sort names | uniq -d # 列出重复行
Tony
$
```

作为一个更具实操性的例子，让我们回到 /etc/passwd 文件。该文件包含系统上每个用户的信息。可以想象，在从文件中添加和删除用户的过程中，可能同一个用户名被无意中输入了多次。你可以通过先对 /etc/passwd 排序并将结果传递给 uniq -d（如之前所做），来轻松地找到此类重复项：

```bash
$ sort /etc/passwd | uniq -d      # 查找 /etc/passwd 中的重复项
$
```

/etc/passwd 中没有重复的行项。但你真的想找到用户名的重复项，所以你只想查看每行的第一个字段（记住，/etc/passwd 每行从开头到冒号之前的字符都是用户名）。这无法直接通过 uniq 的选项完成，但你现在可以使用 `cut` 在将密码文件发送到 uniq 之前，从每行中提取用户名。

```bash
$ sort /etc/passwd | cut -f1 -d : | uniq -d      # 查找重复项
cem
```

事实 /etc/passwd 中 cem 和 harry 有多个条目。如果你想获取有关特定条目的更多信息，现在可以用 grep 从 /etc/passwd 中提取它们：

```bash
$ grep 'cem' /etc/passwd
20:cem*:91:91:/users/cem
166:cem*:91:91:/users/cem
$ grep 'harry' /etc/passwd
29:harry*:103:103:Harry Johnson:/users/harry
79:harry*:90:90:Harry Johnson:/users/harry
$
```

`-n` 选项用于找出重复项发生的行数。在 cem 的情况下，条目位于第 20 行和 166 行；在 harry 的情况下，两个条目位于第 29 行和 79 行。

# 其他选项

uniq 的 `-c` 选项添加出现计数，这在脚本中非常有用：

```bash
$ sort names | uniq -c      # 统计行的出现次数
1 Charlie
1 Emanuel
1 Fred
1 Lucy
1 Ralph
2 Tony
```

uniq -c 的一个更实用的用例是找出文件中最频繁出现的单词。你可以结合使用 sort, uniq -c 和 head 命令：

```bash
$ sort names | uniq -c | sort -nr | head
5
```

uniq 的另一个选项是忽略大小写，这在处理大小不敏感的数据时非常有用：

```bash
$ uniq -i names
Apple
apple
Apple
```

uniq 的另一个选项是合并相邻的重复行，这在统计每个单词次数时很有用：

```bash
$ uniq -c names
```
2 Tony
```

uniq 的 `-d` 选项可以只显示重复的行，这在查找重复项时很有用：

```bash
$ uniq -d names
Tony
```

$ uniq -c -d names
```
2
  Tony
```

uniq 的 `-u` 选项可以只显示不重复的行，这在提取唯一数据时很有用：

```bash
$ uniq -u names
Charlie
Emanuel
Lucy
Ralph
Fred
```

uniq 的 `-w` 选项可以指定比较的宽度，这在处理长字符串时很有用：

```bash
$ uniq -w3 names
```

uniq 的 `-f` 选项可以跳过起始的几个字段，这在处理特定格式时很有用：

```bash
$ uniq -f2 names
```

uniq 的 `-n` 选项可以跳过结束的几个字段，这在处理特定格式时很有用：

```bash
$ uniq -n2 names
```

uniq 的 `-y` 选项可以显示相邻行之间的差异，这在比较两个文件时很有用：

```bash
$ uniq -y names
```

uniq 的 `-s` 选项可以指定一个分隔符，这在处理特定分隔的文件时很有用：

```bash
$ uniq -s names
```

uniq 的 `-a` 选项可以忽略行中的所有空白字符，这在忽略格式差异时很有用：

```bash
$ uniq -a names
```

uniq 的 `-i` 选项可以忽略大小写，这在处理大小写不敏感的数据时很有用：

```bash
$ uniq -i names
```

uniq 的 `-U` 选项可以只输出不重复的行，这在过滤重复项时很有用：

```bash
$ uniq -U names
```

uniq 的 `-D` 选项可以只输出重复的行，这在查看哪些行重复时很有用：

```bash
$ uniq -D names
```

# 第 4 章 编写脚本

根据我们在第 2 章的讨论，“什么是 Shell？”你现在应该意识到，当你输入某些内容时你实际上是在进行编程。在本章中，你将学习如何编写脚本。

# 命令文件

Shell 脚本可以直接输入，如：

```bash
$ who | wc -1
```

也可以将其写入文件。例如，假设你需要找出登录用户。
你可以将任何命令放入文件中，使其可执行，然后只需通过输入其名称即可运行。这非常简单且强大，而且你在命令行中学到的所有知识也适用于脚本。
标准 shell 机制 I/O 重定向和管道适用于你自己的程序：

```bash
$ nu > tally
$ cat tally
8
```

假设你正在处理一个名为 sys.caps 的提案，每次打印你的提案时都需要以下命令序列：

```bash
tbl sys.caps | nroff -mm -Tlp | lp
```

# 编写脚本

哎！忘了提到一点。在从命令行执行脚本之前，你必须更改文件的权限使其可执行。这是通过修改模式命令 chmod 完成的。`+` 表示你想让后面的文件可执行。Shell 要求文件对你来说是可读且可执行的，你才能调用它。

```bash
$ ls -1 nu
-rw-r--r-- 1 steve steve    12 Jul 10 11:42 nu
$ chmod addx nu
Make it executable
$ ls -1 nu
-rwxrxr-x 1 steve steve    12 Jul 10 11:42 nu
$ 
```

现在你已经使其可执行了，再次尝试：

```bash
$ nu
8
$
```

