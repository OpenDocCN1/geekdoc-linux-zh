
# Bash 脚本入门指南：开发者篇

![](img/7521519cf793a2e66883462104020ab5_0_0.png)

- 完整脚本：......................................................................... 133

## 关于本书

这是一份开源的 Bash 脚本入门指南，将帮助你学习 Bash 脚本的基础知识，并开始编写出色的 Bash 脚本，帮助你自动化日常 SysOps、DevOps 和开发任务。无论你是 DevOps/SysOps 工程师、开发者，还是仅仅 Linux 爱好者，都可以使用 Bash 脚本组合不同的 Linux 命令，并自动化枯燥重复的任务，从而让你专注于更具生产力且更有趣的事情。

本指南适用于任何作为开发者、系统管理员或 DevOps 工程师工作，并想要学习 Bash 脚本基础知识的人。

前 13 章将完全专注于打下坚实的 Bash 脚本基础，其余章节将为你提供一些真实生活中的示例和脚本。

## 关于作者

我叫 Bobby Iliev，自 2014 年以来我一直担任 Linux DevOps 工程师。我是一个热衷的 Linux 爱好者和开源运动哲学的支持者。我总是尝试做我不会做的事，以便我学习如何去做，并且我相信分享知识。

我认为始终保持专业性、让自己周围充满优秀的人、努力工作并对每个人都友好是非常关重要的。你必须保持比他人持续更高的水平。这是真正的专业人士的标志。

欲了解更多信息，请访问我的博客 https://bobbyiliev.com，并在 Twitter 上关注我 @bobbyiliev_ 并在 YouTube。

用于实时分析的流式数据库。

Materialize 是一个提供增量视图更新的响应式数据库。Materialize 帮助开发者使用标准 SQL 利用流数据轻松进行构建。

DigitalOcean 是一个云服务平台，提供开发者喜爱的简单性和企业信任的可靠性，用于大规模生产运行。

它提供高可用、安全且可扩展的计算、存储和网络解决方案，帮助开发者更快地构建软件。

DigitalOcean 成立于 2012 年，在纽约和马萨诸塞州剑桥设有办事处，提供透明实惠的价格、优雅的用户界面以及最大的开源资源库之一。

欲了解更多信息，请访问 https://www.digitalocean.com 或在 Twitter 上关注 @digitalocean。

如果你是 DigitalOcean 的新用户，可以通过此推荐链接获得 100 美元的免费额度并启动自己的服务器：

DigitalOcean 免费 $100 额度

## DevDojo

DevDojo 是一个学习所有 Web 开发和网页设计的资源库。在午休时间学习，或者醒来后和我们一起喝杯咖啡学习新知识。

加入这个开发者社区，我们可以共同学习、共同构建、共同成长。

加入 DevDojo

欲了解更多信息，请访问 https://www.devdojo.com 或在 Twitter 上关注 @thedevdojo。

Ibis 是一个 PHP 工具，帮助你用 markdown 编写电子书。

ePub 版本由 Pandoc 生成。

本电子书的封面使用 Canva.com 创建。

如果你需要创建图形、海报、邀请函、标志、演示文稿或其他任何看起来好看的内容——请尝试 Canva。

MIT 许可证

版权所有 (c) 2020 Bobby Iliev

现此授予许可

上述版权声明和本许可声明应包含在软件的所有副本或主要部分中。

软件按“原样”提供，不提供任何形式的明示或隐含保证，包括但不限于对适用性、特定用途适用性和非侵权的保证。在任何情况下，作者或版权所有者均对因合同、侵权或其他诉讼引起的由于软件或对软件的使用或其他交易而引起的任何索赔、损害或其他责任不负责。

## Bash 脚本简介

欢迎阅读本 Bash 基础培训指南！在这门 **bash 速成课程**中，你将学习 **Bash 基础**，以便开始编写自己的脚本并自动化日常任务。

Bash 是一种 Unix Shell 和命令语言。它在各种系统中广泛可用，也是大多数 Linux 系统的命令解释器。

Bash 代表 Bourne-Again Shell（再次 Bourne Shell）。与其他 Shell 一样，你可以直接在终端交互式地使用 Bash，也可以像使用任何编程语言一样使用 Bash 编写脚本。本书将帮助你学习 Bash 基础，包括 Bash 变量、用户输入、注释、参数、数组、条件表达式、条件语句、循环、函数、调试和测试。

Bash 对于自动化重复性负载非常出色，可以帮助你节省大量时间。例如，想象你正与五个开发者一起参与一个需要进行繁琐环境设置的项目。为了让程序正确运行，每位开发者都必须手动设置环境。这是一个相同且非常长的任务（设置环境），至少重复五次。这就是你和 Bash 脚本大显身手的地方！你可以创建一个包含所有必要指令的简单文本文件，并与团队成员共享。现在，他们只需要执行 Bash 脚本，一切就会为他们创建完成。

为了编写 Bash 脚本，你只需要一个 UNIX 终端和一个文本编辑器，如 Sublime Text、VS Code 或基于终端的编辑器 `vim` 或 `nano`。

## Bash 结构

让我们从创建一个 `.sh` 扩展的新文件开始。例如，我们可以创建一个名为 `devdojo.sh` 的文件。

要创建该文件，你可以使用 `touch` 命令：

```
touch devdojo.sh
```

或者你也可以使用你的文本编辑器：

```
nano devdojo.sh
```

为了使用 bash shell 解释器执行/运行 bash 脚本文件，脚本的第一行必须指定 bash 可执行文件的绝对路径：

```bash
#!/bin/bash
```

这也被称为 Shebang（解释器）。

shebang 所做的作用就是指示操作系统使用 `/bin/bash` 可执行文件运行脚本。

## Bash Hello World

一旦我们创建了 `devdojo.sh` 文件并在第一行指定了 shebang，我们就可以准备创建我们的第一个 Hello World 脚本了。

要做到这一点，再次打开 `devdojo.sh` 文件，在 `#!/bin/bash` 这一行之后添加以下内容：

```bash
#!/bin/bash

echo "Hello World!"
```

保存文件并退出。

之后，通过运行以下命令使脚本具有可执行权限：

```bash
chmod +x devdojo.sh
```

然后，执行该文件：

```bash
./devdojo.sh
```

你将在屏幕上看到 "Hello World" 消息。

运行脚本的另一种方式是：

```bash
bash devdojo.sh
```

由于 bash 可以以交互模式使用，你可以直接在终端中运行以下命令，获得相同的结果：

```bash
echo "Hello DevDojo!"
```

当你需要将多个命令组合时，编写脚本是非常有用的。

## Bash 变量

与任何其他编程语言一样，你可以在 Bash 中使用变量。

在 Bash 脚本中，变量可以包含数字以及字符。

要给变量赋值，你只需要使用 `=` 符号：

```bash
name="DevDojo"
```

> 注意：在 `=` 符号前后不能有空格。

之后，要访问变量，你必须使用 `$` 符号如下所示：

```bash
echo $name
```

将变量包裹在花括号中不是强制要求的，但是一个良好的做法，我建议你尽可能使用它们：

```bash
echo ${name}
```

上面的代码将输出：DevDojo，这是我们变量的值。

接下来，让我们更新 `devdojo.sh` 脚本并在其中包含变量。

再次，你可以使用你喜欢的文本编辑器打开 `devdojo.sh` 文件，这里我们使用 `nano` 打开：

```bash
nano devdojo.sh
```

在文件中添加我们的变量，带有欢迎消息。我们的文件现在看起来是这样：

```bash
#!/bin/bash
name="DevDojo"
echo "Hi there $name"
```

保存并使用命令运行文件：

```bash
./devdojo.sh
```

你将在屏幕上看到以下输出：

Hi there DevDojo

这是我们在文件中编写的脚本概述：

- `#!/bin/bash` - 首先，我们指定了 shebang。
- `name=DevDojo` - 然后，我们定义了一个变量并为其赋值了值。
- `echo "Hi there $name"` - 最后，我们在屏幕上输出变量的内容。

你也可以在文件中添加多个变量，如下所示：

```bash
#!/bin/bash
name="DevDojo"
greeting="Hello"
echo "$greeting $name"
```

保存并再次运行文件：

```bash
./devdojo.sh
```

你将在屏幕上看到以下输出：

Hello DevDojo

注意，你并不需要在每行末尾添加分号 `;`。这与 JavaScript 等编程语言不同。



你也可以在 Bash 脚本之外添加变量，它们作为参数传递：

```bash
./devdojo.sh
```

该脚本接收两个由空格分隔的参数。在 `devdojo.sh` 文件中我们有：

```bash
#!/bin/bash
echo "Hello there" $1
```

`$1` 是第一个输入， `$2` 是第二个输入。

使用 `$@` 来引用所有输入是另一种读取变量的有用方法。这表示`$@` 引用了所有输入。

所以现在更改 `devdojo.sh` 文件以更好地理解：

```bash
#!/bin/bash
echo "Hello there" $1
## $1 : 第一参数
echo "Hello there" $2
## $2 : 第二参数
echo "Hello there" $@
## $@ : 所有参数
```

输出为：

```bash
./devdojo.sh
```

将会是：

```
Hello there
```

### Bash 用户输入

在之前的脚本中，我们定义了一个变量并在屏幕上输出该变量的值。

现在让我们请求用户输入。再次再次使用你喜欢的文本编辑器打开文件并如下更新脚本：

```bash
#!/bin/bash
echo "What is your name?"
read name

echo "Hi there $name"
echo "Welcome to DevDojo!"
```

上述将提示用户输入，并将输入作为字符串/文本存储在变量中。

我们可以使用该变量向他们返回消息。

上述脚本的输出将是：

- 首先运行脚本：

```bash
./devdojo.sh
```

- 然后，会提示你输入名字：

```
What is your name?
Bobby
```

- 一旦输入了名字，只需回车，你将获得以下输出：

Hi there Bobby

Welcome to DevDojo!

为了简化代码，我们可以将第一个 `echo` 语句改为 `read -p`，带有 `-p` 标志的 `read` 命令会在提示用户输入之前打印消息：

```bash
#!/bin/bash
read -p "What is your name? " name
echo "Hi there $name"
echo "Welcome to DevDojo!"
```

### Bash 注释

和任何其他编程语言一样，你可以为你的脚本添加注释。注释用于在代码中留下自己的笔记。

在 Bash 中实现这一点，需要在行的开头添加 `#` 符号。注释永远不会显示在屏幕上。

这是一个注释示例：

```bash
### 这是一个注释，不会显示在屏幕上
```

让我们在脚本中添加一些注释：

```bash
#!/bin/bash
### 询问用户名字
read -p "What is your name? " name

### 问候用户
echo "Hi there $name"
echo "Welcome to DevDojo!"
```

注释是描述功能的好方法，以便其他人可以找到路径。

### 参数

在执行 shell 时可以对其传递参数。例如，让我们创建一个名为 `arguments` 的脚本：

```bash
#!/bin/bash
echo "Argument one is $1"
echo "Argument two is $2"
echo "Argument three is $3"
```

保存文件并使其具有可执行权限：

```bash
chmod +x arguments
```

然后运行文件并传递 3 个参数：

```bash
./arguments.sh dog cat bird
```

你得到的输出是：

```

Argument one is dog
Argument two is cat
Argument three is bird
```

要引用所有参数，可以使用 `$@`：

```bash
#!/bin/bash

echo "All arguments: $@"
```

如果你再次运行脚本：

```bash
./arguments.sh dog cat bird
```

All arguments: dog cat bird

```

你需要记住的另一点是，`$0` 用于引用脚本本身。

如果你需要，这是一个创建一个可以“自毁”文件（删除文件）的极佳方法，或者只是为了获取脚本名称。

例如，让我们创建一个打印文件名并在之后删除文件的脚本：

```bash

#!/bin/bash

echo "The name of the file is: $0 and it is going to be self-deleted."

rm $0

```

你需要对自删除小心，并确保在自删除之前备份了脚本。

### 数组

如果你做过任何编程，你可能已经熟悉数组了。

但以防你不是开发者，你需要知道的主要点是与变量不同，数组可以在一个名称下存储多个值。

你可以通过赋值由空格分隔并包含在 `()` 中的值来初始化数组。示例：

```bash

my_array=("value 1" "value 2" "value 3" "value 4")

```

要访问数组中的元素，你需要通过数字索引引用它们。

> 注意：记住使用花括号。

- 访问单个元素，这将输出：value 2

```bash

echo ${my_array[1]}

```

- 这将返回最后一个元素：value 4

```bash

echo ${my_array[-1]}

```

- 就像命令行参数一样，使用 `@` 将返回数组中的所有参数，如下：value 1 value 2 value 3 value 4

```bash

echo ${my_array[@]}

```





-   在数组前面加上一个哈号 (#) 将输出数组中元素的总数，在我们的用例中它是 4：

```bash

echo ${#my_array[@]}

```

确保在你的本地测试此并使用不同的值进行练习。

## Bash 中的子字符串 :: 切片

让我们复习下面这个关于在 Bash 中对字符串进行切片的示例：

```bash

#!/bin/bash

letters=( "A""B""C""D""E" )

echo ${letters[@]}

```

此命令将打印数组的所有元素：

输出：

```

$ ABCDE

```

让我们再看几个例子：

- 示例 1

```bash

#!/bin/bash

letters=( "A""B""C""D""E" )

b=${letters:0:2}

echo "${b}"

```

此命令将打印从起始索引 0 开始到 2 的数组内容（其中 2 不包含在内）。

```

$ AB

```

- 示例 2

```bash

#!/bin/bash

letters=( "A"B"C"D"E" )

b=${letters::5}

echo "${b}"

```

此命令将从基础索引 0 输出到 5，其中 5 不包含在内，且起始索引默认设置为 0。

### $ ABCDE

- 示例 3

```bash

#!/bin/bash

letters=( "A"B"C"D"E" )

b=${letters:3}

echo "${b}"

```

此命令将打印从起始索引 3 到数组末尾的内容（包含在内）。

### $ DE

## Bash 条件表达式

### 条件表达式

在计算机科学中，条件语句、条件表达式和条件结构是编程语言的特性，它们根据程序员指定的布尔条件评估为真或假来执行不同的计算或操作。

在 Bash 中，条件表达式用于复合命令和[内置命令]来测试文件属性并执行字符串和算术比较。

以下是最常用的 Bash 条件表达式列表。你不需要死记硬背它们。每当你需要时，只需查阅此列表即可！

### 文件表达式

- 如果文件存在则为真。

```bash

[[ -a ${file} ]]

```

- 如果文件存在且是块设备文件，则为真。

```bash

[[ -b ${file} ]]

```

- 如果文件存在且是字符设备文件，则为真。

```bash

[[ -c ${file} ]]

```

- 如果文件存在且是目录，则为真。

```bash

[[ -d ${file} ]]

```

- 如果文件存在则为真。

```bash

[[ -e ${file} ]]

```

- 如果文件存在且是普通文件，则为真。

```bash

[[ -f ${file} ]]

```

- 如果文件存在且是符号链接，则为真。

```bash

[[ -h ${file} ]]

```

- 如果文件存在且可读，则为真。

```bash

[[ -r ${file} ]]

```

- 如果文件存在且大小大于零，则为真。

```bash

[[ -s ${file} ]]

```

- 如果文件存在且可写，则为真。

```bash

[[ -w ${file} ]]

```

- 如果文件存在且可执行，则为真。
```bash



[[ -x ${file} ]]

- 如果文件存在且是符号链接，则为真。

```bash
[[ -L ${file} ]]
```

### 字符串表达式

- 如果 shell 变量 `varname` 已设置（已赋值值），则为真。

```bash
[[ -v ${varname} ]]
```

如果字符串长度为 0，则为真。

```bash
[[ -z ${string} ]]
```

如果字符串长度不为 0，则为真。

```bash
[[ -n ${string} ]]
```

- 如果字符串相等则为真。为了符合 POSIX 规定，应配合 `test` 命令使用 `=`。当与 `[[ ]]` 使用时：

```bash
# strings 相等
```

- 如果字符串不相等则为真。

```bash
# strings 不相等
```

- 如果字符串1 在字典序上小于字符串2，则为真。

```bash
### string1 在字典序上小于 string2
```

### 算术运算符

- 如果数字相等则为真。

```bash
### 两个相等
```

- 如果数字不相等则为真。

```bash
### 数字不相等
```

- 如果数字1小于数字2，则为真。

```bash
### 1 小于 2
```

- 如果数字1小于或等于数字2，则为真。

```bash
### 1 小于等于 2
```

- 如果数字1大于数字2，则为真。

```bash
### 1 大于 2
```

- 如果数字1大于或等于数字2，则为真。

```bash
### 1 大于等于 2
```

### 逻辑运算符

如果两个条件都为真，则为真。

```bash
### AND 逻辑
```

如果其中一个条件为真，则为真。

```bash
### OR 逻辑
```

### 退出状态

如果退出状态为 0，则为真。

```bash
### 退出状态为 0
```

如果退出状态不为 0，则为真。

```bash
### 退出状态不为 0
```

## Bash 条件语句

在上一节中，我们涵盖了常用的条件表达式。现在我们可以使用 `if`、`if-else` 和 `switch` 语句。

### if 语句

`if` 语句的格式如下：

```bash
if [[ 条件 ]]
then
    命令
fi
```

这里有一个简单的 `if` 语句示例，它要求你输入名称：

```bash
#!/bin/bash
### if 语句示例
read -p "你的名字是？" name
if [[ -z ${name} ]]
then
    echo "请输入名字！"
fi
```

### if-else 语句

使用 `if-else` 语句，可以在条件不匹配时指定操作。示例如下：

```bash
#!/bin/bash
### if-else 语句示例
read -p "你的名字是？" name
if [[ -z ${name} ]]
then
    echo "请输入名字！"
else
    echo "你好，${name}"
fi
```

你可以结合上一节的条件表达式使用上面的语句：

```bash
#!/bin/bash
admin="root"
read -p "用户名：" username
### 检查用户名是否为管理员
if [[ "${username}" == "${admin}" ]]; then
    echo "你是管理员！"
else
    echo "你不是管理员"
fi
```

这里是另一个 `if` 语句示例，它会检查你的当前用户 ID：

```bash
#!/bin/bash
if [[ $EUID -eq 0 ]]; then
    echo "你是 root 用户"
else
    echo "你不是 root 用户"
fi
```

### case 语句

与其他编程语言一样，当有多个选择时，可以使用 `case` 语句来简化复杂的条件。因此，与其使用多个 `if`、`if-else` 语句，不如使用单个 `case` 语句。

Bash `case` 语句的语法如下：

```bash
case $some_variable in
  pattern_1)
    命令
    ;;
  pattern_2| pattern_3)
    命令
    ;;
  *)
    默认命令
    ;;
esac
```

该结构的简要说明：

- 所有 `case` 语句都以 `case` 关键字开始。
- 在 `case` 关键字的同一行，你需要指定一个变量或表达式，后面跟着 `in` 关键字。
- 之后，你使用用模式，需要使用 `)` 来标识模式的结束。
- 你可以指定多个由竖线 `|` 分隔的模式。
- 在模式之后，你指定你希望在当该模式匹配你所指定的变量或表达式时执行的命令。
- 所有子句必须通过添加 `;;` 来终止。
- 你可以通过添加 `*` 作为模式来设置默认语句。
- 为了关闭 `case` 语句，使用 `esac` 关键字（case 倒过来写）。

```bash
#!/bin/bash
read -p "Enter the name of your car brand: " car
case $car in
Tesla)
  echo -n "${car}'s car factory is in the USA."
  ;;
BMW | Mercedes | Audi | Porsche)
  echo -n "${car}'s car factory is in Germany."
  ;;
Toyota | Mazda | Mitsubishi | Subaru)
  echo -n "${car}'s car factory is in Japan."
  ;;
*)
  echo -n "${car} is an unknown car brand"
  ;;
esac
```

通过这个脚本，我们要求用户输入汽车品牌名称，例如 Tesla、BMW、Mercedes 等。

然后，我们使用 `case` 语句检查品牌名称，如果它匹配我们定义的模式中的任何一个，如果是的话，我们就打印出工厂的位置。

如果品牌名称没有匹配任何 `case` 语句，我们将打印一条默认消息：未知的汽车品牌。

### 结论

我建议你尝试修改这个脚本并玩一玩它，这样你就可以练习在最后两章中学到的内容了！

关于更多 Bash `case` 语句的示例，请务必查看第 16 章，在那里我们将使用 `case` 语句在 Bash 中创建一个交互式菜单来处理用户输入。

## Bash 循环

与任何其他语言一样，循环非常方便。在 Bash 中，你可以使用 `for` 循环、`while` 循环和 `until` 循环。

### For 循环

这是 `for` 循环的结构：

```bash
for var in ${list}
do
  your_commands
done
```

示例：

```bash
#!/bin/bash
users="devdojo bobby tony"
for user in ${users}
do
  echo "${user}"
done
```

对示例的快速复习：

- 首先，我们指定了一个用户列表并将值存储在名为 `$users` 的变量中。
- 之后，我们使用 `for` 关键字开始 `for` 循环。
- 然后我们定义了一个新变量，它代表我们提供的列表中的每个项目。在我们的例子中，我们定义了一个名为 `user` 的变量，它代表 `$users` 变量中的每个用户。
- 接着我们指定 `in` 关键字，后面跟上我们要遍历的列表。
- 在下一行，我们使用 `do` 关键字，它表示我们在循环的每次迭代中要做什么。
- 然后我们指定我们想要运行的命令。
- 最后，我们用 `done` 关键字结束循环。

你也可以用 `for` 来处理一组数字。例如，这里是循环 1 到 10 的一种方法：

```bash
#!/bin/bash
for num in {1..10}
do
  echo ${num}
done
```

### While 循环

`while` 循环的结构与 `for` 循环非常相似：

```bash
while [ your_condition ]
do
  your_commands
done
```

这是一个 `while` 循环的示例：

```bash
#!/bin/bash
counter=1
while [[ $counter -le 10 ]]
do
  echo $counter
  ((counter++))
done
```



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



我每天都会经常使用这些命令，节省了我大量时间。

如果你认为我漏掉了任何内容，欢迎在 DigitalOcean 社区论坛加入讨论！

## 创建自定义 bash 命令

作为开发者或系统管理员，你可能需要在终端中花费大量时间。我总是尝试寻找优化重复性任务的方法。

实现这一点的方法是编写短的 bash 脚本或创建自定义命令（也称为别名，`aliases`）。例如，与其每次都输入一个非常长的命令，你只需为它创建一个快捷方式即可。

### 示例

让我们从以下场景开始：作为系统管理员，你可能经常需要检查 Web 服务器的连接情况，因此我将使用 `netstat` 命令作为示例。

当我访问一个 80 或 443 端口连接出现问题的服务器时，我通常会检查是否有服务在监听这些端口，以及到这些端口的数量。

以下 `netstat` 命令将显示我们目前在 80 和 443 端口上有多少 TCP 连接：

```
netstat -plant | grep '80\|443' | grep -v LISTEN | wc -l
```

这是一个相当长的命令，从长远来看，每次都输入可能会耗时，特别是当你想要快速获取这些信息时。

为了避免这种情况，我们可以创建一个别名，这样与其输入整个命令，我们只需要输入一个短命令。例如，假设我们想要能够输入 `conn`（connections 的缩写）并获取相同的信息。在这种情况下，我们只需要运行以下命令：

```
alias conn="netstat -plant | grep '80\|443' | grep -v LISTEN | wc -l"
```

这样，我们就创建了一个名为 `conn` 的别名，它本质上是我们长 `netstat` 命令的“快捷方式”。现在，如果你直接运行 `conn`：

```
conn
```

你将得到与长 `netstat` 命令相同的输出。你甚至可以更有创意，添加像这样的信息消息：

```
alias conn="echo 'Total connections on port 80 and 443:' ;
netstat -plant | grep '80\|443' | grep -v LISTEN | wc -l"
```

现在如果你运行 `conn`，你将得到以下输出：

```
Total connections on port 80 and 443:
12
```

现在，如果你注销并重新登录，你的别名将会丢失。在下一步中，你将看到如何让它持久化。

### 使更改持久化

为了让更改持久化，我们需要在 shell 配置文件中添加 `alias` 命令。

在 Ubuntu 上，默认是 `~/.bashrc` 文件，对于其他操作系统，这可能是 `~/.bash_profile`。用你喜欢的文本编辑器打开该文件：

```
nano ~/.bashrc
```

移动到底部并添加以下内容：

```
alias conn="echo 'Total connections on port 80 and 443:'; netstat -plant | grep '80\|443' | grep -v LISTEN | wc -l"
```

保存并退出。

这样，现在即使你注销并重新登录，你的更改也将保留，并且你能够运行你的自定义 bash 命令。

### 列出所有可用别名

要列出当前 shell 的所有可用别名，你只需要运行以下命令：

```
alias
```

当你在发现某些命令出现异常行为时，这会非常有用。

### 结论

这是创建自定义 bash 命令或 bash 别名的一种方法。

当然，你实际上可以编写一个 bash 脚本并将其添加到 `/usr/bin` 文件夹中，但如果你没有 root 或 sudo 权限，这种方法将无法运行；而使用别名，你可以在不需要 root 权限的情况下完成。

> **注意**：此内容最初发布在 DevDojo.com。

## 编写你的第一个 Bash 脚本

让我们尝试结合我们为止学到的内容，创建我们的第一个 Bash 脚本吧！

### 规划脚本

作为一个示例，我们将编写一个脚本，收集有关我们服务器的一些有用信息，例如：

- 当前磁盘使用情况
- 当前 CPU 使用率
- 当前内存使用率
- 检查精确的内核版本

你可以通过添加或删除功能来调整脚本，以符合你的需求。

### 编写脚本

你首先需要的是创建一个带有 `.sh` 扩展的新文件。我将创建一个名为 `status.sh` 的文件，因为我们要创建的脚本将提供服务器的状态。

一旦创建了文件，请用你喜欢的文本编辑器打开它。

正如我们在第 1 章中学到的，在 Bash 脚本的第一行，我们需要指定所谓的 Shebang：

```
#!/bin/bash
```

`shebang` 的唯一作用就是指示操作系统使用 `/bin/bash` 可执行文件来运行该脚本。

### 添加注释

接下来，正如第 6 章中讨论的，让我们从添加一些注释开始，以便人们能轻松看出脚本的用途。在 Shebang 之后，你只需添加以下内容：

```bash
#!/bin/bash

### 返回当前服务器状态的脚本
```

### 添加你的第一个变量

让我们应用第 4 章中学到的知识，添加一些我们可能在整个脚本中使用的变量。

在 bash 中为变量赋值，你只需要使用 `=` 符号。例如，我们将主机名存储在变量中：

```
server_name=$(hostname)
```

通过使用 `$()`，我们告诉 bash 实际解释命令然后回显变量：

```
echo $server_name
```

### 添加你的第一个函数

正如你在阅读第 1 章后所知，为了创建一个函数，你需要使用以下结构：

```
function function_name() {
  your_commands
}
```

快速运行该函数：

```bash
function memory_check() {
    echo ""
    echo "The memory usage on ${server_name} is: "
    free -h
    echo ""
}
```

一旦定义了函数，要调用它，只需使用函数名：

```bash
memory_check
```

### 更多函数挑战

在查看解决方案之前，我挑战你使用上面的函数自己编写几个函数。

这些函数应该实现以下功能：

- 当前磁盘使用情况
- 当前 CPU 使用率
- 当前内存使用率
- 检查精确的内核版本

如果你不确定需要哪些命令来获取这些信息，请尽管使用谷歌。

一旦你准备好了，请向下滚动查看我们是如何做的并对比结果！

请注意，实现它有多种方法！

### 示例脚本

这是最终结果的样子：

```bash
#!/bin/bash

##
# 检查内容的 BASH 脚本
### 内存使用情况
### CPU 负载
### TCP 连接数
### 内核版本
##

server_name=$(hostname)

function memory_check() {
    echo ""
    echo "Memory usage on ${server_name} is: "
    free -h
    echo ""
}

function cpu_check() {
    echo ""
    echo "CPU load on ${server_name} is: "
    echo ""
    uptime
    echo ""
}

function tcp_check() {
    echo ""
    echo "TCP connections on ${server_name}: "
    echo ""
    cat /proc/net/tcp | wc -l
    echo ""
}

function kernel_check() {
    echo ""
    echo "Kernel version on ${server_name} is: "
    uname -a
    echo ""
}

### 调用函数
memory_check
cpu_check
tcp_check
kernel_check
```

```bash
uname -r
echo ""
}

function all_checks() {
    memory_check
    cpu_check
    tcp_check
    kernel_check
}

all_checks
```



### 结论

Bash 脚本太棒了！无论你是 DevOps/SysOps 工程师、开发者，还是仅仅是一个 Linux 爱好者，你都可以使用 Bash 脚本组合不同的 Linux 命令并自动化无聊且重复的日常任务，从而让你专注于更有生产力且更有趣的事情！

> **注意：** 本文最初发布于 DevDojo.com

## 在 Bash 中创建交互式菜单

在本教程中，我将向你展示如何在 Bash 中创建一个多选项菜单，以便你的用户可以选择要执行什么操作！

我们将复用上一章节中的部分代码，所以如果你还没有读过，请确保已阅读。

### 功能规划

让我们重新开始，回顾脚本的主要功能：

- 检查当前的磁盘使用情况
- 检查当前的 CPU 使用率
- 检查当前的内存使用情况
- 检查确切的内核版本版本

如果你手头没有脚本，这里是脚本本身：

```bash
#!/bin/bash

##
# BASH菜单脚本用于检查：
### 内存使用
### CPU 负载
### TCP 连接数
### 内核版本
##

server_name=$(hostname)

function memory_check() {
  echo ""
  echo "Memory usage on ${server_name} is:"
  free -h
  echo ""
}

function cpu_check() {
  echo ""
  echo "CPU load on ${server_name} is:"
  echo ""
  uptime
  echo ""
}

function tcp_check() {
  echo ""
  echo "TCP connections on ${server_name}:"
  echo ""
  cat /proc/net/tcp | wc -l
  echo ""
}

function kernel_check() {
    echo "Kernel version on ${server_name} is: "
    echo ""
    echo ""
    uname -r
    echo ""
}

function all_checks() {
    memory_check
    cpu_check
    tcp_check
    kernel_check
}
```

然后我们将构建一个菜单，允许用户选择要执行哪个函数。

当然，你可以根据需要调整函数或添加新函数。

### 添加一些颜色

为了让菜单更加“易读”并且一目了然，我们将添加一些颜色函数。

在脚本的开头添加以下颜色函数：

```bash
### 颜色变量
##
green='\e[32m'
blue='\e[34m'
clear='\e[0m'
### 颜色函数
##
ColorGreen(){
  echo -ne $green$1$clear
}
ColorBlue(){
  echo -ne $blue$1$clear
}
```

你可以如下所示使用颜色函数：

```bash
echo -ne $(ColorBlue 'Some text here')
```

上述代码将输出 `Some text here` 字符串并且将是蓝色的！

### 添加菜单

最后，为了添加菜单，我们将创建一个单独函数，并使用 `case` 语句来处理菜单选项：

```bash
menu() {
  echo -ne "
My First Menu
  ($(ColorGreen '1')) Memory usage
  ($(ColorGreen '2')) CPU load
  ($(ColorGreen '3')) Number of TCP connections
  ($(ColorGreen '4')) Kernel version
  ($(ColorGreen '5')) Check All
  ($(ColorGreen '0')) Exit
  ($(ColorBlue 'Choose an option:')) "
  read a
  case $a in
    1) memory_check; menu;
    2) cpu_check; menu;
    3) tcp_check; menu;
    4) kernel_check; menu;
    5) all_checks; menu;
    0) exit 0;
    *) echo -e "$redWrong option.\$clear"
WrongCommand;
  esac
}
```

### 代码快速概览

首先，我们带上一些颜色输出菜单选项：

```bash
echo -ne "
My First Menu
$(ColorGreen '1') Memory usage
$(ColorGreen '2') CPU load
$(ColorGreen '3') Number of TCP connections
$(ColorGreen '4') Kernel version
$(ColorGreen '5') Check All
$(ColorGreen '0') Exit
$(ColorBlue 'Choose an option:') "
```

然后，我们读取用户的回答并将其存储在变量 `$a` 中：

```bash
read a
```

最后，我们有一个 `switch case` 语句，根据 `$a` 的值触发不同的函数：

```bash
case $a in
  1) memory_check ; menu ;;
  2) cpu_check ; menu ;;
  3) tcp_check ; menu ;;
  4) kernel_check ; menu ;;
  5) all_checks ; menu ;;
  0) exit 0 ;
  *) echo -e $red"Wrong option.\\$clear;"
esac
WrongCommand;
```

在最后，我们需要调用 `menu` 函数来实际打印菜单：

```bash
### 调用菜单函数
menu
```

### 测试脚本

最后，你的脚本看起来像这样：

```bash
#!/bin/bash
##
# BASH菜单脚本用于检查：
### - 内存使用
### - CPU 负载
### - TCP 连接数
### - 内核版本
##
server_name=$(hostname)
function memory_check() {
    echo "Memory usage on ${server_name} is:"
    free -h
    echo ""
}
function cpu_check() {
    echo ""
    echo "CPU load on ${server_name} is:"
    echo ""
    uptime
    echo ""
}
function tcp_check() {
    echo ""
    echo "TCP connections on ${server_name} is:"
    echo ""
    cat /proc/net/tcp | wc -l
    echo ""
}
function kernel_check() {
    echo ""
    echo "Kernel version on ${server_name} is:"
    echo ""
}
uname -r
echo ""
}
function all_checks() {
    memory_check
    cpu_check
    tcp_check
    kernel_check
}
```

##
### 颜色变量
##
`green`='\e[32m'
`blue`='\e[34m'
`clear`='\e[0m'

##
### 颜色函数
##

```bash
ColorGreen(){
    echo -ne $green$1$clear
}
ColorBlue(){
    echo -ne $blue$1$clear
}
```

```bash
menu() {
  echo -ne "
My First Menu
$(ColorGreen '1') Memory usage
$(ColorGreen '2') CPU load
$(ColorGreen '3') Number of TCP connections
$(ColorGreen '4') Kernel version
$(ColorGreen '5') Check All
$(ColorGreen '0') Exit
$(ColorBlue 'Choose an option:') "
  read a
  case $a in
```



```
    1) memory_check; menu;

    2) cpu_check; menu;

    3) tcp_check; menu;

    4) kernel_check; menu;

    5) all_checks; menu;

    0) exit 0;

    *) echo -e "$redWrong option.\$clear"

WrongCommand;

  esac

}
```

### 调用菜单函数

`menu`

```
要测试脚本，创建一个以 `.sh` 扩展的新文件，例如 `menu.sh`，然后运行它：

```bash
bash menu.sh
```

你将获得的输出看起来如下：

My First Menu
1) Memory usage
2) CPU load
3) Number of TCP connections
4) Kernel version
5) Check All
0) Exit
Choose an option:

# BASH 脚本

我将重用上一章节的演示脚本并进行一些微调。它简单地执行一些检查，例如当前内存使用情况、当前 CPU 使用率、TCP 连接数以及内核版本。

```bash
#!/bin/bash

##
# 检查以下内容的 BASH 脚本：
### 内存使用
### CPU 负载
### TCP 连接数
### 内核版本
##
##
### 内存检查
##
server_name=$(hostname)

function memory_check() {
    echo "######"
    echo "${server_name} 当前内存使用情况为: "
    free -h
    echo "######"
}

function cpu_check() {
    echo "######"
    echo "${server_name} 当前的 CPU 负载为: "
    echo ""
    uptime
    echo "######"
}

function tcp_check() {
    echo "######"
    echo "${server_name} 上的 TCP 连接总量: "
    echo ""
    cat /proc/net/tcp | wc -l
    echo "######"
}
```

```bash
function kernel_check() {
    echo "######"
    echo "${server_name} 的精确内核版本为: "
    echo ""
    uname -r
    echo "######"
}

function all_checks() {
    memory_check
    cpu_check
    tcp_check
    kernel_check
}

all_checks
```

复制下面的代码并将其添加到名为 `remote_check.sh` 的文件中。你也可以从此地获取脚本。

### 在所有服务器上运行脚本

现在我们已经准备好了脚本和服务器，并且将这些服务器添加到了 `servers.txt` 文件中，我们可以运行以下命令来遍历所有服务器并远程执行脚本，而无需将脚本复制到每个服务器并单独连接到每个服务器。

```bash
for server in $(cat servers.txt); do ssh your_user@${server} 'bash -s' < ./remote_check.sh ; done
```

这个 `for` 循环的作用是遍历 `servers.txt` 文件中的每个服务器，然后对列表中的每个项目运行以下命令：

```bash
ssh your_user@the_server_ip 'bash -s' < ./remote_check.sh
```

你将得到如下输出：

![](img/7521519cf793a2e66883462104020ab5_92_0.png)

### 结论

这是一个非常简单的示例，演示了如何在多个服务器上执行简单脚本，而无需将其复制到每个服务器，也无需单独访问每个服务器。

当然，你可以在更多服务器上运行更复杂的脚本。

如果你对自动化感兴趣，我建议你查看 DigitalOcean 网站上的 Ansible 资源页面：

Ansible 资源页面

> 注意：此内容最初发布在 DevDojo

# 在 BASH 中使用 jq 处理 JSON

`jq` 命令行工具是一个轻量且灵活的命令行 JSON 解析器。它非常适合解析 BASH 中的 JSON 输出。

`jq` 的优点之一是用用于可移植的 C 语言编写的，并且零运行时依赖。你只需要下载单个二进制文件或使用像 `apt` 这样的包管理器并通过单个命令进行安装。

### 规划脚本

在本教程的演示中我将使用一个返回简单 JSON 输出的外部 REST API，称为 QuizAPI：

https://quizapi.io/

如果你想跟随操作，请确保在此处获取免费的 API 密钥：

https://quizapi.io/clientarea/settings/token

QuizAPI 对开发者是的。

### 安装 jq

有许多方法可以在你的系统上安装 `jq`。最直接的方法之一是根据你的操作系统使用包管理器。

以下是根据你的操作系统需要使用的命令列表：

- 在 Ubuntu/Debian 上安装 `jq`
```bash
sudo apt-get install jq
```

- 在 Fedora 上安装 `jq`
```bash
sudo dnf install jq
```

- 在 openSUSE 上安装 `jq`
```bash
sudo zypper install jq
```

- 在 Arch 上安装 `jq`
```bash
sudo pacman -S jq
```

- 使用 Homebrew 在 Mac 上安装
```bash
brew install jq
```

- 使用 MacPort 在 Mac 上安装
```bash
port install jq
```

如果你使用的是其他操作系统，我建议查看此处的官方文档以获取更多信息：

https://stedolan.github.io/jq/download/

一旦你下载并安装了 `jq`，你可以通过运行此命令来检查当前版本：

```bash
jq --version
```

### 使用 jq 解析 JSON

一旦你安装了 `jq` 并有了 QuizAPI API 密钥，就可以直接在终端中解析 QuizAPI 的 JSON 输出。

首先，创建一个存储 API 密钥的变量：

```bash
API_KEY=YOUR_API_KEY_HERE
```

为了从 QuizAPI 的一个端点获取输出，你可以使用 `curl` 命令：

```bash
curl "https://quizapi.io/api/v1/questions?apiKey=${API_KEY}&limit=1"
```

为了获得更特定的输出，你可以使用这里的 QuizAPI URL 生成器：

https://quizapi.io/api-config

运行 `curl` 命令后，你得到的输出如下：

![](img/7521519cf793a2e66883462104020ab5_98_0.png)

这可能非常难阅读，但感谢 `jq` 命令行工具，我们只需要将 `curl` 命令通过管道传给 `jq`，就能看到格式化良好的 JSON 输出：

```bash
curl "https://quizapi.io/api/v1/questions?apiKey=${API_KEY}&limit=1" | jq
```

注意结尾的 `| jq`。

在这种情况下，你得到的输出看起来像这样：

![](img/7521519cf793a2e66883462104020ab5_98_1.png)

现在这看起来漂亮多了！`jq` 命令行工具为我们格式化了输出并添加了一些好看的颜色！

### 使用 jq 获取第一个元素

假设我们只想从 JSON 输出中获取第一个元素，为了这一点，我们只需要通过以下语法指定我们想要看到的索引：

```bash
jq .[0]
```

现在，如果我们再次运行 `curl` 命令并将输出传给 `jq .[0]`，如下所示：

```bash
curl "https://quizapi.io/api/v1/questions?apiKey=${API_KEY}&limit=1" | jq .[0]
```



你将只获得第一个元素，输出如下：

![](img/7521519cf793a2e66883462104020ab5_100_0.png)

### 只获取特定键的值

有时你可能只想获取某个特定键的值，例如在我们的示例中，QuizAPI 返回了一个问题列表，并带有答案、描述等，但如果你只想获取不带额外信息的题目怎么办？

使用 `jq` 这将非常简单，你只需要在 `jq` 命令后添加键，所以它看起来像这样：

```bash
jq .[].question
```

我们必须添加 `.[]`，因为 QuizAPI 返回的是数组，通过指定 `.[]`，我们告诉 `jq` 我们想要获取数组中所有元素的 `.question` 值。

你得到的输出如下：

![](img/7521519cf793a2e66883462104020ab5_101_0.png)

你可以看到我们现在只获取问题而不其他值。

# 在 BASH 脚本中使用 jq

让我们创建一个小型 bash 脚本，它应该为我们输出以下信息：

- 从输出中获取第一个问题
- 获取该问题的所有答案
- 将答案赋值给变量
- 打印问题和答案
- 为了实现这一点，我编写了以下脚本：

> 注意：请确保将 `API_KEY` 部分替换为你实际的 QuizAPI 密钥：

```bash
#!/bin/bash

##
# 调用 QuizAPI 的 API并将输出存储在变量中
##

output=$(curl 'https://quizapi.io/api/v1/questions?apiKey=API_KEY&limit=10' >/dev/null)

##
### 获取第一个问题
##

output=$(echo $output | jq.[0])

##
### 获取问题
##

question=$(echo $output | jq .question)

##
### 获取答案
##

answer_a=$(echo $output | jq .answers.a)

answer_b=$(echo $output | jq .answers.b)

answer_c=$(echo $output | jq .answers.c)

answer_d=$(echo $output | jq .answers.d)

##
### 输出问题
##

echo "
Question: ${question}

A) ${answer_a}

B) ${answer_b}

C) ${answer_c}

D) ${answer_d}
"
```

如果你运行该脚本，将得到如下输出：

我们甚至可以进一步使其具有交互性，这样我们就可以直接在终端中选择答案。

已经有一个使用 QuizAPI 和 `jq` 实现此点的 bash 脚本：

你可以在这里查看该脚本：

- https://github.com/QuizApi/QuizAPI-BASH/blob/master/quiz.sh

### 结论

`jq` 命令行工具是一个非常强大的工具，它让你能够直接在 BASH 终端中处理 JSON 数据。

通过这种方式，你可以轻松使用 BASH 与各种不同的 REST API 交互。

欲了解更多信息，你可以查看此处的官方文档：

- https://stedolan.github.io/jq/manual/

关于 QuizAPI 的更多信息，你可以查看此处的官方文档：

- https://quizapi.io/docs/1.0/overview

> 注意：此内容最初发布在 DevDojo.com

## 使用 Bash 配合 Cloudflare API

我将我所有的网站都托管在 DigitalOcean Droplets 上，并使用 Cloudflare 作为我的 CDN 供应商。使用 Cloudflare 的用处之一是它可以减少到用户的整体流量，并通过他们的 CDN 隐藏你真实的服务器 IP 地址。

我个人最喜欢的 Cloudflare 功能是他们的免费 DDoS 防护。它多次保护我的服务器免受各种 DDoS 攻击。他们有一个非常酷的 API，你可以用它轻松地启用和禁用 DDoS 防护。

本章将是一个练习！我挑战你编写一个短的 bash 脚本，根据需要自动为你的服务器启用和禁用 Cloudflare DDoS 防护！

### 前提条件

在遵循此指南之前，请设置你的 Cloudflare 账户并准备好你的网站。如果你不确定如何操作，可以遵循这些步骤：创建 Cloudflare 账户并添加网站。

一旦你拥有了 Cloudflare 账户，请确保获取以下信息：

- Cloudflare 账户
- Cloudflare API key
- Cloudflare Zone ID

此外，确保你的服务器上安装了 `curl`：

```bash
curl --version
```

如果未安装 `curl`，你需要运行以下命令：

- 对于 RedHat/CentOS：

```bash
yum install curl
```

- 对于 Debian/Ubuntu

```bash
apt-get install curl
```

### 挑战 - 脚本需求

脚本需要监控你服务器的 CPU 使用情况，如果 CPU 使用率根据 vCPU 数量过高，它将通过 Cloudflare API 自动启用 Cloudflare DDoS 防护。

脚本的主要功能应该是：

- 检查服务器上的脚本 CPU 负载
- 在 CPU 激增时，脚本触发对 Cloudflare 的 API 调用并为指定区域启用 DDoS 防护功能
- 在 CPU 负载恢复正常后，脚本将禁用“正受攻击（I'm under attack）”选项并将其恢复正常

### 示例脚本

我已经准备了一个演示脚本可供你参考。但我鼓励你先尝试自己编写脚本，然后再看我的脚本！

下载脚本只需运行以下命令：

```bash
wget https://raw.githubusercontent.com/bobbyiliev/cloudflare-ddos/main/protection.sh
```

使用你喜欢的编辑器打开脚本：

```bash
nano protection.sh
```

并更新以下细节：

```bash
CF_ZONE_ID="YOUR_ZONE_ID"
CF_EMAIL="YOUR_EMAIL"
CF_API_KEY="YOUR_API_KEY"
```

之后，让脚本具有可执行权限：

```bash
chmod +x protection.sh
```

最后，设置 Cron 每隔 30 分钟运行一次：

```bash
crontab -e
```

并添加以下内容：

```cron
*/30 * * * * /path/to/protection.sh
```

注意：将路径更改为你存储脚本的实际路径。

## 使用 Bash 配合 Cloudflare API

### 前提条件
在遵循此指南之前，请设置你的 Cloudflare 账户并准备好你的网站。如果你不确定如何操作，可以遵循这些步骤：创建 Cloudflare 账户并添加网站。

一旦你拥有了 Cloudflare 账户，请确保获取以下信息：

- Cloudflare 账户
- Cloudflare API key
- Cloudflare Zone ID

此外，确保你的服务器上安装了 `curl`：

```bash
curl --version
```

如果未安装 `curl`，你需要运行以下命令：

- 对于 RedHat/CentOS：

```bash
yum install curl
```

- 对于 Debian/Ubuntu

```bash
apt-get install curl
```

### 挑战 - 脚本需求

脚本需要监控你服务器的 CPU 使用情况，如果 CPU 使用率根据 vCPU 数量过高，它将通过 Cloudflare API 自动启用 Cloudflare DDoS 防护。

脚本的主要功能应该是：

- 检查服务器上的脚本 CPU 负载
- 在 CPU 激增时，脚本触发对 Cloudflare 的 API 调用并为指定区域启用 DDoS 防护功能
- 在 CPU 负载恢复正常后，脚本将禁用“正受攻击（I'm under attack）”选项并将其恢复正常

### 示例脚本

我已经准备了一个演示脚本可供你参考。但我鼓励你先尝试自己编写脚本，然后再看我的脚本！

下载脚本只需运行以下命令：

```bash
wget https://raw.githubusercontent.com/bobbyiliev/cloudflare-ddos/main/protection.sh
```

使用你喜欢的编辑器打开脚本：

```bash
nano protection.sh
```

并更新以下细节：

```bash
CF_ZONE_ID="YOUR_ZONE_ID"
CF_EMAIL="YOUR_EMAIL"
```



CF_API_KEY="YOUR_API_KEY"

之后，让脚本具有可执行权限：

```bash
chmod +x protection.sh
```

最后，设置 Cron 每隔 30 分钟运行一次：

```cron
crontab -e
```

并添加以下内容：

```cron
*/30 * * * * /path/to/protection.sh
```

... (为了简洁已截略)

## 使用 Bash 和 SSMTP 发送电子邮件

SSMTP 是一种将电子邮件从计算机或服务器发送到已配置的邮件主机的工具。

SSMTP 本身并不是电子邮件服务器，它不接收邮件或管理队列。

它的主要用途之一是将自动生成的电子邮件（如系统警报）从你的机器转发到外部电子邮件地址。

### 先决条件

为了能够成功完成本教程，你需要以下条件：

- 拥有 Ubuntu 18.04 服务器的访问权限，用户为具有 sudo 权限的非 root 用户，且服务器上已安装活跃的防火墙。要设置这些内容，请参考我们的[Ubuntu 18.04 初始服务器设置指南](https://www.digitalocean.com/community/tutorials/initial-server-setup-guide-for-ubuntu-18-04)
- 一个 SMTP 服务器以及相应的 SMTP 服务配置，或者你可以按照此教程中的步骤建立你自己的 SMTP 服务器：[https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-postfix-as-a-send-only-smtp-server-on-ubuntu-16-04](如何在 Ubuntu 16.04 上安装和配置 Postfix 作为仅发送 SMTP 服务器)

### 安装 SSMTP

为了安装 SSMTP，你首先通过以下命令更新 apt 缓存：

```bash
sudo apt update
```

然后运行以下命令安装 SSMTP：

```bash
sudo apt install ssmtp
```

你可能还需要安装的是 mailutils，执行此操作请运行以下命令：

```bash
sudo apt install mailutils
```

### 配置 SSMTP

现在你已经安装了 ssmtp，为了配置它在发送送邮件时使用你的 SMTP 服务器，你需要编辑配置文件。使用你喜欢的文本编辑器打开 `/etc/ssmtp.conf` 文件：

```bash
sudo nano /etc/ssmtp.conf
```

你需要包含你的配置：

```bash
root=postmaster
mailhub=your_smtp_host:587
hostname=your_hostname
AuthUser=your_username@gmail.com
AuthPass=your_password
From=YES
STARTTLS=YES
```

保存文件并退出。

### 使用 SSMTP 发送电子邮件

配置完成后，只需运行以下命令即可发送电子邮件：

```bash
echo "email body" | mail -s "email subject" recipient_email@domain.com
```

你可以直接在终端中运行它，或将其包含在 bash 脚本中。

### 使用 SSMTP 发送文件（可选）

如果你需要发送文件附件，可以使用 `mutt`。安装 `mutt` 请运行以下命令：

```bash
sudo apt install mut
```

接下来，要发送带文件的电子邮件，请运行以下命令：

```bash
mutt -s "Your Subject" -- file.zip -- recipient_email@domain.com
```

上述命令将发送一封带附件的电子邮件。

### 结论

SSMTP 是 bash 脚本中实现电子邮件功能的一种优秀且可靠的方法。关于 SSMTP 的更多信息，我建议查看官方文档。

**注意：** 此内容最初发布在 [DigitalOcean 社区](https://www.digitalocean.com/community)。

## 密码生成器 Bash 脚本

在很多情况下，你需要生成一个随机密码，用于任何软件或注册任何网站，这并不罕见。有很多方法可以实现这一点。你也可以在终端（命令行）中使用 bash 来快速生成密码。我将涵盖其中的几种方法，并由你选择最符合你需求的选项。

### 安全

安全不是开玩笑，所以请确保不要以明文形式将密码保存在本地文件中，或手写下来。我强烈建议大家使用安全的供应商来生成和保存密码。

## 脚本总结

让我先简要总结一下我们的脚本将执行的操作：

1. 在脚本执行时必须选择密码长度。
2. 脚本将根据步骤 1 中指定的长度生成随机密码。

### 先决条件

你需要一个 bash 终端和一个文本编辑器。你可以使用任何文本编辑器，如 vi、vim、nano 或 Visual Studio Code。如果你使用的是 Windows 电脑，可以 ssh 到你选择的任何服务器并在那里执行脚本。虽然脚本非常简单，但具备一些 bash 脚本知识将帮助你更好地理解脚本及其工作原理。

### 生成随机密码

Linux 的巨大优势之一是你可以使用不同的方法来完成很多事情。在生成随机字符字符串时也是如此。我将涵盖几种方法并提供示例：

- 使用 `date` 命令。`date` 命令将输出当前的日期和时间。我们进一步对输出进行处理将其作为随机生成的密码。我们可以使用 md5、sha 对日期进行哈希处理，或直接通过 base64 运行。以下是几个示例：

```bash
date | md5sum
94cb1cdec0699ed98acd9a7b8f6fed
```

使用 sha256sum：

```bash
date | sha256sum
30a0c6091e94c8c7785f0d7bb6e1eac9b76c528f02213d1b6a5fbcc7cef4
```

使用 base64：

```bash
date | base64
0YHQssDRj9C90YmAgMTk6NTE6NDGGVUDIwEK
```

- 我们可以使用 `openssl` 来生成伪随机字节并将输出通过 base64。示例输出如下：

```bash
openssl rand -base64 10
9+soM9btmhdcw==
```

请记住，你的系统可能没有安装 openssl，因此你可能需要先安装才能使用。

- 最优的方法是使用伪随机数生成器 `/dev/urandom`，因为它旨在用于大多数加密用途。我们还需要使用 `tr` 对输出进行处理以转换。示例命令为：

```bash
tr -cd '[:alnum:]' < /dev/urandom | fold -w10 | head -n 1
```

通过此命令，我们从 `/dev/urandom` 获取输出，使用 `tr` 进行转换（保留所有字母和数字），并打印指定数量的字符。

### 脚本

首先我们用 shebang 开始脚本。我们用它来告诉操作系统使用哪种解释器来解析文件的其余部分：

```bash
#!/bin/bash
```

然后我们可以继续请求用户输入。在这种情况下，我们想知道密码需要多少字符：

```bash
### 询问用户密码长度
clear
printf "\n"
read -p "How many characters you would like the password to have?" pass_length
printf "\n"
```

生成密码并打印，以便用户可以使用：

```bash
### 这就是魔法发生的地方
for i in $(seq 1 $pass_length)
do
  pass_output+=$(tr - '[:alnum:]' < /dev/urandom | head -c 1)
done
echo $pass_output
```



### 结论

这就是你可以使用简单的 bash 脚本生成随机密码的方法。

⚠️ 正如前面提到的，请务必使用强密码以确保你的账户受到保护。此外，在可能的情况下，请使用双重身份验证，因为这将为你的账户提供额外的安全保障。

虽然该脚本运行正常，但它假设用户会提供请求的输入。为了防止任何问题，你可能需要对用户输入进行更高级的检查，以确保即使提供的输入不符合我们的需求，脚本也能继续正常工作。

### 贡献者

`Alex Georgiev`

## Bash 中的重定向

Linux 超级用户必须对 Bash 中的管道（pipes）和重定向（redirection）有良好的了解。这是系统的核心组成部分，在 Linux 系统管理领域通常非常有帮助。

当你运行像 `ls`、`cat` 等命令时，你会在终端上看到一些输出。如果你写了错误的命令、传递了错误的标记或错误的命令行参数，你会在终端上得到错误输出。在这两种情况下，你都会得到一些文本。对你来说这似乎仅仅是“文本”，但系统处理这些文本的方式是不同的。这个标识符被称为文件描述符（File Descriptor， `fd`）。

在 Linux 中，有 3 个文件描述符：`STDIN` (`0`)、`STDOUT` (`1`) 和 `STDERR` (`2`)。

- `STDIN` (`fd: 0`): 管理终端的输入。
- `STDOUT` (`fd: 1`): 管理终端的输出文本。
- `STDERR` (`fd: 2`): 管理终端的错误文本。

### 管道与重定向的区别

*管道*和*重定向*都会重定向执行进程的流（文件描述符）。主要的区别在于，*重定向*处理的是*文件流*，将输出流发送到文件，或将给定文件的内容发送到进程的输入流。

另一方面，管道通过将第一个命令的输出流发送到第二个命令的输入流来连接两个命令，而无需指定任何重定向。

## Bash 中的重定向

### STDIN（标准输入）

当你为要求要求输入的命令输入一些输入文本时，你实际上是在向 `STDIN` 文件描述符输入这些文本。运行不带任何命令行参数的 `cat` 命令。看起来进程似乎暂停了，但实际上是 `cat` 在请求 `STDIN`。`cat` 是一个简单的程序，它会打印传递给 `STDIN` 的文本。然而，你可以通过重定向输入到接收 `STDIN` 的命令来扩展其用法。

使用 `cat` 的示例：

```
cat << EOF

Hello World!

How are you?

EOF
```

这将简单地在终端屏幕上打印提供的文本：

```
Hello World!

How are you?
```

其他通过 `STDIN` 接收输入的命令也可以进行相同的操作。例如，`wc`：

```
wc -l << EOF

Hello World!

How are you?

EOF
```

`wc` 的 `-l` 标记统计行数。这段 bash 代码将向终端屏幕上打印行数：

```
2
```

### STDOUT（标准输出）

你终端屏幕上的正常非错误文本是通过 `STDOUT` 文件描述符打印的。命令的 `STDOUT` 可以重定向到文件，使得命令的输出被写入文件而不是打印在终端屏幕上。这简单地通过 `>` 和 `>>` 运算符来实现。

示例：

```
echo "Hello World!" > file.txt
```

接下来的命令不会在终端屏幕上打印 "Hello World"，它会创建一个名为 `file.txt` 的文件并将字符串 "Hello World" 写入其中。可以通过在 `file.txt` 文件上运行 `cat` 命令来验证。

```
cat file.txt
```

然而，当你多次将任何命令的 `STDOUT` 重定向到同一个文件时，它会移除文件的现有内容并写入新内容。

示例：

```
echo "Hello World!" > file.txt

echo "How are you?" > file.txt
```

在 `file.txt` 文件上运行 `cat` 时：

```
cat file.txt
```

你只会得到打印出的 "How are you?" 字符串。

```
How are you?
```

这是因为 "Hello World" 字符串被覆盖了。可以使用 `>>` 运算符避免这种行为。

上面的示例可以写成：

```
echo "Hello World!" > file.txt

echo "How are you?" >> file.txt
```

在 `file.txt` 文件上运行 `cat`，你将得到预期的结果：

```
Hello World!

How are you?
```

或者，`STDOUT` 的重定向运算符也可以写为 `1>`。例如，

```
echo "Hello World!" 1> file.txt
```

### STDERR（标准错误）

终端屏幕上的错误文本是通过命令的 `STDERR` 打印的。
例如：

```
ls --hello
```

会给出错误消息。此错误消息就是命令的 `STDERR`。

可以使用 `2>` 重定向 `STDERR`：

```
ls --hello 2> error.txt
```

然后你可以通过查看 `error.txt` 看到错误：

```
cat error.txt
```

你也可以使用 `2>>` 来追加错误信息：

```
ls --hello 2>> error.txt
```

此外，还可以将 `STDOUT` 和 `STDERR` 同时重定向到同一个文件：

```
ls --hello > output.txt 2> output.txt
```

或者使用 `2>&1` 将 `STDERR` 重定向到 `STDOUT`：

```
ls --hello > output.txt 2>&1
```

### 管道

到为止，我们已经了解了如何通过重定向 `STDOUT`、`STDIN` 和文件。为了将程序（命令）的输出作为另一个程序（命令）的输入，可以使用管道符 `|`。

示例：

```
ls | grep ".txt"
```

语法：

```
command1 | command2
```

你也可以通过将它们组合成任意链来实现强大的结果。这个示例创建了目录下拥有文件的用户列表，以及他们有多少文件和目录：

```bash
ls -l /projects/bash_scripts | tail -n +2 | sed 's/\s*/ /g' | cut -d ' ' -f 3 | sort | uniq -c
```

输出：

- 8 anne
- 34 harry
- 37 tina
- 18 ryan

### Here

可以使用 `<<` 创建临时 heredoc 并在命令行处重定向。

```
COMMAND << EOF

ContentOfDocument

...

...

EOF
```

注意这里的 `EOF` 代表 heredoc 的结束符（文件结束）。实际上，我们可以在此处使用任何字母数字单词来表示文件的开始和结束。例如，这是一个有效的 heredoc：

```
cat << randomword1

This script will print these lines on the terminal.

Note that cat can read from standard input. Using this heredoc, we can

create a temporary file with these lines as it's

content and pipe that

to cat.

randomword1
```

实际上，这看起来就像是 heredoc 的内容被管道传输到了命令。如果需要将多行管道到程序，这可以让脚本变得非常整洁。

此外，我们可以如所示附加更多管道：

```
cat << randomword1 | wc

This script will print these lines on the terminal.

Note that cat can read from standard input. Using this

heroc, we can

create a temporary file with these lines as it's

content and pipe that

into cat.

randomword1
```

此外，可以在 heredoc 中使用预定义的变量。

```
cat << EOF

$VAR

EOF
```

它们都可以重定向到文件：

```
cat << EOF > file.txt
```

还有另一种更短的方法来这样做：

```
./install_package.sh > file.txt 2>&1
```

### HereString

Herestring 与 heredoc 非常相似，但使用的是 `<<<`。这些用于必须管道到某些程序的单行字符串。这看起来比 heredoc 更整洁，因为我们不需要指定分隔符。



`wc <<<this is an easy way of passing strings to the stdin of a program (here wc)"`

就像 heredoc 一样，herestring 也可以包含变量。

### 摘要

操作描述

- `>` 将输出保存到文件
- `>>` 将输出追加到文件
- `<` 从文件读取输入
- `2>` 重定向错误消息
- `|` 将一个程序的输出作为另一个程序的输入
- `<<` 清洁地将多行管道到程序
- `<<<` 清洁地将单行管道到程序

# 使用 BASH 在 LAMP 上自动 Wordpress

这是一个适用于任何基于 Debian 机器的完整 LAMP 和 Wordpress 安装示例。

### 前提条件

- 一台基于 Debian 的机器（Ubuntu, Debian, Linux Mint 等）

### 功能规划

让我们重新回顾一下脚本的主要功能：

### Lamp 安装

- 更新包管理器
- 安装防火墙 (`ufw`)
- 允许 SSH、HTTP 和 HTTPS 流量
- 安装 Apache2
- 安装并配置 MariaDB
- 安装 PHP 及所需的插件
- 启用所有所需的 Apache2 模块

### Apache 虚拟主机设置

- 在 `/var/www` 中创建目录
- 配置该目录的权限
- 在 `/etc/apache2/sites-available` 下创建 `$domain` 文件并追加所需的 Virtualhost 内容
- 启用站点
- 重启 Apache2

### SSL 配置

- 生成 OpenSSL 证书
- 将 SSL 证书追加到 `ssl-params.conf`
- 将 SSL 配置追加到虚拟主机文件
- 启用 SSL
- 重新加载 Apache2

### 数据库配置

- 创建数据库
- 创建用户
- 刷新权限

### Wordpress 配置

- 安装所需的 Wordpress PHP 插件
- 安装 Wordpress
- 将所需信息追加到 `wp-config.php` 文件

话不多说，让我们开始编写脚本。

### 脚本

我们首先设置变量并要求用户输入他们的域名：

```
echo `Please enter your domain of preference without www:`

read DOMAIN

echo "Please enter your Database username:"

read DBUSERNAME

echo "Please enter your Database password:"

read DBPASSWORD

echo "Please enter your Database name:"

read DBNAME

ip=`hostname -I | cut -f1 -d' '`
```

我们现在准备好开始编写函数了。从创建 `lamp_install()` 函数开始。在函数内部，我们将更新系统、安装 `ufw`、允许 SSH、HTTP 和 HTTPS 流量、安装 Apache2、MariaDB 和 PHP。我们还将启用所有所需的 Apache2 模块。

```
lamp_install () {

    apt update -y

    apt install ufw

    ufw enable

    ufw allow OpenSSH

    ufw allow in "WWW Full"

    apt install apache2

    apt install mariadb-server

    mysql secure_installation -y

    apt install libapache2-mod-php php-mysql -y

    sed -i "2d" /etc/apache2/mods-enabled/dir.conf

    sed -i "2i\tDirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm" /etc/apache2/mods-enabled/dir.conf

    systemctl reload apache2

}
```

接下来，我们将创建 `apache_virtualhost_setup()` 函数。在函数内部，我们将在 `/var/www` 中创建一个目录，配置该目录的权限，在 `/etc/apache2/sites-available` 下创建 `$domain` 文件并追加所需的 Virtualhost 内容，启用站点并重启 Apache2。

```
apache_virtual_host setup() {

    mkdir /var/www/$DOMAIN

    chown -R $USER:$USER /var/www/$DOMAIN

    echo "<VirtualHost *:80>" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$serverName $DOMAIN" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$serverAlias www.$DOMAIN" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$serverAdmin webmaster@localhost" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$documentRoot /var/www/$DOMAIN" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$errorLog \${APACHE_LOG_DIR}/error.log" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$customLog \${APACHE_LOG_DIR}/access.log combined" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo "</VirtualHost>" >> /etc/apache2/sites-available/\DOMAIN.conf

    a2ensite $DOMAIN

    a2dissite 000-default

    systemctl reload apache2

}
```

接下来，我们将创建 `ssl_config()` 函数。在函数内部，我们将生成 OpenSSL 证书，将 SSL 证书追加到 `ssl-params.conf` 文件，将 ssl 配置追加到虚拟主机文件，启用 SSL 并重启 Apache。

```
ssl_config() {

    openssl req -x509 -days 365 -newkey rsa:2048

    key /ssl/private/apache-selfsigned.key -out /etc/certs/apache-selfsigned.crt

    echo "SSLCipherSuite EECDH+GCM:AES256+GCM+ECDH:AES256+EDH" >> /etc/apache2/conf-available/ssl-params.conf

    echo "SSLProtocol All -SSLv2 -TLSv1 -TLSv1.1" >> /etc/apache2/conf-available/ssl-params.conf

    echo "SSLHonorCipherOrder On" >> /etc/apache2/conf-available/ssl-params.conf

    echo "Header always set X-Frame-Options DENY" >> {}

}
```

接下来，我们将创建 `db_setup()` 函数。在函数内部，我们将创建数据库、创建用户并向该用户授予所有权限。

```
db_config () {

    mysql -e "CREATE DATABASE $DBNAME;"

    mysql -e "GRANT ALL ON $DBNAME.* TO '$DBUSERNAME'@localhost' IDENTIFIED BY '$DBPASSWORD' WITH GRANT OPTION;"

    mysql -e "FLUSH PRIVILEGES;"

}
```

接下来，我们将创建 `wordpress_config()` 函数。在函数内部，我们将下载最新版本的 WordPress，将其解压到 `/var/www/` 目录，创建 `wp-config.php` 文件并向其追加所需内容。

```
wordpress_config() {
```



`db_setup()`

`apt install php-gd php-mbstring php-xml php-soap php-intl php-zip -y`

`systemctl restart apache2`

`curl -s https://wordpress.org/latest.tar.gz -O`

`tar xvzf latest.tar.gz`

`cd /var/www/$DOMAIN`

`chown -R www-data:www-data /var/www/$DOMAIN`

`find . -type d -exec chmod 755 {} \;`

`find . -type f -exec chmod 644 {} \;`

`cp wp-config.sample wp-config.php`

`sed -i "s/DB_NAME/$DBNAME/g" wp-config.php`

`sed -i "s/DB_USER/$DBUSERNAME/g" wp-config.php`

`sed -i "s/DB_PASSWORD/$DBPASSWORD/g" wp-config.php`

`sed -i "s/DB_HOST/'localhost'/'localhost'/g" wp-config.php`

}

最后，我们将执行 `execute()` 函数。在函数内部，我们将调用我们创建的所有函数。

```
execute () {

  lamp_install

  apache_virtual_host_setup

  ssl_config

  wordpress_config

}
```

至此，你的脚本已经准备就绪，并且准备好运行它了。如果你需要完整的脚本，可以在下一个部分找到它。

### 完整脚本

```bash
#!/bin/bash

echo 'Please enter your domain of preference without www:'

read DOMAIN

echo "Please enter your Database username:"

read DBUSERNAME

echo "Please enter your Database password:"

read DBPASSWORD

echo "Please enter your Database name:"

read DBNAME

ip=`hostname -I | cut -f1 -d ' '`

lamp_install () {

    apt update -y

    apt install ufw

    ufw enable

    ufw allow OpenSSH

    ufw allow in "WWW Full"

    apt install apache2

    apt install mariadb-server

    mysql secure_installation -y

    apt install libapache2-mod-php php-mysql -y

    sed -i "2d" /etc/apache2/mods-enabled/dir.conf

    sed -i "2i\tDirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm" /etc/apache2/mods-enabled/dir.conf

    systemctl reload apache2

}

apache_virtual_host_setup() {

    mkdir /var/www/$DOMAIN

    chown -R $USER:$USER /var/www/$DOMAIN

    echo "<VirtualHost *:80>" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$serverName $DOMAIN" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$serverAlias www.$DOMAIN" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$serverAdmin webmaster@localhost" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$documentRoot /var/www/$DOMAIN" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$errorLog \${APACHE_LOG_DIR}/error.log" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo -e "$customLog \${APACHE_LOG_DIR}/access.log combined" >> /etc/apache2/sites-available/$DOMAIN.conf

    echo "</VirtualHost>" >> /etc/apache2/sites-available/\DOMAIN.conf

    a2ensite $DOMAIN

    a2dissite 000-default

    systemctl reload apache2

}

ssl_config() {

    openssl req -x509 -days 365 -newkey rsa:2048

    key /ssl/private/apache-selfsigned.key -out /etc/certs/apache-selfsigned.crt

    echo "SSLCipherSuite EECDH+GCM:AES256+GCM+ECDH:AES256+EDH" >> /etc/apache2/conf-available/ssl-params.conf

    echo "SSLProtocol All -SSLv2 -TLSv1 -TLSv1.1" >> /etc/apache2/conf-available/ssl-params.conf

    echo "SSLHonorCipherOrder On" >> /etc/apache2/conf-available/ssl-params.conf

    echo "Header always set X-Frame-Options DENY" >> {}

}

db_config () {

    mysql -e "CREATE DATABASE $DBNAME;"

    mysql -e "GRANT ALL ON $DBNAME.* TO '$DBUSERNAME'@localhost' IDENTIFIED BY '$DBPASSWORD' WITH GRANT OPTION;"

    mysql -e "FLUSH PRIVILEGES;"

}

wordpress_config() {

  db_setup()

  apt install php-gd php-mbstring php-xml php-soap php-intl php-zip -y

  systemctl restart apache2

  curl -s https://wordpress.org/latest.tar.gz -O

  tar xvzf latest.tar.gz

  cd /var/www/$DOMAIN

  chown -R www-data:www-data /var/www/$DOMAIN

  find . -type d -exec chmod 755 {} \;

  find . -type f -exec chmod 644 {} \;

  cp wp-config.sample wp-config.php

  sed -i "s/DB_NAME/$DBNAME/g" wp-config.php

  sed -i "s/DB_USER/$DBUSERNAME/g" wp-config.php

  sed -i "s/DB_PASSWORD/$DBPASSWORD/g" wp-config.php

  sed -i "s/DB_HOST/'localhost'/'localhost'/g" wp-config.php

}

execute () {

  lamp_install

  apache_virtual_host_setup

  ssl_config

  wordpress_config

}
```



```bash
available/$DOMAIN.conf
echo -e "\tAlias www.$DOMAIN" >> /etc/apache2/sites-available/$DOMAIN.conf
echo -e "\tAdmin webmaster@localhost" >> /etc/apache2/sites-available/$DOMAIN.conf
echo -e "\tDocumentRoot /var/www/$DOMAIN" >> /etc/apache2/sites-available/$DOMAIN.conf
echo -e "\tErrorLog ${APACHE_LOG_DIR}/error.log" >> /etc/apache2/sites-available/$DOMAIN.conf
echo -e "\tCustomLog ${APACHE_LOG_DIR}/access.log combined" >> /etc/apache2/sites-available/$DOMAIN.conf
echo "</VirtualHost>" >> /etc/apache2/sites-available/$DOMAIN.conf
a2ensite 000-default
a2ensite default
systemctl reload apache2
```

```bash
ssl_config () {
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-signed.key -out /etc/ssl/certs/apache-signed.crt
echo "\tCipherSuite ECDH+AESGCM:EDH+AES256:AES256+EDH" >> /etc/apache2/conf-available/ssl-params.conf
echo "\tSSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1" >> /etc/apache2/conf-available/ssl-params.conf
echo "\tSSLHonorCipherOrder On" >> /etc/apache2/conf-available/ssl-params.conf
echo "\tHeader always set X-Frame-Options DENY nosniff" >> /etc/apache2/conf-available/ssl-params.conf
echo "\tHeader always set X-Content-Type-Options nosniff" >> /etc/apache2/conf-available/ssl-params.conf
echo "\tSSLCompression Off" >> /etc/apache2/conf-available/ssl-params.conf
echo "\tSSLUseStapling On" >> /etc/apache2/conf-available/ssl-params.conf
echo "\tSSLStaplingCache \"shmc:logs/stapling-cache(150000)\"" >> /etc/apache2/conf-available/ssl-params.conf
echo "\tSSLessionTickets Off" >> /etc/apache2/conf-available/ssl-params.conf
cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
}
```

```bash
sed -i "/var/www/html/var/\$DOMAIN/1" /etc/apache2/sites-available/default-ssl.conf
sed -i "/etc/ssl/certs/ssl-cert-snakeoil.pem/etc/ssl/certs/apache-selfsigned.crt/1" /etc/apache2/sites-available/default-ssl.conf
sed -i "/etc/ssl/private/ssl-cert-snakeoil.pem/etc/ssl/private/apache-selfsigned.key/1" /etc/apache2/sites-available/default-ssl.conf
sed -i "4i\tVirtualServerName $ip" /etc/apache2/sites-available/default-ssl.conf
sed -i "22i\tRedirect permanent \"https://\$ip\"" /etc/apache2/sites-available/000-default.conf
a2enmod ssl
a2enmod headers
a2ensite default-ssl
a2conf ssl-params
systemctl restart apache2
```

```bash
db_config() {
  mysql -e "CREATE DATABASE $DBNAME"
  mysql -e "GRANT ALL ON $DBNAME.* TO '$DBUSERNAME'@'localhost' IDENTIFIED BY '$DBPASSWORD' GRANT OPTION;"
  mysql -e "FLUSH PRIVILEGES;"
}
```

```bash
wordpress_config() {
  db_config
  apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-int php-zip
  systemctl restart apache2
  sed -i "8i\tDirectory /var/www/$DOMAIN>" /etc/apache2/sites-available/$DOMAIN.conf
  sed -i "9i\tOverride All" /etc/apache2/sites-available/$DOMAIN.conf
  sed -i "10i\t<Directory>" /etc/apache2/sites-available/$DOMAIN.conf
  a2enmod rewrite
  systemctl restart apache2
  apt install curl
  cd /tmp
  curl -0 https://wordpress.org/latest.tar.gz
}
```

```bash
tar xzvf latest.tar.gz
touch /tmp/wordpress/.htaccess
cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php
mkdir /tmp/wordpress/wp-content/upgrade
cp -a /tmp/wordpress/. /var/$DOMAIN
chown -R www-data:www-data /var/www/$DOMAIN
find /var/www/$DOMAIN -type d -exec chmod 750 {} \;
find /var/www/$DOMAIN -type f -exec chmod 640 {} \;
curl -s https://api.wordpress.org/secret-key/1.1/salt/ >> /var/www/$DOMAIN/wp-config.php
echo "define('FS_METHOD', 'direct')" >>/var/www/$DOMAIN/wp-config.php
sed -i "51,58d" /var/www/$DOMAIN/wp-config.php
sed -i "s/database_name_here/$DBNAME/1" /var/www/$DOMAIN/wp-config.php
sed -i "s/username_here/$DBUSERNAME/1" /var/www/$DOMAIN/wp-config.php
sed -i "s/password_here/$DBPASSWORD/1" /var/www/$DOMAIN/wp-config.php
```

```bash
execute () {
  lamp_install
  apache_virtual_host_setup
  ssl_config
  wordpress_config
}
```

### 总结

该脚本执行了以下操作：

字体 安装 LAMP

- 创建虚拟主机
- 配置 SSL
- 安装 WordPress
- 配置 WordPress



尽管如此，希望你喜欢这个示例。如果你有任何问题，请随时直接通过 `denctl` 与我联系。

### 结语

恭喜！你刚刚完成了 Bash 基础指南！

如果你觉得这个指南有所帮助，请务必在 GitHub 上为该项目点星（star）！

如果你有任何改进建议，请提交 pull 请求（pull requests）或开启 issue。

在本本 Bash 脚本入门书籍中，我们刚刚涵盖了基础知识，但你已经掌握了足够的技能来编写出色的脚本并自动化日常任务！

下一步的建议是编写你自己的脚本并与世界分享！这是学习任何新编程或脚本语言的最佳方式！

如果这本书激发了你编写一些酷炫的 Bash 脚本，请务必在 Twitter 上发布并艾特 @bobbyiliev_，以便我们可以看到！

再次恭喜你完成这本书！
