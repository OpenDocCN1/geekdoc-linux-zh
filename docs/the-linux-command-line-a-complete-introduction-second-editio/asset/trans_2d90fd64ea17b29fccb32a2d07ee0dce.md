

```
2. Display Disk Space
3. Display Home Space Utilization
0. Quit
"

read -p "Enter selection [0-3] > "

if [[ "$REPLY" =~ ^[0-3]$ ]]; then
    if [[ "$REPLY" == 0 ]]; then
        echo "Program terminated."
        exit
    fi
    if [[ "$REPLY" == 1 ]]; then
        echo "Hostname: $HOSTNAME"
        uptime
        exit
    fi
    if [[ "$REPLY" == 2 ]]; then
        df -h
        exit
    fi
    if [[ "$REPLY" == 3 ]]; then
        if [[ "$(id -u)" -eq 0 ]]; then
            echo "Home Space Utilization (All Users)"
            du -sh /home/*
        else
            echo "Home Space Utilization ($USER)"
            du -sh "$HOME"
        fi
        exit
    fi
else
    echo "Invalid entry." >&2
    exit 1
fi
```

该脚本在逻辑上分为两个部分。第一部分显示菜单并输入用户的响应。第二部分识别响应并执行所选操作。注意本脚本中使用了 exit 命令。在这里使用它是为了防止脚本在操作执行后继续执行不必要的代码。在程序中存在多个退出点通常是不好的做法（它使程序逻辑更难理解），但在本脚本中它可行。

## 总结

在本章中，我们迈出了实现交互性的第一步，允许用户通过键盘向我们的程序输入数据。利用迄今为止介绍的技术，可以编写许多有用的程序，例如专用计算程序和用于深奥命令行工具的易于使用的前端。在下一章中，我们将在菜单驱动程序概念的基础上进行扩展，使其变得更好。

## 额外学分

仔细研究本章中的程序并完全理解它们的逻辑结构非常重要，因为接下来的程序会越来越复杂。作为练习，请使用 test 命令而不是 [[ ]] 复合命令重写本章中的程序。提示：使用 grep 来评估正则表达式并评估退出状态。这将是一个很好的练习。

## 29

## 流程控制：使用 while/until 进行循环

![](img/314a0280bc10c5c0d45be132de172677_495_0.png)

在上一章中，我们开发了一个菜单驱动程序来生成各种系统信息。该程序可以工作，但仍然存在一个显著的可用性问题。它只执行一次选择然后终止。更糟糕的是，如果做出无效选择，程序会带着错误终止，而不给用户重试的机会。如果我们能以某种方式构建程序，使其能够重复显示菜单和选择，直到用户选择退出程序，那就更好了。

在本章中，我们将研究一个称为循环的编程概念，可用于使程序的某些部分重复。shell 提供了三个用于循环的复合命令。我们将在本章中介绍其中两个，第三个将在后面的章节中介绍。

## 循环

日常生活充满了重复的活动。每天去上班、遛狗和切胡萝卜都是涉及重复一系列步骤的任务。让我们考虑切胡萝卜。如果我们用伪代码表达这种活动，它可能看起来像这样：

- 1. 拿切菜板。
- 2. 拿刀。
- 3. 将胡萝卜放在切菜板上。
- 4. 举起刀。
- 5. 推进胡萝卜。
- 6. 切胡萝卜。
- 7. 如果整个胡萝卜都被切了，则退出；否则转到步骤 4。

步骤 4 到 7 形成了一个循环。循环内的操作会重复执行，直到满足“整个胡萝卜被切”这一条件。

## while

bash 可以表达类似的想法。假设我们想按顺序从 1 到 5 显示五个数字。一个 bash 脚本可以构造如下：

```
#!/bin/bash

# while-count: display a series of numbers

count=1

while [[ "$count" -le 5 ]]; do
    echo "$count"
    count=$((count + 1))
done
echo "Finished."
```

执行时，该脚本显示如下内容：

```
[me@linuxbox ~]$ while-count
1
2
3
4
5
Finished.
```

while 命令的语法如下：

