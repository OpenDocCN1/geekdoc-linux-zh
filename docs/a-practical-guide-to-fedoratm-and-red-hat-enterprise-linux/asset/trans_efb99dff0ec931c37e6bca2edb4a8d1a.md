

接受在单引号或双引号内包含参数的命令。对`commands`进行引用会使shell将整个命令作为单个参数传递给`trap`。

执行`commands`后，shell将从中断处继续执行脚本。如果你希望`trap`在接收到信号时阻止脚本退出，但不显式运行任何命令，你可以指定一个空（null）的`commands`字符串，如`lockitty`脚本（第1004页）所示。以下命令捕获信号15，之后脚本继续执行：

```
trap '' 15
```

以下脚本展示了`trap`内建命令如何捕获终端中断信号（2）。你可以使用SIGINT、INT或2来指定此信号。该脚本返回的退出状态为1：

```
$ cat inter
#!/bin/bash
trap 'echo PROGRAM INTERRUPTED; exit 1' INT
while true
do
 echo "Program running."
 sleep 1
done
$ ./inter
Program running.
Program running.
Program running.
CONTROL-C
PROGRAM INTERRUPTED
$
```

`inter`的第二行使用INT设置了对终端中断信号的陷阱。当`trap`捕获到该信号时，shell会执行`trap`命令中单引号内的两个命令。`echo`内建命令显示消息`PROGRAM INTERRUPTED`，`exit`终止运行脚本的shell，父shell显示提示符。如果没有`exit`，shell在显示消息后会返回控制权给`while`循环。`while`循环会持续重复，直到脚本接收到信号为止，因为`true`实用程序总是返回`true`退出状态。你可以用`:(null)`内建命令代替`true`，它写作冒号，总是返回`0 (true)`状态。

当脚本被过早终止时，`trap`内建命令经常删除临时文件，从而确保不会留下文件杂乱文件系统。以下名为`addbanner`的shell脚本使用两个陷阱，在脚本正常终止或因挂起、软件中断、`quit`或软件终止信号而终止时删除临时文件：

```
$ cat addbanner
#!/bin/bash
script=$(basename $0)

if [ ! -r "$HOME/banner" ]
    then
        echo "$script: need readable $HOME/banner file" 1>&2
        exit 1
fi

trap 'exit 1' 1 2 3 15
trap 'rm /tmp/%%.$$.$script 2> /dev/null' EXIT

for file
do
    if [ -r "$file" -a -w "$file" ]
    then
        cat $HOME/banner $file > /tmp/%%.$$.$script
        cp /tmp/%%.$$.$script $file
        echo "$script: banner added to $file" 1>&2
    else
        echo "$script: need read and write permission for $file" 1>&2
    fi
done
```

当使用一个或多个文件名参数调用时，addbanner循环处理这些文件，在每个文件的顶部添加标题。当你在文档顶部使用标准格式（例如备忘录的标准布局）或想为shell脚本添加标准标题时，此脚本非常有用。标题保存在名为~/banner的文件中。由于addbanner使用包含用户主目录路径名的HOME变量，多个用户无需修改即可使用该脚本。如果Max在脚本中用/home/max代替$HOME，然后将脚本交给Zach，那么Zach要么必须修改它，要么当Zach运行时addbanner会使用了Max的banner文件（假设Zach对该文件具有读权限）。

addbanner中的第一个陷阱使其在接收到挂起、软件中断（终端中断或quit信号）或软件终止信号时以状态1退出。第二个陷阱用EXIT代替signal_number，这导致trap在脚本因接收到退出命令或达到其末尾而退出时执行其命令参数。这些陷阱共同作用，无论脚本是正常终止还是过早终止，都会删除临时文件。第二个陷阱的标准错误在trap尝试删除不存在的临时文件时被发送到/dev/null。在这些情况下，rm会将错误消息发送到标准错误；由于标准错误被重定向，用户不会看到该消息。

有关使用trap的另一个示例，请参见第1004页。

## kill：终止进程

kill内建命令向进程或作业发送信号。kill命令的语法如下：

*kill* [–*signal*] *PID*

其中*signal*是信号名称或编号（例如，INT或2），*PID*是要接收信号的进程的进程标识号。你可以指定作业号（第163页）作为*%n*来代替*PID*。如果省略*signal*，*kill*发送*TERM*（软件终止，编号15）信号。有关信号名称和编号的更多信息，请参见第1047页的表27-5。

以下命令向作业编号1发送*TERM*信号，无论其在后台是正在运行还是已停止：

```
$ kill --TERM %1
```

由于*TERM*是*kill*的默认信号，你也可以将此命令写为*kill* *%1*。使用命令*kill* -l（小写“el”）可以显示信号名称列表。被中断的程序可能会将事情留在不可预测的状态：可能会留下临时文件（正常情况下它们会被删除），权限可能会改变。编写良好的应用程序会捕获信号并在退出前进行清理。大多数精心编写的应用程序都会捕获INT、QUIT和*TERM*信号。要终止程序，首先尝试INT（如果正在运行的作业在前景中，则按CONTROL-C）。由于应用程序可能被编写为忽略此信号，你可能需要使用*KILL*信号，该信号不能被捕获或忽略；这是一种“确保终止”。有关更多信息，请参见第465页的“Kill：向进程发送信号”。

## eval：扫描、求值并执行命令行

*eval*内建命令扫描命令行之后的命令。在此过程中，*eval*处理命令行，就像* bash*在执行命令行时一样（例如，它展开变量，将变量名替换为其值）。有关更多信息，请参见第403页的“处理命令行”。在扫描（并展开）命令行后，它将结果命令行传递给* bash*以执行。

以下示例首先将值*frog*赋给变量*name*。接下来，*eval*扫描命令*\$name=88*，并将变量*\$name*展开为*frog*，生成命令*frog=88*，并将其传递给* bash*以执行。最后一条命令显示*frog*的值。

```
$ name=frog
$ eval \$name=88
$ echo \$frog
88
```

### 使用序列表达式

下一个示例使用*eval*使带有序列表达式（第406页）的花括号展开接受变量，通常它并不这样做。以下命令演示了带有序列表达式的花括号展开：

```
$ echo {2..5}
2 3 4 5
```

`bash`处理命令行时做的第一件事之一是执行花括号展开；稍后它展开变量（第403页）。当你在花括号展开中提供无效参数时，`bash`不执行花括号展开；相反，它将*字符串*传递给被调用的程序。在下一个示例中，`bash`无法在花括号展开阶段展开`{$m..$n}`，因为它包含变量，所以继续处理命令行。当它进入变量展开阶段时，它展开`$m`和`$n`，然后将字符串`[2..5]`传递给`echo`。

```
$ m=2 n=5
$ echo {$m..$n}
{2..5}
```

当`eval`扫描相同的命令行时，它如前所述展开变量，生成命令`echo [2..5]`。然后它将该命令传递给`bash`，现在`bash`可以执行花括号展开：

```
$ eval echo {$m..$n}
2 3 4 5
```

## getopts：解析选项

`getopts`内建命令解析命令行参数，使编写遵循Linux参数约定的程序变得更加容易。`getopts`的语法为

```
getopts optstring varname [arg ...]
```

其中*optstring*是有效选项字母的列表，*varname*是逐个接收选项的变量，*arg*是要处理的可选参数列表。如果不存在*arg*，`getopts`处理命令行参数。如果*optstring*以冒号(:)开头，脚本必须负责生成错误消息；否则，`getopts`生成错误消息。

`getopts`内建命令使用`OPTIND`（选项索引）和`OPTARG`（选项参数）变量来跟踪和存储与选项相关的值。当shell脚本启动时，`OPTIND`的值为1。每次调用`getopts`并定位到一个参数时，它都会将`OPTIND`递增到要处理的下一个选项的索引。如果选项需要参数，`bash`将参数的值赋给`OPTARG`。

要指示某个选项需要参数，请在*optstring*中对应的字母后跟随一个冒号(:) 。例如，*optstring* `dx:or:`指示`getopts`搜索-d、-x、-o、-l、-t和-r选项，并告知它-o和-t选项需要参数。

将`getopts`用作`while`控制结构中的*test-command*，允许你逐个循环处理选项。`getopts`内建命令检查选项列表中*optstring*中的选项。每次循环时，`getopts`将其找到的选项字母存储在*varname*中。

