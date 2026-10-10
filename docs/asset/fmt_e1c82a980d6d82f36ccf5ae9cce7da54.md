
```bash
[root@server1 ~]# cat myscript
#!/bin/bash
echo -e "Today’s date is: \c"
date

echo -e "\nThe people logged into the system include:"
who

echo -e "\nWould you like to see the contents of /? (y/n) -- > \c"
read ANSWER
if [ $ANSWER = "y" -o $ANSWER = "Y" ]
then
    echo -e "\nThe contents of the / directory are:"
    ls -F /
fi
```

```bash
[root@server1 ~]# ./myscript
Today's date is: Fri Aug 20 12:01:22 EDT 2015

The people logged into the system include:
user1 tty1 2015-08-20 07:47 (:0)
root tty2 2015-08-20 11:36

Would you like to see the contents of /? (y/n) -- > Y

The contents of the / directory are:
bin/ dev/ media/ proc/ sbin/ sys/ var/
boot/ etc/ lib/ mnt/ public/ selinux/ tmp/
data/ extras/ lost+found/ opt/ root/ srv/ usr/

[root@server1 ~]# 
```

### case 结构

之前使用的 `if` 结构非常适合有限的选择数量。在以下示例中，使用前面展示的 `myscript` 示例，几个 `elif` 语句根据用户输入执行任务：

```bash
[root@server1 ~]# cat myscript
#!/bin/bash
echo -e "What would you like to see?
Today's date (d)
Currently logged-in users (u)
The contents of the / directory (r)

Enter your choice (d/u/r) -- > \c"
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
```

```bash
[root@server1 ~]# ./myscript
What would you like to see?
Today's date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice (d/u/r) --> d
Today's date is: Fri Aug 20 12:13:12 EDT 2015

[root@server1 ~]# 
```

随着可用选择数量的增加，上面的 shell 脚本变得越来越难以阅读。因此，在呈现多个选择时，通常使用 `case` 结构。`case` 结构的语法如下：

```bash
case variable in
    pattern1 ) do_this
              ;;
    pattern2 ) do_this
              ;;
    pattern3 ) do_this
              ;;
esac
```

`case` 语句将变量的值与几个不同的文本或数字模式进行比较。当发生匹配时，模式右侧的命令被执行（在前面的语法中为 `do_this`）。与 `if` 结构一样，`case` 结构必须由反向的“case”（ `esac` ）结束。

使用 `case` 结构简化之前 `myscript` 示例的一个如下输出所示：

```bash
[root@server1 ~]# cat myscript
#!/bin/bash
echo -e "What would you like to see?
Today's date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice (d/u/r) --> \c"
read ANSWER

case $ANSWER in
d | D ) echo -e "\nToday's date is: \c"
          date
          ;;
u | U ) echo -e "\nThe people logged into the system include:"
          who
          ;;
r | R ) echo -e "\nThe contents of the / directory are:"
          ls /
          ;;
* ) echo -e "Invalid choice!\n"
    ;;
esac
```

```bash
[root@server1 ~]# ./myscript
What would you like to see?
Today's date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice (d/u/r) --> d
Today's date is: Fri Aug 20 12:33:08 EDT 2015

[root@server1 ~]# 
```

前面的示例提示用户一个菜单，并允许用户选择一个项目，该项目随后被放入 `ANSWER` 变量中。如果 `ANSWER` 变量等于字母“d”或“D”，则执行 `date` 命令；但是，如果 `ANSWER` 变量等于字母“u”或“U”，则执行 `who` 命令，如果 `ANSWER` 变量等于字母“r”或“R”，则执行 `ls` 命令。如果 `ANSWER` 变量包含上述字母以外的任何内容，`*` 通配符元字符将匹配它并在屏幕上打印错误消息。与 `if` 结构一样，shell 脚本中跟在 `case` 结构之后的任何语句都会在 `case` 结构之后执行。

### && 和 || 结构

尽管 `if` 和 `case` 结构很灵活，但当程序执行期间只需要做一个决定时，使用 `&&` 和 `||` 结构速度更快。这些结构的语法列表如下：

```bash
command && command
command || command
```

对于前面的 `&&` 语法，只有当 `&&` 结构左侧的命令成功完成时，`&&` 结构右侧的命令才会被执行。`||` 语法的情况则相反；只有当 `||` 结构左侧的命令未成功完成时，`||` 结构右侧的命令才会被执行。

考虑本章节前面介绍的 `testmdir` 示例：

```bash
[root@server1 ~]# cat testmdir
#!/bin/bash
if mkdir /etc/sample
then
    cp /etc/hosts /etc/sample
    echo "The hosts file was successfully copied to /etc/sample"
else
    echo "The /etc/sample directory could not be created."
fi

[root@server1 ~]# 
```

你可以使用 `&&` 结构重写上述 shell 脚本，如下所示：

```bash
[root@server1 ~]# cat testmkmkdir
#!/bin/bash
mkdir /etc/sample && cp /etc/hosts /etc/sample
[root@server1 ~]#
```

上述 shell 脚本创建目录 `/etc/sample`，并且只有在 `mkdir /etc/sample` 命令成功执行的情况下，才将 `/etc/hosts` 文件复制到该目录中。你也可以使用 `||` 结构，当其中一个命令未能正常执行时生成错误消息：

```bash
[root@server1 ~]# cat testmkmkdir
#!/bin/bash
mkdir /etc/sample || echo "Could not create /etc/sample"
cp /etc/hosts /etc/sample || echo "Could not copy /etc/hosts"
[root@server1 ~]#
```

### 循环结构

要重复执行命令，你可以编写包含循环结构的 shell 脚本。与决策结构类似，循环结构会根据特定语句的结果改变程序的流程。但与决策结构不同，决策结构根据测试语句的结果执行程序的不同部分，而循环结构则简单地重复执行整个程序。虽然 `BASH` shell 中有几种可用的循环结构，但最常见的是 `for` 和 `while`。

#### for 结构

`for` 结构对 Linux 管理员来说是最有用的循环结构，因为它可以用来处理对象列表，例如文件、目录、用户、打印机等等。`for` 结构的语法如下：

```bash
for var_name in string1 string2 string3 ...
do
  these commands
done
```

当执行 `for` 结构时，它会创建一个变量（`var_name`），将其值设置为 `string1`，并执行位于 `do` 和 `done` 之间的命令，这些命令可以访问 `var_name` 变量。接下来，`for` 结构将 `var_name` 的值设置为 `string2`，并再次执行 `do` 和 `done` 之间的命令。随后，`for` 结构将 `var_name` 的值设置为 `string3`，并再次执行 `do` 和 `done` 之间的命令。只要还有字符串需要处理，此过程就会重复。因此，如果有三个字符串，`for` 结构将执行三次。如果有 20 个字符串，`for` 结构将执行 20 次。

以下示例使用 `for` 结构通过电子邮件向用户列表发送新的时间表：

```bash
[root@server1 ~]# cat emailusers
#!/bin/bash
for NAME in bob sue mary jane frank lisa jason
do
  mail -s "Your new project schedule" < newschedule $NAME
  echo "$NAME was emailed successfully"
done
[root@server1 ~]# chmod a+x emailusers
[root@server1 ~]# ./emailusers
bob was emailed successfully
sue was emailed successfully
mary was emailed successfully
jane was emailed successfully
frank was emailed successfully
lisa was emailed successfully
jason was emailed successfully
[root@server1 ~]#
```

当执行前述示例中的 `for` 结构时，它会创建一个 `NAME` 变量并将其值设置为 `bob`。然后执行 `mail` 命令，以“Your new project schedule”为标题，将 `newschedule` 文件的内容通过电子邮件发送给 `bob`。接下来，它将 `NAME` 变量设置为 `sue`，并执行 `mail` 命令向 `sue` 发送相同的电子邮件。此过程重复执行，直到最后一位用户收到邮件。

在 shell 脚本中，`for` 结构更常见的用途是处理多个文件。以下示例将指定目录中的每个文件重命名为包含 `.txt` 扩展名的文件名。

```bash
[root@server1 ~]# ls stuff
file1 file2 file3 file4 file5 file6 file7 file8
[root@server1 ~]#
[root@server1 ~]# cat multiplierename
#!/bin/bash
echo -e "What directory has the files that you would like to rename? --> \c"
read DIR
for NAME in $DIR/*
do
mv $NAME $NAME.txt
done
[root@server1 ~]# chmod a+x multiplierename
[root@server1 ~]# ./multiplierename
What directory has the files that you would like to rename? --> stuff
[root@server1 ~]# ls stuff
file1.txt file2.txt file3.txt file4.txt file5.txt file6.txt file7.txt
file8.txt
[root@server1 ~]#
```

当执行前一个示例中的 `for` 结构时，它将字符串列表设置为 `stuff/*`（这扩展为 `file1 file2 file3 file4 file5 file6 file7 file8`）。然后创建一个 `NAME` 变量，将其值设置为 `file1`，并执行 `mv` 命令将 `file1` 重命名为 `file1.txt`。接下来，`for` 结构将 `NAME` 变量的值设置为 `file2`，并执行 `mv` 命令将 `file2` 重命名为 `file2.txt`。此过程重复执行，直到处理完所有文件。注意，你还可以使用 `seq` 命令生成一个数字列表，以便在 `for` 循环中使用。

#### while 结构

`while` 结构是 shell 脚本中使用的另一种常见循环结构。与 `for` 结构不同，`while` 结构以测试语句开始。只要（或者说在……期间）测试语句返回真，循环结构内的命令就会被执行。当测试语句返回假时，`while` 结构内的命令停止执行。`while` 结构通常包含一个称为 `计数变量` 的变量，其值在每次循环时都会发生变化。为了让 `while` 结构正常工作，必须设置好条件，使得当计数变量达到某个值时，测试语句返回假。这可以防止循环无限执行。

`while` 结构的语法如下：

```bash
while this returns true
do
    these commands
done
```

以下示例说明了 `while` 结构的一般用法。

```bash
[root@server1 ~]# cat echoripeat
#!/bin/bash
COUNTER=0
while [ $COUNTER -lt 7 ]
do
    echo "All work and no play makes Jack a dull boy" >> /tmp/redrum
    COUNTER=`expr $COUNTER + 1`
done
[root@server1 ~]# chmod a+X echoripeat
[root@server1 ~]# ./echoripeat
[root@server1 ~]# cat /tmp/redrum
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
[root@server1 ~]#
```

上面所示的 `echoripeat` shell 脚本创建了一个名为 `COUNTER` 的计数变量，并将其值设置为 0。接下来，`while` 结构使用测试语句在循环内执行命令之前判断 `COUNTER` 变量的值是否小于 7。由于 `COUNTER` 变量的初始值为 0，它将文本 `All work and no play makes Jack a dull boy` 追加到 `/tmp/redrum` 文件，并将 `COUNTER` 变量的值递增为 1。注意 `expr` 命令周围的反引号，这是为了在数值上将 `COUNTER` 变量加 1 ($0 + 1 = 1$) 所必需的。由于此阶段 `COUNTER` 变量的值（1）仍小于 7，`while` 结构再次执行命令。此过程重复执行，直到 `COUNTER` 变量的值等于 8。

![](img/c27875544958897d817484d558c208c8_363_0.png)

你可以使用 `true` 或 `:` 代替 `test` 语句来创建无限执行的 `while` 结构。

### 章节总结

- 命令具有三个组件：标准输入（`stdin`）、标准输出（`stdout`）和标准错误（`stderr`）。并非所有命令都使用每个组件。

- 标准输入通常是从键盘获取的用户输入，而标准输出和标准错误默认发送到终端屏幕。

- 你可以使用重定向符号将命令的标准输出和标准错误重定向到文件。同样，你可以使用重定向符号将文件重定向到命令的标准输入。
