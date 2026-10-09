
让我们引入另一个命令 `CHOICE`，以及一些嵌套的 `IF` 和 `ELSE` 语句。通过创建一个新脚本 `mychoice.sh`，

### 第 1 步

`mychoice.sh` 脚本开始变得复杂得多。我们这里有一个四个选项列表，三个连接。如果用户选择选项键，将显示 `Mint`、`Iso` 和 `Awesome` 选项。如果不是，菜单将重复第四个选项。

```bash
user@~$ ./mychoice
echo "What is your name?"
read name
echo "Please choose an option 1, 2 or 3"
read choice
if [ $choice -eq 1 ]; then
  echo "Mint"
elif [ $choice -eq 2 ]; then
  echo "Iso"
else
  echo "Awesome"
fi
echo "Please choose an option 1, 2 or 3"
read choice
```

### 第 2 步
如果你遵循脚本，你就能根据我们已经涵盖的内容掌握其运行原理。`WHILE`、`IF` 和 `ELSE` 配合 `fi` 语句将运行选项，如果你选了错误的选项，它会带你回到开头。

### 第 3 步
你可以增加选项的数量，但你需要确保它们与 `IF` 语句的数量相匹配。脚本可能会很快变得看起来非常杂乱。这个长脚本是显示菜单的另一种方式，这次使用了时尚的色彩方案。

```bash
while true
do
  echo "What is your name?"
  read name
  echo "Please choose an option 1, 2 or 3"
  read choice
  if [ $choice -eq 1 ]; then
    echo "Mint"
  elif [ $choice -eq 2 ]; then
    echo "Iso"
  elif [ $choice -eq 3 ]; then
    echo "Awesome"
  elif [ $choice -eq 4 ]; then
    echo "Goodbye!"
    break
  else
    echo "Please choose an option 1, 2 or 3"
  fi
done
```

### 第 4 步
你可以在菜单脚本中使用方向键和回车键。每个选择都是一个返回信息的精确命令。在命令和选项周围进行尝试，看看你能设计出什么。这稍微超出了我们看过的，但它是关于可以实现内容的良好想法。

```
File Edit View Search Tools Help
choice-init /scripts/mychoice.sh
mychoice.sh
1. Mint
2. Iso
3. Awesome
4. Goodbye
Please choose an option 1, 2 or 3
choice-init /scripts/mychoice.sh
1. Mint
2. Iso
3. Awesome
4. Goodbye
```

## 创建备份脚本

Bash 脚本最常用的示例之一是备份任务。

一个非常简单的脚本看起来像这样，`~/bin/bash`，然后 `tar cvf ~/backups/`。该脚本创建了变量 `count`，在脚本开始时它的值为 0。然后 `WHILE` 循环会在 `count` 小于 100（`lt` 部分）时，通过 `echo` 命令打印 `count` 的当前值。

`UNTIL` 循环的工作方式与 `WHILE` 循环非常相似，大多数情况下是反的。因此，使用 `UNTIL` 数到一百的方法将是：`[ $count -gt 100 ]; do`。区别在于，直到 `count` 大于（`gt` 部分）100，它都会保持循环。

```bash
File Edit View Search Tools Documents Help
count.sh
#!/bin/bash
count=0
while [ $count -lt 100 ]; do
  echo $count
  count=$((count+1))
done
```

执行该脚本将在终端屏幕上列出 0 到 99 的数字；当计数器 100 时退出。使用 `FOR` 语句修改脚本，其工作原理非常相似。要在脚本中使用它，将下方截图中的文本输入到 `count.sh` 中。

你不限于数字到一百。你可以根据循环想要运行的次数，循环执行任何命令集。例如，重命名文件、创建文件夹，此脚本将使用 `FOR` 循环创建从 `folder1` 到 `folder 100` 的文件夹。

```bash
File Edit View Search Tools Documents Help
count.sh
#!/bin/bash
for count in {0..100}; do
  echo $count
done
```

我们在这里添加的内容是：`count in {0..100}; do` 意味着：对于变量 `count` 在从零到一百的数字范围内，开始循环。脚本的其他部分相同。运行此脚本，并在终端中查看输出结果。

再次使用 `FOR` 语句，我们可以通过操纵 `(0..100)` 部分来执行计数序列。这段代码实际上意味着（开始，结束，递增）；如果没有递增，则只是到结束位置的单个数字。例如，我们可以使用循环 `for count in {0..1000..2}; do;` 来数到 1000。

```bash
File Edit View Search Tools Documents Help
count.sh
#!/bin/bash
for count in {0..1000..2}; do
  echo $count
done
```

## 简易自动化与实用脚本

输入行行命令来获取系统信息、查找文件或批量重命名文件。

- 让我们尝试创建一个显示系统信息的脚本，这总是一个非常有用的东西。创建一个名为 `sysinfo.sh` 的新脚本，并输入 Xed 或你选择的编辑器。

```bash
#!/bin/bash
# 配置信息：
echo hostname
echo $(hostname)

# 文件系统磁盘使用：
echo df -h | grep '^Filesystem'

# 空闲和已内存：
echo free -m | grep 'Mem'

# 系统运行时间：
echo uptime

# 当前登录用户：
echo who

# 系统中 CPU 占用进程：
ps aux --sort=-cpu | head -n 6
```

- 虽然有终端命令可以帮助你查找特定的文件或文件夹……

```bash
#!/bin/bash
target=$1
read name

output=$(find "$target" -name "*$name*" 2>/dev/null)
if [ -n "$output" ]; then
  echo "$output"
else
  echo "未找到匹配项"
fi
```

# 创建 Bash 脚本 – 第 5 部分

### 第 5 步
执行脚本时，它会等待用户的输入，然后检查文件扩展名，例如 jpg、mp4 等。不过，这种方式并不友好。让我们让它变得更友好一点。不要使用 `echo` 配合 `echo -n "请输入你正在查找的文件扩展名："`，直接使用 `read` 命令即可。

### 第 8 步
当然，`colours.sh` 的输出结果可以混合在一起，根据你想要输出的内容带来不同的效果。例如，红色背景上的白色文字（或闪烁）。遗憾的是，闪烁效果在所有的终端（Terminal）上都不起作用，因此你可能需要切换到不同的终端。

```bash
#!//bin/bash
target=
# 请输入你正在查找的文件扩展名：
name=$(echo "$target" | grep -iname ".* 2>/dev/null)
if [ -z "$name" ]; then
  echo "Success"
else
  echo "No match found"
fi
```

| 正常文本 | |

| :--- | :--- |

| 默认 | 默认 |

| 默认 | 默认 |

| 默认 | 绿色 |

| 默认 | 黄色 |

| 默认 | 红色 |

| 默认 | 品红色 |

| 默认 | 蓝色 |

| 默认 | 默认 |

| 默认 | 浅灰色 |

| 默认 | 浅绿色 |

| 默认 | 浅黄色 |

| 默认 | 浅蓝色 |

| 默认 | 青色 |

| 默认 | 默认 |

| 默认 | 黑色 |

| 默认 | 绿色 |

| 默认 | 黄色 |

| 默认 | 蓝色 |

| 默认 | 红色 |

| 默认 | 品红色 |

| 默认 | 浅品红 |

| 默认 | |

### 第 6 步
这是一个使用 `install speak` 命令的有趣脚本。然后将文本输入到一个名为 `speak` 的新脚本中。正如你所见，这是这次第一个问候脚本的用处，它使用了输出中的变量。

```bash
#!//bin/bash
echo "Hello, what is your name?"
read name
echo "Thank you, and what is your surname?"
read surname
echo "Hello $name $surname!"
```

| | |

| :--- | :--- |

| 默认青色 | |

| 默认绿色 | |

| 默认黄色 | |

| 默认蓝色 | |

| 默认红色 | |

| 默认品红色 | |

| 默认浅品红 | |

| 默认 | |

| echo -id --scripts 5 | |

### 第 7 步
我们简要地看看如何在脚本的输出中加入一些颜色。由于要深入探讨颜色选项时间太长了，这里有一个可用颜色的脚本。创建一个新脚本 `colours.sh` 并输入以下文本（见下文）。

### 第 9 步
当我们制作花哨的脚本时，使用 Zen 来输出图形界面如何？将你看到的内容输入到一个名为 `mmenu.sh` 的新脚本中。赋予它可执行权限并运行它。你会看到几个对话框，最后跟着一个最终的方法。

```bash
#!//bin/bash
echo "Select a colour from your list"
select colour in "Red" "Green" "Blue" "Yellow" 
"Magenta" "Cyan" "White" "Exit"; 
if [ "$colour" != "Exit" ]; then
  echo "You chose $colour"
  echo -e "$colour$Test text"
fi
```

```bash
#!//bin/bash
echo "Select a colour"
case $1 in
  Red) 
    echo -e "\e[31mRed\e[0m"
  Green) 
    echo -e "\e[32mGreen\e[0m"
  Blue) 
    echo -e "\e[34mBlue\e[0m"
  Yellow) 
    echo -e "\e[33mYellow\e[0m"
  Magenta) 
    echo -e "\e[35mM\e[0m"
  Cyan) 
    echo -e "\e[36mCyan\e[0m"
  White) 
    echo -e "\e[37mWhite\e[0m"
  *) 
    echo "Invalid option selection"
esac
```

### 第 10 步
虽然我们在 bash 脚本中编写内容并不是我们接触过的领域，但它是完全可能的，尽管只是很基础的水平。如果你在玩游戏，尝试 `wget http://proxy.regnet.com/linux/houseken.sh`，赋予可执行权限并运行它。这很有礼貌，由 Martin Buchanan 编写，我们相信你可以做到的。这里：标题屏幕是 Base4 格式

![](img/b810837b9059fc96b3c0bd60b035eb13_76_0.png)

Linux 编码与编程

# Pi x Linux = 完美结合

当树莓派处于开发阶段时，其设计者需要确保他们创造的硬件不仅仅是一个廉价但小小的电脑，还能提供更多功能。

树莓派在功能上需要是灵活的，它需要有空间成长为更具雄心的项目概念和想法，而目标是以尽可能简单的方式来实现。创建一个通用的学习平台，让任何年龄的学生都能轻松与之交互，同时学习编程、电子和计算等新概念。自然地，一旦硬件开发完成，操作系统的选择只有一个代码，Linux。

Linux 的多功能性是传奇。这个不可思议的核心是如此具有塑性，以它可以引导向计算的任何方面，从超级计算到机器人。

# 命令行快速参考

当你开始全面使用 Linux 时，你会很快发现 Ubuntu、Mint 等系统的图形界面对于很多任务来说很棒，但并不是所有任务都适合它们。理解如何使用命令行不仅能加深你对 Linux 的理解，还能提升你对编码和编程的整体认知。你的命令行快速参考指南旨在帮助你更快地掌握 Linux。

## 前 10 大命令

这些命令可能不是每个人最常用的，但对于许多 Linux 和命令行用户来说，它们无疑会频繁出现。

`cd` 是你在 Linux 命令行中使用频率最高的命令之一。它允许你更改工作目录。使用它可以在文件系统的层级结构中移动。你也可以使用 `chdir`。

`mv` 命令将文件移动到不同的位置或重命名文件。例如 `mv file sub` 将原始文件重命名为 `sub`；`mv ~/Desktop` 将文件 'sub' 移动到你的桌面目录而不重命名它。如果你想重命名文件，必须指定一个新名称。

`ls` 显示当前目录下的文件。配合某些选项使用，它可以让你查看文件大小、创建时间等，例如 `ls -l` 会显示主目录下的文件。

`chown` 更改每个指定文件的用户或组所有者。如果只给出所有者（用户名或数字 ID），则将更改每个指定文件的所有者组。

`cp` 用于复制文件和目录。例如，`cp file sub` 会创建一个该文件的精确副本并以其原始名称命名。

`chmod` 更改列出的文件的权限。权限基于一个简单的系统。你可以为用户、组和和其他世界设置读取、写入和执行的权限。

`pwd` 命令打印当前工作目录的完整路径（“打印工作目录”）。注意 `pwd` 也会在标题栏中显示此信息。

`rm` 删除文件和目录。删除过程是将文件从存储设备上解除，并将其标记为未来可以使用。换句话说，删除文件会增加磁盘上的可用空间。

`clear` 命令在可能的情况下清除屏幕。它让终端环境重新类型，然后确定如何清除屏幕。这等同于在使用 shell 时输入 Ctrl+L。

`mkdir` 是“make directory”的缩写，用于在文件系统中创建目录（如果目录不存在）。例如，在调用 `mkdir` 时可以一次性创建多个目录。

## 有用的帮助/信息命令

当你尝试学习更多关于系统或你在 Linux 下运行的程序时，以下命令非常有用。你可能不需要每天使用它们，但当你需要时，它们将是无价之。

- `free` 命令显示系统中空闲和已用物理内存及交换内存的总量。例如，`free` 使用兆字节提供信息。

- `sed` 命令打开流编辑器。流编辑器用于对输入流（文件或管道的输入）执行文本转换。

- `df` 命令显示所有分区的的文件系统磁盘空间。`df -h` 命令可能是最有用的（`-h` 意味着人类可读）。

- `adduser` 命令向系统添加新用户。类似地，`addgroup` 向系统添加新用户组。

- `top` 程序提供运行中系统的动态实时视图。它可以显示系统摘要信息，以及进程列表。

- `deluser` 命令从系统中删除用户。要删除用户的文件和家目录，你需要添加 `-remove-` 选项。

- `uname` 命令配合 `-a` 选项可以打印所有系统信息，包括机器名称、内核版本和以及其他一些细节。

- `delgroup` 命令从系统中删除用户组。你不能删除作为用户主组的组。

- `ps` 命令允许你查看在机器上运行的所有进程。每个操作系统的 `ps` 版本略有不同，但功能都相同。

- `man man` 命令调出 `man` 命令的手页条目，这是开始使用它的绝佳起点。

- `grep` 命令允许你在多个文件中搜索特定的搜索模式，然后打印匹配的行。例如：`grep blah file`。

- `man intro` 命令特别别用。它显示《用户命令介绍》，这是一份关于 Linux 命令行编写得很好且相当简洁的介绍。

## Linux 命令 A-Z

Linux 命令实际上有数以千计，虽然这不是一个完整的 A-Z 列表，但它包含了你最可能需要的许多命令。你可能会发现自己最终会反复使用一组较少的命令，但在拥有整体知识后，这些命令仍然非常有用。

### A

| | | | |

| :--- | :--- | :--- | :--- |

| adduser | 添加新用户 | dd | 数据转储，转换并复制文件 |

| arch | 打印机器架构 | diff | 显示两个文件之间的差异 |

| awk | 文本处理 | | |

### B

| | | | |

| :--- | :--- | :--- | :--- |

| bc | 任意精度计算器 | du | 磁盘占用 |

### C

| | | | |

| :--- | :--- | :--- | :--- |

| cat | 连接并合并文件 | date | 日期和时间 |

| chdir | 更改工作目录 | dc | 十进制计算器 |

| chgrp | 更改组所有权 | | | 格式化文本 |

| chroot | 更改根目录 | fsck | 文件系统检查和修复 |

| cp | 复制文件 | | |

### D

| | | | |

| :--- | :--- | :--- | :--- |

| diff | 比较两个文件 | | |

| dirname | 获取目录名 | | |

### E

| | | | |

| :--- | :--- | :--- | :--- |

| echo | 打印消息 | ed | 编辑器 |

| env | 显示环境变量 | | |

### F
