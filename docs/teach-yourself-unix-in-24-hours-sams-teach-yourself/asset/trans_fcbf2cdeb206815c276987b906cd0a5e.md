
# 基础 Shell 

这里的输出只是 Joe is basically。Shell 无法区分 `$learning` 和 `$learning` 变量。因为 `$learning` 没有被赋值任何值。要解决这个问题，请将变量用大括号括起来：

```bash
$ echo Joe is basically ${learning}
Joe is basically anti-taxes
```

如果 `learning` 未定义，输出可能不符合逻辑。它应该是 Joe is basically taxes。幸运的是，Shell 提供了一种方法在变量未定义时设置默认值：

```bash
$ echo Joe is basically ${learning:-pro}
Joe is basically pro to taxes
```

如果 `learning` 未定义，`:-` 语法会让 Shell 使用后面的字符串（包括空格在内），导致输出为空。这并没有给变量赋值。如果你需要重复使用该变量，可能希望在未定义时给它一个值。`:-` 字符可以做到这一点：

```bash
$ echo Joe is basically ${learning:-pro} ${learning}spending.
Joe is basically pro taxes and pro spending.
```

第一次解析变量时发现它未定义，Shell 将 `pro` `变量并输出。第二次解析变量时，它就有了 `pro` 的值。

变量通过 `read` 命令赋值。它会将单个单词赋值给指定的变量，列表中的最后一个变量接收剩余的单词。

```bash
$ read city state message
Morristown, New Jersey Hi Mom!
$ echo city is city
Morristown, is city
$ echo $state is state
New is state
$ echo $message is message
Jersey Hi Mom! is message
```

你可以看到，只有 `New` 被赋值给了 `state`。解决此问题的最好方法是用反斜杠转义空格：

```bash
$ read city state message
Morristown, New Jersey Hi Mom!
$ echo city is city
Morristown, is city
$ echo $state is state
New is state
$ echo $message is message
Jersey Hi Mom! is message
```

## 16.2：Shell 算术

尽管 Shell 将变量视为字符串，但仍方法方法对变量进行基础算术运算。同样，C 和 Korn Shell 提供了丰富的数学能力。

如果给 Shell 赋值了一个数值，可以使用 `expr` 命令对值进行基础算术运算。该命令接受多个参数来执行算术：

```bash
$ expr 1 + 1
```

参数之间必须有空格且存在，`expr` 命令才能工作。如果变量未定义或没有值（有时称为零长度），结果将是语法错误。这就是 `:-` 语法非常有帮助的地方：

```bash
$ expr ${undefined}
expr: syntax error
$ expr ${undefined:-0} + 1
```

0 和 1 的正常默认值是有用的。在数字上加上 0，你将得到相同的数字。同样，乘以或除以 1 也不会改变数字的值。`expr` 还支持减法、乘法、整数除法和取余。示例所示：

```bash
$ expr 11 - 5
```
![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_358_0.png)

# 基础 Shell 编程

```bash
$ expr 11 *** 5
55
$ expr 11 / 5
2
$ expr 11 % 5
1
```

注意，我必须在单引号中包含星号。如果我没那么做，Shell 会将其展开为当前目录下的文件列表，`expr` 程序将无法理解。

你可以通过用反引号包裹命令将算术结果赋值给其他变量：

```bash
$ newvalue=$(expr ${oldvalue:-0} + 1)
```

如果 `oldvalue` 被赋值，它就会加 1。如果 `newvalue` 被设置为 1，这在对数据进行指定次数循环时非常有用。

`expr` 命令也可以处理复杂的算术运算。你可以写一个表达式将两个数字相加并乘以第三个数字。通常，你需要担心运算符优先级，但 `expr` 并没有那么复杂。你只需要在括号中对操作分组：

```bash
$ expr \( 11 + 5 \) \* 6
```

这会将 11 和 5 相加，并将结果乘以 6。因为括号是重要的 Shell 字符，我需要用反斜杠转义它们。

> `expr` 是在 Bourne Shell 中执行算术运算非常有用的命令。字符串必须是数字，否则会报错，`expr` 命令的结果可以赋值给其他变量。
![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_359_0.png)

> `expr` 命令比这里描述的更强大；它包含了执行逻辑操作和对字符串进行操作的能力。更多信息请查看 man 页。
![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_359_1.png)

# 任务 16.3：常用函数

在编写程序时，你可能希望操作取决于某些值。一个简单的例子是 `rm -i` 命令，其中 `-i`  `rm` 在删除文件之前提示你。输入 `y`，文件被删除；输入 `n`，文件被保留。Shell 也有类似的选项。接下来的两个任务将介绍如何使用这些选项。

# 操作 (ACTION)

正如 `expr` 是在 Bourne Shell 中执行算术运算的强大命令。字符串必须是数字，否则会报错，`expr` 命令的结果可以赋值给其他变量。

变量赋值的另一种方法是从命令行参数。Shell 有内置变量来访问命令行。如果你写了一个复制文件的脚本并命名为 `copy-files`，你可能想列出命令行所有的文件：

```bash
$ copy-files file1 file2
```

程序将通过 `$1`、 `$2` 和 `$3` 访问这些内容：

```bash
cp $1 destination
cp $2 destination
cp $3 destination
```

`$` 变量是查看命令名的特殊情况，`*` 列出了所有的命令行变量。任何 Shell 程序中的标准数据都是变量。这些变量可以通过多种方式赋值：直接赋值、从用户输入或通过命令行赋值。Shell 还提供了对变量进行某些默认操作的方法。
