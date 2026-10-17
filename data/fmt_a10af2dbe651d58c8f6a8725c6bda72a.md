
```
#!/bin/csh
# program to run netstat at every specified interval
# Usage: netcheck interval

set limit=9		# set limit on number times
			# to run netstat

echo " "
netstat -i | grep Name	# print netstat line with headings
set count=0
while ($count<$limit)	# if limit hasn't reached
			# limit run netstat
		netstat -i | grep le0
		sleep $1		# sleep for interval
				# specified on command line
		@ count++		# increment limit
end
echo "count has reached $limit, run netcheck again to see le0 status"
```

以下是 `netcheck` 程序的运行示例：

```
martyp $ netcheck 3
Name Mtu Net/Dest Address Ipkts Ierrs Opks Oerrs Collis Queue
le0 1500 sunsys sunsys 314374989 0 17252200 52135 7580906
le0 1500 sunsys sunsys 314375038 0 17252203 52135 7580906
le0 1500 sunsys sunsys 314375114 0 17252206 52135 7580906
le0 1500 sunsys sunsys 314375185 0 17252209 52135 7580906
le0      1500 sunsys      sunsys        314375257 0    17252212 52135 7580906
le0      1500 sunsys      sunsys        314375332 0    17252215 52135 7580906
le0      1500 sunsys      sunsys        314375444 0    17252218 52135 7580906
le0      1500 sunsys      sunsys        314375508 0    17252221 52135 7580906
le0      1500 sunsys      sunsys        314375588 0    17252224 52135 7580906
count has reached 9, run netcheck again to see le0 status
martyp $
```

![](img/75f39fc91296b889c0653851accdfd46_767_0.png)

`netcheck` 的输出以我们指定的三秒间隔产生九个 `netstat` 输出。请记住，当你在自己的系统上使用此程序时，可能需要修改 LAN 接口名称等信息。

该程序通过以下方式对表达式进行自增：

```
@ count++
```

如果表达式为真，则命令将会执行。`@count++` 是以下形式的赋值运算符：

```
@ variable_name operator expression
```

在这种情况下，变量首先通过 `=` 进行赋值，然后自动递增（`++`）。可以在变量上执行许多操作，如表 11-2 所述。

## 表 11-2 赋值运算符

| 操作 | 符号 | 示例 (`count` = 100) | 结果 |
|---|---|---|---|
| 存储值 | `=` | `@count=100` | 100 |
| 自动递增 | `++` | `@count++` | 101 |
| 自动递减 | `--` | `@count--` | 99 |
| 增加值 | `+=` | `@count+=50` | 150 |
| 减去值 | `-=` | `@count-=50` | 50 |
| 乘以值 | `*=` | `@count*=2` | 200 |
| 除以值 | `/=` | `@count/=2` | 50 |

还有比较运算符，例如示例中使用的`<`，以及算术、位运算和逻辑运算符。随着你编写越来越多的 Shell 脚本，你将希望使用所有这些运算符。

在编写使用文件的 Shell 脚本时，有一组与文件相关的测试条件非常有用。使用 `- 运算符 文件名` 的格式，你可以使用表 11-3 中的测试。

## 表 11-3 文件名称测试运算符

| 运算符 | 含义 |
| :--- | :--- |
| `r` | 读取访问权限 |
| `w` | 写入访问权限 |
| `x` | 执行访问权限 |
| `o` | 所有权 |
| `z` | 零长度 |
| `f` | 是文件，不是目录 |
| `d` | 是目录，不是文件 |

下面的程序名为 `filetest`，它使用这些运算符来测试文件 `.profile`。由于 `.profile` 不可执行、非零长度且不是目录，我预计 `filetest` 会判定这些条件为假。

以下是 `.profile` 的详细列表：

```
martyp $ ls -al .profile
-rw-r--r-- 1 martyp staff 594 May 21 09:29 ../.profile
martyp $
```

以下是 Shell 脚本 `filetest` 的列表：

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
