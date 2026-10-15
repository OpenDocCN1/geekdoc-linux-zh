
```
[root@server1 ~] # cat myscript
#!/bin/bash
echo -e "\nToday's date is: \
date
echo -e "\nPeople logged into the system include:"
who
echo -e "\nWould you like to see the contents of /?(y/n)-->\c"
read ANSWER
if [ $ANSWER = "y" -o $ANSWER = "Y" ]
then
echo -e "\nThe contents of the / directory are:"
ls -F /
fi
[root@server1 ~] ./myscript
Today's date is: Fri Aug 20 12:01:22 EDT
```

登录系统的用户包括：

```
user      tty1      2019-08-20 07:47
root      tty2      2019-08-20 11:36
```

Would you like to see the contents of `/?(y/n)`--> Y

```
The contents of the / directory are:
bin/  dev/  home/  media/  proc/  sbin/ sys/ var/
boot/ etc/  lib/  mnt/  public/ selinux/ tmp/
data/ extras/ lost+found/ opt/  root/  srv/  usr/
[root@server1 ~]#
```

## case 结构

之前构建的 `if` 结构适用于有限数量的选择。在接下来的示例中（使用了之前展示的 `myscript` 示例），`elif` 语句根据用户输入执行任务：

```
[root@server1 ~]# cat myscript
#!/bin/bash
echo -e "What would you like to see?\
Today's date (d)
Currently logged in users (u)
The contents of the / directory are (r)
Enter your choice(d/u/r)-->\c"
read ANSWER
if [ $ANSWER = "d" -o $ANSWER = "D" ]
then
echo -e "\nToday's date is \c"
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
[root@server1 ~]#
[root@server1 ~]# ./myscript
What would you like to see?
Today's date (d)
Currently logged in users (u)
The contents of the / (r)
Enter your choice(d/u/r) --> d
Today's date is: Fri Aug 20 12:13:12 EDT 2019
[root@server1 ~]#
```

随着选择数量的增加，前面的 shell 脚本变得越来越难以阅读。因此，在呈现多个选择时，使用 `case` 结构是常见的。`case` 结构的语法如下：

```
case variable in
pattern1 ) do this
      ;;
pattern2 ) do this
      ;;
pattern3 ) do this
      ;;
esac
```

`case` 语句将变量的值与多个文本或数字模式进行比较。当发生匹配时，将执行模式右侧的命令（在先述语法中为 `do this`）。与 `if` 结构一样，`case` 结构必须以反向的 "case" (`esac`) 结束。

以下输出显示了使用 `case` 结构简化之前示例的例子：

```
[root@server1 ~]# cat myscript
#!/bin/bash
echo -e "What would you like to see?
Today's date (d)
Currently logged in users (u)
The contents of the / directory are (r)
Enter your choice(d/u/r) -->\c"
read ANSWER
case $ANSWER in
d|D)
echo -e "\nToday's date is \c"
date
u|U)
echo -e "\nThe people logged into the system include:"
who
r|R)
echo -e "\nThe contents of the / directory are:"
ls -F /
*)
echo "Invalid choice"
;;
esac
[root@server1 ~]# ./myscript
What would you like to see?
Today's date (d)
Currently logged in users (u)
The contents of the / directory (r)
Enter your choice(d/u/r) --> d
Today's date is: Fri Aug 20 12:13:12 EDT 2019
```

*(注：原文在示例代码块中似乎漏掉了 `case $ANSWER in` 关键字，翻译时根据逻辑连贯性保持了结构清晰，但严格遵循原文内容)*

# 382 第 7 节 使用 BASH

`echo -e "哪个目录下包含你想要重命名的文件？ -->\\"`

`read DIR`

`for NAME in $DIR/*`

`do`

`mv $NAME $NAME.txt`

`done`

```
[root@server1 ~]# chmod a+x multiplerename
[root@server1 ~]# ./multiplename
```

哪个目录下包含你想要重命名的文件？ --> stuff

[root@server1 ~]# ls stuff

file1.txt file2.txt file3.txt file4.txt file5.txt file6.txt

file7.txt file8.txt

```
[root@server1 ~]#
```

当执行上一个示例中的 `for` 结构时，它会将字符串列表设置为 `stuff/*`（展开为 `file1 file2 file3 file4 file5 file6 file7 file8`）。它会创建一个 `NAME` 变量，将其值设置为 `file1`，并执行 `mv` 命令将 `file1` 重命名为 `file1.txt`。接下来，`for` 结构将 `NAME` 变量的值设置为 `file2`，并执行 `mv` 命令将 `file2` 重命名为 `file2.txt`。此过程重复直到所有文件处理完毕。

你还可以通过使用命令生成字符串列表来指定 `for` 结构的运行次数。`seq` 命令通常用于此目的；它生成一个递增的整数列表。例如，下面输出中的 脚本使用 `for` 循环显示了次消息：

```
[root@server1 ~]# seq 5
1
2
3
4
5
```

```
[root@server1 ~]# 
[root@server1 ~]# cat echorepeat
!/bin/bash
for NUM in `seq 5`
do
	echo "All work and no play makes Jack a dull boy"
done
[root@server1 ~]# chmod a+x echorepeat
[root@server1 ~]# ./echorepeat
```

# 第 7 节 使用 BASH 383

All work and no play makes Jack a dull boy

All work and no play makes Jack a dull boy

All work and no play makes Jack a dull boy

All work and no play makes Jack a dull boy

All work and no play makes Jack a dull boy

[root@server1 ~]#
