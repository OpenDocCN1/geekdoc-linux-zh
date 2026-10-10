
在`until`循环之前，`Username`变量最初设置为位置参数`$1`的值。`until`循环的测试条件检查`Username`变量的值为空。如果测试返回假，则执行`do`和`done`之间的命令。在`do/done`命令的接近是`shift`命令。`shift`命令移除`$1`参数的值并如前所述移动位置参数的值。注意，在`shift`命令之后必须将`Username`重新设置为`$1`的值，因为`$1`的值已经发生了。循环将一直持续，直到一个空值被移动到`$1`参数中。

为了帮助你更好地理解其工作原理，展示了修改后的`mkuser.sh`脚本的运行。注意传递给脚本了四个参数：

```
$ sudo ./mkuser.sh Wash Zoe Simon Shepherd
[sudo] password for Christine:
[... 这里是 Wash 的记录：
Wash:x:511:514::/home/Wash:/bin/bash
[...
这里是 Zoe 的记录：
Zoe:x:512:515::/home/Zoe:/bin/bash
[...
这里是 Simon 的记录：
Simon:x:513:516::/home/Simon:/bin/bash
[...
这里是 Shepherd 的记录：
Shepherd:x:514:517::/home/Shepherd:/bin/bash
Account is ready for use.
Leaving script...
$
```

这运行得非常棒！现在你可以将需要账户的用户名传递给脚本，这将迅速加快账户创建过程。

## 查看 for 循环

`for`循环在操作上与`while`和`until`循环大不同。`for`循环不测试任何条件，而是对一定数量的列表项执行其命令。`for`循环的基本语法如下：

```
for variable in list
do
  commands
done
```

当循环开始时，`variable`被赋值为列表值中的第一个项。`do/done`结构中的命令执行一次。然后，`variable`被赋值为第二个项的值，`do/done`结构中的命令再次执行。这种持续一直持续，直到每个列表项的值都赋值给`variable`为止。

此处的`showfor.sh`脚本展示了一个简单的`for`循环示例：

```
$ cat showforloop.sh
#!/bin/bash
#
# 演示 for 循环
################################
#
for Number in 1 2 3
do
  echo $Number
done
#
$
```

该脚本的循环将为每个列表项处理`do/done`部分的命令。在这种情况下，列表项是数字 1、2 和 3。以下是脚本的运行情况：

```
$ chmod u+x showforloop.sh
$
$ ./showforloop.sh
1
2
3
$
```

你可以看到脚本将列表中的每个项赋值给变量`Number`。然后它执行`do/done`结构中的命令。因为命令是`echo $Number`，所以脚本的输出显示了`for`循环每次迭代时变量的值。

> 注意

> 注意，所有三种循环类型都使用`do/done`结构来包裹在循环内执行的命令。

`for`循环的方便之处在于你不需要在列表中使用数字。你也可以使用单词，如下所示：

```
$ cat showforloop.sh
#!/bin/bash
# 演示 for 循环
#################################
# for Pet in Cat Dog Bird
do
    echo $Pet
done
#
$ ./showforloop.sh
Cat
Dog
Bird
$
```

`seq`命令是另一个与`for`循环配合使用的方便命令。如果你在列表中需要大量数字，它非常棒。你不需要手动输入所有数字，`seq`命令允许你生成一个范围。`seq`的基本语法为：

```
seq [START] [结束]
```

例如，如果你使用`seq 1 10`，它将生成从 1 到 10 的数字。如果你使用`seq 5`，它将生成从 1 到 5 的数字。

`seq`命令经常用于`for`循环中：

```bash
for i in $(seq 5)
do
  echo $i
done
```

这是一个无需手动列出数字即可遍历序列的有用方法。

## 使用列表

你可以使用各种运算符在单行中组合多个命令。这对于执行依赖于前一个命令成功结果的任务非常有用。你已经看到了一些运算符：

- 分号（`;`）

- 安符（`&`）

- 双与符号（`&&`）

- 双管道（`||`）

分号（`;`）允许你顺序执行多个命令，无论前一个命令是否成功。例如：

```bash
$ command1; command2
```

安符（`&`）在后台运行命令，允许你立即继续在终端工作。例如：

```bash
$ command1 &
```

双与符号（`&&`）仅在前一个命令成功（返回状态为 0）时才执行第二个命令。这对于条件逻辑很有用：

```bash
$ command1 && command2
```

双管道（`||`）仅在前一个命令失败（返回非零状态）时执行第二个命令。这对于错误处理很有用：

```bash
$ command1 || command2
```

你还可以组合这些运算符。例如：

```bash
$ command1 && command2 || command3
```

在这种情况下，`command2`仅在`command1`成功时运行，而`command3`仅在`command2`失败时（意味着`command1`失败）运行。

以下是这些运算符运行的一些示例：

```bash
$ ls /non_existent_directory && echo "Directory found"
ls: cannot access '/non_existent_directory': No such file or directory
$ ls /non_existent_directory || echo "Directory not found"
Directory not found

$ ls / && echo "Root directory exists"
bin  boot  dev  etc  home  lib  media  root  root  sbin  usr  var
Root directory exists
```

你可以通过使用`useradd`命令配合列表来修复这个问题。所需的修改如下：

```
useradd $Username || break
```

除了`useradd`之外，命令列表中还添加了一个额外的命令`break`。如果`useradd`命令没有执行成功，双管道运算符将触发`break`命令，导致`while`循环终止。这使得在出现问题时，脚本的执行看起来要清晰得多，如下所示：

```
$ ./mkuser.sh Saffron
./mkuser.sh: line 14: /usr/bin/useradd: Permission denied
Leaving script...
$
```

这样好多了！现在如果发生错误，脚本将显示错误信息并立即退出。

# 使用函数

函数是脚本的一部分，用于执行特定的子任务，并可以从脚本的其他部分通过名称进行调用。函数的定义方法是在函数名后放置一组括号`()`，并将构成函数的代码行包含在花括号`{}`之中：

```
function_name() {
  commands
}
```

`function`关键字可以选择性位于函数名之前。无论哪种情况，函数都是通过名称调用的，就像普通的内部或外部命令一样。

函数在帮助创建模块化脚本方面非常有用。回到`mkuser.sh`脚本，我们可以组合出一个可以在整个脚本中使用的函数：

```
# Function Declarations ###
#
err_function() {
  echo "An error has occurred!"
  echo "Exiting script immediately..."
  exit
}
}
```

这个新函数将有助于`useradd`命令列表。原始列表看起来如下：

```
useradd $Username    || break
```

在声明了`err_function`函数后，命令列表可以如下所示：

```
useradd $Username    || err_function
```

如果`useradd`命令没有成功完成，将会调用`err_function`。这为 shell 脚本提供了更大的灵活性。

> 函数不会直接运行，也不会按照它们在脚本中出现的顺序运行。它们只有在脚本的主体中被调用时才会运行。
