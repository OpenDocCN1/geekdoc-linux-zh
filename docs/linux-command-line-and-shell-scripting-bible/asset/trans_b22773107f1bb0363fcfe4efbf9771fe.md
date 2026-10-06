

```bash
echo "$file is a file"
done
./test6
/home/rich/test/dir is a directory
/home/rich/test/myprog.c is a file
/home/rich/test/myprog is a file
/home/rich/test/myscript is a file
/home/rich/test/newdir is a directory
/home/rich/test/newfile is a file
/home/rich/test/newfile2 is a file
/home/rich/test/testdir is a directory
/home/rich/test/testing is a file
/home/rich/test/testprog is a file
/home/rich/test/testprog.c is a file
```

该命令遍历了 `/home/rich/test/*` 列出的结果。代码使用 `test` 命令测试每个条目，判断它是目录（使用方括号方法）还是文件（使用 `-f` 参数）。参见第 9 章“使用结构化命令”）。

注意在此中，我在 `if` 语句中采取了一些不同的处理：

```bash
if [ -d "$file" ]
```

在 Linux 中，包含空格的目录和文件名是完全合。为了适应这一点，你应该将 `$file` 变量包含在双引号中。如果不这样做，当你遇到包含空格的目录或文件名时，将会得到错误：

- /test6: line 6: [: too many arguments
- /test6: line 9: [: too many arguments

bash shell 会将额外的单词解释为 `test` 命令的参数，导致错误。

你也可以在同一个 `for` 语句中结合目录搜索方法和列表方法，通过在命令中列出一系列目录通配符：

```bash
$ cat test7
#!/bin/bash
# iterating through multiple directories
```

```bash
for file in /home/rich/* /home/rich/badtest
do
if [ -d "$file" ]
then
echo "$file is a directory"
elif [ -f "$file" ]
then
```

## 第二部分 Shell 脚本基础

```bash
echo "$file is a file"
else
  echo "$file doesn't exist"
fi
done
$test7
/home/.backup.timestamp is a file
/home/.bash_history is a file
/home/.bash_logout is a file
/home/.bash_profile is a file
/home/.bashrc is a file
/home/.badtest doesn't exist
```

第一条语句使用文件通配（globbing）来遍历通配符字符生成的文件列表，然后遍历列表中的下一个文件。你可以组合列表中的任意数量的通配符条目进行遍历。

> 注意：请注意你可以在列表中输入任何内容——即使文件或目录不存在，该语句也会尝试处理你放置在列表中的任何内容。这在处理文件和目录时可能会成为一个问题。你无法知道自己是否正在尝试遍历一个不存在的目录：在尝试处理每个文件或目录之前，对其进行测试总是一个好主意。

## C 风格 for 命令

如果你用 C 编程语言进行过任何编程，你可能会对 bash shell 使用 `for` 命令的方式感到惊讶。在 C 语言中，`for` 循环通常定义一个变量，然后在每次迭代中自动更改它。通常情况下，程序员使用该变量作为计数器，并在每次迭代中将计数器加 1 或减 1。bash `for` 命令也可以提供这种功能。本节展示了如何在 bash shell 脚本中使用 C 风格的 `for` 命令。

## C 语言 for 命令

C 语言 `for` 命令有特定的方法来指定变量、一个必须保持为真以继续迭代的条件，以及一种每次迭代更改变量的方法。当指定的条件变为假时，循环停止。条件使用标准符号定义。例如，取 C 语言代码：

```c
for (i = 0; i < 10; i++) {
  printf("The next number is %d\n", i);
}
```

## 更多结构化命令

这段代码产生了一个简单的迭代循环，变量 `i` 被用计数器。第一部分为变量分配了默认值。中间部分定义了循环迭代的条件。当定义的条件变为假时，循环停止。最后部分定义了迭代过程。每次迭代后，变量都会加 1。

bash shell 还支持一种与 C 风格 `for` 循环相似的 `for` 循环版本，尽管它存在细差异以及一些让 shell 程序员困惑的地方。以下是 C 风格 bash 的基本格式：

```bash
for (( variable; condition; iteration ))
```

C 风格 `for` 循环的格式会让 shell 程序员感到困惑，因为它使用了 C 风格的变量引用而不是 shell 变量引用。它看起来如下：

```bash
for (( a = 1; a < 10; a++ ))
```

注意有几点不符合标准的 bash `for`：

- 变量赋值可以包含空格。
- 迭代中的变量前没有加 `$`。
- 迭代过程没有使用 `expr`。

shell 开发者创建这种格式是为了更贴近 C 风格的 `for` 命令。这对于 C 程序员来说很棒，但可能会让 shell 程序员措手无策。在脚本中使用 C 风格 `for` 循环时要小心。这里是在 bash shell 中使用 C 风格 `for` 命令的示例：

```bash
$ test7
#!/bin/bash
# testing the C-style for loop

for (( i=1; i < 10; i++ ))
do
    echo "The next number is $i"
done
./test7
The next number is 1
The next number is 2
The next number is 3
The next number is 4
The next number is 5
The next number is 6
The next number is 7
The next number is 8
The next number is 9
The next number is 10
```

## Shell 脚本基础

`for` 循环通过 `for` 中定义的变量（此例中的字母 `i`）遍历命令。在每次迭代中，`i` 变量包含分配给 `for` 循环的值。每次迭代后，循环过程应用于该变量，在本例中它加 1。

## 使用多个变量

C 风格 `for` 命令还允许使用多个变量进行迭代。循环分别处理每个变量，允许你为每个变量定义不同的迭代过程。虽然你可以多个变量，但在 `for` 中只能定义一个条件：

```bash
$ cat test7
#!/bin/bash
# multiple variables

for (( a=1, b=10; a <= 10; a++, b-- ))
do
  echo "$a $b"
done
./test7
1 10
2 9
3 8
4 7
5 6
6 5
7 4
8 3
9 2
10 1
```

`a` 和 `b` 变量分别初始化为不同的值，并定义了不同的迭代过程。循环在增加 `a` 的同时减少 `b`。

## while 命令

`while` 命令是 `if-then` 语句和 `for` 循环的结合。`while` 命令允许定义一个测试命令，只要该命令返回零退出状态，就会循环一组命令。它在每次迭代开始时测试命令。当测试命令返回非零退出状态时，`while` 命令停止执行命令组。

## 基础 格式

`while` 命令的格式为：

```bash
while test command
do
  other commands
done
```

`while` 中定义的测试命令与 `if-then` 语句（第 9 章）中的格式完全相同。与 `if-then` 语句一样，可以使用任何 bash shell 命令，或者可以使用测试命令测试条件，例如变量值。

`while` 命令的关键在于指定的测试命令的退出状态必须根据循环期间运行的命令发生变化。如果退出状态从未改变，`while` 循环将陷入死循环。

最常见的情况使用测试命令括号来检查循环命令中 shell 变量的值：

```bash
$ cat test10
#!/bin/bash
# while command test

var=10
while [ $var -gt 0 ]
do
  echo $var
  var=$((var - 1))
done
$ ./test10
10
9
8
7
6
5
4
3
2
1
```

`while` 命令定义了每次迭代检查的测试条件：

```bash
while [ $var -gt 0 ]
```

只要测试条件为真，`while` 命令就会继续循环定义的命令。在命令中，测试条件使用的变量必须是

