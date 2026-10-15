
`set` `book` "Red Fedora Linux Secrets"

`set` `year` 2005

`set` `price` $49.99

要引用变量的值，请在变量名添加美元符号 (`$`)。要打印变量，请使用以下格式：

```bash
% puts $book
Red Fedora Linux Secrets
```

如果你使用单个参数，`set` 会返回参数的值。因此，如下例所示，`set` 等同于 `$book`：

```bash
% puts [set book]
Red Fedora Linux Secrets
```

### 编写表达式

你可以通过将变量与数学运算符（如 `+` (加)、`-` (减)、`*` (乘) 和 `/` (除))结合来编写表达式。以下是一些表达式的示例：

```tcl
set count 1
$count+1
$count + 5 - 2
2 + 3.5
```

你可以在表达式中使用数字以及变量名。使用空格来增强可读性。使用括号指定你希望如何评估表达式。

除了基础数学运算符外，Tcl 还包含了内置的数学函数，如 `sin`、`cos`、`tan`、`log` 和 `sqrt`。像在 C 语言一样调用这些函数，括号中带有参数，如下：

```tcl
set angle 1.5
2*sin($angle)
```

此外，你还可以使用布尔运算符，例如 `!` (非)、`&&` (与) 和 `||` (或)。比较运算符如 `<` (小于)、`>` (大于)、`<=` (小于等于)、`==` (等于) 和 `!=` (不等于) 也是表达式。你可以使用布尔或比较运算符，真时评估为 1，假时评估为 0。你可以编写如下表达式：

```tcl
count == 10
angle < 3.1415
```

表达式本身并不是命令。你只能将表达式作为接受表达式作为参数的命令参数。例如，`if` 和 `while` 命令期望表达式作为参数。

Tcl 还存储了 `expr` 命令来评估表达式。接下来的示例显示了你如何在 Tcl 命令中评估表达式：

```bash
% set angle 1.5
1.5
% puts Result = [expr 2*sin($angle)]
Result = 1.9998997321
```

Tcl 将所有内容存储为字符串，你必须在需要数字的地方使用数字。但定义为 "Red Hat Linux Secrets"，例如，你无法编写表达式 `$count`。

### 使用控制流命令

Tcl 包含了控制流命令来控制程序的流程。其中最常见的有 `if`、`while` 和 `switch`。

`if` 命令允许在条件为真时执行代码块。`if` 命令的最简单形式是：

```tcl
if {condition} {
    # 如果条件为真执行代码
}
```

你还可以使用 `else` 子句在条件为假时执行代码块：

```tcl
if {condition} {
    # 如果条件为真执行代码
} else {
    # 如果条件为假执行代码
}
```

对于更复杂的条件，可以使用 `else if`：

```tcl
if {condition1} {
    # 如果 condition1 为真执行代码
} else if {condition2} {
    # 如果 condition2 为真执行代码
} else {
    # 如果以上都不为真执行代码
}
```

`while` 命令在条件为真时持续执行代码块：

```tcl
while {condition} {
    # 当条件为真时执行代码
}
```

`for` 命令用于固定次数地执行代码块或遍历项目集合：

```tcl
for {init} condition { step} {
    # 执行的代码
}
```

`switch` 命令用于根据变量的值执行代码块：

```tcl
switch variable {
    pattern1 {
        # 如果变量匹配 pattern1 则执行代码
    }
    pattern2 {
        # 如果变量匹配 pattern2 则执行代码
    }
    default {
        # 如果都不匹配模式则执行代码
    }
}
```

# 第25 章：Tcl/Tk 脚本 (第 81 页)

```tcl
while { 1 } {
    incr i                        # 增加 i
    if {$i == 5} { continue }     # 如果 i 是 5 则跳过
    if {$i > 10} { break }        # 如果 i 超过 10 则退出循环
    set sum [expr $sum+$i]        # 否则将 i 加到 sum 中
}
puts Sum = "$sum"
```

运行此脚本时，它应该显示如下内容：

```
Sum = 50
```

## 使用 for 命令

Tcl 的 `for` 命令接受四个参数，您应该按照以下方式输入：

```tcl
for {expr1} {expr2} {expr3} {
    commands
}
```

`for` 命令在循环开始时评估 `expr1`，并在 `expr2` 为真时执行最后一对大括号内的 `commands`。`for` 命令在每次执行命令后都会评估第三个表达式——`expr3`。你可以省略任何命令，但必须使用所有的大括号。下面的示例使用 `for` 循环来相加 1 到 10 的数字：

```tcl
#!/usr/bin/tcl
for {set i 0; set sum 0} {$i <= 10} {set sum [expr $sum+$i]; incr i}
puts Sum = "$sum"
```

运行此脚本时，它显示如下内容：

```
Sum = 55
```

## 使用 foreach 命令

在 C 语言中没有像 `foreach` 这样的命令，但当你想要对变量列表中的每个值执行某些操作时，`foreach` 非常好用。你可以按照如下方式添加一组数字：

```tcl
set sum 0
foreach i {1 2 3 4 5 6 7 8 9 10} {
    set sum [expr $sum+$i]
}
puts Sum = "$sum"
```

运行此脚本时，它也会打印 Sum = 55，因为脚本正在累加 1 到 10 的数字。

如果你在变量中有一个列表，可以使用该变量的值来代替第一对大括号内显示的列表。紧接 `foreach` 循环可以回显列表中的字符串：

```tcl
set users {root naba}
foreach user $users {
    puts "$user"
}
```

## 使用 switch 命令

Tcl 的 `switch` 命令与 C 语言的 `switch` 语句不同。Tcl 的 `switch` 命令不是评估数学表达式，而是将字符串与一组模式比较，并根据匹配到的模式执行一组命令。通常，模式是用正则表达式表示的。

访问第 24 章关于正则表达式的介绍。

下面的脚本说明了 `switch` 命令的语法和典型用法：

```tcl
#!/usr/bin/tcl
# 此脚本从用户处读取命令并使用 switch 语句处理
# 命令。
set prompt "Enter command \"quit\" to exit: *"
puts -nonline $prompt; flush stdout
while { [gets cmd] != -1 } {
    switch -exact $cmd {
        quit { puts "Bye!"; exit }
        start { puts "Started" }
        stop { puts "Stopped" }
        draw { puts "Draw.." }
        default { puts "Unknown command: $cmd" }
    }
    # 再次提示用户
    puts -nonline $prompt; flush stdout
}
```

以下是此脚本的示例会话（用户输入为加粗字体）：

```
Enter command "quit" to exit: help
Unknown command: help
Enter command "quit" to exit: start
Started
Enter command "quit" to exit: stop
Stopped
Enter command "quit" to exit: quit
Bye!
```
