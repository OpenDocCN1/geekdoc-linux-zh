
## if 结构

最常见的决策结构类型称为 `if` 结构；`if` 结构的语法如下所示：

```bash
if this is true
   then
      do these commands
   elif this is true
   then
      do these commands
   else
      do these commands
   fi
```

`if` 结构受一些常见规则约束：

- 1. `elif`（否则如果）和 `else` 语句是可选的。
- 2. 你可以有无限数量的 `elif` 语句。
- 3. *do these commands* 部分可以由多个命令组成，每行一个命令。
- 4. 为了提高可读性，*do these commands* 部分通常从文本文件的左侧进行缩进，但这并非必需。
- 5. 语句的末尾必须是一个反向的 “`if`”（`fi`）。
- 6. 前面所示 `if` 语法中的 *this is true* 部分可以是命令或测试语句：
    - 如果命令正确执行其功能，则返回 true。
    - 测试语句包含在方括号 `[ ]` 内或以单词 “test” 为前缀，用于测试系统中的某些条件。

下面输出展示了一个使用基本 `if` 结构来确保仅在 /etc/sample 目录成功创建时，才将 /etc/hosts 文件复制到 /etc/sample 目录的示例：

```bash
[root@server1 root]# cat testmkdir
#!/bin/bash
if mkdir /etc/sample
then
    cp /etc/hosts /etc/sample
    echo "The hosts file was successfully copied to /etc/sample"
else
    echo "The /etc/sample directory could not be created."
fi
```

```bash
[root@server1 root]# chmod a+x testmkdir
[root@server1 root]# ./testmkdir
The hosts file was successfully copied to /etc/sample
[root@server1 root]#
```

在上面的输出中，`mkdir /etc/sample` 命令始终会执行；如果它运行成功，shell 脚本将继续执行 `cp /etc/hosts /etc/sample` 和 `echo "The hosts file was successfully copied to /etc/sample"` 命令。如果 `mkdir /etc/sample` 命令未成功，shell 脚本将跳过并执行 `echo "The /etc/sample directory could not be created."` 命令。如果在上述 shell 脚本中 `fi` 之后还有更多行文本，无论 `if` 结构的结果如何，它们都将在 `if` 结构之后执行。

通常，使用 `if` 结构根据用户输入来改变程序流程是非常有用的。回顾前面使用的 `myscript` shell 脚本：

```bash
[root@server1 root]# cat myscript
#!/bin/bash
echo -e "Today's date is: \c"
date
echo -e "\nThe people logged into the system include:"
who
echo -e "\nthe contents of the / directory are:"
ls -F /
[root@server1 root]#
```

为了询问用户是否要显示 `/` 目录的内容，你可以在 `myscript` 文件中使用以下 `if` 结构：

```bash
[root@server1 root]# cat myscript
#!/bin/bash
echo -e "Today's date is: \c"
date
echo -e "\nThe people logged into the system include:"
who
echo -e "\nWould you like to see the contents of /?(y/n)...\)\c"
read ANSWER
if [ $ANSWER = "y" ]
then
    echo -e "\nthe contents of the / directory are:"
    ls -F /
fi
[root@server1 root]# ./myscript
Today's date is: Sat Jun  4 09:13:31 EDT 2005

The people logged into the system include:
root  pts/0  Jun  1 08:44 (3.0.0.2)
```

你想查看 / 目录的内容吗？(y/n) -> **y**

/ 目录的内容是：

```
bin/    etc/     lib/    mnt/    root/    sys/    udev/
boot/   home/    lost+found/    opt/    sbin/    tftpboot/   usr/
dev/    initrd/   misc/    proc/    selinux/   tmp/    var/
[root@server1 root]# _
```

从上文的输出中可以看到，测试语句 `[ $ANSWER = "y" ]` 用于测试 `ANSWER` 变量的内容是否等于字母 “y”。该变量中的任何其他字符都会导致这个 **test statement** 返回 false，并完全跳过目录列表。之前使用的比较类型称为字符串比较，因为两个值是按照字符字符串进行比较的；它由测试语句的操作符指示，在本例中是等号（`=`）。表 8-5 列出了测试语句中常用的操作符及其定义。

> **注意**
>
> 测试语句 `[ $ANSWER = "y" ]` 等同于测试语句 `test $ANSWER = "y"`。
>
> 确保在开始方括号之后和结束方括号之前有一个空格字符非常重要；否则，测试语句会产生错误。

**表 8-5 常见测试语句**

| 测试语句 | 返回 true 的条件： |
| :--- | :--- |
| `[ A = B ]` | 字符串 A 等于字符串 B。 |
| `[ A != B ]` | 字符串 A 不等于字符串 B。 |
| `[ A -eq B ]` | A 在数值上等于 B。 |
| `[ A -ne B ]` | A 在数值上不等于 B。 |
| `[ A -lt B ]` | A 在数值上小于 B。 |
| `[ A -gt B ]` | A 在数值上大于 B。 |
| `[ A -le B ]` | A 在数值上小于或等于 B。 |
| `[ A -ge B ]` | A 在数值上大于或等于 B。 |
| `[ -r A ]` | A 是存在且可读（r 权限）的文件/目录。 |
| `[ -w A ]` | A 是存在且可写（w 权限）的文件/目录。 |
| `[ -x A ]` | A 是存在且可执行（x 权限）的文件/目录。 |
| `[ -f A ]` | A 是存在的文件。 |
| `[ -d A ]` | A 是存在的目录。 |

你还可以使用特殊比较操作符 `-o`（OR）和 `-a`（AND）将任何测试语句与另一个测试语句组合，或者使用 `!`（NOT）操作符反转测试语句的含义；在测试语句中使用这些操作符的示例列在表 8-6 中。

> **注意**
>
> 一个测试语句中可以包含多个 `-o`、`-a` 和 `!` 操作符。

**表 8-6 测试语句中的特殊操作符**

| 测试语句 | 返回 true 的条件： |
| :--- | :--- |
| `[ A = B -o C = D ]` | 字符串 A 等于字符串 B 或者 字符串 C 等于字符串 D。 |
| `[ A = B -a C = D ]` | 字符串 A 等于字符串 B 并且 字符串 C 等于字符串 D。 |
| `[ ! A = B ]` | 字符串 A 不等于字符串 B。 |

考虑 `myscript` shell 脚本，在下面的示例中，如果用户输入 "y" 或 "Y"，你可以继续进行目录列表：

```bash
[root@server1 root]# cat myscript
#!/bin/bash
echo -e "Today's date is: \c"
date
echo -e "\nThe people logged into the system include:"
who
echo -e "\nWould you like to see the contents of /?([y/n]->)\c"
read ANSWER
if [ $ANSWER = "y" -o $ANSWER = "Y" ]
then
    echo -e "\nThe contents of the / directory are:"
    ls -F /
fi
```

```bash
[root@server1 root]# ./myscript
Today's date is: Sat Jun  4 09:13:31 EDT 2005

The people logged into the system include:
root    pts/0      Jun  1 08:44 (3.0.0.2)

Would you like to see the contents of /?(y/n) -> Y

The contents of the / directory are:
bin/     etc/     lib/      mnt/     root/    sys/       udev/
boot/    home/    lost+found/  opt/     sbin/    tftpboot/  usr/
dev/     initrd/  misc/     proc/    selinux/ tmp/       var/
[root@server1 root]# _
```

## case 结构

前面使用的 `if` 结构非常适合于选择有限的情况。但考虑前面使用的 `myscript` 示例，这次带有几个 `elif` 语句，根据用户输入执行不同的任务：

```bash
[root@server1 root]# cat myscript
#!/bin/bash
echo -e "What would you like to see?
Todays date (d)
Currently logged in users (u)
The contents of the / directory (r)"

Enter your choice(d/u/r)->c"
read ANSWER
if [ $ANSWER = "d" -o $ANSWER = "D" ]
then
    echo -e "Today's date is: \c"
    date
elif [ $ANSWER = "u" -o $ANSWER = "U" ]
then
    echo -e "\nThe people logged into the system include:"
    who
elif [ $ANSWER = "r" -o $ANSWER = "R" ]
then
    echo -e "\nThe contents of the / directory are:"
    ls -F /
fi
[root@server1 root]# _
```

```bash
[root@server1 root]# ./myscript
What would you like to see?
Todays date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice(d/u/r/)-> d
Today’s date is: Sat Jun  4 11:10:03 EDT 2005
[root@server1 root]# _
```

随着可用选择数量的增加，前面的 shell 脚本变得越来越难以阅读。因此，当提供几个选择时，使用 `case` 结构是很常见的。`case` 结构的语法如下所示：

```bash
case variable in
    pattern1 ) do this
              ;;
    pattern2 ) do this
              ;;
    pattern3 ) do this
              ;;
esac
```

`case` 语句将变量的值与几个不同的文本或数字模式进行比较。如果匹配，则执行位于模式右侧的命令（前面语法中的 *do this*）。与 *if* 结构一样，*case* 结构必须由反向的 “case”（*esac*）结束。

下面输出展示了一个使用 `case` 结构简化之前 `myscript` 示例的实例：

```bash
[root@server1 root]# cat myscript
#!/bin/bash

echo -e "What would you like to see?
Todays date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice(d/u/r/->)c*"
read ANSWER

case $ANSWER in
    d | D )  echo -e "\nToday’s date is: \c"
              date
              ;;
```
