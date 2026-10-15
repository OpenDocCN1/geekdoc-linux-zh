
# 第 8 章：信息传递

UNIX shell 最强大的功能之一是管道（pipe）。管道允许你将一个命令的输出作为另一个命令的输入。这使你能够通过简单、专门的工具来构建复杂的程序。

管道符号用竖线（`|`）表示。当你使用管道时，shell 将第一个命令的 `stdout` 连接到第二个命令的 `stdin`。

以下是使用管道的示例：

```bash
$ ls -l | grep .txt
```

在这个示例中，`ls -l` 以长格式列出所有文件，`grep .txt` 过滤出包含 `.txt` 的行。

## 标准错误（stderr）重定向

以下是标准错误（stderr）重定向的示例：

```bash
$ command 2> error.log  # 将 stderr 重定向到文件
$ command 2> /dev/null  # 抑制错误消息
$ command > file 2>&1   # 同时重定向 stdout 和 stderr
```

## 标准输入（stdin）重定向

如果你能重定向标准输出，你就必须能够重定向标准输入。`stdin` 的符号是 `<`。

以下是标准输入（stdin）重定向的示例：

```bash
$ payroll file_containing_employee_hours and rates
$ mailx obrien < spammail # 将垃圾文件内容邮件给 obrien
$ tr "OB" "ob" < f1 > f2 # 重定向输入和输出
# 将 f1 中的 Os 和 bs 改为
# f2 中的 os 和 bs。
```

## 协进程

管道允许你将一个命令的输出作为另一个命令的输入。这使你能够通过简单、专门的工具来构建复杂的程序。

管道符号用竖线（`|`）表示。当你使用管道时，shell 将第一个命令的 `stdout` 连接到第二个命令的 `stdin`。

以下是使用管道的示例：

```bash
$ ls -l | grep .txt
```

在这个示例中，`ls -l` 以长格式列出所有文件，`grep .txt` 过滤出包含 `.txt` 的行。

![](img/de6a3b5a3b516159c825f1c10314d877_214_0.png)

**图 8.1:** 协进程通过管道与另一个进程通信。

![](img/de6a3b5a3b516159c825f1c10314d877_214_1.png)

**图 8.2:** 没有协进程的情况下，dbx 会连续查看 lbolt 内核单元 50 次。

lbolt 不需要被连续查看 50 次；它只是一个内核单元。不过，如果你好奇的话，它存储了系统时间。注意，示例输出让你大致了解当脚本不使用协进程时，必须创建多少个 UNIX 进程：

```bash
# echo $$
725
# ksh
# echo $$
1440
## exit
# time ./copro2 /vmunix /dev/mem
real 0m21.06s # 不使用协进程时大约需要 21 秒
user 0m19.46s
sys 0m1.21s #
```

```bash
# ksh
# echo $$
echo 1596 # 创建了多少个进程 (-156)
#
```

下一个示例使用协进程执行相同的操作。注意，脚本中的代码稍微复杂一些，但回报可能是巨大的，正如从性能对比中所示：

```bash
# time ./copro1 /vmunix /dev/mem
real 0m3.90s
user 0m0.00s
sys 0m0.03s
#
```

```bash
# ksh
# echo $$
大约创建了 3 个进程
# 与协进程一起运行
#
```

在查看那个让你的代码性能提升了 7000% 的脚本之前，让我向你展示一下 dbx 的交互会话是什么样的。此示例使用实时内核作为目标，因此你必须拥有 root 权限才能执行以下命令。注意在实际向工具输出某些内容之前的所有提示消息。在交互模式下，你可以忽略这些输出。但在脚本中，你必须清除这些数据，只捕获你想要的数据。你在两个脚本中看到了处理这些多余输出的两种方法：

```bash
# dbx -k /vmunix /dev/mem
dbx version 5.1
输入 'help' 获取帮助。
```

![](img/de6a3b5a3b516159c825f1c10314d877_215_0.png)

```
stopped at [thread_block:3074 , 0xfffffffc0002d0450] Source not available
```

```
warning: Files compiled -g3: parameter values probably wrong
(dbx) p lbolt
5190922
(dbx) quit
#
```

第一个脚本没有使用协进程，因此性能较差。注意对命令行参数的简洁检查。它询问参数数量是否等于二，并执行 `&&` 之后的命令。脚本的主体位于一个 50 次的循环内部，在循环中重复地将 `print` 命令的输出作为 `dbx` 命令的输入。这就像你在交互式 dbx 提示符下输入了两个命令：`p bolt` 和 `quit`。`2>/dev/null` 语法通过重定向 `stderr` 移除了 dbx 输出中以 warning 开头的显示行。`tail -1` 表示你唯一感兴趣的是输出的最后一行，你将其追加到名为 `times` 的文件中。

如果你认为可以使用这种相同的管道技术将 `print`（或 `echo`）命令的输出传递到几乎任何交互式工具，你是正确的。然而，不要急着开始修改你的生产脚本。等你看过协进程示例再说：

```bash
# cat copro2
!/bin/ksh

[ $1 -ne 2 ] && { # 如果没有两个参数，则显示消息
  print 'Usage: $0 vmunix vmzcore'
  exit 1
}
# 主循环
ntimes=0;
while (( ntimes < 50 )); do
  print 'lbolt;quit' | dbx $1 2>/dev/null | tail -1>>times
  # 创建一个进程
  ntimes=$ntimes+1
done
exit
```

下一个示例使用运行 dbx 的协进程来处理对名为 `innocuous-looking` 的内核单元当前值的 5 次请求。一个看起来非常强大的命令在用法帮助之后显示。它简单地显示 `>times`。这看起来就像你正试图将无的标准输出重定向到名为 `times` 的文件中。shell 看到 `>times`，进入截断模式，并将 `times` 的当前内容置为零字节，这正是你想要的。这防止了脚本每次运行时输出的无限制增长。它还有效地删除了文件的当前内容，并读取它进行后续处理。

# 文件与目录操作

当你接收到一个重要文档时，你可能会将其储存在文件柜中。文件柜很可能有一个包含几个抽屉、各种文件夹，可能甚至子文件夹的组织结构。另一种方法是将所有重要文档扔进一个鞋盒并塞在床底下。请注意，这两种方法都能实现存储文档的目标。

需要检索文档时，区别就显而易见了。如果你是鞋盒派，你可能需要花时间翻找堆在鞋盒里的所有杂乱纸张。相反，如果纸张被组织在抽屉、文件文件夹和子文件夹中，检索适当的文件只需要打开正确的抽屉并取出正确的文件夹即可。后者与目录层次结构中文件存储的描述非常相似。

所有现代文件系统都提供目录层次结构来帮助组织文件的存储和检索。对文件和目录的访问是 shell 与系统及用户交互非常显著的一部分。

本章将教你以下内容：

- `PATH` 变量是如何工作的
- 文件和目录如何相互作用
- 文件属性如何描述文件
- 设备特殊文件的使用
- 如何使用硬链接和符号链接
- 文件访问方法
- 过滤器命令的本质
- 创建临时文件的安全方法

## 路径

用户或脚本可以使用*绝对文件规范*或*相对文件规范*来请求访问文件。绝对文件规范提供了定位文件的目录和子目录层次结构路径。相对文件规范则相对于当前工作目录定位目标文件。下面的示例首先使用相对文件规范访问文件。在更改默认目录后，相对规范将不再有效，但无论你的目录位于何处，绝对规范将始终有效。

下面的示例成功地使用了相对文件规范，更改了默认目录，然后在尝试使用相对文件规范重新执行相同命令时失败了。随后通过使用绝对文件规范解决了这个问题：

```bash
$ cat params # 相对规范
!/bin/ksh
print "Argument 1 is ${1}"
print "Argument 2 is ${2}"
print "Argument 3 is ${3}"
print "There are $# arguments."
```

```bash
$ pwd
/home/obrien/scripts
$ cd / # 更改默认目录
$ cat params # 相对规范失败
-ksh: cat: params: cannot open [No such file or directory]
$ cat /home/obrien/scripts/params # 绝对规范有效
!/bin/ksh
print "Argument 1 is ${1}"
print "Argument 2 is ${2}"
print "Argument 3 is ${3}"
print "There are $# arguments."
```

相对文件规范乍一看是不完整的文件规范。如果你在当前工作目录（通过 `pwd` 命令显示）中输入命令 `ls -l obrien`。如果 shell 正在寻找一个命令文件——例如当寻找命令、脚本或程序时——它会查看 `PATH` 变量的内容，列出查找该文件的目录列表。

shell 可以根据命令行上的位置来决定是使用 `PATH` 变量还是使用当前工作目录。紧跟在 shell 提示符（`$`）之后的文件名被视为命令，因此会在 `PATH` 变量中列出的目录中查找。

在命令 `ls -l mydata` 中，`ls` 在 `PATH` 目录中查找，而 `mydata` 则从当前工作目录查找。这两个搜索位置都可以被绝对文件规范所覆盖，例如 `/usr/bin/ls -l /usr/users/obrien/mydata`。
