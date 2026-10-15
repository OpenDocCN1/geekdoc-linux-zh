
| `[ -gt B ]` | A 数值大于 B。 |

| `[ -le B ]` | A 数值小于等于 B。 |

| `[ -ge B ]` | A 是存在且可读的文件/目录（r 权限）。 |

| `[ -w A ]` | A 是存在且可写的文件/目录（w 权限）。 |

| `[ -x A ]` | A 是存在且可执行的文件/目录（x 权限）。 |

| `[ -f A ]` | A 是存在的文件。 |

| `[ -d A ]` | A 是存在的目录。 |

你还可以使用特殊运算符 `-o` (OR) 和 `-a` (AND) 将任何测试语句与其他测试语句组合，并使用 `!` (NOT) 运算符反转测试语句的含义；这些运算符在测试语句中的示例列于表 8-6。

一个测试语句中可以有多个 `-o`、`-a` 和 `!` 运算符。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_376_2.png)

# 表 8-6 测试语句中的特殊运算符

| 测试语句 | 满足时返回真 |
|---|---|
| `[ A=B -o C=D ]` | 字符串 A 等于字符串 B 或者字符串 C 等于字符串 D。 |
| `[ A=B -a C=D ]` | 字符串 A 等于字符串 B 且字符串 C 等于字符串 D。 |
| `[ !A=B ]` | 字符串 A 不等于字符串 B。 |

考虑到 `myscript` shell 脚本，如果用户在下面的示例中输入 "y" 或 "Y"，就可以继续列出目录：

```
[root@server1 root]# cat myscript
!/bin/bash
echo -e "Today's date is: \c"
date
echo -e "\nThe people logged into the system include:"
who
echo -e "\nWould you like to see the contents of /? (y/n)-->\c"
read ANSWER
if [ $ANSWER = "y" -o $ANSWER = "Y" ]
then
    echo -e "\nThe contents of the / directory are:"
    ls -F
fi
[root@server1 root]# ./myscript
Today's date is: Sat Jun 4 09:13:31 EDT 2005
```

登录系统的用户包括：

rootroot pts/0 Jun 1 08:44 (3.0.0.2)

Would you like to see the contents of /? (y/n)--> Y

The contents of the / directory are:

bin/ etc/ lib/ mnt/ root/ sys/ udev/

boot/ home/ lost+found/ opt/ sbin/ tftpboot/ usr/

dev/ initrd/ misc/ proc/ selinux/ tmp/ var/

[root@server1 root]#

### Case 结构 (The Case Construct)

之前使用的 `if` 结构适用于有限数量的选择。但考虑之前使用的 `myscript` 示例，这次使用几个 `elif` 语句来根据用户的输入执行不同的任务：

```
[root@server1 root]# cat myscript
!/bin/bash
echo -e "What would you like to see?\nToday's date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice (d/u/r)-->\c"
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
    echo -e "\nThe contents of the / directory are:\nls -F"
fi
[root@server1 root]# myscript
[root@server1]# ./myscript
What would you like to see?
Today's date (d)
Currently logged in users (u)
The contents of the / directory (r)
```

Enter your choice(d/u/r)--> d

Today's date is: Sat 4 11:10:03 EDT 2005

[root@server1 root]#

随着选择数量的增加，前面的脚本将变得越来越难以阅读。在呈现多个选择时，使用 `case` 结构是常见的做法。`case` 结构的语法所示：

```
case variable in
pattern1 ) do this
      ;
pattern2 ) do this
      ;
pattern3 ) do this
      ;
esac
```

`case` 语句将变量的值与几种不同的文本或数字模式进行比较。如果匹配成功，将执行模式右侧的命令（*在前面的语法中执行此操作*）。与 `if` 结构一样，`case` 结构必须用反向的 "case"（esac）结束。

下面的输出显示了使用 `case` 结构简化之前的 `myscript` 示例示例：

```
[root@server1 root]# cat myscript
!/bin/bash
echo -e "What would you like to see?
Today's date (d)
Currently logged in users (u)
The contents of the / directory 

Enter your choice (d/u/r)-->\c"
read ANSWER

```

case $ANSWER in

d | D ) echo -e "\nToday's date is: \c"

    date

    ;

u | U ) echo -e "\nThe people logged into the system include:"

    who

    ;

r | R ) echo -e "\nThe contents of the / directory are:"

    ls -F

    ;;

*) echo -e "\Invalid choice! \a"

    ;

esac

[root@server1]# ./myscript

What would you like to see?

Today's date (d)

Currently logged in users (u)

The contents of the / directory (r)
