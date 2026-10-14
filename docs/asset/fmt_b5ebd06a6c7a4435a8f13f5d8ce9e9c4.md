
在 SH 中，“列表”（`list`）被定义为“一组零或多个命令，由换行符、分号和和符号（`&`）分隔，并可选地由这三个字符之一终止”。因此，在 `if` 的通用定义中，列表将决定脚本采取哪种执行路径。例如，UNIX 上有一个名为 `test` 的命令，它会评估一个表达式，如果结果为真则返回 0，否则返回 1，这就是我们可以在 `if` 的列表部分测试条件的原因，因为 `test` 是一个命令。

我们实际上不需要直接将 `test` 命令输入到列表中来使用它；可以通过将测试用例封装在 `()` 和 `[ ]` 字符中来隐含表示，如下面的（愚蠢）示例所示：

```sh
#!/bin/sh
if [ "$1" = "1" ]
then
    echo "The first choice is nice"
elif [ "$1" = "2" ]
then
    echo "The second choice is just as nice"
elif [ "$1" = "3" ]
then
    echo "The third choice is excellent"
else
    echo "I see you were wise enough not to choose"
    echo "You win"
fi
```

这个示例的作用是将第一个参数（在本例中为命令行参数）与字符串“1”“2”和“3”进行比较，使用等号 `=` 进行相等测试，如果匹配其中任何一个，就会打印相应的消息。如果一个都不匹配，就会打印最后一种情况。好吧，这个示例很愚蠢而且实际上有缺陷（使用户输入 (4) 或其他内容时用户也会赢），但它说明了 `if` 语句是如何工作的。

注意在 `(if)` 与 `()` 之间、`[` 与测试内容之间、测试内容与 `]` 之间必须存在空格，这些空格必须存在，否则 shell 会报错。在测试的操作符和操作数之间也必须有空格，否则它将无法正常工作。注意它是以 `(if)` 开始并以 `(fi)` 结束的，此外，注意 `(then)` 与上面的测试单独成行，且 `(else)` 不需要 `(then)` 语句。你必须完全这样构造才能正常工作。

还可以通过分别使用 `&` 或 `||` 分隔的两个测试将逻辑与（AND）或或（OR）集成到测试中。例如，我们可以将示例中的第三个测试用例替换为：

如果第一个参数是“3”或“4”，脚本将打印“The third choice is excellent”。为了说明 `&&` 的用法，我们可以将第三个测试用例替换为：

当且仅当第一个参数为“3”且第二个参数为“4”时，脚本将打印“The third choice is excellent”。

`&&` 和 `||` 都是懒惰性求值的（lazily evaluating），这意味着在 `&&` 的情况下，如果第一个测试失败，它就不会去评估第二个测试，因为列表只有在两者都通过时才为真，既然其中一个已经失败了，就没有必要等待评估该情况。在 `||` 的情况下，如果第一个测试通过，它就不会去评估第二个测试，因为我们只需要其中一个测试通过，整个列表即为真。请查看测试页面获取可能的测试列表（除了此处提到的字符串相等测试）。

## Do...While

`Do...While` 采用以下通用形式：

```sh
while list
do list
done
```

用 SH 手册的话来说，“第一个列表的退出状态为零时，这两个列表会被重复执行。”这里有一个变体使用 `until` 代替 `while`，执行直到第一个列表的退出状态为零为止。这里是 `while` 语句的一个示例用法：

```sh
#!/bin/sh
count=$1 # 将计数初始化为第一个参数
while [ $count -gt 0 ] # 当 count 大于 0 时
do
  echo $count seconds till supper time!
  count=$(expr $count -1) # 计数减 1
  sleep 1 # 睡眠一秒
  # Unix sleep 命令
done
echo Supper time!!, YEAH!!    # 我们完成了
```

如果从命令行带参数 4 调用此脚本，它将输出：

```
4 seconds till supper time!
3 seconds till supper time!
2 seconds till supper time!
1 seconds till supper time!
Supper time!!, YEAH!!
```

你可以看到我们使用了 `[` 和 `]` 隐式调用的测试命令中的 `-gt`，它代表“大于”。请仔细注意格式和间距。

```sh
for variable in word ...
do list
done
```

SH 手册指出：“单词会被展开，然后变量依次设置为单词中的每个单词，并重复执行列表。”单词本质上是其他变量，其中包含某种类型的值列表。`for` 结构将 `word` 中的每个值赋值给变量，然后在构造体内部使用；在构造体完成后，变量将赋值为 `word` 中的下一个值，直到 `word` 中没有更多值为止。这个示例应该让这一点更清晰：

```sh
#!/bin/sh
fruitlist="Apple Pear Tomato Peach Grape"
for fruit in $fruitlist
do
    if [ "$fruit" = "Tomato" ] || [ "$fruit" = "Peach" ]
    then
        echo "I like $fruit"
    else
        echo "I do not like $fruit"
    fi
done
```

在这个示例中，`fruitlist` 是一个包含水果列表的变量。`for` 循环遍历列表中的每个水果，将其赋值给 `fruit` 变量。在循环内部，`if` 语句检查 `fruit` 是否为“Tomato”或“Peach”。如果是，打印“I like $fruit”；否则，打印“I do not like $fruit”。

## Functions

SH 函数的语法定义为：

```sh
name ( )
```

它通常布局如下：

```sh
name() {
    commands
}
```

函数将以默认退出状态零返回，可以通过 `return` 返回不同的状态。变量可以在函数内部局部定义 `name=value`。下面的示例展示了自定义递增的用法：

### 递增函数示例

```sh
#!/bin/sh
inc() { # 先定义递增以便使用
    echo $(($1 + $2)) # 我们打印第一个参数加第二个参数的结果
}
```

## 我们检查所有命令行参数是否存在

```sh
if [ "$1" = "" ] || [ "$2" = "" ] || [ "$3" = "" ]
then
    echo USAGE:
    echo counter startvalue incrementvalue
else
    count=$1	# 使用更清晰的名称重命名
    value=$2
    end=$3
    while [ $count -lt $end ]; do # 当 count 小于 end 时循环
    do
        echo $count
        count=$((inc $count $value)) # 使用 count 和 value 调用递增，使 count 增加 value
    done
fi
```

```sh
inc() {
    echo $(($1 + $2))
}
```

我们使用命令替换，用命令的值替换函数调用的值并将其赋值给 `count` 变量，如下函数调用所示：

```sh
count=$(inc $count $value)
```

如果我们愿意，也可以使用另一种命令替换符号来调用函数：

```sh
count='inc $count $value'
```

## 这里是另一个说明变量范围的示例：

### 变量范围，示例

```sh
#!/bin/sh
inc() {
  local value=4
  echo "value is $value within the function\n"
  echo "$1 is $1 within the function"
}
value=5
echo value is $value before the function
echo "$1 is $1 before the function"
echo
echo -e $(value)
echo
echo value is $value after the function
echo "$1 is $1 after the function"
```

```sh
inc() {
  local value=4
  echo "value is $value within the function\n"
```
