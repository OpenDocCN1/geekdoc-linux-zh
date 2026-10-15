
```bash
    echo "$REPLY is not an integer."
fi
```

## 菜单

一种常见的交互类型被称为菜单驱动。在菜单驱动程序中，用户会看到一个列表并被要求选择一个。例如，我们可以想象一个显示以下内容的程序：

1. 显示系统信息
2. 磁盘空间
3. 显示目录占用
4. 退出

`选择 [1-4] >`

利用我们从 `sys_info` 程序中学到的知识，我们可以构建一个菜单驱动的程序：

```bash
#!/bin/bash

## read-menu: 一个菜单驱动的系统信息

clear
echo ""
Please Select:
1. Display System Information
2. Disk Space
3. Display Home Utilization
4. Quit

read -p "Enter selection [1-4] > "

if [[ $REPLY =~ ^[1-4]$ ]]; then
    echo "Program terminated."
    exit
    elif [[ $REPLY == 1 ]]; then
        echo "Hostname: $HOSTNAME"
        uptime
        exit
    elif [[ $REPLY == 2 ]]; then
        df -h
        exit
    elif [[ $REPLY == 3 ]]; then
        if [[ $(id -u) -eq 0 ]]; then
            echo "Home Utilization (All Users)"
            du -sh /home/*
        else
            echo "Home Utilization ($USER)"
            du -sh $HOME
        fi
        exit
    fi
else
    echo "Invalid entry." >&2
    exit 1
fi
```

## 第 28 章 流程控制：使用 `WHILE` 和 `UNTIL` 进行循环

在上一章中，我们开发了一个菜单驱动的程序来生成各种类型的系统信息。该程序可以运行，但它仍然存在一个严重的易用性问题。它只会执行单次选择然后终止。更糟糕的是，如果选择了无效选项，程序将报错并终止，而没有给用户再次尝试的机会。如果我们能以某种方式构造程序，使其能够不断重复菜单显示和选择，直到用户选择退出程序，那会更好。

在本章中，我们将学习一种名为“循环”的编程概念，它可以用于使程序的某些重复执行。shell 提供了三个用于循环的复合命令。我们将在本章介绍其中两个，第三种将在第 33 章中介绍。

## 循环

日常生活充满了重复的活动。每天去上班、遛狗、切萝卜都是涉及重复一系列步骤的任务。让我们考虑切萝卜这种活动。如果我们用伪代码来表达这种活动，它看起来可能像这样：

1. 获取菜板。
2. 获取刀。
3. 将萝卜放在菜板上。
4. 拿起刀。
5. 移动萝卜。
6. 切萝卜。
7. 如果整个萝卜已切完，则退出，否则回到第 4 步。

步骤 4 到 7 构成一个循环。循环内的动作将重复，直到达到“整个萝卜已切完”这一条件。

### `while`

`bash` 可以表达类似的思路。假设我们想按顺序从 1 到 5 显示五个数字。一个 `bash` 脚本可以构造如下：

```bash
#!/bin/bash

## while-count: 显示一系列数字

count=1
while [ $count -le 5 ]; do
    echo $count
    count=$((count + 1))
done

echo "Finished."
```

执行此脚本时，它显示以下内容：

```text
@linuxbox ~$ while-count
1
2
3
4
5
Finished.
```

`while` 命令的语法为：

```text
while commands; do commands; done
```

就像 `if` 一样，`while` 会评估命令列表的退出状态。只要退出状态为 0，它就会执行循环内部命令。在上面的脚本中，变量 `count` 被创建并赋予了初始值 1。`while` 命令评估测试命令的退出状态。只要测试命令返回的退出状态 0，循环内的命令就会执行。在每个循环结束时，都会重复测试命令。在循环六次后，`count` 的值已增加到 6，测试命令不再返回退出状态 0，循环终止。程序继续执行循环后的下一个语句。

我们可以使用 `while` 循环来改进 `read-menu` 程序：

```bash
#!/bin/bash

while-menu: 一个菜单驱动的系统信息程序

DELAY=3 # 显示结果的秒数

while [[ $REPLY != 0 ]]; do
  clear

  cat << EOF_
    请选择：

    1. 显示系统信息

    2. 显示磁盘空间

    3. 显示主空间利用率

    0. 退出

EOF

  read -p "输入选择 [0-3] > "

  if [[ $REPLY =~ ^[0-3]$ ]]; then
    if [[ $REPLY == 1 ]]; then
      echo "Hostname: $HOSTNAME"
      sleep $DELAY
    fi

    if [[ $REPLY == 2 ]]; then
      df -h
      sleep $DELAY
    fi

    if [[ $REPLY == 3 ]]; then
      if [[ $(id -u) -eq 0 ]]; then
        echo "主空间利用率 (所有用户)"
        du -sh /home/*
      else
        echo "主空间利用率 ($USER)"
        du -sh $HOME
      fi
      sleep $DELAY
    fi

    echo "无效输入。"
    sleep $DELAY
  fi
done

echo "程序终止。"
```

通过将菜单封装在 `while` 循环中，我们能够让程序在每次选择后重复显示菜单。只要 `REPLY` 不等于 0，循环就会继续，并再次显示菜单，给用户提供另其他选择的机会。在每个动作结束时，都会执行一个 `sleep` 命令；程序将暂停几秒钟，以便看到选择的结果，然后清除屏幕并重新播放菜单。一旦 `REPLY` 等于 0（表示选择了“退出”），循环终止，执行将从随其后的行继续。

## 跳出循环

`bash` 提供了两个内置命令可以用于控制循环内部的程序流。`break` 命令立即终止循环，程序控制将从循环后的下一个语句恢复。`continue` 命令导致跳过循环的剩余部分，程序控制将从循环的下次迭代恢复。在这里我们看到一个结合了 `break` 和 `continue` 的 `while-menu` 程序版本：

```bash
#!/bin/bash

## while-menu2: 一个菜单驱动的系统信息程序

DELAY=3 # 显示结果的秒数

while true; do
  clear

  cat << EOF
  请选择：

  1. 显示系统信息

  2. 显示磁盘空间

  3. 显示主空间利用率

  0. 退出

EOF

  read -p " 输入选择 [0-3] > "

  if [[ $REPLY =~ ^[0-3]$ ]]; then
    if [[ $REPLY == 1 ]]; then
      echo "Hostname: $HOSTNAME"
      sleep $DELAY
    fi

    if [[ $REPLY == 2 ]]; then
      df -h
      sleep $DELAY
    fi

    if [[ $REPLY == 3 ]]; then
      if [[ $(id -u) -eq 0 ]]; then
        echo "主空间利用率 (所有用户)"
        du -sh /home/*
      else
        echo "主空间利用率 ($USER)"
        du -sh $HOME
      fi
      sleep $DELAY
    fi
  else
    echo "无效输入。"
    sleep $DELAY
  fi

  if [[ $REPLY == 0 ]]; then
    break
  fi
done

echo "程序终止。"
```

