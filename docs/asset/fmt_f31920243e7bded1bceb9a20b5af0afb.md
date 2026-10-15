
这里还有另一个示例，用于测试 `$1`（第一个命令行参数）是否为有效选项（以 `-` 开头且我们认识到的字符）。

```bash
case $1 in
    -l | -d)
        # Perform a listing
        echo "All files in $HOME:\n"
        ll -R $HOME | more
        ;;
    -i)
        # -i means set to an interactive flag to true
        interactive="TRUE"
        ;;
    *)
        # Invalid input
        echo "$0: $1 is an invalid option"
        exit 1
        ;;
esac
```

本章稍后的一个示例中将使用 `case` 语句。

## 循环

很多时候，你需要重复执行某个操作。在 shell 中，有两种方法可以做到这一点：

- `for` 循环获取一个项目列表，并对列表中的每个项目执行一次循环中的命令。
- `while` 循环在某个命令（通常是 `test` 命令）执行成功时执行某些命令。（如果测试条件为真，则执行循环中的命令，并再次执行该命令以检查是否应该继续循环。）

`for` 循环的基本格式如下：

```bash
for var in list_of_items
do
    cmdA
    cmdB
    cmdC
done
```

当循环开始时，变量 `var` 的值被设置为 `list_of_items` 中待遍历的第一个单词。然后，执行 `do` 和 `done` 语句之间的三条命令。当程序到达 `done` 语句后，它回到循环顶部，将 `var` 赋值给列表中的下一个项，执行命令，依此类推。在循环的最后一次迭代中，程序继续执行 `done` 语句之后的下一个可执行语句。

`list_of_items` 可以是任何由空白字符分隔的单词列表。你可以输入单词，或使用变量或命令替换来构建列表。例如，假设我们要将一个名为 `.kshrc` 的新文件复制到几个用户的主目录中。使用 `for` 循环是最简单的方法：

```bash
for name in ralph norton alice edith archie
do
    echo $name
    cp /tmp/.kshrc.new /users/$name/.kshrc
done
```

该示例可以扩展为使用 `rcp` 命令将某些文件复制到几台机器上，并使用 `remsh` 命令验证它们是否已到位：

```bash
for host in neptune jupiter mars earth sun
do
    echo $host
    rcp /etc/passwd /etc/hosts $host:/etc
    rcp /.profile $host:/.profile
    remsh $host ll /etc/passwd /etc/hosts /.profile
done
```

你也可以使用命令替换生成 `list_of_items`，从而处理当前目录中的文件列表：

```bash
for file in `ls`
do
    if [ -r $file ]
    then
        echo "$file is readable"
    fi
done
```

请注意，`for file in *` 也能起到相同的作用。

![](img/75f39fc91296b889c0653851accdfd46_745_0.png)

如果你有一个较大的列表想要遍历，并且不想在命令行上输入它们，你可以将它们输入到一个文件中。然后，使用 `cat` 命令和命令替换，你可以生成 `list_of_items`：

```bash
for i in `cat important_files`
do
    # do something with each of the files listed in the
    # important_files file.
done
```

然而，`for` 循环通常用于处理命令行参数列表（`$*`）：

```bash
for name in $*
do
    if [ ! -f $name -a ! -d $name ]
    then
        echo "$name is not a valid file or directory name"
    else
        # do something with the file or directory
    fi
done
```

即将介绍的 `trash` 程序包含一个以类似方式处理命令行参数的 `for` 循环。

### `while` 循环

`while` 循环的格式如下：

```bash
while cmd1
do
    cmdA
    cmdB
    cmdC
done
```

首先执行 `cmd1`。如果它执行成功，则执行 `do` 和 `done` 语句之间的命令。然后再次执行 `cmd1`；如果成功，则再次执行循环中的命令，依此类推。当 `cmd1` 失败时，程序跳转过 `done` 语句，并继续执行下一个可执行语句。

大多数情况下，代替 `cmd1` 执行的命令是 `test` 命令。然后你可以执行如 `if` 部分所述的逻辑测试。如果测试成功（为真），则执行循环中的命令，脚本再次测试该条件。如果你希望循环运行固定次数，或者希望某事发生直到满足某些条件，`while` 循环非常有用。

现在让我们看一下使用 `while` 的一个示例。我们将每 30 秒运行一次 `netstat` 命令，总共运行十次，查看我们主要局域网接口的输出。对于我们正在运行的 Solaris 系统，这将是 `le0`。请记住，你的主要局域网接口可能有不同的名称，如果你不是使用 Solaris 系统，那几乎肯定如此。让我们首先看一下我们的简短程序：

![](img/75f39fc91296b889c0653851accdfd46_746_0.png)

该程序使用 `netstat` 显示主要局域网接口（lan0）的统计数据，共十次，每 30 秒一次：

```bash
#!/bin/ksh
i=1
while [ $i -le 10 ]
do
    print $i
    netstat -i | grep le0
    sleep 30
    let i=i+1
done
```

我们以非常简单的方式增加 `i`，每次循环都加一。每次循环我们都评估 `i` 的值，以确定它是否小于或等于（`le`）十。如果是，则运行 `netstat -i`。

在运行这个名为 `net1` 的程序之前，让我们运行 `netstat -i` 命令查看其输出，然后运行 `net1`：
