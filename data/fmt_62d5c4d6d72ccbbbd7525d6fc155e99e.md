
文本编辑器 `Emacs` 是一款非常出色的软件，但它还包含一个隐藏的彩蛋！你知道吗？在安装了 `Emacs` 的情况下（`sudo apt-get install emacs25`），切换到终端会话并输入：

```bash
emacs -batch -l dunnet
```

### 终端浏览

是否曾经想过从终端浏览互联网？虽然不是特别实用，但这是一个非常引人注目的现象。要这样做，请输入：

```bash
sudo apt-get install elinks
```

`Dunnet` 是 `Ron Schnell` 在 1982 年编写的一款文字冒险游戏，自 1994 年起一直隐藏在 `Emacs` 中。

输入你想要访问的网站。

### 月球车

基于 1982 年的经典街机游戏《月球巡逻》（`Moon Patrol`），月球车在 1985 年出现在家用电脑上，并备受赞誉。它是一款非常棒的雅达游戏，通过输入以下命令可以在 Linux 终端中运行：

```bash
sudo apt-get install moon-buggy
```

### 让雪落下

终端控制台可能会任何一天下雪。如果你感兴趣，请输入：

```bash
wget https://github.com/semtek/15058483/raw/7/d024716ea57e69fb52632fee09f4427353164a2/snowjob.job
chmod +x snowjob.job
```

## 内存大户

删除一个文件，可能会消耗系统的大部分内存。查看内存大户，只需输入：

```bash
ps aux --sort -rnk 4
```

这将根据内存使用情况对输出进行排序。

## BBS

在拨号连接时代，在线世界是由公告板（`BBS`）组成的。这些系统一直是用户聊天、交换代码、玩游戏的聚集地，通过 `Telnet`，我们仍然可以连接到一些活跃的 `BBS`。

```bash
telnet startbestarrars.dyndns.org
```

有无数 `BBS` 可用，你可以查看 https://www.telnetbse.com/bbs/list/ 获取更多信息。

## 彻底粉碎

当你想要删除整个具有树形结构的目录（或文件夹）时，拥有正确软件的人可以恢复它。然而，要安全且永久地删除文件：

```bash
mkdir -p New-Dir/
# subfolder1, subfolder2, subfolder3, subfolder4
shred -zu FILENAME.txt
```

这将创建一个包含四个子文件夹的 `New-Dir`。将 `FILENAME` 替换为文件名。

## ASCII 艺术

`ASCII` 应用于某些图像时会非常醒目。但这很难实现。你可以使用 `img2txt` 从图像创建一些很棒的 `ASCII` 艺术：

```bash
img2txt FILENAME.png
```

将 `FILENAME` 替换为系统中实际的文件。

## 忘记的命令

想要记住所有的 Linux 命令并不容易。坦率说，我们可以使用 `apropos` 来帮助。只需使用它，并带有描述：

```bash
apropos "copy files"
```

1. 复制文件和目录
2. 复制文件和目录
3. 复制文件并设置属性
1. 重命名文件
2. 在标准输出中写入注释，编辑并重命名
3. 重命名

## 使用终端

## Linux 与大爆炸

`Linux` 是碰撞的粒子，因此我们可以理解宇宙是如何运作的。

## 你知道吗...

`Linux` 是大型对子对撞机背后科学的核心吗？通过将 `Red Hat` 和 `CentOS`（一个基于 `Red Hat` 核心构建的超稳定发行版）作为基础，欧洲核研究中心（`CERN`）的聪明人们开发了多个不同版本的自己的发行版来协助各个方面。最著名的是 `SLC`，也称为 `CERN`。据报告，有超过 6000 个系统正在运行，超过 15000 个正在运行。

# 创建 Bash 脚本 – 第一部分

## 脚本编写

脚本仅仅是 `Bash` 将运行以完成特定任务的一系列命令。它们可能非常复杂，取决于具体情况。最终，你将在终端内并配合文本编辑器工作，但为了方便起见，我们将通过以下方式进行示例：

- **第 1 步**：有几种文本编辑器我们可以创建 `Bash` 脚本；`Nano`、`Vim`、`GNU Emacs` 等。根结底取决于个人偏好。使用 `Nano` 纯粹是为了方便在截图中读取脚本。
- **第 2 步**：首先，在你开始编写任何脚本之前，你需要创建一个文件夹，将所有的脚本都放在里面。这将我们的工作文件夹，如果你需要，你可以在这里创建子文件夹。
- **第 3 步**：让我们从简单的脚本开始，向终端输出一些内容。输入 `nano helloworld.sh`。这将启动 `Nano` 并创建一个名为 `helloworld.sh` 的文件。在 `Nano` 中输入以下内容：

```bash
#!/bin/bash
echo Hello World!
```

- **第 4 步**：保存文件并返回终端。
- **第 5 步**：`#!/bin/bash` 行告诉 shell 你将使用什么。井号（`#`）表示注释行，系统会忽略它；感叹号（`!`）表示跳过命令，并将强制脚本将该行作为命令执行。这被称为 `Shebang`（井号）。
- **第 6 步**：当你再次输入 `ls` 时，你可以看到 `helloworld.sh` 现在已经从黑色变成了绿色，这意味着它现在是一个可执行文件。运行脚本，换句话说让它执行你输入的内容：`./helloworld.sh`。
- **第 7 步**：你可以点击 `Save` 保存文件，并返回终端。要让任何脚本变得可执行并能够修改权限，请执行 `chmod +x helloworld.sh`。你应该对创建的每个脚本都这样做。
- **第 8 步**：虽然这并不非常有趣，但“`Hello World!`”单词将显示在终端中。`echo` 命令负责输出其后面的单词，因此无论你让命令输出什么，它都会存储。
- **第 9 步**：将 `echo` 想象成 `BASIC` 的打印命令。它显示文本或存储在系统的变量，例如当前日期。尝试：`echo Hello World! Today is $(date)`。
- **第 10 步**：注意：`$(date +A)` 正在调用存储今天日期的变量。

## 创建 Bash 脚本 – 部分 2

之前我们查看了如何创建你的第一个 `Bash` 脚本 `Hello World`，并添加了一个系统变量。现在你可以扩展这些内容，看看当你开始尝试创建自己的独特变量时可以做什么。

### 变量

与其他所有编程语言一样，`Bash` 脚本可以存储和调用系统的某些变量，无论是通用的还是自定义。

- 步骤1：让我们创建一个名为 `hello.sh` 的脚本；`xed hello.sh`。在编辑器中：`#!/bin/bash`，然后输入 `echo Hello $1`。保存文件并退出 `xed`。使用 `chmod +x hello.sh` 使脚本具有执行权限。
- 步骤2：由于脚本是可执行的，使用 `./hello.sh` 运行它。现在，正如你预期的那样，终端显示了“`Hello`”。如果你对变量使用该命令，它就会变得有趣起来。例如，尝试 `./hello.sh David`。
- 步骤3：现在的输出将是 `Hello David`。这是因为 `Bash` 会自动为用户分配变量，这些变量会被持有并传递给脚本。`$1` 现在持有 `David`。你可以通过输入不同的内容来更改变量：`./hello.sh Mint`。

```
File Edit View Search Terminal
david@david-mint ~/scripts$ edit hello.sh
david@david-mint ~/scripts$ chmod +x hello.sh
david@david-mint ~/scripts$ $
Edit View Search Documents Help
hello.sh x
#!/bin/bash
echo Hello $1
```

```
File Edit View Search Terminal Help
david@david-mint ~/scripts$ ./hello.sh
Hello David
david@david-mint ~/scripts$ ./hello David
david@david-mint ~/scripts$ ./hello.sh Mint
Hello Mint
david@david-mint ~/scripts$ $
```

- 步骤4：你可以重命名变量。使用以下内容修改 `hello.sh` 脚本：`firstname=$1`, `surname=$2`, `echo $firstname $surname`。将每个语句放在新的一行。保存脚本并返回终端。

```
File Edit View Search Documents Help
david@david-mint ~/scripts$ ./hello.sh
Hello David
david@david-mint ~/scripts$ ./hello David
david@david-mint ~/scripts$ ./hello.sh Mint
Hello Mint
david@david-mint ~/scripts$ 
.hello.sh x
#!/bin/bash
firstname=$1
surname=$2
echo Hello $firstname $surname
```

接下来

- 步骤5：当你运行脚本时，现在可以使用自定义变量了：`./hello.sh David Hayward`。自然地根据你的名字更改这两个变量；除非你也是 `David Hayward`。目前我们只是在打印内容，所以让这两个变量派上用场。
- 步骤6：创建一个名为 `addition.sh` 的新脚本，使用与 `hello.sh` 相同的格式。在这里我们定义了变量 `firstname` 和 `surname`，并使用 `echo` 命令通过让一个表达式执行简单的算术运算：`echo The sum is $((firstname+surname))`。保存脚本并使其具有执行权限（`chmod +x addition.sh`）。
- 步骤7：当你运行 `addition` 脚本时，我们可以输入两个数字：`./addition.sh 1 2`。结果将是 3。尝试不同的数字看看会发生什么。同时也修改脚本并重命名为 `multiplication`。
- 步骤8：让我们进一步扩展。创建一个名为 `greetings.sh` 的新脚本。输入下面的脚本并使用 `chmod` 命令使其具有执行权限。你可以看到脚本现在增加了一些内容。
- 步骤9：我们在 `echo` 命令中添加了 `-n`，这会让光标留在与新行的同一行。`read` 命令将用户的输入存储到变量 `firstname` 和 `surname` 中以供稍后读取。`clear` 命令清除屏幕。
- 步骤10：作为最后的完善，让我们包含上一节中使用的变量。修改脚本末尾以 `echo Hello $firstname $surname`。输出应该显示当前日期，调用了一个系统变量。

```
File Edit View Search Terminal
david@david-mint ~/scripts$ ./hello.sh David Hayward
david@david-mint ~/scripts$ ./hello.sh Mint Hello Mint
david@david-mint ~/scripts$ $
```

```
File Edit View Search Documents Help
$ greetings.sh
#!/bin/bash
echo -n "Hello, what is your name?"
read firstname
echo -n "Thank you, what is your surname?"
read surname
echo Hello $firstname, how are you?
```

## 创建 Bash 脚本 – 部分 3

在之前的页面中，我们查看了 `If`、`Else` 语句，现在是一个非常基础的 `Bash` 脚本，涉及向屏幕输出文本、获取用户输入、存储并输出到屏幕，以及包含变量。现在让我们结合目前已取得的并引入循环。

### IF, THEN, ELSE

在大多数编程结构中，总会有需要循环遍历你输入的命令以创建更好功能的时候。

- 步骤1：让我们现在查看 `If`, `Then` 和 `Else` 语句，当正确执行时，它们会带来一组指令，并简单地判断某些内容是否存在，如果存在则执行不同的操作。创建一个新脚本 `greeting.sh` 并输入下面的文本。
- 步骤2：`greeting.sh` 是 `greeting.sh` 的副本，但略有不同。在这里我们在 `if` 语句处添加了一个循环。这意味着如果 `IF` 变量等于 `David`，那么下一行 `THEN` 就是对所发生情况的反应，它将在屏幕上输出“`Awesome name`”，然后是变量（即 `David`）。
- 步骤3：下一行 `ELSE` 是当变量不等于“`David`”时发生的情况。在这种情况下，它只是在屏幕上输出第一行的“`Hello...`”。最后一行，命令是用于结束循环的语句。如果你有一个没有命令的 `if`，你就会得到错误。

```
greeting.sh
#!/bin/bash
echo "Hello, what is your name?"
read firstname
echo "Thank you, what is your surname?"
read surname
clear
if [ "$firstname" == "David" ]; then
  echo "David"
```

```
greeting.sh
#!/bin/bash
echo "Hello, what is your name?"
read firstname
echo -n "Thank you, what is your surname?"
read surname
clear
if [ "$firstname" == "David" ] && [ "$surname" == "Hayward" ];
then
  echo "Awesome $firstname $surname"
else
  echo "Hello $firstname $surname, how are you on this"
```

## 更多循环

你可以使用 `FOR`、`WHILE` 和 `UNTIL` 语句来循环数据。如果你正在进行批量命名、复制或运行需要计数器的脚本，这些会非常有用。

- 步骤1：创建一个名为 `count.sh` 的新脚本。输入截图中的文本并使其具有执行权限。这创建了变量 `count`，它在脚本开始时等于零。然后是 `WHILE` 循环，当 `count` 小于（`LT` 部分）100 时，将在 `echo` 中打印计数器的当前值。
- 步骤2：执行 `count.sh` 脚本将产生 0 到 99 的数字显示；当它达到 100 时脚本结束。使用 `FOR` 语句修改脚本使其工作相同。在这种情况下，你将截图中的文本输入 `count.sh`。
- 步骤4：`UNTIL` 循环与 `WHILE` 循环的工作相同，只是更多时候是反向的。所以数到一百，使用 `UNTIL`，我们将是：`[ count -gt 100 ]`。区别在于，直到计数器大于（`gt` 部分）100，继续循环。

```
count.sh
#!/bin/bash
count=0
while [ $count -lt 100 ]; do
  echo $count
  ((count+=1))
done
```

- 步骤5：你不限于数字到一百。你可以循环执行你喜欢的任何命令集，运行你想循环运行的次数。重命名文件、创建五个文件夹等。此脚本将使用 `FOR` 循环创建从 `folder1` 到 `folder10` 的文件夹。

```
count.sh
#!/bin/bash
until [ $count -gt 100 ]; do
  echo $count
  ((count+=1))
done
```

- 步骤6：再次使用 `FOR` 语句，我们可以通过操作 `(0-100)` 部分来执行以下序列。此部分实际上意味着起始、增量；如果没有增量，它只是一个跳转到结束的单数字，例如我们可以将循环设置到 1000 且步长为 2：`for count in {0..1000..2}; do:` 

```
count.sh
#!/bin/bash
for count in {0..100}; do
  echo $count
  ((count+=1))
done
```

# 创建 Bash 脚本 – 第 4 部分

你已经遇到过脚本与用户交互的情况，例如用户名等。你还查看了如何在脚本中创建循环来计数或简单地多次执行某些操作。让我们结合并扩展更多内容。

## 选择与循环

让我们引入另一种方法 `CHOICE`，以及一些嵌套的 `IF` 和 `ELSE` 语句。从创建一个新脚本 `mychoice.sh` 开始。

### 第 1 步

![](img/2f5daccbaef9a995b10c4942ee31a6fa_73_0.png)

`mychoice.sh` 脚本开始变得复杂许多。现在我们有一个四个选项的列表，其中三个是选项。如果用户选择了选项键，将显示 **Mint** 和 **Awesome**。否则，菜单将重复直到第四个选项为止。

### 第 3 步

当然，你可以增加选项的数量以匹配 `IF` 语句的数量，但你需要确保脚本不会变得眼花缭乱。这个长脚本是设计菜单的另一种方式，这次使用了花哨的配色方案。

![](img/2f5daccbaef9a995b10c4942ee31a6fa_73_1.png)

### 第 2 步

如果你顺利运行了脚本，基于我们已经涵盖的 `WHILE`、`IF` 和 `ELSE`，你已经掌握了它的运行原理。`FI` 循环语句将遍历选项，并在你选了错误选项时带你回到起点。

![](img/2f5daccbaef9a995b10c4942ee31a6fa_73_2.png)

### 第 4 步

你可以在菜单中使用方向键和回车键来选择脚本。`choice` 是一个反馈信息的外部命令。关于命令、选择以及你可以得到的结果，比我们之前看到的要好一点，让你对可以实现的内容有了很好的理解。
