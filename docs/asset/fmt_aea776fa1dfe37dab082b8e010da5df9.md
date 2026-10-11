
首先，我们指定了一个计数器变量并将其设置为 1，然后在循环内部，我们使用这条语句 `((counter++))` 为计数器加 1。这样，我们就能确保循环将运行 10 次而不会无限运行。一旦计数器变为 10，循环就会完成，因为这是我们设置的条件：`while [[ $counter -le 10 ]]`。

让我们创建一个脚本，询问用户的姓名且不允许空输入：

```bash
#!/bin/bash

read -p "What is your name? " name

while [[ -z ${name} ]]

do

    echo "Your name can not be blank. Please enter a valid name!"

    read -p "Enter your name again? " name

done

echo "Hi there ${name}"
```

现在，如果你运行上面的代码并直接按回车而不输入，循环将再次运行并反复询问你的名字，直到你输入提供了输入。

### Until 循环

`until` 循环和 `while` 循环的区别在于，`until` 循环会执行循环内的命令，直到条件变为真。

结构：

```bash
until [[ your_condition ]]

do

    your_commands

done
```

示例：

```bash
#!/bin/bash

count=1

until [[ $count -gt 10 ]]

do

    echo $count

    ((count++))

done
```

### Continue 和 Break

与其他语言一样，你也可以在 bash 脚本中使用 `continue` 和 `break`：

- `continue` 告诉你的 bash 脚本停止当前的循环迭代并开始下一次迭代。

`continue` 语句的语法如下：

```bash
continue [n]
```

参数 `[n]` 是可选的，可以大于等于 1。当给出 `[n]` 时，将恢复第 n 个外层循环。`continue 1` 等同于 `continue`。

```bash
#!/bin/bash

for i in 1 2 3 4 5

do

    if [[ $i -eq 2 ]]

    then

        echo "skipping number 2"

        continue

    fi

    echo "i is equal to $i"

done
```

我们也可以以类似于 `break` 命令的方式使用 `continue` 命令来控制多个循环。

- `break` 告诉你的 bash 脚本立即结束循环。

`break` 语句的语法形式如下：

```bash
break [n]
```

`[n]` 是一个可选参数，必须大于等于 1。

注意：`break` 默认用于跳出循环。

```bash
#!/bin/bash

for i in 1 2 3 4 5

do

    if [[ $i -eq 2 ]]

    then

        echo "skipping number 2"

        continue

    fi

    echo "i is equal to $i"

done
```

我们也可以以类似于 `break` 命令的方式使用 `continue` 命令来控制多个循环。

`break` 告诉你的 bash 脚本立即结束循环。

`break` 语句的语法形式如下：

```bash
break [n]
```

`[n]` 是一个可选参数，必须大于等于 1。

注意：`break` 默认用于跳出循环。

示例：

```bash
#!/bin/bash

num=1

while [[ $num -le 5 ]]

do

  if [[ $num -eq 3 ]]

  then

    break

  fi

  echo $num

  ((num++))

done
```

`break 2` 会跳出嵌套的两层循环。

示例：

```bash
#!/bin/bash

for i in {1..3}

do

    for j in {1..3}

    do

        if [[ $i -eq 2 && $j -eq 2 ]]

        then

            break 2

        fi

        echo "i: $i, j: $j"

    done

done
```

### 函数

函数是复用代码的极佳方法。Bash 中函数的结构与大多数语言相似：

```bash
function function_name() {

  your_commands

}
```

你也可以省略开头的 `function` 关键字，这也是有效的：

```bash
function_name() {

  your_commands

}
```

我更喜欢放在那里以提高可读性。"Hello!" 函数示例：

```bash
#!/bin/bash

function hello() {

  echo "Hello!"

}

hello
```

> 注意：需要记住的是，调用函数时不需要加括号。

向函数传递参数与向脚本传递参数相同：

```bash
#!/bin/bash

function hello() {

    echo "Hello $1!"

}

hello Devojo
```

函数应该包含描述、全局变量、参数、输出和返回值（如果适用）：

```bash
###########################################
### Description: Hello 函数
### Globals:
### None
### Arguments: 单个输入参数
### Outputs: 输入参数的值
### Returns: 成功返回 0，错误返回非零
###########################################
function hello() {

    echo "Hello $1!"

}
```

在接下来的几章中我们将大量使用函数！

### 调试、测试快捷

为了调试你的 bash 脚本，可以在执行脚本时使用 `-x`：

```bash
bash -x ./your_script.sh
```

或者你可以在想要调试的特定行之前添加 `set -x`，`set -x` 会开启一种模式，将执行的所有命令打印到终端。

测试脚本的另一种方法是使用这个强大的工具：

https://www.shellcheck.net/

只需将代码粘贴到文本框中，工具就会提供一些改进脚本的建议。

你也可以直接在终端运行该工具：

https://github.com/koalaman/shellcheck

如果你喜欢这个工具，请确保在 GitHub 上 star 它并做出贡献！

作为一名系统管理员/DevOps 工程师，我每天的大部分时间都在终端度过。以下是我最喜欢的在编写 Bash 脚本或在终端工作时帮助更快完成任务的快捷键。

如果你有一个非常长的命令，以下两个特别有用：

- 删除从光标到行尾的所有内容：

```
Ctrl + k
```

- 删除从光标到行首的所有内容：

```
Ctrl + u
```

- 从光标向后删除单词：

```
Ctrl + w
```

- 反向搜索历史记录。这可能是我最常用的命令。它非常方便，极大地加快了我的工作流：

```
Ctrl + r
```

- 清除屏幕，我用它代替输入 `clear` 命令：

```
Ctrl + l
```

- 停止屏幕输出：

```
Ctrl + s
```

- 恢复屏幕输出（以之前被 Ctrl + s 停止的情况下）：

```
Ctrl + q
```

- 终止当前命令

```
Ctrl + c
```

- 将当前命令推至后台：

```
Ctrl + z
```
