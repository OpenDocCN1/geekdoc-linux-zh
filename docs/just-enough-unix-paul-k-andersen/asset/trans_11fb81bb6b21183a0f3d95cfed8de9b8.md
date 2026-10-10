

## 清单 24-3B
del 脚本

```sh
#!/bin/sh
# Delete a file interactively
filename=$1
if test ! -f $filename
then
    echo "There is no file \"$filename\"."
else
    echo "Do you want to delete \"$filename\"?"
    read choice
    if test $choice = y
    then
        rm $filename
        echo "\"$filename\" deleted."
    else
        echo "\"$filename\" not deleted."
    fi
fi
```

### 24.4 每日提醒系统：tickle

我们已经看到如何使用 calendar 实用程序来提醒自己重要事件。calendar 的一个局限在于，你必须单独输入每个事件及其日期。对于每天或每周发生的一次性例行事件，这可能是一个问题。对于提醒自己此类事件，下面的 tickle 脚本非常有用。它使用 date 命令来检查星期几，然后打印出相应的消息。

**清单 24-4A**
tickle 脚本概要。

> NAME
> tickle--每日提醒服务
> SYNOPSIS
> tickle
> DESCRIPTION
> 以下是 tickle 的概要：
> 选择 sh
> 使用 set 捕获来自 date 的输出
> 打印消息
> 检查天数 ($1) 并打印相应的消息

```bash
#!/bin/sh
# A daily reminder service
set `date`
echo "Remember for today:"
case $1 in
  Mon) echo "Plan the week.";;
  Tue) echo "Take clothes to the cleaners.";;
  Wed) echo "Attend group meeting.";;
  Thu) echo "Make plans for the weekend."
        echo "Pick up clothes at the cleaners.";;
  Fri) echo "Answer e-mail.";;
  Sat) echo "You should not be here working."
        echo "Finish your work and log off.";;
  Sun) echo "Call Grandma and Grandpa.";;
esac
```

**清单 24-4B**
tickle 脚本。

研究完概要后，创建脚本：

- 1. 使用文本编辑器创建脚本文件。打开一个名为 *tickle* 的文件并输入清单 24-4B 中显示的脚本。完成后保存并退出文件。

- 2. 使脚本可执行。使用 *chex* 来实现这一点：
  ```
  $ chex tickle (Return)
  ```
  *tickle* 现在可执行：
  ```
  -rwxr-xr-x 1 yourlogin 457 Date time tickle
  ```

- 3. 测试新脚本。输入 *tickle* 命令：
  ```
  $ tickle (Return)
  ```
  这应该会打印出当天相应的消息。但是，我们还没有结束。如果你必须记得输入 "*tickle*" 才能使用它，那么提醒服务就没太大用处。最好让 shell 每次登录时自动运行该脚本。

- 4. 如有必要，将文件 *tickle* 移至你的主目录。回想一下，变量 *HOME* 包含你的主目录路径：
  ```
  $ mv tickle $HOME (Return)
  ```

- 5. 修改你的登录初始化文件以执行 *tickle*。使用文本编辑器，将以下行添加到你的 *.login* 或 *.profile* 中：
  ```
  tickle
  ```

- 6. 执行你的登录初始化文件。根据需要使用 source 或 "dot" 命令：
  ```
  $ source .login (Return)
  $ . .profile (Return)
  ```
  你的 tickle 消息应该会显示出来。

### 24.5 改进的拼写检查程序：myspell

spell 程序非常有用，但它有一个严重的局限：它列出文件中（可能）拼写错误的单词，但不会告诉你在文件中的什么位置存在拼写错误的单词。清单 24-5A 概述了一个可以解决此问题的脚本。

**清单 24-5A**
myspell 脚本概要。

```text
NAME
    myspell -- an improved spelling-checker

SYNOPSIS
    myspell file

DESCRIPTION
    Here is the outline for myspell:

        Select sh
        Run spell on the file; for each misspelling
        do
            Run grep to find lines with misspellings
            Print the misspelled word
            Print the line(s) containing the misspellings
        done
```

**图 24-5B**
myspell 脚本。

```sh
#!/bin/sh
# An improved spelling-checker
file=$1
for word in `spell $file`
do
    line=`grep -n $word $file`
    echo "          "
    echo "Misspelled word: $word"
    echo "$line"
done
```

研究完概要后，创建脚本：

1. 使用文本编辑器创建脚本文件。打开一个名为 *myspell* 的文件并输入清单 24-5B 中显示的脚本。完成后保存并退出文件。
2. **使脚本可执行。** 使用 *chex* 来实现这一点：
   ```
   $ chex myspell (Return)
   ```
   *myspell* 现在可执行：
   ```
   -rwxr-xr-x 1 yourlogin 140 Date time myspell
   ```
3. **测试新脚本。** 在包含拼写错误的文件上尝试 *myspell*：
   ```
   $ myspell file (Return)
   ```

### 24.6 多次回显参数：echo.by

标准的 *echo* 命令只回显一次其参数。这里提供的脚本回显用户选择次数的参数。

**清单 24-6A**
*echo.by* 脚本概要。

```text
NAME
	echo.by-echo the arguments n times
SYNOPSIS
	echo.by n arguments(s)

DESCRIPTION
	Here is the outline for echo.by:

		Select sh
		Get $count from the command line ($1)
		Use shift to get rid of the first argument
		Get the message from the command line ($*)

		While $count is greater than 0
		do
			print the message
			subtract 1 from $count
		done
```

![](img/52d592fcd97ba67dcb2b4a36fde4eb4c_267_0.png)

请确保你理解了清单 24-6A 中的概要，然后创建脚本：

1. **使用文本编辑器创建脚本文件。** 打开一个名为 *echo.by* 的文件并输入清单 24-6B 中显示的脚本。完成后保存并退出文件。
2. **使脚本可执行。** 使用 *chex* 来实现这一点：
   ```
   $ chex echo.by (Return)
   ```

![](img/52d592fcd97ba67dcb2b4a36fde4eb4c_268_0.png)

```shell
#!/bin/sh
# Echo a line n times
count=$1
shift
message=$*

while test $count -gt 0
do
    echo $message
    count=`expr $count - 1`
done
```

*echo.by* 现在可执行：
```shell
-rwxr-xr-x 1 yourlogin 111 Date time echo.by
```

3. **测试新脚本。** 尝试以下操作：
   ```shell
   $ echo.by 5 Play it again, Sam. (Return)
   ```
   第一个参数 (5) 将被读取，然后命令行剩余的其余部分将重复五次：
   ```shell
   Play it again, Sam.
   Play it again, Sam.
   Play it again, Sam.
   Play it again, Sam.
   Play it again, Sam.
   ```

## 24.7 练习

1. 编写一个 shell 脚本 *cnohex*，通过移除文件的执行权限来逆转 *chex* 的效果。
2. 编写一个 shell 脚本 *private*，使用 *chmod* 更改文件的访问权限，使得只有所有者可以读取、写入或执行它。请务必在输出中标记说明对文件做了什么。
3. 编写一个 shell 脚本 *public*，逆转你在上一个练习中编写的 *private* 脚本的效果。
4. 修改 *del* 脚本，使其检测用户是否指定了要删除的目录。（提示：使用带有 *-d* 选项的 *test* 来测试目录。）
5. 重写 `tickle` 以使用 `if/then/elif.../fi` 结构。
6. 重写 `echo.by` 以使用 `until` 循环。
7. 如果尚未这样做，请编写并运行上一章中的示例 shell 脚本。

## 第八部分：
## UNIX 下的编程

# 25 UNIX 下的编程

UNIX 最初是由专业程序员编写供其他专业程序员使用的。因此，UNIX 提供了许多出色的编程工具也就不足为奇了。传统上，UNIX 系统配备了 C 编程语言。（UNIX 本身是用 C 编写的。）许多 UNIX 系统还提供 Fortran 和 Pascal 语言以及其他语言。

在本章中，我们将看到如何编写和运行 UNIX 下的 Fortran、Pascal 和 C 程序。

### 25.1 编程语言

*计算机程序* 是一组编码指令，告诉计算机如何执行某些任务。计算机（目前）不理解英语或任何其他人类语言。相反，计算机响应的是所谓的*机器语言*，其中一切均由二进制数表示——0 和 1 的组合。例如，考虑程序片段以二进制形式可能呈现的样子：

```text
00000000011000110000000000000011000
00000000000000000000111000000010010
00000000011100010000110000001000000
00100000110001100000000000000000001
```

显然，使用像这样的二进制代码进行编程是繁琐的。更好的替代方案是使用*汇编语言*进行编程，它符号化地表示机器的每个二进制指令。例如，前面的四行二进制代码可以用以下四行汇编语言表示：

```text
mult $6, $6
mflo $7
add $2, $7, $2
addi $6, $6, 1
```

