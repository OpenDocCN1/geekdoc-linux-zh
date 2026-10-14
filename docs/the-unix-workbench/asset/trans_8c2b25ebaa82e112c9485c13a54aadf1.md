

chapter_number=5

为了打印变量中的数据（也称为变量的值），我们可以使用 `echo`。当你想获取变量的值时，必须在变量名前加上美元符号（`$`）。让我们试试看：

```
echo $chapter_number
```

```
5
```

可以使用 `let` 命令通过算术运算符修改变量的值：

```
let chapter_number=$chapter_number+1
echo $chapter_number
```

```
6
```

你也可以将字符串存储在变量中：

```
the_empire_state="New York"
echo $the_empire_state
```

```
New York
```

有时你可能想像在命令行中那样运行一条命令，并将该命令的结果存储在变量中。我们可以通过将命令包裹在美元符号和括号（`$( )`）中来实现。这种语法称为命令替换。命令被执行后，替换为运行该命令所得出的字符串。例如，如果我们想存储 `math.sh` 中的行数：

```
math_lines=$(cat math.sh | wc -l)
echo $math_lines
```

```
7
```

带美元符号的变量名也可以用在其他字符串中，以便将变量的值插入到字符串中：

```
echo "I went to school in $the_empire_state."
```

```
I went to school in New York.
```

编写 Bash 脚本时，脚本会为你免费提供几个变量。让我们用以下代码创建一个名为 `vars.sh` 的新文件：

```
#!/usr/bin/env bash
# File: vars.sh
echo "Script arguments: $@"
echo "First arg: $1. Second arg: $2."
echo "Number of arguments: $#"
```

现在让我们用几种不同的方式运行这个脚本几次：

```
bash vars.sh
```

```
Script arguments:
First arg: . Second arg: .
Number of arguments: 0
```

```
bash vars.sh red
```

```
Script arguments: red
First arg: red. Second arg: .
Number of arguments: 1
```

```
bash vars.sh red blue
```

```
Script arguments: red blue
First arg: red. Second arg: blue.
Number of arguments: 2
```

```
bash vars.sh red blue green
```

```
Script arguments: red blue green
First arg: red. Second arg: blue.
Number of arguments: 3
```

你的脚本可以像命令行程序一样接受参数！脚本的第一个参数存储在 `$1` 中，第二个参数存储在 `$2` 中，依此类推。传给脚本的所有参数形成的数组存储在 `$@` 中，我们将在本章后面讨论如何处理数组。传给脚本的参数总数存储在 `$#` 中。

## 总结

- 可以使用等号（`=`）运算符给变量赋值。
- 可以将字符串或数字赋值给变量。
- 可以通过在变量名前加美元符号（`$`）来访问变量的值。
- 可以使用美元符号加括号的语法（命令替换）来执行命令并将输出保存到变量中。
- 可以在自己的脚本中通过美元符号后跟参数编号来访问命令行参数。

## 练习

- 编写一个 Bash 程序，将两个数字赋值给不同的变量，然后程序打印这些变量的和。
- 编写另一个 Bash 程序，将两个字符串赋值给不同的变量，然后程序打印这两个字符串。写一个版本让两个字符串打印在同一行，再写一个版本让两个字符串打印在不同行。
- 编写一个 Bash 程序，打印传给该程序的参数个数乘以传给该程序的第一个参数的结果。

## 用户输入

如果你正在编写供自己或他人使用的 Bash 程序，获取用户输入的一种方法是指定用户需要提供给程序的参数，就像我们在上一节中讨论的那样。你也可以通过使用 `read` 命令暂时停止程序的执行，来让用户在命令行中键入字符串。让我们编写一个小脚本，看看 `read` 命令是如何工作的：

```
#!/usr/bin/env bash
# File: letsread.sh

echo "Type in a string and then press Enter: "
read response
echo "You entered: $response"
```

现在让我们运行这个脚本：

