

# until 命令 173

else

fi

```
if [ "$# -eq 0 -o "$# -gt 1 ]
then
  echo "Usage: waitfor [-m] user"
  echo "-m means to be informed by mail"
  exit 1
fi
```

user="$1"

```
#
# 每分钟检查一次用户是否登录
#
```

```bash
until who | grep "^user" > /dev/null
do
  sleep 60
done
```

```
#
# 当我们到达这里时，用户已经登录
#
```

```bash
if [ "$mailopt = FALSE ]
then
  echo "$user has logged on"
else
  echo "$user has logged on" | mail steve
fi
```

第一个测试是检查是否指定了 -mailopt 选项。如果指定了，mailopt 将被赋值为 TRUE，执行 `shift` 来“移出”第一个参数（将要监控的用户名移动到 $1 并将 $# 减 1）。如果没有指定 -m 选项，则 mailopt 被设置为 FALSE。

执行过程与之前的版本相同，但在主代码块完成时，会测试 mailopt 变量以确定是通过电子邮件输出通知还是通过 echo 语句输出。

```bash
$waitfor sandy -m
Usage: waitfor [-m] user
  -m means to be informed by mail
$waitfor -m sandy &
[1] 5435
```

$ vi newmemo
Work continues

...
you have mail
$ mail
From steve Wed Aug 28 17:44:46 EDT 2002
sandy has logged on

```
?d
$
```

当然，我们可以编写 waitfor 让它接受 -m 选项作为第一个或第二个参数，但不符合 Unix 语法的运行方式：在命令行上，所有选项都应该位于任何其他类型的参数之前。

此外请注意，旧版本的 waitfor 的执行方式如下：

```bash
$ waitfor sandy | mail steve &
[1] 5522
$
```

通过添加 -m 选项可以达到相同的结果，但这显然不优雅得多。

目前的程序允许向 steve 发送新邮件，如果其他人想运行它，这并不特别有用。更好的方法是确定运行程序的用户，如果他们指定了 -m 选项，则向他们发送邮件。但如何做到这一点？一种方法是执行带有 am i 选项的 who 命令，获取用户名并将其作为邮件收件人。

这一切都可以在 waitfor 的最后一个 if 命令中完成，只需将其更改为如下：

```bash
if [ $(echo "user has logged on") ]; then
  runner=$(who am i | cut -cl-8)
  echo "$user has logged on" | mail $recipient
fi
```

现在任何人都可以运行该程序，邮件通知将发送给正确的收件人。

# 关于循环的更多

## 退出循环

有时程序逻辑要求立即退出循环语句。若要退出循环但不退出程序，请使用 `break` 命令：

```bash
break
```

# 关于循环的更多

当执行 `break` 时，控制将立即移动到循环外部，然后在那里继续正常执行。

处理这种情况的一种常见方法是使用无限循环，这种代码块旨在循环执行相同的命令，直到被 `break` 停止。

在这些情况下，可以使用 `true` 命令返回一个零的退出状态。`false` 命令也可以用于相反的情况，因为它返回一个非零的退出状态。如果你写：

```bash
while true
do
  ...
done
```

`while` 循环将被执行，因为 `true` 总是返回零退出状态。

由于 `false` 总是返回非零退出状态，循环

```bash
until false
do
  ...
done
```

也将永远执行。

因此，`break` 命令用于退出这类无限循环，通常在检测到错误条件或处理结束时：

```bash
while true
do
  cmd=$(getcmd)

  if [ "$cmd" = quit ];
    break
  else
    processcmd "$cmd"
  fi
done
```

`while` 循环将继续执行 `getcmd` 和 `processcmd` 程序，直到 `cmd` 等于 `quit`。此时，将执行 `break` 命令，导致循环退出。

如果 `break` 命令以如下形式使用

```bash
break 
```

最内层的循环将立即退出，因此在

```bash
for file
do
  ...
  while [ "$count" -lt 10 ]
  do
    ...
    if [ -n "$error" ]
    then
      break 2
  fi
  fi
  done
```

如果 `error` 不为空，则 `while` 和 `for` 循环都会退出。

# 跳过循环中的剩余命令

`continue` 命令与 `break` 类似，它不会导致循环退出，只是跳过循环当前迭代中的剩余命令。程序立即移动到循环的下一次迭代并继续进行。与 `break` 类似，`continue` 后面可以跟一个可选数字，所以

`continue n`

会导致跳过内层 n 个循环中的命令，之后程序的执行将恢复正常进行。

```bash
for file
do
  if [ ! -e "$file" ]
  then
    echo "$file not found!"
    continue
  fi

  #
  # 处理文件
  #
  ...
done
done
```

会检查 `file` 的每个值以确保文件存在。如果文件不存在，则打印一条消息，并跳过 `for` 循环内对文件的进一步处理。执行继续列表中的下一个值。

前一个示例等同于编写

```bash
for file
do
  if [ ! -e "$file" ]
  then
    echo "$file not found!"
  else
    #
    # 处理文件
    #
    ...
  fi
done
```

# 在后台执行循环

只需通过在 `done` 语句后放置一个符号 `&`，即可将整个循环发送到后台执行：

```bash
$ file in memo[1-4]
do
> run $file
> done & Send it to the background
[1] 9932
$
request id is laser1-85 (standard input)
request id is laser1-87 (standard input)
request id is laser1-88 (standard input)
request id is laser1-92 (standard input)
request id is laser1-94 (standard input)
```

# 循环的 I/O 重定向

你可以在循环上执行 I/O 重定向。输入重定向循环适用于从标准输入读取的命令。输出重定向循环适用于写入标准输出的命令。

```bash
$ for i in 1 2 3 4
do
> echo $i
> done > loopout
$ cat loopout
1
2
3
4
$
```

单个语句可以覆盖块重定向，就像 shell 中的任何其他语句显式重定向源或发送输出一样。

要强制输入或输出进入终端，利用 `/dev/tty`，无论你在 Mac、Linux 还是 Unix 系统上，它始终指向终端。

在下面的循环中，所有内容重定向到文件 `output`，但 `echo` 命令的输出显式重定向到终端：

```bash
for file
do
  echo "Processing file $file" > /dev/tty
done > output
```

你也可以重定向循环的标准错误输出，只需在 `done` 后面加上 `2> file`：

```bash
while [ "$endofdata" -ne TRUE ]
do
  ...
done 2> errors
```

在这里，循环中写入标准错误的输出将重定向到文件。

`2> file 1&2` 格式通常用于确保即使脚本可能将其输出重定向到文件或管道，错误信息也能发送到终端：

```bash
echo "Error: no file $file" 1&2
```

默认情况下，`echo` 将其输出发送到标准输出（文件描述符 1），而文件描述符 2 仍然是标准错误，且没有被重定向。上面的符号表示 `echo` 的错误消息应将其 `file #1` 输出重定向到 `file #2`，这是标准做法。你可以使用如下代码进行测试：

```bash
for i in "once"
do
  echo "Standard output message"
  echo "Error message" 1>&2
done > /dev/null
```

# 向循环输入和输出数据

命令的输出可以管道到循环（通过让循环结束前的命令以管道符号结尾），循环的输出也可以管道到另一个命令。这里有一个 `for` 命令输出管道到 `wc` 的示例：

```bash
$ for i in 1 2 3 4
do
done | wc
```

