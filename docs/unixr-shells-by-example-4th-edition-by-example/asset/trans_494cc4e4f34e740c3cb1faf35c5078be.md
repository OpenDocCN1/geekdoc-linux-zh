

## 图 11.2 标准输出和错误的重定向

```
$ grep john /etc/passwd > tmp 2> /dev/null
```

父 ksh 运行中
pid=1256
导出变量 HOME、PATH、USER 等
0: 标准输入，终端
1: 标准输出，终端
2: 标准错误，终端
ksh 的局部变量

父 ksh 休眠中
pid=1256
导出变量 HOME、PATH、USER 等
0: 标准输入，终端
1: 标准输出，终端
2: 标准错误，终端
ksh 的局部变量
wait(&status)

子 ksh 运行中
pid=1258
导出变量 HOME、PATH、USER 等
0: 标准输入，终端
1: 标准输出，终端
2: 标准错误，终端
ksh 的局部变量

fork()

wait(&status)

exec()

子进程处理重定向

父 ksh 休眠中
pid=1256
导出变量 HOME、PATH、USER 等
0: 标准输入，终端
1: 标准输出，终端
2: 标准错误，终端
ksh 的局部变量

子 ksh 作为子进程运行
pid=1258
导出变量 HOME、PATH、USER 等
0: 标准输入，终端
1: 标准输出，tmp
2: 标准错误，/dev/null
grep 的局部变量

父 ksh 运行中
pid=1256
导出变量 HOME、PATH、USER 等
0: 标准输入，终端
1: 标准输出，终端
2: 标准错误，终端
ksh 的局部变量

子进程退出

grep 代替子进程运行

## 示例 11.65

```
1 $ ls | more
< lists (ls) all files one page at a time (more) >
2 $ du -s | sort -n | sed -n '$p'
72388 /home/jody/ellie
3 $ cat | lp or cat | lpr
```

## 说明

- 1 `ls` 的输出通过管道传递给 `more` 命令，后者接受输入。输出一次显示一页。
- 2 `du` 命令（磁盘使用情况）的输出按数字排序，并通过管道传递给 `sed` 命令（流编辑器），后者只显示最后一行（`$p`）。
- 3 `cat` 命令从标准输入读取；其输出通过管道传递给行式打印机（SVR4 中为 `lp`，BSD 中为 `lpr`）。

### 11.14.1 此处文档与输入重定向

此处文档为 `mail`、`sort` 和 `cat` 等程序捕获内联输入。输入放在两个单词或符号之间。第一个单词前面是 UNIX 命令和 `<<` 符号。下一行是命令要接收的输入。最后一行是与第一个单词完全匹配的第二个单词。这个单词称为最终终止符，标记输入的结束。它的使用方式与 Ctrl-D 结束输入的方式相同。最终终止符前后不能有空格。如果第一个单词前面是 `<<`，则最终终止符前面可以有前导制表符（且只能是制表符）。通常，此处文档在 shell 脚本中使用，而不是交互式使用。此处文档的一个好用途是在脚本中创建菜单。

## 格式

```
UNIX command << TERMINATOR
lines of input
input
TERMINATOR
```

## 示例 11.66

```
(The Command Line)
1 $ cat << FINISH
2 > Hello there $LOGNAME
3 > The time is $(date)
4 > I can't wait to see you!!!
5 > FINISH
```

## 示例 11.66（续）

```
5 Hello there ellie
The time is Sun May 30 19:42:16 PDT 2004
I can't wait to see you!!
6 $
```

## 说明

- 1. UNIX/Linux 的 `cat` 程序将接受输入，直到单词 FINISH 单独出现在一行上。FINISH 被称为用户自定义终止符。
- 2. 在此处文档内进行变量替换。`>` 是 Korn shell 的辅助提示符。
- 3. 在此处文档内进行命令替换。
- 4. 用户自定义终止符 FINISH 标记 `cat` 程序输入的结束。它的前后不能有任何空格，并且单独位于一行上。
- 5. 显示 `cat` 程序的输出。
- 6. shell 提示符重新出现。

## 示例 11.67

```
(From the .profile File)
1 print "Select a terminal type"
2 cat << EOF
[1] sun
[2] ansi
[3] wyse50
3 EOF
4 read TERM
...
```

## 说明

- 1. 要求用户选择终端类型。
- 2. 菜单将出现在屏幕上。这是一个此处文档，意味着从现在开始，直到第 3 行匹配的 EOF 为止，输入将提供给 `cat` 命令。你可以使用一系列 `echo` 命令获得相同的结果，但从视觉上看，此处文档更美观。
- 3. EOF 是一个用户自定义终止符，标志着此处文档的结束。它必须位于左边缘，周围没有空格。
- 4. 将从键盘读取用户输入并赋值给 TERM。

