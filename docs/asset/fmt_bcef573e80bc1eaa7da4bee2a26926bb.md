
**步骤 10** 将 `echo` 想象成旧的 `BASIC` `Print` 命令。它显示文本、数字或存储在系统中的任何变量，例如当前系统日期。尝试这个例子：`echo Hello World! Today is $(date +%A)`。`$(date +%A)` 调用了存储当前星期的系统变量。

![](img/5019375da05cbf0090115165d80772a1_68_5.png)

### 创建 Bash 脚本 – 第二部分

之前我们看了创建你的第一个 Bash 脚本 `Hello World`，并添加了一个系统变量。现在你可以扩展这些内容，看看当你开始与自己独特的变量玩耍时能做什么。

#### 变量

就像在所有其他编程语言中一样，Bash 脚本可以从系统中存储和调用某些变量，无论是通用的还是用户创建的。

- **步骤 1**
让我们通过创建一个名为 `hello.sh` 的新脚本开始；`xed hello.sh.` 在其中输入：`#!/bin/bash`，然后，`echo Hello $1`。保存文件并退出 `Xed`。回到终端，使用 `chmod +x hello.sh.` 使脚本可执行。

![](img/5019375da05cbf0090115165d80772a1_69_0.png)

- **步骤 2**
既然脚本现在可执行，用 `./hello.sh.` 运行它。现在，正如你可能预期的那样，终端中显示了一个简单的 'Hello'。然而，如果你随后使用变量发出命令，情况开始变得有趣起来。例如，尝试 `./hello.sh David`。

![](img/5019375da05cbf0090115165d80772a1_69_1.png)

- **步骤 3**
输出现在是 `Hello David`。这是因为 Bash 自动为用户分配变量，这些变量随后被保存并传递给脚本。所以变量 `'$1'` 现在持有 ‘David’。你可以通过输入不同的内容来改变变量：`./hello.sh Mint`。

![](img/5019375da05cbf0090115165d80772a1_69_2.png)

- **步骤 4**
你甚至可以重命名变量。用以下内容修改 `hello.sh` 脚本：`firstname=$1, surname=$2, echo Hello $firstname $surname.` 将每条语句放在新的一行。保存脚本并退出回到终端。

![](img/5019375da05cbf0090115165d80772a1_69_3.png)

- **步骤 5**
现在运行脚本时，你可以使用两个自定义变量 ..，`/hello.sh David Hayward`。当然，可以用你自己的名字改变这两个变量，除非你也叫 `David Hayward`。目前我们只是在打印内容，所以让我们稍微扩展一下两个变量的使用。

![](img/5019375da05cbf0090115165d80772a1_70_0.png)

- **步骤 6**
创建一个名为 `addition.sh` 的新脚本，使用与 `hello.sh` 脚本相同的格式，但改变变量名称。这里我们添加了 `firstnumber` 和 `secondnumber`，并使用 `echo` 命令进行简单算术运算，通过放置一个整数表达式 `first` `number`。 `echo The sum is $(($firstnumber+$secondnumber))`。保存脚本，并使其可执行（`chmod +x addition.sh`）。

![](img/5019375da05cbf0090115165d80772a1_70_1.png)

- **步骤 7**
现在运行 `addition.sh` 脚本时，我们可以输入两个数字： `./addition.sh 1 2`。结果希望是 3，终端将显示 `The sum is 3`。尝试几个不同的数字，看看会发生什么。也看看你是否可以修改脚本并将其重命名以执行乘法和减法。

![](img/5019375da05cbf0090115165d80772a1_70_2.png)

- **步骤 8**
让我们进一步扩展。创建一个名为 `greetings.sh` 的新脚本。在截图中输入下方的脚本内容，保存它并使用 `chmod` 命令使其可执行。你可以看到脚本现在有一些新的添加内容。

![](img/5019375da05cbf0090115165d80772a1_70_3.png)

- **步骤 9**
我们在这里的 `echo` 命令中添加了一个 `-n`，这将使光标停留在与问题相同的行上。而不是新的一行。 `read` 命令将用户输入存储为变量 `firstname` 和 `surname`，然后在最后一个 `echo` 行稍后读回。并且 `clear` 命令清除屏幕。

![](img/5019375da05cbf0090115165d80772a1_70_4.png)

- **步骤 10**
作为最后的添加，让我们包括上一节中使用的日期变量。修改脚本的最后一行以读取： `echo Hello $firstname $surname, how are you on this fine $(date +%a)?`。输出应显示当前的星期几，从系统变量中调用。

![](img/5019375da05cbf0090115165d80772a1_70_5.png)

### 创建 Bash 脚本 – 第 3 部分

在前面的页面中，我们介绍了一些非常基础的 Bash 脚本知识，包括向屏幕输出文本、获取用户输入并存储该输入、将其输出到屏幕，以及使用 `Date` 命令包含一个系统变量。现在让我们把目前所学的内容结合起来，并介绍循环（Loops）。

#### IF、THEN、ELSE

在大多数编程结构中，迟早会需要循环执行你输入的指令，以创建更好的功能，并最终打造更好的程序。

- **步骤 1** 现在让我们来学习 `If`、`Then` 和 `Else` 语句。当正确执行时，它们会比较一组指令，并简单地确定：如果某事物存在，`THEN` 做某事，`ELSE` 做另一件事：创建一个名为 `greeting2.sh` 的新脚本，并将下方截图中的文本输入其中。

- **步骤 2** `Greeting2.sh` 是 `greeting.sh` 的副本，但有一个细微差别。在这里我们添加了一个从 `If` 语句开始的循环。这意味着，如果输入的变量等于 `David`，下一行 `THEN` 就是对此的反应，在这种情况下，它会在屏幕上输出“Awesome name”，随后是变量（即 `David`）。

- **步骤 3** 下一行 `ELSE` 是当变量不等于‘David’时发生的情况。在这种情况下，它只是在屏幕上输出我们现在熟悉的‘Hello...’。最后一行 `FI` 语句是结束循环的命令。如果你有 `if` 命令但没有 `FI` 命令，就会得到错误。

- **步骤 4** 显然你可以稍微玩玩这个脚本，改变触发响应的姓名变量；或者甚至发出一个响应，让名字和姓氏变量匹配一个特定变量。

```bash
#!/bin/bash

echo -n 'Hello, what is your name? '
read firstname
echo -n 'Thank you, and what is your surname? '
read surname
clear
if [ $firstname == 'David' ]
then
  echo $firstname
else
  echo Hello $surname
fi
```

```bash
$ mkdir scripts
$ cd scripts
$ nano greeting2.sh
```

```bash
#!/bin/bash

echo -n 'Hello, what is your name? '
read firstname
echo -n 'Thank you, and what is your surname? '
read surname
clear
if [ $firstname == 'David' ] && [ $surname == 'Hayard' ]
then
  echo "Awesome name, $firstname $surname"
else
  echo "Hello $firstname $surname, how are you on this fine Wednesday?"
fi
```

```text
david@david-mint ~ 
$ ./scripts/greeting2.sh
Hello, what is your name? David
Thank you, and what is your surname? Hayard
Awesome name, David Hayard
```

#### 更多循环

你可以使用 `FOR`、`WHILE` 和 `UNTIL` 语句对数据进行循环。如果你批量命名、复制或运行需要计数器的脚本，这些语句会很有用。
