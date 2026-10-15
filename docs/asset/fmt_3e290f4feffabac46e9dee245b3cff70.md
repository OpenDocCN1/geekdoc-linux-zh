
这种类型复合命令的一个经典示例是：

```bash
parentDir=`cd ..; pwd`
```

此行将 `parentDir` 变量设置为父目录名称。如果当前目录是 `/var/local`，则 `parentDir` 被设置为 `/var`。让我们看看在交互式运行以下命令会发生什么：

```bash
% PS1="[\w] " # 1
[/var/local] % cd ..; pwd # 2
/var
[/var/local] % (cd ..; pwd) # 3
/var
[/var/local] %
```

第 1 行更改了 shell 的提示符，显示当前目录——让你更容易看到命令的结果。

```bash
echo "breaking."
break 1;
fi
let y=$y-1
done
let x=$x-1
done
```

### 以下是脚本运行演示：

```
% chmod +x nested_loop
./nested_loop
[3, 3]
[3, 2]
breaking.
[2, 3]
[2, 2]
breaking.
[1, 3]
[1, 2]
breaking.
```

你可以看到，每当内层循环变量 `y` 等于 2 时，内部循环就会中断，外层循环继续下一次迭代。`y` 被称为循环变量，因为它控制了内层循环的迭代。

现在让我们看看如果你告诉 `break` 退出两个循环会发生什么：

#### 列表 4.18 double_loops 双循环——跳出两个嵌套循环

```bash
#!/bin/bash

x=3
while test $x -gt 0
do
	y=3
	while test $y -gt 0
	do
		echo "[$x. $y]"
		if test $y -eq 2
		then
			echo "breaking."
			break 2;
		fi
		let y=$y-1
	done
	let x=$x-1
done
```

### 以下是脚本运行演示：

```
% chmod +x double_loops
% ./double_loops
[3, 3]
[3, 2]
breaking.
```

这一次，一旦遇到 `break` 命令，两个循环都会终止。

## continue 命令

语法：

`continue [n]`

概要：

跳过命令块中剩余的命令。

`continue` 命令会立即开始循环命令的下一次迭代。你能猜出如果将将列表 4.18 中的 `break` 命令替换为 `continue` 语句会发生什么吗？列表 4.19 正是这样做的。

#### 列表 4.19 using_continue——使用 continue 命令

```bash
#!/bin/bash
x=3
while test $x -gt 0
do
  y=3
  while test $y -gt 0
  do
    echo "[$x, $y]"
    if test $y -eq 2
    then
      echo "continuing"
      continue;
    fi
    let y=$y-1
  done
let x=$x-1
done
```

## 总结

以下是脚本运行演示：

```
% chmod +x double_loops
./double_loops
[3, 3]
[3, 2] <- 这两行
continuing <- 无限重复
[3, 2]
continuing
[3, 2]
continuing
```

为什么使用 `continue` 命令而不是 `break` 命令会创建一个无限循环？这是因为脚本从未执行到递减 `x` 和 `y` 的代码行，因此 `test` 命令永远不会导致失败。

如果你使用 `continue 2` 命令，情况会发生细微变化。与 `break` 命令一样，你可以使用带有参数的 `continue` 命令指定要影响的循环数量。当使用 `continue 2` 时，脚本会显示：

```
./double_loops
[3, 3] <- 这些
[3, 2] <- 三行
continuing <- 无限重复。
[3, 3]
continuing
```

## 总结

本章涵盖的九个 shell 命令可以让你控制脚本的执行。它们可以分为四类：

- *杂项*——`exit` 和 `trap`。
- 决策命令——`if` 和 `case`。
- 循环命令——`for`, `while` 和 `until`。
- 跳跃命令——`break` 和 `continue`。

这些命令共同为你的脚本在如何执行上提供了极大的灵活性。`exit` 命令允许你在任何地方停止脚本。`trap` 命令允许你忽略信号，或者在检测到任何信号时启动某些命令。`if` 命令非常适合在少数选项之间做出决策。当需要更大的灵活性时，可以使用 `case` 语句。它可以测试变量是否等于任意数量的值，并为指定的每个值执行不同的命令或一组命令。`for`, `while`, 和 `until` 命令用于控制循环。`for` 命令遍历列表中的值。`while` 和 `until` 命令持续循环，直到 `test` 命令失败或成功。最后，`break` 和 `continue` 命令让你对循环迭代确切地如何以及何时开始和结束进行精细控制。

下一章，“控制 Shell”将讨论命令如何与 shell 交互作用的许多不同方面。它详细介绍了如何让命令在后台执行、如何序列化命令以使一个命令的执行取决于另一个命令的执行，以及许多其他主题。

# 控制 Shell

本章涵盖了 shell 编程的一些零碎知识。你将学习如何创建一个命令列表来一次执行多个命令，以及为什么这种技术有用。此外，你还学习了如何使用文件而不是键盘向程序提供输入，以及许多其他有趣的技巧。

91

## 创建命令列表

第 1 章指出每个 shell 命令都是一个进程。为了简单起见，没有提供关于进程的过多细节。但在你完全理解命令列表之前，你需要更多关于进程的细节。

> 注意

对于本章而言，命令和进程这两个术语几乎可以互换。命令列表是多个命令组合成一个单一命令的集合。

每个命令在停止时都会产生一个退出值。一个典型的成功命令退出值为 0。任何其他退出值都表示某种失败。

# 创建复合命令

第 2 行执行了两个命令：`cd` 命令和 `pwd` 命令。`cd` 命令切换到新目录；`pwd` 命令显示当前工作目录。请注意，`cd` 命令改变了当前目录，这并不是我们需要的行为。我们的目标是在不改变当前 shell 的情况下获取父目录的名称。

第 3 行中的括号表达式运行了与第 2 行相同的命令，不同之处它们是在一个子 shell（child shell）中运行的。`cd` 命令会正常地影响子 shell，因此 `pwd` 显示的是登录 shell 的父目录的名称。

现在，让我们回到原始的复合命令示例：`parentDir=$(cd .. :pwd)`

反引号中的字符串会被执行，其结果输出将替换原始命令中的反引号字符串。因此，这个示例简化为：

`parentDir=/var`

> 顺便一下，即使在“更强大”的 Perl 和 Tcl 语言中，使用 `(cd .. :pwd)` 转义到 shell 可能是确定父目录名称最简单的方法。学习基础（即 shell 语言）始终是一个好主意。

### 提示

接下来的示例如果 `init.dat` 文件不存在，将显示错误消息。在运行此示例之前，我确保了不存在 `init.dat` 文件，因此错误肯定会发生。

在运行测试或示例（例如从从书中！）时，确定测试的初始环境应该是什么，对于测试产生预期结果非常重要。在运行测试或示例时，唯一应该改变的是代码。

### 注意

```bash
% test -e init.dat || echo "Bad File.
Bad File
echo $? # 显示上一个命令的退出值。
0
```
