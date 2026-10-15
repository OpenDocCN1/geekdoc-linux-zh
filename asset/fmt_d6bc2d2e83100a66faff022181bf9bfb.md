
```sh
#!/bin/sh
count=$1 # 初始化 count 为第一个参数
while [ $count -gt 0 ] # 当 count 大于 0 时执行
do
	echo $count seconds till supper time!
	count=$(expr $count -1) # count 减 1
	sleep 1 # 使用 Unix sleep 命令休眠一秒
done
echo Supper time!! , YEAH!!! # 完成了
```

如果从命令行调用该脚本并传入参数 4，该脚本将输出：

```text
4 seconds till supper time!
3 seconds till supper time!
2 seconds till supper time!
1 seconds till supper time!
Supper time!! , YEAH!!
```

你可以看到，这次我们使用了由 `[` 和 `]` 隐式调用的 `test` 命令的 `-gt` 选项，它代表“大于”。请仔细注意格式和空格。

## For

`for` 命令的语法如下：

```sh
for variable in word ...
do list
done
```

SH 手册指出：单词会被展开，然后列表会反复执行，`variable` 依次设置为 `word` 中的每个单词。

单词本质上是包含某种值列表的其他变量，`for` 结构将 `word` 中的每个值分配给 `variable`，然后 `variable` 可以在结构体内部使用，当结构体执行完毕后，`variable` 将被赋值为 `word` 中的下一个值，直到 `word` 中不再有值。

这个例子应该让这段代码更清晰：

```sh
#!/bin/sh
fruitlist="Apple Pear Tomato Peach Grape"
for fruit in $fruitlist
do
    if [ "$fruit" = "Tomato" ] || [ "$fruit" = "Peach" ]
    then
        echo "I like ${fruit}es"
    else
        echo "I like ${fruit}s"
    fi
done
```

在这个例子中，`fruitlist` 是一个单词列表，`fruit` 是一个变量，语句的主体部分输出这个人喜爱各种水果的程度。它包含一个 `if... then... else` 语句，用于处理在描述水果复数形式时正确添加字母的问题。

注意，变量 `fruit` 被表示为 `${fruit}`，因为否则 Shell 会将前面的字符解释为变量名的一部分，这可能会导致错误，因为诸如 `fruits` 和 `fruites` 这样的变量并未定义。

当执行时，该脚本将输出：

```
I like Apples
I like Pears
I like Tomatoes
I like Peaches
I like Grapes
```

在 `for` 结构中，`do` 和 `done` 可以用 `{` 和 `}` 替换。

## case 语句

`case` 结构具有以下语法：

```sh
case word in
    pattern) list ;;
    ...
esac
```

一个示例应该能让大家更清楚：

```sh
#!/bin/sh
case $1
in
    1) echo "First Choice";;
    2) echo "Second Choice";;
    *) echo "Other Choice";;
esac
```

“1”、“2”和“*”是模式。`word` 会与每个模式进行比较，如果找到匹配项，则执行对应模式的主体部分。我们使用 `*` 来代表其他所有内容。由于这是最后检查的，我们仍然会捕获“1”和“2”，因为它们首先被检查。在我们的例子中，`word` 是 `$1`，即第一个参数。因此，如果脚本以参数“1”运行，它将输出“First Choice”；“2”输出“Second Choice”，其他任何内容输出“Other Choice”。

在这个例子中，我们与数字进行了比较（本质上仍然是字符串比较），但模式可以更加复杂。有关更多信息，请参阅 `sh` 手册页。

## 函数

SH 函数的语法定义如下：

```
name ( ) command
```

通常格式如下：

```sh
name() {
    commands
}
```

函数返回时默认退出状态为零。可以使用 `return exit_status` 表示法返回不同的退出状态。可以使用 `local name=value` 在函数内定义局部变量。

### 自增函数示例

下面的示例展示了使用用户定义的 `increment` 函数：

```sh
#!/bin/sh
inc() {
    echo $(( $1 + $2 ))
}

# 我们检查是否所有命令行参数都存在
if [ "$1" = "" ] || [ "$2" = "" ] || [ "$3" = "" ]
then
    echo "USAGE:"
    echo "    counter startvalue incrementvalue endvalue"
else
    count=$1
    value=$2
    end=$3
    while [ $count -lt $end ]
    do
        echo $count
        count=$(inc $count $value)
    done
fi
```

函数使用 `inc() {` 定义并展开。行 `echo $(( $1 + $2 ))` 使用算术表达式替换表示法 `$(( expression ))` 来包裹表达式 `$1 + $2`，该表达式将传递给函数的第一个和第二个参数相加。开头的 `echo` 将它们回显到标准输出。

我们可以通过将函数调用赋值给变量来捕获此值，如函数调用所示：

```sh
count=$(inc $count $value)
```

我们使用命令替换，它替换命令的值，来替换函数调用的值，然后将其赋值给 `count` 变量。命令替换块中的命令是 `inc $count $value`，最后两个值是其参数。然后从函数内部使用 `$1` 和 `$2` 引用它们。

如果愿意，我们可以使用另一种命令替换表示法来调用函数：

```sh
count=`inc $count $value`
```

## 变量作用域示例

这里是另一个说明变量作用域的示例：

```sh
#!/bin/sh
inc() {
    local value=4
    echo "value is $value within the function\n"
    echo "\b$1 is $1 within the function"
}

value=5
echo "value is $value before the function"
echo "\$1 is $1 before the function"
echo
echo -e $(inc $value)
echo
echo "value is $value after the function"
echo "\$1 is $1 after the function"
```

我们为变量 `value` 分配了局部值 4。接下来的几行构建输出。请记住，这是回显到一个缓冲区，当函数退出时，它将替换为函数内传递给标准输出的所有内容。因此，调用代码将替换为我们在函数内定向到标准输出的任何内容。

函数的调用方式如下：

```sh
echo -e $(inc $value)
```

我们向 `echo` 命令传递了选项 `-e`，使其处理 C 风格的反斜杠转义字符，因此我们可以处理函数调用生成的字符串中包含的任何反斜杠转义字符。

如果我们只是回显我们希望函数返回的行，即使我们明确使用转义字符引用，它也不会将换行符传递到缓冲区。因此，我们实际做的是包含将生成换行的字符序列，以便当调用代码使用 `-e` 进行回显时，转义字符将被处理，换行符将放置在我们想要的位置。

```sh
echo "value is $value within the function\n"
```

注意换行符是如何通过 `\n` 插入的。两个反斜杠表示我们想要回显一个字面反斜杠，后跟 `n`。这是因为在双引号内，反斜杠表示按字面处理下一个字符。我们必须这样做，因为我们在双引号之间，而不是字面文本的单引号。如果使用了单引号，我们就必须将包含换行符的部分与包含 `$value` 的部分分开回显；否则，`$value` 将不会被展开。

```sh
echo "\b$1 is $1 within the function"
```

这是我们的第二行，包含在双引号中，以便变量 `$1` 将展开。包含 `\b`，以便在回显的行中放置 `\b`，我们的调用代码将此处理为退格字符。如果我们不这样做，Shell 会在第二行前加一个空格；退格符移除了这个空格。

该脚本以 2 作为第一个参数调用的输出是：
