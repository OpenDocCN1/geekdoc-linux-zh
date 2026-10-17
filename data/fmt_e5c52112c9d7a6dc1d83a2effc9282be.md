
```bash
lpstat -a | grep 'not accepting' | while read LINE
do
  Q=$(echo $LINE | awk '{print $1}')
  lpc enable $Q
done
lpstat -p | grep disabled | while read LINE
do
  P=$(echo $LINE | awk '{print $2}')
  lpc start $P
done
```

**列表 16.13** 使用 `-a` 和 `-p` 对 `lpstat` 命令进行脚本化。

# 打印队列地狱：保持打印持续

注意**列表 16.13**，我们必须通过两个独立的循环分别处理打印队列和打印机。在第一个 `while` 循环中，所有队列都被启动。在第二个循环中，我们为每个打印机启用打印功能。这种方法的缺点是当你有几百台打印机时，扫描所有打印机并重新扫描打印服务的时间可能非常长。当然，如果你有几百台打印机，应该使用 `lpc all` 一次启动所有内容。

正如我之前所说，我们也可以将**列表 16.13** 中的两个循环写成单行命令。我们可以在同一行组合 `grep` 和 `awk` 命令，并使用命令替换来执行 `lpc` 命令。以下两个命令替换了 `while` 循环。

```bash
lpc enable $(lpstat -a | grep 'not accepting' | awk '{print $1}')
lpc start $(lpstat -p | grep disabled | awk '{print $2}')
```

第一条命令启用队列，第二条命令启动打印。由 `$(command)` 符号指定的命令替换执行相应的 `lpstat` 命令，然后对标签进行 grep 并提取打印机/队列名称。结果被用 `lpc` 命令的参数。

# 整合一切

现在我们需要合并针对不同 Unix 变体的 shell 脚本，以便一个脚本完成所有工作。请不要认为获取几个 shell 脚本、提取它们并将新函数组合进新脚本中是一项困难的任务。为了制作本章的单一脚本，我们将采取脚本中的精华并提取代码。对于每个 shell 脚本，我们创建一个新函数，这只需要 `function` 关键字、函数名以及用大括号包围的代码块，`function function_name { code stuff here }`。让我们看看**列表 16.14** 中的合并 shell 脚本，并在最后介绍这些函数。

```ksh
#!/bin/ksh
#
# SCRIPT: PQ_all_in_one.ksh
#
## AUTHOR: Randy Michael
# DATE: 03/14/2002
# REV: 1.1.P
#
# PLATFORM: AIX, HP-UX, Linux and Solaris
```

**列表 16.14** PQ_all_in_one.ksh shell 脚本列表。（续）
