
# 示例 8.16

（脚本）

```bash
#!/bin/sh

1 if `ypmatch` "$name" `passwd` > /dev/null 2>&1
2 then
  `echo` Found $name!
3 else
4   `echo` "Can't find $name."
  `exit` 1
5 fi
```

a. 如果使用 NIS+，该命令应读为：If `nismatch` "$name" `passwd.org.dir`.

### EXPLANATION

+   1 `ypmatch` 命令在 NIS `passwd` 数据库中搜索其参数 `name`。因为用户不需要看到输出，标准输出和标准错误被重定向到 `/dev/null`，即 UNIX 位桶。
+   2 如果 `ypmatch` 命令的退出状态为 0，程序控制进入 `then` 语句并执行命令直到到达 `else`。
+   3 `else` 语句下的命令在 `ypmatch` 命令未能在 `passwd` 数据库中找到 `$name` 时执行；即 `ypmatch` 的退出状态必须为非零，`else` 块中的命令才会被执行。
+   4 如果 `$name` 的值在 `passwd` 数据库中未找到，此 `echo` 语句将被执行，程序以 1 退出，表示失败。
+   5 `fi` 终止了 `if`。

# EXAMPLE 8.17

(The Script)

```bash
#!/bin/sh

# Scriptname: idcheck
# purpose: check user ID to see if user is root.
# Only root has a uid of 0.
# Format for id output:uid=9496(eillie) gid=40 groups=40
# root's uid=0
```

```bash
1 id=`id | nawk -F'[=]' '{print $2}'`   # Get user ID
echo your user id is: $id
2 if [ $id -eq 0 ]
then
3     echo "you are superuser."
4 else
echo "you are not superuser."
5 fi
```

(The Command Line)

```bash
$ idcheck
your user id is: 9496
you are not superuser.
```

```bash
7 $ su
Password:
8 # idcheck
your user id is: 0
you are superuser
```

### EXPLANATION

+   1 `id` 命令通过管道传递给 `awk` 命令。`awk` 使用等号或左括号作为字段分隔符，从输出中提取用户 ID，并将输出赋给变量 `id`。
+   2 如果 `id` 的值等于 0，则执行第 3 行。
+   4 如果 `id` 不等于 0，则执行 `else` 语句。
+   5 `fi` 标记了 `if` 命令的结束。
+   6 `idcheck` 脚本由当前用户执行，其 UID 为 9496。
+   7 `su` 命令将用户切换为 `root`。
+   8 `#` 提示符表示超级用户 `root` 是新用户。`root` 的 UID 为 0。

#### 8.5.6 The if/elif/else Command

`if/elif/else` 命令允许多路决策过程。如果 `if` 之后的命令失败，则测试 `elif` 之后的命令。如果该命令成功，则执行其 `then` 语句下的命令。如果 `elif` 之后的命令失败，则检查下一个 `elif` 命令。如果没有任何命令成功，则执行 `else` 命令。`else` 块称为默认值。

### FORMAT

```
if command
then
    command(s)
elif command
then
    commands(s)
elif command
then
    command(s)
else
    command(s)
fi
```

# EXAMPLE 8.18

```bash
(The Script)
#!/bin/sh
# Scriptname: tellme
1 echo -n "How old are you? "
read age
```

```bash
2 if [ $age -lt 0 -o $age -gt 120 ]
then
    echo "Welcome to our planet! "
    exit 1
fi
```

```bash
3 if [ $age -ge 0 -a $age -lt 13 ]
then
    echo "A child is a garden of verses"
elif [ $age -ge 13 -a $age -lt 20 ]
then
    echo "Rebel without a cause"
elif [ $age -ge 20 -a $age -lt 30 ]
then
    echo "You got the world by the tail!!!"
elif [ $age -ge 30 -a $age -lt 40 ]
then
    echo "Thirty something..."
```

```bash
4 else
    echo "Sorry I asked"
```

```bash
5 fi
```

(The Output)

```bash
$ tellme
How old are you? 200
Welcome to our planet!
$ tellme
How old are you? 13
A child is a garden of verses
$ tellme
How old are you? 55
Sorry I asked
```

### EXPLANATION

1 用户被要求输入。输入被赋给变量 `age`。
2 在方括号内执行数值测试。如果 `age` 小于 0 或大于 120，则执行 `echo` 命令，程序以退出状态 1 终止。交互式 shell 提示符将出现。
3 在方括号内执行数值测试。如果 `age` 大于或等于 0 且小于 13，测试命令返回退出状态 0，即 true，然后执行 `then` 之后的语句。否则，程序控制转到 `elif`。如果该测试为假，则测试下一个 `elif`。
4 `else` 构造是默认值。如果以上任何语句都不为真，则将执行 `else` 命令。
5 `fi` 终止了初始的 `if` 语句。

#### 8.5.7 文件测试

在编写脚本时，脚本通常要求某些文件可用，并且这些文件具有特定的权限、属于特定类型或具有其他属性。 （参见第 333 页的表 8.4。）你会发现文件测试是编写可靠脚本的必要部分。

当 `if` 语句嵌套时，`fi` 语句始终与最近的 `if` 语句配对。对嵌套的 `if` 进行缩进可以更轻松地看出哪个 `if` 语句与哪个 `fi` 语句对应。

### EXAMPLE 8.19

(The Script)

```bash
#!/bin/sh
file=./testing
1 if [ -d $file ]
then
    echo "$file is a directory"
2 elif [ -f $file ]
then
3   if [ -r $file -a -w $file -a -x $file ]
   then  # nested if command
      echo "You have read, write, and execute permission on $file."
4   fi
5 else
    echo "$file is neither a file nor a directory."
6 fi
```

### EXPLANATION

- 1 如果文件测试为目录，则打印 `testing is a directory`。
- 2 如果文件 `testing` 不是目录，否则如果文件是普通文件，则...
- 3 如果文件 `testing` 可读、可写且可执行，则...
- 4 `fi` 终止最内层的 `if` 命令。
- 5 如果第 1 行和第 2 行均不为真，则执行 `else` 命令。
- 6 这个 `fi` 与第一个 `if` 对应。

#### 8.5.8 空命令

空命令由冒号表示，是一个内置的、无操作的命令，返回退出状态 0。它用作 `if` 命令之后的占位符，当你没有要执行的操作，但需要一个命令，否则程序会因 `then` 语句后需要内容而产生错误信息。空命令常被用作循环命令的参数，使循环成为无限循环。

### EXAMPLE 8.20

(The Script)

```bash
1 name=Tom
2 if grep "$name" databasefile > /dev/null 2>&1
then
3 :
4 else
echo "$1 not found in databasefile"
exit 1
fi
```
