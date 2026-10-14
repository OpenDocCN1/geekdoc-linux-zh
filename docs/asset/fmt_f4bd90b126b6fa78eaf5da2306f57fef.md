
你的函数名称为 `function_name`，你将在脚本的其他地方用它来调用函数。函数名后面必须紧跟括号，括号之后是用大括号括起来的命令列表。

## 示例

使用函数的示例——

```bash
#!/bin/sh

#在此处定义你的函数

Hello() {

  echo "Hello World"

}
```

```bash
## 调用你的函数

Hello
```

## 输出

```
$.test.sh

Hello World

$
```

## 向函数传递参数

你可以定义一个函数，它在调用这些函数时接受参数。这些参数将由 `$1`、`$2` 等表示。以下是一个示例，我们传递了两个参数 `Zara` 和 `Ali`，然后在函数中捕获并打印了这些参数。

```bash
#!/bin/sh

#在此处定义你的函数

Hello () {

    echo "Hello World $2"

}
```

```bash
## 调用你的函数

Hello Zara Ali
```

## 输出

```
$./test.sh

Hello World Zara Ali

$
```

## 从函数返回数值

如果你在函数内部执行 `exit` 命令，它的效果不仅是终止函数的执行，还会终止调用该函数的 Shell 程序。如果你只想终止函数的执行，那么有一种方法可以退出定义的函数。根据具体情况，你可以使用 `return` 命令从函数返回任何值，其语法如下——

```
return code
```

在这里，`code` 可以是你选择的任何内容，但显然你应该选择在整个脚本语境下有意义或有用的值。

## 示例

以下函数返回返回值 1 ——

```bash
#!/bin/sh

#在此处定义你的函数

Hello () {

    echo "Hello World $1 $2"

    return 10

}
```

```bash
## 调用你的函数

Hello Zara Ali
```

```bash
## 接收上一个命令返回的值

ret=$?
```

```bash
echo "Return value is $ret"
```

## 输出

```
$./test.sh

Hello World Zara Ali

Return value is 10

$
```

## 嵌套函数

函数较有趣的特性之一是它们既可以调用自己，也可以调用其他函数。调用自身的函数被称为递归函数。

下面的示例演示了两个函数的嵌套——

```bash
#!/bin/sh

# 从一个函数调用另一个函数

number_one () {

  echo "This is the first function speaking..."

  number_two

}

number_two () {

  echo "This is now the second function speaking..."

}

## 调用函数一。

number_one
```

## 输出

```
This is the first function speaking...

This is now the second function speaking...
```

## 从提示符调用函数

你可以在你的 profile 文件中定义常用的函数，这样在每次登录时都可以使用它们。或者，你可以将定义分组在一个文件中（例如 `test.sh`），然后通过输入以下命令在当前 Shell 中执行该文件——

```bash
$ test.sh
```

这将导致 `test.sh` 中定义的任何函数读取并定义到当前 Shell 中，如下所示——

```bash
$ number_one
```

This is the first function speaking...

This is now the second function speaking...

$
若要从 Shell 中移除函数的定义，请使用 `unset` 命令配合 `-f` 选项。这与你从 Shell 中移除变量定义使用的命令相同。

```bash
$ unset -f function_name
```

## Unix - 管道与过滤器

你可以将两个命令连接在一起，使得一个程序的输出成为下一个程序的输入。以这种方式连接的两个或多个命令形成一个管道。要创建管道，在命令行中的命令之间放置一个竖线 (`|`)。当一个程序从另一个程序获取输入，对该输入执行某些操作，并将结果写入标准输出时，它被称为过滤器。

## grep 命令

`grep` 在文件或文件中搜索包含特定模式的行。其语法为——

```bash
$grep pattern file(s)
```

"grep" 的名称源于 ed（一种 UNIX 编辑器）命令 `g/re/p`，其意思是“全局搜索正则表达式并打印所有包含该内容的行”。正则表达式可以是纯文本（例如一个单词）和/或用于模式匹配的特殊字符。`grep` 最简单的用法是查找由单个单词组成的模式。它可以在管道中使用，这样只有输入文件中包含给定字符串的的行才会被发送到标准输出。如果你不给 `grep` 提供要读取的文件名，它将读取标准输入；这就是所有过滤器程序的工作方式——

```bash
$ls -l | grep "Aug"
-rw-rw-rw- 1 john doc 11008 Aug 6 14:10 ch02
-rw-rw-rw- 1 john doc 8515 Aug 6 15:30 ch07
```
