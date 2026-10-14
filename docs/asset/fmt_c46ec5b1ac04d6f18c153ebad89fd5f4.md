
第 1 步让我们开始创建一个名为 `hello` 的新脚本：`nano hello.sh`。在编辑器中输入：`#!/bin/bash`，然后是 `echo hello $1`。保存文件并退出 `nano`。在终端中让脚本变为可执行：`chmod +x hello.sh`。

第 2 步由于脚本现在是可执行的，使用 `./hello.sh` 运行它。现在，正如你预期的，终端中显示了简单的“Hello”。然而，如果你接着使用带有变量的命令，事情变得有趣起来。例如，尝试 `./hello.sh David`

![](img/21ee864cf339a60c6b969b7bda291087_69_0.png)

第 3 步输出现在将是 Hello David。这是因为 Bash 会自动为用户分配变量，这些变量会被持有并传递给脚本。变量 `$1` 保存了“Hello David”。你可以通过输入不同的内容来更改变量：`./hello.Mint`

第 4 步你可以重命名变量。使用以下内容修改 `hello` 脚本：`firstname=$1, surname=$2, echo Hello $firstname $surname`。每个语句放在新行。保存脚本并返回终端。

![](img/21ee864cf339a60c6b969b7bda291087_69_1.png)

# 创建 Bash 脚本 – 第二部分（重复）

第 5 步当你运行脚本时，现在可以使用自定义变量了：`./hello.sh David`。自然地改变看看当你开始尝试创建自己的独特变量时可以做什么。

（注：后续原文内容存在大量逻辑混乱和重复，已按原文顺序字面翻译如下：）

第 8 步当你再次输入 `ls` 时，你会发现 `helloworld.sh` 现在从白色变成了绿色，这意味着它现在是一个可执行文件。运行该脚本，换句话说就是让它执行你输入的内容，输入：`./helloworld.sh`

（代码块保持不变...）

```
File Edit View Search Tools Documents Help
*helloworld.sh x
#!/bin/bash
echo Hello World!
```

第 6 步 `#!/bin/bash` 这一行告诉系统你将成为什么，在本例中是 Bash。井号（`#`）和感叹号（`!`）表示注释行，系统会忽略它，这意味着注释会被跳过，并强制脚本将该后的行作为命令执行。这被称为 Hash-Bang。

第 9 步虽然这并不特别有趣，但“Hello World!”这些单词将显示在终端中。`echo` 命令负责在终端中输出其后的单词，或者你让命令输出到其他任何地方。

```
File Edit View Search Tools Documents Help
*helloworld.sh x
#!/bin/bash
daviddaid-mint ./helloworld.sh
daviddaid-mint ./helloworld.sh
daviddaid-mint echo Hello World
echo Hello World! This is my first script in Linux Mint!
```

第 7 步你可以保存文件，点击 Save（保存），并返回终端。输入 `ls` 将显示文件夹中的脚本。要让任何脚本变得可执行并能够运行，你需要赋予它权限。使用 `chmod +x helloworld.sh` 执行此操作。创建的每个脚本都需要这样做。

第 10 步将 `echo` 想象成旧的 BASIC `print` 命令。它显示文本、数字或存储在系统中的任何变量，例如当前日期。尝试这个命令：`echo Hello World! Today is $(date +A)`。日期（`%A`）是存储今天日期的系统变量。

```
File Edit View Search Terminal Help
daviddaid-mint --scripts nano helloworld.sh
daviddaid-mint --scripts ls
helloworld.sh
daviddaid-mint --scripts chmod +x helloworld.sh
daviddaid-mint --scripts $
```

```
File Edit View Search Tools Documents Help
Hello World Today is $(date +A)
#!/bin/bash
echo Hello World! Today is $(date +A)
```

Linux 编码与编程 69

# 创建 Bash 脚本 – 第二部分

（注：此处起原文开始重复且逻辑混乱，已按原文字面翻译）

之前我们查看了如何创建第一个 Bash 脚本“Hello World”并添加系统变量。现在你可以扩展这些内容，看看当你开始尝试创建自己的独特变量时可以做什么。

# 变量 (VARIABLES)

...（后续重复内容略）

# 循环

你可以使用 `FOR`、`WHILE` 和 `UNTIL` 语句对数据进行循环。当你需要批量命名、复制或运行需要计数器的脚本时，这些语句会非常有用。

步骤 1 创建名为 `count.sh` 的新脚本。输入下方截图中的文本，保存并赋予可执行权限。这创建了一个变量 `count`，它在脚本开始时赋值为 0。然后是 `WHILE` 循环，当 `count` 小于（`lt` 部分） 100 时，`echo` 命令将打印 `count` 的当前值。

```
count.sh
File Edit View Search Tools Documents Help
count.sh
#!/bin/bash
count=0
while [ $count -lt 100 ]; do
echo $count
let count=$((count+1))
done
```

步骤 2 执行 `count.sh` 脚本将在终端列出 0 到 99 的数字；当达到 100 时，脚本将结束。使用 `FOR` 语句修改脚本使其更容易以相同的方式使用。为了编写脚本，请将截图中的文本输入 `count.sh` 中。

步骤 3 我们在这里添加的内容是：`for count in {0..100}; do`。意味着：对于变量 `count` 在从零到一百的数字中，开始循环。脚本的其他部分相同。运行此脚本，输出应该出现在终端中。

步骤 4 `UNTIL` 循环的工作方式与 `WHILE` 循环非常相似，通常是反向的。我们使用 `UNTIL` 计数到一百，直到：`[ $count -gt 100 ]`；区别在于，`UNTIL` 在 `count` 大于（`gt` 部分）一百时继续循环。

步骤 5 你并不局限于数字到一百。在循环内部，你可以设置任何喜欢的命令集，并根据所需的循环次数执行它们。例如，重命名文件、创建五个文件夹，此脚本将使用 `FOR` 循环创建名为 1 到 100 的文件夹。

```
count.sh
File Edit View Search Tools Documents Help
count.sh
#!/bin/bash
for count in {0..100}; do
echo $count
let count=$count+1
done
```

步骤 6 再次使用 `FOR` 语句，我们可以通过操作 (0-100) 部分来执行计数序列。这段代码集实际上意味着 开始-增量；如果没有增量，它只是从一个数字到结束。例如，我们使用循环每隔 2 位数到 1000：`for count in {0..1000..2}; do`。

``` evencount.sh
File Edit View Search Tools Documents Help
count.sh
#!/bin/bash
for count in {0..100..2}; do
echo $count
let count=$count+1
done
```

![](img/21ee864cf339a60c6b969b7bda291087_72_0.png)

# 创建 Bash 脚本 – 第 4 部分

你已经遇到过脚本的交互，询问用户的姓名等。你还查看了在脚本内部创建循环以进行计数或简单地执行多次操作。让我们结合并进一步扩展。

## 选择与循环

让我们引入另一个命令 `CHOICE`，以及一些嵌套的 `IF` 和 `ELSE` 语句。从创建一个新脚本 `mychoice.sh` 开始。

![](img/21ee864cf339a60c6b969b7bda291087_73_0.png)

### 步骤 1 `mychoice.sh` 脚本开始变得复杂。我们这里有一个四个选择的列表，其中三个是嵌套的。选项：Mint，如果用户提供了正确的选项，将会显示。如果不是，菜单将显示第四个选项。

![](img/21ee864cf339a60c6b969b7bda291087_73_2.png)

### 步骤 2 如果你遵循脚本就能掌握发生了什么。通过 `IF` 和 `ELSE`，循环将运行选项，并在你选择错误选项时带你回到。

![](img/21ee864cf339a60c6b969b7bda291087_73_3.png)
