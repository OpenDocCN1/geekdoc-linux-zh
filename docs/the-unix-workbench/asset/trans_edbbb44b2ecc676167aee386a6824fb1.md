

```bash
#!/usr/bin/env bash
# File: foreverloop.sh

count=3

while [[ $count -gt 0 ]]
do
echo "count is equal to $count"
let count=$count+1      # We only changed this line!
done

## ...
## count is equal to 29026
## count is equal to 29027
## count is equal to 29028
## count is equal to 29029
## count is equal to 29030
## ...
```

如果程序正在运行，那么 `count` 正在被非常快速地递增，你会在终端里看到数字飞速闪过！别担心，你可以使用 Control + C 来终止任何陷入无限循环的程序。使用 Control + C 来恢复提示符，以便我们继续。

在构造 WHILE 循环时，务必确保你已经将程序结构化为循环会终止！如果 `while` 之后的条件表达式永远不会变为 false，那么程序将永远运行下去，这很可能不是你为程序计划的行为。

## Nesting

就像 IF 语句一样，FOR 和 WHILE 循环也可以相互嵌套。在下面的示例中，一个 FOR 循环嵌套在另一个 FOR 循环内部。

```bash
#!/usr/bin/env bash
# File: nestedloops.sh

for number in {1..3}
do
    for letter in a b
    do
        echo "number is $number, letter is $letter"
    done
done
```

根据我们对 FOR 循环的了解，试着在运行程序之前预测这个程序会打印出什么。现在你已经写下或输入了你的预测，让我们运行它。

```bash
bash nestedloops.sh
```

```text
## number is 1, letter is a
## number is 1, letter is b
## number is 2, letter is a
## number is 2, letter is b
## number is 3, letter is a
## number is 3, letter is b
```

让我们仔细看看这里发生了什么。最外层的 FOR 循环开始遍历由 `{1..3}` 生成的序列。在循环的第一次遍历中，内层循环遍历序列 `a b`，首先打印 `number is 1, letter is a` 然后打印 `number is 1, letter is b`。外层循环的第一次迭代随后结束，整个过程以 `number` 的值为 `2` 重新开始。这个过程会一直通过内层循环，直到外层循环的序列耗尽。我再次强烈建议你暂停片刻并根据上面的代码编写一些自己的嵌套循环。在运行程序之前，试着预测你的嵌套循环程序会打印什么。如果打印结果与你的预测不符，请追踪程序的执行过程并尝试找出原因。不要只局限于嵌套 FOR 循环——使用嵌套 WHILE 循环，或 FOR 和 WHILE 循环的嵌套组合。

除了将循环嵌套在彼此内部之外，你还可以将循环嵌套在 IF 语句中，并在循环中嵌套 IF 语句。让我们看一个例子：

```bash
function [name of function] {
    # code here
}
```

很简单，对吧？让我们新建一个名为 `hello.sh` 的文件，以便我们可以编写我们的第一个简单函数。

```bash
#!/usr/bin/env bash
# File: hello.sh

function hello {
    echo "Hello"
}

hello
hello
hello
```

函数的整个结构——包括 `function` 关键字、函数名以及写在括号内的函数代码——构成了**函数定义**。函数定义将函数内的代码分配给函数名（本例中为 `hello`）。在函数定义之后，它可以像任何其他命令一样使用。使用我们的 `hello` 命令三次应该等同于使用 `echo "Hello"` 三次。让我们运行这个脚本来确认：

```bash
bash hello.sh
```

```text
## Hello
## Hello
## Hello
```

看起来这个函数的工作方式正如我们所期望的那样。

函数与单个 bash 脚本在很多行为上是相似的，包括它们如何处理参数。像 `$1`、`$2` 和 `$@` 这样的常规 bash 脚本参数在函数内部同样有效，这使你能够指定函数参数。让我们创建一个 `hello.sh` 的稍微修改版本，我们称之为 `ntmy.sh`：

```bash
#!/usr/bin/env bash
# File: ntmy.sh

function ntmy {
  echo "Nice to meet you $1"
}
```

在上面的文件中，注意我们在定义它之后并没有使用 `ntmy` 函数。那是因为我们将开始把我们定义的函数用作命令行程序。到目前为止，本章中我们一直使用 `bash [name of script]` 的语法来执行脚本的内容。现在我们将开始使用 `source` 命令，它允许我们将 bash 脚本中的函数定义用作命令行命令。让我们使用 `source` 运行这个文件，这样我们就可以使用 `ntmy` 命令了：

