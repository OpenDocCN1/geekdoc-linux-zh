
```bash
    IFS=":" read user pw uid gid name home shell <<< "$file_info"
    echo "User = \$User"
    echo "UID = \$uid"
    echo "GID = \$gid"
    echo "Full Name = \$name"
    echo "Home Dir. = \$home"
    echo "Shell = \$shell"
else
    echo "No such user \$user_name:" >&2
    exit 1
fi
```

此脚本提示用户输入系统中账户的用户名，然后显示在`/etc/passwd`文件的用户记录中找到的不同字段。脚本包含两个有趣的行。第一行是：

`file_info=$(grep "$user_name:" $FILE)`

该行将`grep`命令的结果赋值给变量`file_info`。正则表达式确保用户名只匹配`/etc/passwd`文件中的单行。

第二个有趣的行是：

```bash
IFS=":" read user pw uid gid name home shell <<< "$file_info"
```

该行由三部分组成：变量赋值、带有参数的`read`命令以及重定向运算符。我们先来看变量赋值。

`OLD_IFS="$IFS"`

壳允许在命令之前执行一个或多个变量赋值。这些赋值改变了后续命令的环境。赋值的影响是临时的；在我们案例中，`IFS`的值被改为冒号。或者我们可以这样编写：

```bash
OLD_IFS="$IFS"
read user pw uid gid name home shell <<< "$file_info"
IFS="$OLD_IFS"
```

在这里我们存储了`IFS`的值，分配了新值，执行`read`命令，然后恢复`IFS`。显然，将变量赋值放在命令前面是实现相同功能的更简洁的方法。`<<<`运算符指示在此字符串（here string）。在示例中，来自`/etc/passwd`的行被输入`read`命令的标准输入。我们可能会疑惑为什么这样做而不是：

## 你不能通过管道传递 `read`

虽然`read`命令通常从标准输入读取内容，但你不能这样做：
`echo "foo" | read`
我们期望这能正常工作，但并没有。`REPLY`将始终为空。这是为什么呢？

解释在于壳处理管道的方式。在`bash`（以及其他如`sh`的壳）中，管道会创建子壳。子壳是壳及其环境的副本，用于执行管道中的命令。在我们的示例中，`read`在子壳中执行。Unix类系统中的子壳会在进程执行期间创建环境的副本。当进程结束时，环境副本会被销毁。这意味着赋值的影响丢失了。使用在此字符串是绕过这种行为的一种方法。另一种方法将在第36章讨论。

### 输入验证

随着我们能够获取键盘输入，带来了一个额外的编程挑战：输入验证。很多时候，编写良好的程序和编写糟糕的程序之间的区别在于程序处理意外情况的能力。经常，意外情况以错误输入的形式出现。我们在上一章的评估程序中已经做过这一点，检查了整数的值并过滤了空值和非数字字符。在程序接收输入时，执行这些类型的编程检查是非常重要的，以防止无效数据。这对于多个用户共享的程序尤为重要。

### 验证输入

出于效率考虑，如果一个程序仅供作者使用一次且用于执行某些特殊任务，那么这些保护措施是可以被原的。即便如此，如果程序执行的是删除文件等危险任务，为了以防万一，包含数据验证也是明智的。

我们有一个验证各种类型输入的示例程序：

```bash
#!/bin/bash
### read-validate: validate input
invalid_input () {
  echo "Invalid input '$REPLY" >&2
  exit 1
}
read -p "Enter a single item "
### 输入为空（无效）
[[ -z $REPLY ]] && invalid_input
### 输入为多个项（无效）
(( $(echo $REPLY | wc -w) > 1 )) && invalid_input
# 输入是否为有效文件名？
if [[ $REPLY =~ ^[[:alnum:]\.-]+$ ]]; then
  echo "$REPLY' is a valid filename."
  if [[ -e $REPLY ]]; then
    echo "And file '$REPLY' exists."
  else
    echo "However, file '$REPLY' does not exist."
  fi
# 输入是否为浮点数？
if [[ $REPLY =~ ^?[[:digit:]]*\.[[:digit:]]+$ ]]; then
  echo "$REPLY' is a floating point number."
else
  echo "$REPLY' is not a floating point number."
fi
# 输入是否为整数？
if [[ $REPLY =~ ^-?[[:digit:]]+$ ]]; then
  echo "$REPLY' is an integer."
else
  echo "$REPLY' is not an integer."
fi
else
  echo "The string '$REPLY' is not a valid filename."
fi
```

## 28 – 读取键盘输入

该脚本提示用户输入一个项。随后对该项进行分析以确定其内容。正如我们看到的，该脚本使用了我们为止涵盖的许多概念，包括 shell 函数、`[[ ]]`、`(( ))`、控制运算符`&&`以及大量的正则表达式。

## 菜单

一种常见的交互类型被称为菜单驱动。在菜单驱动程序中，用户会看到一个选项列表，并被要求选择其中一个。例如，我们可以想象一个显示以下内容的程序：

```text
Please Select:

1. Display System Information

2. Display Disk Space

3. Display Home Space Utilization

0. Quit

Enter selection [0-3] >
```

利用我们从编写`sys_info_page`程序中中学到的知识，我们可以构建一个菜单驱动的程序来执行上述菜单上的任务：

```bash
#!/bin/bash
read-menu: a menu driven system information program
clear
echo ""
echo "Please Select:
1. Display System Information
2. Display Disk Space
3. Display Home Space Utilization
0. Quit"
read -p "Enter selection [0-3] > "
if [[ $REPLY =~ ^[0-3]$ ]]; then
  if [[ $REPLY == 0 ]]; then
    echo "Program terminated."
    exit
  fi
  if [[ $REPLY == 1 ]]; then
    echo "Hostname: $HOSTNAME"
    uptime
    exit
  fi
  if [[ $REPLY == 2 ]]; then
    df -h
    exit
  fi
  if [[ $REPLY == 3 ]]; then
    if [[ $(id -u) -eq 0 ]]; then
      echo "Home Space Utilization (All Users)"
      du -sh /home/*
    else
      echo "Home Space Utilization ($USER)"
      du -sh $HOME
    fi
    exit
  fi
else
  echo "Invalid entry." >&2
  exit 1
fi
```
