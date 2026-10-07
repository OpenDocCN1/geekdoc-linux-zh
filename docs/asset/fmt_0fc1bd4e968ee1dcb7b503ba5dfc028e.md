
```
$ cat /etc/passwd
root:0:0:The super user:/usr/bin/bash
steve:100:0:/users/steve:/usr/bin/bash
bin:3:3:The owner of system files:
cron:1:1:Cron Daemon for periodic tasks:
george:5:75:/users/george:/usr/bin/bash
np:300:300:/users/np:/usr/bin/bash
uooico:5:5:/users/uooico:/usr/bin/uooico
amg:6:6:The Owner of assignable services:
sysinfo:10:10:access to System Information:/usr/bin/bash
mail:301:301:/usr/mail
```

如果你想按用户名（每行的第一个字段）排序，只需执行该命令即可。

如果改为按冒号分隔的字段（包含你的用户 ID）对文件排序，你需要使用算术排序，跳过前两个字段 (`+2n`)，并指定该字符作为字段分隔符 (`-:`)。

```
$ sort -2n -t:/ /etc/passwd 按用户 ID 排序
root:0:0:The Super User:/usr/bin/bash
cron:1:1:Cron Daemon for periodic tasks:
bin:3:3:The owner of system files:
uooico:5:5:/users/uooico:/usr/bin/uooico
amg:6:6:The Owner of Assignable Services:
```

## 工具箱

```
$ sed 644 /etc/passwd > /tmp/passwd
$ mv /tmp/passwd /etc/passwd
mv: 444 mode denied
mv: cannot unlink /etc/passwd
```

自然地，`/etc/passwd` 是 Unix 系统中最重要的文件之一。因为只有超级用户被允许对该文件进行写入。这就是为什么 `mv` 命令失败了。

## 其他选项

`uniq` 的 `-c` 选项类似于带有选项的 `uniq`（即删除重复行），每行输出的前面都会显示该行在输入中出现的次数。

| 名字 | uniq -c | 出现次数 |
| :--- | :--- | :--- |
| Charlie | 1 |  |
| Emanuel | 1 |  |
| Fred | 1 |  |
| Lucy | 1 |  |
| Ralph | 1 |  |
| Tony | 2 |  |

## 练习

1: 下列正则表达式会匹配什么内容？

```
x*
xx
x(1,5)
x(5,)
x(10)
[0-9]*
[0-9]
[0-9][0-9]*
[A-Za-z][A-Za-z0-9]*
[A-Za-z0-9]{1,1}
*Regular
\.,.\|#
```

2: 下列命令的效果是什么？

```
who | grep 'mary'
who | grep 'mary'
grep 'tomilla' ch*
ls -1 | sort -c
sed 's/.*/ > text.out
sed 's/\/[H]ailix\/(TM)/g > text.out
date | cut -d: -f1-16
date | cut -c11-25 | sed 's/[0-9]\(1,2\)/\1/'
```

3: 编写命令完成

- a. 查找所有用户名至少四个字符的登录用户
- b. 查找系统中所有用户 ID 大于 99 的用户
- c. 查找系统中用户 ID 大于 99 的用户数量
- d. 按文件大小从大到小列出你目录中的所有文件

# 第 5 章：我们出发了

本章内容

- 脚本文件
- 变量
- 内置整数算术
- 练习

基于第 3 章“什么是 Shell？”的讨论，你应该意识到，每当你输入类似下面的内容时：

```
who | wc -l
```

你实际上是在为 shell 编写程序！这是因为 shell 正在解释命令行，识别管道符号，将第一个命令的输出连接到第二个命令的输入上，并启动这两个命令的执行。

在本章中，你将学习如何编写自己的命令以及如何使用 shell 变量。

## 脚本文件

shell 程序可以直接在终端中输入，例如：

```
$ who | wc -l
```

或者，可以先将其输入到一个文件中，然后由 shell 执行该文件。例如，假设你一天中需要多次查找登录用户的数量。每次需要信息时都输入一遍管道命令是不合理的，但为了示例起见，让我们使用文件 `nu`（number of users 的缩写），其内容就是之前显示的管道命令：

```
$ cat nu
who | wc -l
$
sh: nu: cannot execute
```

要执行文件 `nu` 包含的命令，你只需要将 `nu` 作为命令名称输入到 shell 中：

```
$ nu
sh: nu: cannot execute
```

哎！我们忘记提到了一点。在你以这种方式执行程序之前，你必须更改文件的权限并使其具有可执行性。这是通过 `chmod` 命令实现的。要给文件 `nu` 添加权限，你只需输入：

> 注意，这里的错误在不同的 shell 之间会有不同。

```
$ chmod 755 nu
```

## 我们出发了

`chmod` 命令的 `+x` 告诉 shell 将后面的文件设为可执行。shell 要求文件在被执行之前必须同时是可读和可执行的。

```
$ls -l nu
-rw-r--r-- 1 user group Jul 10 11:42 nu
chmod +x nu
$ls -l nu
-rwxr-xr-x 1 user group Jul 10 11:42 nu
```

现在你已经将其设置为可执行，请再次尝试：

```
$ nu
```

这次成功了。你可以将任何命令放入一个文件中，将该文件设为可执行，然后只需通过向 shell 输入其文件名即可执行其内容。这既简单又强大。标准的 shell 机制如 I/O 重定向和管道也可以应用于你自己的程序：

```
$ nu > tally
```

假设你正在处理一个名为 `stats` 的文件，每当你想要打印一份提案的新副本时，都需要以下命令序列：

```
$ cat stats | wc -l | sort
```

再次，你可以通过简单将此命令序列放入一个文件中——让它运行——每当你需要获取提案的新副本时只需使用该名称（标准输入由其发出）。在下一个示例中，假设你想编写一个名为 `stats` 的 shell 程序，打印日期和时间、登录用户数以及你的当前目录。你知道获取这些信息的三个命令序列是 `date`、`wc -l` 和 `pwd`：

```
$ cat stats
date
wc -l
pwd
chmod +x stats
```

你可以给 `stats` 添加一些 `echo` 命令来使输出更有信息量：

```
$ cat stats
echo The current date and time is: date
echo The number of users on the system is: wc -l
echo Your working directory is: pwd
$ stats
```

执行它：

the current date and time is: Jul 10 12:27

The number of users on the system is: 13

Your working directory is: /users/documents

记得 `echo` 不带任何参数时会跳过一行。不久后将看到如何让消息和数据显示在同一行，如下：

The current date and time is: Jul 10 12:27

## 注释

shell 语言如果没有注释语句是不完整的。注释是在程序内部插入备注或说明的方法，这些内容对程序的执行没有影响。

当 shell 在单词开头遇到特殊字符 `#` 时，它会将从 `#` 开始到行尾的所有内容视为注释并忽略。如果 `#` 在行首，整行都被 shell 视为注释。以下是有效注释的示例：

```
## Here is an entire comment line
who | wc -l      # count the number of users
```

```
## Test to see if the correct arguments were supplied
#
```

注释对于目的不直观或足够复杂的命令非常有用，如果你在一周后再次查看程序，可能会忘记它们为什么在那里或它们的作用是什么。明智地使用注释有助于 shell 程序更容易调试和维护——无论是对于你自己还是对于可能支持你程序的他人。

让我们回到 `stats` 程序并插入一些注释：

```
$ cat stats
## stats -- prints: number of users logged on, current working directory
echo The current date and time is: date
```

> 注意，# 可能是你的默认删除字符。如果是这样，要在 emacs 或 vi 等编辑器输入该字符，你需要在它前面加一个 \ 对其进行“转义”。或者，你可以使用 `escape` 命令更改你的删除字符。

## 我们出发了

```
echo
echo The number of users on the system is:
who | wc -l
```

```
echo
echo Your current working directory is:
pwd
```

额外的空行在程序空间上占用的微乎其微，但极大地提高了程序的可读性。shell 会直接忽略它们。

## 变量

与几乎所有的编程语言一样，shell 允许你将值存储在*变量*中。变量以字母、数字或下划线 `_` 开头，后面跟着零或多个字母、数字或下划线字符。

要在变量中存储一个值，你只需编写变量名，紧接着是一个等号，然后紧接着你想要存储在变量中的值：

```
variable=value
```

例如，要将值 1 赋值给 shell 变量，你只需要写：

```
count=1
```

将值 `/users/steve/bin` 赋值给 shell 变量 `my_bin`，你只需要写：

```
my_bin=/users/steve/bin
```

这里有几点很重要。首先，等号两边都不允许空格。记住这一点，尤其是当你习惯了在运算符周围插入空格时。在 shell 语言中，不能插入空格。

其次，与其他编程语言不同，shell 完全没有数据类型的概念。当你给 shell 变量赋值时，无论该值是什么，shell 都会将其解释为一个字符串。当你将 1 赋值给变量 `count` 时，shell 仅仅是将字符 1 存储在变量中，并没有存储一个整数值。如果你在用 C 或 Pascal 等语言进行编程，所有变量都必须声明。由于 shell 没有数据类型的概念，变量在使用之前不需要声明；你只需要在需要使用它们时赋值即可。正如你将在在本节后面部分看到的，shell 支持通过内置操作对包含字符串的 shell 变量进行操作。由于 shell 是一种解释型语言，你可以直接在终端上为变量赋值：

```
$count=1               将 1 赋值给 count
$ my_bin=/users/steve/bin  将 /users/steve/bin 赋值给 my_bin
$
```

现在你已经知道如何给变量赋值了，接下来是什么？Unix® Shell Programming, Third Edition。Unix® Shell Programming, Third Edition, ISBN: 0-672-32490-3 Prepared for architect@opensource.com. 此下载文件仅供个人使用，并受服务条款限制。任何其他用途均需版权所有者的事先书面许可。© 2003 Llikely Publishing。严禁未经的使用、复制和分发，否则将违反法律。保留所有权利。

## 显示变量

`echo` 命令用于显示存储在 shell 变量中的值。要这样做，你只需写：

```
echo $variable
```

`$` 对 shell 来说是一个特殊字符。如果 `$` 后面跟着一个有效的变量名，shell 将认为此指示该变量中存储的值应在该处被替换。因此，当你输入：

```
echo $count
```

shell 会将 `$count` 替换为其中存储的值；然后执行 `echo` 命令：

```
echo count
```

记住，shell 在执行命令之前会执行变量替换（见图 5.1）。你可以同时替换多个变量的值：

```
$ echo $my_bin
/users/steve/bin
$ echo $my_bin $count
/users/steve/bin 1
```

在第二个示例中，shell 替换了 `my_bin` 和 `count` 的值，然后执行 `echo` 命令（见图 5.2）。变量的值可以用于命令行的任何地方，如下面的示例所示：

```
$ ls $my_bin
text
$ pwd
/users/steve/documents/ 我们在哪里？
$ cd $my_bin 切换到我的 bin 目录
$ pwd
/users/steve/bin
```

Unix® Shell Programming, Third Edition.Unix® Shell Programming, Third Edition. ISBN: 0-672-32490-3 Prepared for architect@opengroup.edu. 此下载文件仅供个人使用，并受服务条款限制。任何其他用途均需版权所有者的事先书面许可。(C) 2003 O'Reilly Media。严禁未经的使用、复制和分发，否则将违反法律。保留所有权利。

```
$ number=99
echo There are number bottles of beer on the wall
There are 99 bottles of beer on the wall
$
```

这里是更多示例：

- `$ command=sort`
- `$ command names`
- Charles
- Emmanuel
- Fred
- Lucy
- Tony
- Tony
- `$ command=wc`
- `$ options=-l`
- `$ file=name`
- `$ command option $file`
- names

所以你看到，甚至命令的名字也可以存储在变量中。由于 shell 在确定要执行的程序名称及其参数之前执行替换，它会扫描行：

```
command option $file
```

并转换为：

```
wc -l names
```

然后它执行 `wc`，传递 `-l` 和 `names` 两个参数。变量可以赋值给其他变量，如下一个示例所示：

```
$ value=10
$ value2=value1
echo $value2
Value1
$ value2=$value1
$ echo $value2
10
```

没做对。

这样好多了。

记住，每当你想要使用该变量的值时，必须在变量名之前放置一个美元符号。

## 空值

当你尝试显示一个没有赋值的变量时，会发生什么？尝试一下。

```
$ echo noise
没有给它赋值
$
```

你没有得到错误信息。`echo` 命令到底显示了任何内容吗？让我们更精确地确定一下：

```
$ echo Scrooge:
用冒号包围它的值
```

$

所以你看到，`count` 的值没有被替换为字符。不包含值的变量被称为包含空值。当 shell 执行替换时，任何空值都会从命令行中完全移除，不留痕迹：

```
$ wc -1 names
names
$
```

这解释了为什么它行得通。有时你可能需要在程序中显式地将变量设为空。可以通过简单地为变量赋值来实现，例如：

```
dataflag=
```

或者，你可以在等号后列出相邻的引号。所以

```
dataflag=""
```

和

```
dataflag=''
```

都有给 `dataflag` 赋值空值的效果。注意，赋值

```
dataflag=" "
```

与上述三个不等，因为它给 `dataflag` 赋值了一个空格字符；这与赋值没有字符不同。

文件名替换与变量

这里有一个谜题：如果你输入：

```
x="*"
```

shell 是将字符存储到变量 `x` 中，还是将当前目录下所有文件的名称存储到变量 `x` 中？让我们试试看：

```
我们现在有哪些文件？
```

```
$ ls -n
addresses
intro
lotspaces
names
nu
numbers
phonebook
stat
x="*"
$ echo $x
addresses intro lotspaces names nu numbers phonebook stat
```

## 我们出发了

从这个小示例中可以学习到很多东西。当执行

```
x="*"
```

时，文件列表是存储在变量 `x` 中的，还是在执行

```
echo $*
```

时由 shell 执行了替换？

答案是，shell 在给变量赋值时并不会执行文件名替换。因此，

```
x="*"
```

将单个字符 `*` 赋值给 `x`。这意味着在执行 `echo` 命令时，是由 shell 执行了文件名替换。事实上，当执行

```
echo $*
```

时，发生的精确步骤顺序如下：

1. shell 扫描该行，将 `\*` 替换为 `x` 的值。
2. shell 重新扫描该行，遇到 `\*`，然后替换为当前目录下所有文件的名称。
3. shell 启动 `echo` 的执行，将文件列表作为参数传递（见图 5.3）。

这种求值顺序非常重要。记住，shell 首先进行变量替换，然后进行文件名替换，最后将该行解析为参数。

## ${variable} 结构
