
```bash
$ cat DoubleBrackets.sh
#!/bin/bash
# 使用双括号进行模式匹配
#
if [[ $BASH_VERSION == 5.* ]]
then
    echo "You are using the Bash Shell version 5 series."
fi
$
./DoubleBrackets.sh
nYou are using the Bash Shell version 5 series.
$
```

在前面的脚本中，注意使用了双等号（`=`）。这些双等号将右侧的字符串（`5.*`）视为模式，并应用模式匹配规则。双括号命令匹配 `$BASH_VERSION` 环境变量，以检查它是否以字符串 `5` 开头。如果是，命令执行成功，Shell 将执行相应的命令。

# Case 命令

通常情况下，你会发现自己正在尝试评估变量的值，在一组可能的值中寻找特定的值。在这种情况下，你最终会写出一个长长的 `then-else` 语句，如下：

```bash
$ cat LongIf.sh
#!/bin/bash
```

（续）

```bash
fi
$ ./LongIf.sh
Welcome christine
Please enjoy your visit.
$
```

`if-then` 语句继续进行 `if-then` 检查，为单变量比较寻找特定的值。

与其编写所有的 `elif` 语句来继续检查同一个变量的值，不如你使用 `case` 命令。`case` 命令以列表形式格式检查单个变量的多个值：

```bash
case variable
pattern1 | pattern2 commands1;
pattern3 commands2;
    *) default commands;
esac
```

`case` 命令将指定的变量与不同的模式进行比较。如果变量匹配模式，Shell 将执行该模式指定的命令。你可以在同一行列出多个模式，使用竖线运算符分隔模式。星号符号 `*` 是不匹配任何列出模式值的通配符。以下是将 `if-then-else` 程序转换为使用 `case` 命令的示例：

```bash
$ cat ShortCase.sh
#!/bin/bash
# 使用短的 case 语句
#
case $USER in
rich | christine
    echo "Welcome $USER"
    echo "Please enjoy your visit."
barbara | tim
    echo "Hi, $USER"
    echo "We're glad you could join us.";
testing)
    echo "Please log out when done with test.";
esac
echo "Sorry, you are not allowed here."
$
$ ./ShortCase.sh
Welcome christine
Please enjoy your visit.
$
```

`case` 命令提供了一种更清晰的方法来指定可能变量值的各种选项。

# 实例演练

在本节中，我们将描述一个脚本，该脚本将在本章中学过的结构化命令应用于实际用途——确定当前系统上可用哪些包管理器。它还根据已安装的包管理器引导，快速判断当前系统基于哪个 Linux 发行版。

为了进行分析，第一个脚本检查了标准的基于 Red Hat 的包管理器（`rpm`, `dnf` 和 `flatpak`）。它对每个包管理器都使用此命令，并在 `if` 条件语句中使用圆括号。如果找到了包管理器，则将该特定管理器的特殊布尔变量设置为 TRUE (`1`)，如果未找到，则设置为 FALSE (`0`)，如下所示：

（续）

```bash
（续）
#
else
  item_rpm=0
#
fi
[...]
if (which flatpak &>dev/null)
then
  item_flatpak=1
  echo "You have the flatpak application."
#
else
  item_flatpak=0
#
fi
[...]
```

对于 `dnf` 和 `yum` 还有特殊处理（见第 9 章“安装软件”），以防您在一个还没有 `dnf` 工具的旧版 Red Hat 发行版上运行脚本。注意在未找到 `dnf` 时使用了 `elif` 语句来检查 `yum`：

```bash
$ cat PackageMgr.sh
[...]
if (which dnf &>dev/null)
then
  item_dnfy=1
  echo "You have the dnf package manager."
#
elif (which yum &>dev/null)
then
  item_dnfy=1
  echo "You have the yum package manager."
else
  item_dnfy=0
#
fi
[...]
$
```

> 注意：`which` 命令使用了输出重定向，用于对发行版做出假设。错误重定向将在第 10 章详细介绍。

脚本完成包管理器分析后，它会计算出一个分数：

```bash
$ cat PackageMgr.sh
...
redhatscore=$item_rpm + item_dnfy + item_flatpak
...
$
```

它还涵盖了 Debian 管理器（`dpkg`, `apt`, `snap`），并确定了一个 Debian 分数，如下：

```bash
$ cat PackageMgr.sh
...
debianscore=$item_dpkg + item_aptget + item_snap
...
$
```

对这两个分数 `redhatscore` 和 `debianscore` 进行比较，并声明一个发行版类型：

```bash
$ cat PackageMgr.sh
...
if [debianscore -gt $redhatscore]
then
  echo "Most likely your Linux distribution is Debian-based."
elif [redhatscore -gt $debianscore]
then
  echo "Most likely your Linux distribution is Red Hat-based."
else
  echo "Unable to determine distribution base."
fi
...
$
```

```bash
item_flatpak=1
echo "You have the flatpak application container."
#
else
item_flatpak=0
#
fi
####
redhotscore=$[$item_rpm + $item_dfyum + $item_flatpak]
############################# Debian Checks #############################
#
echo
echo "Checking for Debian-based package managers &"
echo "application containers..."
####
if (which dpkg & /dev/null)
then
item_dpkg=1
echo "You have the basic dpkg utility."
#
else
item_dpkg=0
#
fi
####
if (which apt & /dev/null)
then
item_aptaptget=1
echo "You have the apt package manager."
#
elif (which apt-get & /dev/null)
then
item_aptaptget=1
echo "You have the apt-get/apt-cache package manager."
#
else
item_aptaptget=0
####
if (which snap & /dev/null)
then
item_snap=1
echo "You have the snap application container."
#
else
item_snap=0
#
fi
####
```

# 第二部分：Shell 脚本基础

（续上）
