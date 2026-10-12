
# 模块 4：TCSH Shell 编程 111

```
#
echo Enter s to list file sizes.
echo otherwise all file information is listed.
echo -n "Please enter option : "
set option = $?
```

```
if ($option == "s") then
    ls -s
else
    ls -l
endif
echo Goodbye
```

接下来是 `elsels` 脚本的运行：

```
> elsels
Enter s to list file sizes.
otherwise all file information is listed.
Please enter option: s
total 2
1 monday 2 today
Good-bye
>
```

### 专家提问

**问题：** 我如何使用 `if` 结构来检查参数？

**回答：** `if` 结构通常用于检查用户是否为 shell 脚本输入了数量参数。特殊的 shell 变量 `$#`（或 `$argv` 相关）包含了用户输入的参数数量。在测试操作中使用 `$#` 允许你判断用户是否输入了正确数量的参数。如果输入的参数数量错误，你可能需要退出 shell 脚本。在 BASH shell 中一样，你可以通过 `exit` 命令来实现。`exit` 命令结束 shell 脚本并返回一个退出状态。`exit` 接受一个数字参数：参数为 `0` 表示

# 模块 4：TCSH Shell 编程 109

## 控制结构

| 结构 | 描述 |
| :--- | :--- |
| `if` | 如果表达式为真，则执行后续命令。你可以指定多个 Linux 命令。`if ( expression ) then commands endif` |
| `if-else` | 如果表达式为真，则执行 `then` 之后的命令。如果表达式为假，则执行 `else` 之后的命令。`if ( expression ) then command else command defif` |
| `switch` | 允许你在多个备选命令之间进行选择。`switch(string) case pattern: command breaksw default: command endsw` |

表 4-4 TCSH 条件控制结构

shell 脚本成功结束：任何其他参数（例如 `1`）均表示发生了错误。

在下一个示例中，`if` 脚本只接受一个参数。如果用户未输入参数或输入了多个参数，`if` 测试将为真，打印错误信息，并且脚本将带有错误值退出。

# 参数数量

```bash
# $argv

if ($argv != 1) then
    echo "Invalid number of arguments"
    echo "Enter only one argument"
endif
```

以下是 `if` 脚本的运行示例：

> `ifarg`
> Invalid number of arguments
> Enter only one argument

**问题：** 我可以嵌套 `if` 结构来创建复杂的决策吗？

**答案：** 要嵌套 `if-then` 操作，你只需将一个 `if` 结构附加到 `else` 之后，而不是一个代码块。这样，你可以在几种替代方案之间进行选择。第一个替代方案由 `if` 结构指定，随后是其他方案，每个方案由其自己的 `else-if` 组件指定。最后一个 `if` 的替代方案由 `else` 指定。如果第一个 `if` 结构的测试失败，控制将传递到下一个 `else` 之后的下一个 `if` 结构，并执行其测试。如果它失败，控制将传递到下一个 `if` 结构并检查其测试。此过程持续直到某个测试返回真。这时该 `if` 将执行其命令，控制将离开 `if` 结构，进入 `endif` 关键字之后的下一个命令。

下面的示例说明了嵌套 `else-if` 操作的使用。

```bash
if ($option == "s") then
    ls -s
else if ($option == "l") then
    ls -1
else if ($option == "d") then
    ls -F
else
    echo "Invalid Option"
endif
```

# switch 结构

`switch` 结构在多个可能的替代命令之间进行选择。它类似于 BASH Shell 的 `case` 结构，通过将字符串与多个可能的模式比较来做出选择。每个可能的模式都与一组命令关联。如果找到匹配，则执行关联的命令。

`switch` 结构以关键字 `switch` 开始，后面跟着括号内的测试字符串。该字符串通常源于变量评估。接着是一组模式——每个模式之前都有关键字 `case`，并以冒号结束。与该选择关联的命令列在冒号之后。命令以关键字 `breaksw` 结束。在所有列出的模式之后，关键字 `endsw` 结束 `switch` 结构。`switch` 结构的语法所示：

```bash
switch (test-string)
    case pattern:
        commands
        breaksw
    case pattern:
        commands
        breaksw
    default:
        commands
        breaksw
endsw
```

## 注意

每个模式将与测试字符串进行匹配，直到找到匹配为止。如果没有找到匹配，则执行默认选项。默认选择用关键字 `default` 表示。默认选项是可选的。然而，它对于通知用户未匹配的测试字符串非常有帮助。

# 项目 4-1：使用 switch 的菜单

`switch` 结构通常用于实现菜单。在下一个示例中，用户被要求输入一个选项以不同的方式列出文件。请注意警告无效输入的默认选项。程序开始显示选项菜单并提示用户输入一个。`switch` 结构检测用户输入的内容并执行相应的命令。

## 步骤详解

1. 创建一个包含三个选项的菜单，用于列出大小、完整文件信息或仅文件（带有 `.c` 文件扩展名的文件）。使用三个简单的 `echo` 命令。
2. 提示用户输入选择，然后使用 `set` 命令和 `$` 操作符将其读取到 `choice` 变量。
3. 使用 `switch` 结构确定用户做的选择。在 `switch` 表达式中评估 `choice` 变量，并使用其值检查与 `case` 条目中每个模式值是否匹配。
4. 设置三个 `case` 条目。第一个用于 `s` 模式，匹配后将执行带有 `-s` 选项的 `ls` 命令，列出文件名及其大小。条目以 `breaksw` 命令结束。
5. 使用第二个 `case` 条目持有模式 `l`，如果匹配，将列出带有所有文件信息的文件，包括更改日期和访问权限。条目以 `breaksw` 命令结束。
6. 使用第三个 `case` 条目持有模式 `*.c`。在此匹配将执行 `ls *.c` 命令，它将显示所有以字符 `.c` 结尾的文件名（`*` 是匹配任何模式的通配符）。条目以 `breaksw` 命令结束。
7. 对于 `default` 条目，显示错误信息 "Invalid Option."。也将以 `breaksw` 命令结束。
8. 使用 `endsw` 命令结束 `switch` 结构。

`lschoice` 脚本所示：

```bash
echo s. List Sizes
echo l. List All File Information
echo c. List C Files
echo -n "Please enter choice: "
set choice = $
switch ($choice)
    case s)
        ls -s
        breaksw
    case l)
        ls -1
        breaksw
    case c)
        ls *.c
        breaksw
    default)
        echo Invalid Option
        breaksw
endsw
```

以下是 `lschoice` 脚本的运行示例。

```
> lschoice
s. List Sizes
l. List All File Information
c. List C Files
Please enter choice: c
io.c lib.c main.c
```
