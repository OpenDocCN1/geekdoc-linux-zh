
> 提示 使用 `echo` 命令可以在当用户输入命令时让他们觉得某些事情正在发生，当命令没有输出时持续几秒或更长时间。

`echo` 命令在你想跟踪脚本时也有用。在关键点使用 `echo` 命令可以告诉你脚本发生了什么。这里是添加了 `echo` 命令的 `whatsup` 文件：

```bash
echo "Let's see who is on the system."

who

echo "Any appointments? "

calendar

date

echo "All done"
```

当你运行 `whatsup` 文件时，你会看到以下：

```text
$ whatsup

Let's see who is on the system.

sarah tty01 Dec 20 08:51

brad tty03 Dec 20 08:12

ernie tty07 Dec 20 08:45

Any appointments?

12/20 Sales meeting at 1:45

12/21 party after work!

Mon Dec 20 09:02 EST 1993

All done

$
```

使用注释：可能在你写了一个 shell 脚本一段时间没有使用后，你会忘记脚本在做什么以及如何完成任务的。在你的 shell 脚本中放入注释来解释任务以及任务是如何实现的。注释是你写给自己或阅读脚本的人的笔记。shell 会忽略注释；它们对人类很重要。

井号（`#`）向 shell 标志着注释的开始。从井号到行尾的所有字符都是该注释的一部分。这里是你可能对 shell 脚本注释的方式：

```bash
# Name: whatsup
# Written: 1/19/07, Patty Stygian
# Purpose: 显示谁登录了、安排、日期
echo "Let's see who is on the system."
who # 查看谁登录了
echo "Any appointments? "
calendar # 查看安排
date # 显示日期
echo "All done"
```

再次运行 shell 脚本，你会看到之前相同的结果。注释不会以任何方式改变 shell 脚本的行为。

# 在 Shell 程序中使用变量 (Using Variables in Shell Programs)

要使用变量，你必须知道如何给变量赋值以及如何访问存储在变量中的值。访问变量值非常直接，但有四种方法给变量赋值：

- 使用直接赋值
- 使用 `read` 命令
- 使用命令行参数
- 替换命令的输出

## 使用直接赋值

给变量赋值最直接的方法是编写一个类似下面的表达式：

```bash
myemail=edsgar@crty.com
```

该表达式将变量 `myemail` 赋值为 `edsgar@crty.com`。在等号（`=`）的两边都不要包含空格。给变量赋值的直接赋值方法格式如下：

```text
variable-name=variable-value
```

如果 `variable-value` 包含空格，请用引号将值括起来。例如，要将 `Room 21, Suite C` 赋值给变量 `myoffice`，请使用以下命令：

```bash
myoffice='Room 21, Suite C'
```

每当 shell 看到美元符号（`$`）后跟变量名时，它就会检索该变量的值。你可以看到以下两个语句被执行：

```bash
echo My e-mail address is $myemail
echo My office is $myoffice
```

假设你经常将文件复制到名为 `/corporate/info/public/sales` 的目录。要将名为 `current` 的文件复制到该目录，输入：

```bash
cp current /corporate/info/public/sales
```

为了方便操作，你可以使用以下表达式将长目录名赋值给变量 `corpsales`：

```bash
corpsales=/corporate/info/public/sales
```

现在，要将当前文件复制到该目录，你输入：

```bash
cp $corpsales
```

shell 将 `$corpsales` 替换为变量 `corpsales` 的值，然后执行复制命令。

## 使用 `read` 命令

`read` 命令读取下一行输入并赋值给变量。shell 脚本扩展了之前的 `corpsales` 示例，要求用户指定要复制的文件名：

```bash
# Name: copycorp
# Purpose: copy specified file to
# /corporate/info/public/sales
corpsales=/corporate/info/public/sales
echo Enter name of file to "copy" # 提示用户
read filename # 获取文件名
cp $filename $corpsales # 执行复制
```

`read` 命令会暂停脚本并等待键盘输入。当按下 `<Return>` 键时，脚本继续执行。如果在 `read` 命令等待输入时按下 `<Ctrl-d>`（有时表示为 "D"），则脚本将终止。

## 使用命令行参数

当 shell 解析命令时，它为命令行上的每个项附加变量名。命令行上的项是空格或制表符分隔的字符序列。（使用引号表示一组由空格分隔的字符代表一个项）。附加到命令行上的变量有 `$0`、`$1`、`$2` 直到 `$9`。这 10 个变量对应项在行中的位置。命令名是 `$0`，命令的第一个参数是 `$1`，以此类推。为了演示这一概念，请考虑以下 shell 脚本 `shovars`：

```bash
# Name: shovars
# Purpose: demonstrate command-line variables
echo $0
echo $1
echo $2
echo $3
```

现在假设你输入

`shovars -s hello "look at me" bart`

该 shell 脚本的输出为：

```text
shovars

hello bart!

look at me
```

在输出中，第一行是命令名（变量 `$0`），第二行是第二个和第四个参数（变量 `$2` 和 `$4`），最后一行是第三个参数（变量 `$3`）。

下面是一个更复杂的示例。该 shell 脚本首先删除一个文件，然后将其复制到 `/tmp` 目录，以便在需要时检索它：

```bash
# Name: safrm
# Purpose: copy file to directory /tmp and then remove it
# from the current directory
# first copy $1 /tmp
cp $1 /tmp
# 现在删除文件
rm $1
```

如果你输入 `safrm abc def`，只有 `abc` 会从当前目录中删除，因为 `safrm` 脚本只删除变量 `$1`。不过，你可以用 `$` 表示命令行上的所有参数。通过将每个 `$` 替换为 `*` 使 `safrm` 更通用。如果你输入 `safrm abc def xx guio`，四个文件（`abc`、`def`、`xx` 和 `guio`）都会从当前目录中删除。

## 替换命令的输出

你可以将变量赋值给执行的结果。例如，要将当前工作目录的名称存储在名为 `cwd` 的变量中，请输入：

```bash
cwd=`pwd`
```

注意 `pwd`（打印工作目录的命令）被反引号括起来，而不是单引号。

## 使用 Shell 脚本

以下 shell 脚本通过为文件名追加当前月份和年份来更改文件名：

```bash
# Name: stamp
# Purpose: rename file: append today's date to its name
# 将 td 设置为格式为 mmddy 的当前日期
td=$(date +%m%d%y)
# 重命名文件
mv $1 $1.$td
```
