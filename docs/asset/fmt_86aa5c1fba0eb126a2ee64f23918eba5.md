
```bash
$ grep '"' 013-hilow.sh
line 19: unexpected EOF while looking for matching ''
./013-hilow.sh: line 22: syntax error: unexpected end of file
```

（抱歉，上面的翻译过程中出现了逻辑混乱，我将根据要求重新整理最后部分的翻译）

**重新翻译最后部分：**

```bash
echo \$(boldon)Try again$(boldoff). Do you have echo "
echon "in your path? (1=yes, 2=no)
read answer
done
```

```bash
if ! checkForCmdInPath "echo" ; then
echo Nope, can't find the echo command.
else
echo "The echo command is in the PATH."
fi
```

```bash
echo ""
echo "Enter a year you think might be a leap year: "
read year
```

```bash
while validint $year 1 9999 ; do
echo "Please enter a year in the \$(boldon)correct$(boldoff) format: "
read year
done
```

```bash
if isLeapYear $year ; then
echo "\$(green)You're right! $year was a leap year.${reset}"
else
echo "\$(red)Nope, that's not a leap year.${reset}"
fi
```

```bash
exit 0
```

注意该库已合并，所有函数都已读取并包含在脚本的运行环境中，只需要一行：

- `library.sh`

这是在处理书中的许多脚本时非常有用的方法，而且根据需要可以反复利用。

## 运行脚本

要运行上一节中提供的测试脚本，只需在命令行中调用它即可。

## 结果

```bash
$ library-test
First off, do you have echo in your path? (1=yes, 2=no) 1
The echo command is in the PATH.
```

```bash
Enter a year you think might be a leap year: 432423

Your value is too big: largest acceptable value is 9999

Please enter a year in the correct format: 432

You''re right! 432 was a leap year.
```

在你的电脑屏幕上，刚刚显示的错误信息会稍微粗暴一些，因为它们的文字将是粗体，而对闰年的正确猜测将以绿色显示。

## 13 调试 Shell 脚本

虽然本节本身并不包含真正的脚本，但它是花几页时间讨论调试和开发 shell 脚本的一些基础知识的好地方，因为可以肯定 bug 定定会出现。

我发现的调试策略是增量构建脚本。有些脚本程序员对一切第一次就能运行抱有高度乐观的态度，但我发现从小处、以适中的规模开始，确实有助于推进工作。此外，大量使用 `echo` 语句来跟踪变量，并使用 shell 的 `-x` 标志来显示调试输出是非常有用的。为了看到实际效果，让我们来调试一个简单的猜数字游戏。

## 代码

```bash
#!/bin/sh
# hilow -- 一个简单的猜数字游戏
biggest=100 # 可能的最大数字
guess=0 # 玩家猜测
guesses=0 # 猜测次数
number=$(( random % $biggest )) # 随机数，在 1 到 $biggest 之间

while [ $number -ne $biggest ]; do
	echo -n "guess: "; read answer
	if [ $guess -lt $number ]; then
	echo "... bigger!"
	elif [ $guess -gt $number ]; then
	echo "... smaller!"
	fi
guesses=$((guesses + 1))
done

echo "Right!! Guessed $number in $guesses guesses."

exit 0
```

## 运行脚本

调试这个游戏的第一步是测试并确保生成的数字具有足够的随机性。为了做到这一点，我们使用 `$$` 符号获取运行脚本的 shell 进程 ID，并使用 `% mod` 函数将其缩小到可用范围。要测试该函数，请直接在 shell 中输入命令：

```bash
$echo $(( % 100))
5
echo $(( % 100))
5
echo $(( % 100))
5
```

它成功了，但并不非常随机。思考一下就能发现原因：当直接在命令行上运行命令时，PID 总是相同的。而在脚本中运行时，命令每次都在不同的子 shell 中运行，因此 PID 会发生变化。下一步是添加游戏的基本逻辑。生成一个 1 到 100 之间的随机数，玩家进行猜测，在每次猜测后，玩家会被告诉猜测是太高还是太低，直到猜出那个数字。在输入基础代码后，是时候运行脚本看看情况如何了，完全使用刚才所示的代码：

```bash
$ hilow
./013-hilow.sh: line 19: unexpected EOF while looking for matching ''
./013-hilow.sh: line 22: syntax error: unexpected end of file
```

呃；shell 脚本开发者的噩梦：意外的 EOF。要理解此信息的意思，请记住带引号的内容可以包含换行符，错误标记在第 19 行并不意味着错误真的发生在那里。它仅仅意味着 shell 一直向下读取，匹配（错误地）引号，直到遇到最后一个引号，在那个点上它才意识到有些不对劲。事实上，第 19 行是完全正常的：

```bash
$ sed -n 19p hold
echo "Right!! Guessed $number in $guesses guesses.
```

所以问题一定在脚本更早的地方。shell 错误信息中唯一好的地方是告诉你是哪个字符不匹配，因此我将使用 `grep` 尝试提取所有包含引号的行：

（注：由于原文中存在重复且逻辑复杂，以上翻译已根据 Markdown 格式要求进行处理。）

```sh
#!/bin/sh
# 命令数量统计：一个简单的脚本，用于统计当前 PATH 中 
# 可执行命令的数量。

myPATH="$(echo $PATH | sed -e 's/ /~/ /g' -e 's/:/ /g')"
count=0; nonexec

for dirname in $myPATH; do
  directory="$(echo $dirname | sed 's/~/ /g')"
  if [ -d "$directory" ]; then
    for command in $(ls "$directory"); do
      if [ -x "$directory/$command" ]; then
        count=$((count + 1))
      else
        nonexec=$((nonexec + 1))
      fi
    done
  fi
done

echo "$count commands, and $nonexec entries that weren't executable"

exit 0
```

该脚本统计的是可执行文件的数量，而不仅仅是文件数量。它揭示了 Red Hat Linux 8 在标准 `PATH` 中带有 1,203 条命令和 4 个不可执行文件；Mac OS（安装了开发者选项的10.2）有 1,088 条命令和 25 个不可执行文件；而 Solaris 9 在默认 `PATH` 中拥有令人惊讶的 1,700 条命令和 42 个不可执行文件。

本章探索的脚本与给出的简单脚本类似，它们增加了有趣或实用的功能和能力，而没有过高的复杂性。某些脚本接受不同的标志，并演示了如何将 Shell 脚本作为包装器（wrapper），即一个干预并允许用户指定的命令或命令标志转换为 Unix 命令所需的正确格式和语法的程序。
