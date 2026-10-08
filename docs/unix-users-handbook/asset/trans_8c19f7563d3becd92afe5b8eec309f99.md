
还有比较运算符，例如示例中使用的“<”，以及算术、位运算和逻辑运算符。随着你编写越来越多的 Shell 脚本，你将希望使用所有这些运算符。

在编写使用文件的 Shell 脚本时，有一组与文件相关的测试条件非常有用。使用 `- 运算符 文件名` 的格式，你可以使用表 11-3 中的测试。

## 表 11-3 文件名称测试运算符

| 运算符 | 含义 |
| :--- | :--- |
| r | 读取访问权限 |
| w | 写入访问权限 |
| x | 执行访问权限 |
| o | 所有权 |
| z | 零长度 |
| f | 是文件，不是目录 |
| d | 是目录，不是文件 |

下面的程序名为 **filetest**，它使用这些运算符来测试文件 `.profile`。由于 `.profile` 不可执行、非零长度且不是目录，我预计 **filetest** 会判定这些条件为假。

以下是 **.profile** 的详细列表：

```
martyp $ ls -al .profile
-rw-r--r-- 1 martyp staff 594 May 21 09:29 ../.profile
martyp $
```

以下是 Shell 脚本 **filetest** 的列表：

![](img/75f39fc91296b889c0653851accdfd46_768_0.png)

```
#!/bin/csh
#   Program to test file $1

if (-e $1) then
	echo "$1 exists"
else
	echo "$1 does not exist"
endif

if (-z $1) then
	echo "$1 is zero length"
else
	echo "$1 is not zero length"
endif

if (-f $1) then
	echo "$1 is a file"
else
	echo "$1 is not a file"
endif

if (-d $1) then
	echo "$1 is a directory"
else
	echo "$1 is not a directory"
endif

if (-o $1) then
	echo "you own $1"
else
	echo "you don't own $1"
endif

if (-r $1) then
	echo "$1 is readable"
else
	echo "$1 is not readable"
endif

if (-w $1) then
	echo "$1 is writable"
else
	echo "$1 is not writable"
endif

if (-x $1) then
	echo "$1 is executable"
else
	echo "$1 is not executable"
endif
```

这是一个测试文件的较为极端的例子；然而，我希望包含许多文件测试。

以下是使用 `.profile` 作为输入运行 `filetest` 的输出：

```bash
martyp $ filetest /home/martyp/.profile
/home/martyp/.profile exists
/home/martyp/.profile is not zero length
/home/martyp/.profile is a file
/home/martyp/.profile is not a directory
you own /home/martyp/.profile
/home/martyp/.profile is readable
/home/martyp/.profile is writable
/home/martyp/.profile is not executable
martyp $
```

在 `.profile` 上运行 `filetest` 的结果得出了我们预期的文件测试结果。

下一节介绍了一种使用 `switch` 进行决策的方法。

# 使用 `switch` 进行决策

你可以使用 `switch` 在 Shell 程序中进行决策。你可以使用 `switch` 来测试 Shell 程序的命令行参数或交互输入，如下面的示例所示。例如，如果你想在 Shell 程序中创建一个菜单，并且需要确定用户在运行此 Shell 程序时选择了哪个选项，你可以使用 `switch`。

`switch` 的语法如下所示：

```
switch (pattern_to_match)
    case pattern1
        commands
        breaksw
    case pattern2
        commands
        breaksw
    case pattern3
        commands
        breaksw
default
        commands
        breaksw
endsw
```

**pattern_to_match** 是你正在测试的用户输入，如果它等于 **pattern1**，则执行 **pattern1** 下的命令。如果 **pattern_to_match** 与 **pattern2** 相同，则执行 **pattern2** 下的命令，以此类推。如果 **pattern_to_match** 与任何 case 语句的模式之间没有匹配，则执行默认分支。下面的程序允许你通过其菜单在两个脚本中进行选择。这两个 Shell 程序是我们本章早些时候编写的。你可以扩展此脚本以包含你希望的任何数量的程序。此示例使用 **switch**：

```
#!/bin/csh
# Program pickscript to run some of
# the C shell scripts we've created
# Usage: pickscript
echo " -----------------------------------------"
echo "          Sys Admin Menu          "
echo "-----------------------------------------"
echo " 1               netcheck for network interface "
echo " 2             hostck to check connection     "
echo "                       to hosts in /etc/hosts       "
echo " ----------------------------------------"
echo " "
echo " Please enter your selection --> \c"

set pick = $<        # read input which is number of script
echo " "             # and assign to variable pick
switch ($pick)

    case 1              # if 1 was selected execute this
    $HOME/cshscripts/netcheck 5
    breaksw

    case 2              # if 2 was selected, execute this
    $HOME/cshscripts/hostck
    breaksw

    default
    echo "Please select 1 or 2 next time"
    breaksw

endsw
```

该程序允许我们在两个脚本之间进行选择以运行。让我们看一下运行此程序的示例：

```
martyp $ pickscript
--------------------------------------------------
			Sys Admin Menu
--------------------------------------------------

1		netcheck for network interface
2		hostck to check connection
			to hosts in /etc/hosts

--------------------------------------------------
Please enter your selection
1
Name	Mtu	Net/Dest	Address	Ipkts	Ierrs Opkts	Oerrs Collis Queue
le0	1500	sunsys	sunsys	314996747 0	17261251 52135 7580952
le0	1500	sunsys	sunsys	314996862 0	17261256 52135 7580952
le0	1500	sunsys	sunsys	314997189 0	17261263 52135 7580952
le0	1500	sunsys	sunsys	314997319 0	17261269 52135 7580952
le0	1500	sunsys	sunsys	314997420 0	17261272 52135 7580952
le0	1500	sunsys	sunsys	314997630 0	17261275 52135 7580952
le0	1500	sunsys	sunsys	314997774 0	17261278 52135 7580952
le0	1500	sunsys	sunsys	314997904 0	17261281 52135 7580952
le0	1500	sunsys	sunsys	314998020 0	17261284 52135 7580952
count has reached 9, run netcheck again to see lan0 status
martyp $
```

我们在运行 **pickscript** 时选择了选项 1。你可以将此程序作为运行你可能编写的许多 Shell 程序的基础。

# 调试 C Shell 程序

当你开始 C Shell 编程时，你可能会犯很多简单的语法相关错误。使用 `csh` 的 **-n** 选项，你可以让 C Shell 在无需执行的情况下检查你的程序的语法。我也使用 **-v** 选项来生成详细输出。这有时会导致信息过多，所以我先从 **-v** 开始，如果反馈结果太多，我就取消它。

下面的示例是早期的 `search1` 程序，其中包含检查是否提供了三个参数的内容。在检查 `$#argv` 是否等于 3 时，我遗漏了左括号。以下是程序的列表和显示错误的语法检查：

![](img/75f39fc91296b889c0653851accdfd46_773_0.png)

![](img/75f39fc91296b889c0653851accdfd46_773_1.png)

```
martyp $ cat search1
#!/bin/csh
# search
# Usage: search directory pattern files

if ($#argv !3 3 then    # if < 3 args provided
        echo "Usage: search directory pattern files"    # then print Usage
else
        echo " "    # else print line and
        cd $1    # change to search dir
        grep -n "$2" $3    # search for $2 in $3
        echo " "    # print line
endif

martyp $ csh -nv search1
if ( $#argv != 3 then
Too many ( 's
martyp $
```

`csh -nv` 执行了带有详细输出的语法检查。首先，打印出相关行，然后是一个告知该行存在什么问题的错误消息。在这种情况下，很明显我遗漏了左括号。

修复问题后，我可以使用 **-x** 运行该程序，它会立即回显所有命令。下面的示例显示了搜索程序的一次运行：

```
martyp $ csh -xv search1 shellprogs grep csh_hostck
if ( $#argv != 3 ) then
if ( 3 != 3 ) then

echo " "
echo

cd $1
cd /home/martyp/shellprogs
grep -n "$2" $3
grep -n grep csh_hostck
25:    /usr/sbin7ping $sys 64 1 | grep "is alive" > /dev/null
echo " "
echo

endif
endif
martyp $
```

你可以逐行跟踪正在发生的事情。以 25 开头的行是文件 **csh_hostck** 中包含 **grep** 的那一行，也就是说，如果程序没有使用 **-xv** 选项运行，你将会得到的输出。

我建议使用新的 Shell 程序执行语法检查（**-n**），然后仅当运行程序时得到意外结果时，才使用 **-x** 选项回显所有命令。调试选项在你编写 Shell 程序遇到问题的某个时刻肯定会帮助你。

![](img/75f39fc91296b889c0653851accdfd46_774_0.png)

