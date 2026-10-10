

## 为图形化桌面编写脚本

### 本章内容

- 创建文本菜单
- 处理窗口
- 获取图形化界面

多年来，Shell 脚本一直被认为枯燥乏味。但情况并非必然如此，尤其是当你计划在图形化环境中运行脚本时。除了 `read` 和 `echo` 语句外，还有许多方式可以与脚本用户进行交互。本章将深入探讨几种可用于为交互式脚本增添活力的方法，使其不再显得过时。

### 创建文本菜单

创建交互式 Shell 脚本最常见的方式是利用菜单。为用户提供各种选项的选择有助于引导他们了解脚本能做什么以及不能做什么。

菜单脚本通常会清除显示区域，然后显示可用选项列表。用户可以通过按下分配给每个选项的相关字母或数字来选择选项。图 18.1 展示了一个示例菜单的布局。

Shell 脚本菜单的核心是 `case` 命令（参见第 12 章，“使用结构化命令”）。`case` 命令根据用户从菜单中选择的字符执行特定的命令。

以下章节将指导你完成创建基于菜单的 Shell 脚本的步骤。

![](img/0798d50a0e5dbf1265fbda3832b3e015_456_0.png)

![](img/0798d50a0e5dbf1265fbda3832b3e015_457_0.png)

#### 创建菜单布局

创建菜单的第一步显然是确定你希望菜单中显示哪些元素，并将它们布局为你希望呈现的样子。

在创建菜单之前，通常最好清除监视器显示。这样做可以确保你在一个干净的环境中显示菜单，没有干扰文本。

`clear` 命令使用终端会话的终端设置信息（参见第 2 章，“进入 Shell”）来清除监视器上显示的任何文本。在 `clear` 命令之后，你可以使用 `echo` 命令来显示你的菜单元素。

默认情况下，`echo` 命令只能显示可打印的文本字符。在创建菜单项时，使用不可打印项目（如制表符和换行符）通常很有帮助。要在 `echo` 命令中包含这些字符，你必须使用 `-e` 选项。因此，命令

```
echo -e "1.\tDisplay disk space"
```

产生的输出行为

1.        Display disk space

这大大有助于格式化菜单项的布局。只需几个 `echo` 命令，你就可以创建一个外观合理的菜单：

```
clear
echo
echo -e "\t\tSys Admin Menu\n"
echo -e "\t1. Display disk space"
echo -e "\t2. Display logged on users"
echo -e "\t3. Display memory usage"
echo -e "*\t0. Exit menu\n"
echo -en "\t\tEnter option: "
```

最后一行的 `-en` 选项在不添加换行符的情况下显示该行。这使菜单看起来更专业，因为光标停留在行尾等待用户输入。

创建菜单的最后一步是获取用户输入。这是使用 `read` 命令完成的（参见第 14 章，“处理用户输入”）。由于你只期望单字符输入，好的做法是使用 `read` 命令的 `-n` 选项来获取一个字符。这样允许用户输入一个数字而无需按 Enter 键：

```
read -n 1 option
```

接下来，你需要创建你的菜单函数。

#### 创建菜单函数

Shell 脚本菜单选项作为一组独立的函数更容易创建。这种方法使你能创建一个简单、简洁且易于遵循的 `case` 命令。

为此，你必须为每个菜单选项创建独立的 Shell 函数。创建菜单 Shell 脚本的第一步是确定你希望脚本执行哪些功能，并将它们作为代码中的独立函数进行布局。

为尚未实现的功能创建存根函数是常见做法。存根函数是一个尚未包含任何命令或可能仅包含一个表示最终应有什么内容的 `echo` 语句的函数：

```
function diskspace {
    clear
    echo "This is where the diskspace commands will go"
}
```

存根函数使你的菜单在工作期间能够平稳运行。你不需要编码所有函数就能让你的菜单工作。你会注意到函数以 `clear` 命令开始。这使你能在干净的监视器屏幕上开始函数，而不显示菜单。

在 Shell 脚本菜单中有帮助的一件事是将菜单布局本身创建为一个函数：

```
function menu {
    clear
    echo
    echo -e "*\t\tSys Admin Menu\n"
    echo -e "*\t1. Display disk space"
    echo -e "*\t2. Display logged on users"
    echo -e "*\t3. Display memory usage"
    echo -e "*\t0. Exit program\n"
    echo -e "\t\t\nEnter option: "
    read -n 1 option
}
```

这种策略使你可以通过调用 `menu` 函数轻松地在任何时候重新显示菜单。

#### 添加菜单逻辑

既然你有了菜单布局和函数，你需要创建将两者结合起来的编程逻辑。如前所述，这需要 `case` 命令。

`case` 命令应根据从菜单预期的字符选择调用相应的函数。使用默认的 `case` 命令字符（星号）来捕获任何错误的菜单输入始终是个好主意。

以下代码说明了在典型菜单中 `case` 命令的使用：

```
menu
case $option in
0)
     break ;;
1)
     diskspace ;;
2)
     whosen ;;
3)
     memusage ;;
*)
     clear
     echo "Sorry, wrong selection";;
esac
```

此代码首先使用 `menu` 函数清除监视器屏幕并显示菜单。`menu` 函数中的 `read` 命令暂停直到用户在键盘上按下一个字符。完成之后，`case` 命令接管。`case` 命令根据返回的字符调用相应的函数。函数完成后，`case` 命令退出。

#### 将所有内容整合在一起

既然你已经看到了组成 Shell 脚本菜单的所有部分，让我们将它们放在一起，看看它们如何协同工作。这是一个完整菜单脚本的示例：

```
$ cat menu1
#!/bin/bash
# simple script menu

function diskspace {
     clear
     df -k
}

function whoseon {
    clear
    who
}

function memusage {
    clear
    cat /proc/meminfo
}

function menu {
    clear
    echo
    echo -e "\t\t\tSys Admin Menu\n"
    echo -e "\t1. Display disk space"
    echo -e "\t2. Display logged on users"
    echo -e "\t3. Display memory usage"
    echo -e "\t0. Exit program\n\n"
    echo -en "\t\tEnter option: "
    read -n 1 option
}

while [ 1 ]
do
    menu
    case $option in
    0)
        break ;;
    1)
        diskspace ;;
    2)
        whoseon ;;
    3)
        memusage ;;
    *)
        clear
        echo "Sorry, wrong selection";;
        esac
        echo -en "\n\n\t\tHit any key to continue"
        read -n 1 line
done
clear
$
```

此菜单创建三个函数，使用常见命令获取关于 Linux 系统的管理信息。它使用 `while` 循环不断循环通过菜单，直到用户选择选项 0，该选项使用 `break` 命令跳出 `while` 循环。

你可以使用此模板创建任何 Shell 脚本菜单界面。它提供了一种与用户交互的简单方式。

### 使用 select 命令

你可能已经注意到，创建文本菜单的一半挑战在于创建菜单布局并获取你输入的答案。Bash Shell 提供了一个方便的小工具，可以自动完成所有这些工作。

`select` 命令允许你从单行命令创建菜单，然后获取输入的答案并自动处理它。`select` 命令的格式如下：

```
select variable in list
do
    commands
done
```

`list` 参数是一个空格分隔的文本项列表，用于构建菜单。`select` 命令将列表中的每个项目显示为带编号的选项，然后显示由 `PS3` 环境变量定义的特定提示符用于选择。

以下是 `select` 命令工作的简单示例：

```
$ cat smenu
#!/bin/bash
# using select in the menu
function diskspace {
    clear
    df -k
}
function whoseon {
    clear
    who
}
function memusage {
    clear
    cat /proc/meminfo
}
PS3="Enter option: "
select option in "Display disk space" "Display logged on users" "Display memory usage" "Exit program"
do
    case $option in
        "Exit program")
            break ;;
        "Display disk space")
            diskspace ;;
        "Display logged on users")
            whoseon ;;
```

