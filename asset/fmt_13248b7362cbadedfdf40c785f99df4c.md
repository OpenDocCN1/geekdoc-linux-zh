
> When will this end?
> When the quote is matched
> oh'

```

```

oh'

```

## 示例 13.73（续）

```

hi there

how are you?

When will this end?

When the quote is matched

oh

```

```

2 $ echo Don\'t you need '$5.00'?
Don\'t you need $5.00?

```

```

3 $ echo 'Mother yelled, "Time to eat!"'
Mother yelled, "Time to eat!"

```

# 说明

- 1 这一行中单引号没有匹配。`bash` shell 产生一个二级提示符，正在等待引号匹配。
- 2 单引号保护所有元字符不被解释。`Don\'t` 中的撇号用反斜杠转义（反斜杠保护单个字符，而不是字符串）。否则，它会与 `$` 前面的单引号匹配，那么字符串末尾的单引号就没有配对。`$` 和 `?` 被一对单引号括起来，保护它们不被 shell 解释，从而将它们视为字面量。
- 3 单引号保护此字符串中的双引号。

## 13.11.3 双引号

双引号必须成对匹配，允许变量替换和命令替换，并保护其他任何特殊元字符不被 shell 解释。

## 示例 13.74

```

1 $ name=Jody

```

```

2 $ echo "Hi $name, I'm glad to meet you!"
Hi Jody, I'm glad to meet you!

```

```

3 $ echo "Hey $name, the time is $(date)"
Hey Jody, the time is Wed Jul 14 14:04:11 PST 2004

```

# 说明

- 1 变量 `name` 被赋值为字符串 `Jody`。
- 2 字符串两侧的双引号保护所有特殊元字符不被解释，但 `$name` 中的 `$` 除外。变量替换在双引号内执行。
- 3 变量替换和命令替换都在双引号内执行。变量 `name` 被展开，括号中的命令 `date` 被执行。（参见下一节“命令替换”。）

## 13.12 命令替换

命令替换用于将命令的输出赋值给变量，或在字符串中替换命令的输出。所有 shell 都使用反引号执行命令替换。¹² `Bash` 允许两种形式：旧形式是将命令放在反引号中；新的 Korn 风格形式是将命令放在前面带美元符号的一组括号内。

`Bash` 通过执行命令并返回命令的标准输出（删除所有尾随换行符）来进行展开。当使用旧式反引号替换形式时，反斜杠保留其字面含义，除非后面跟有 `$`、` 或 `\`。使用 `$(command)` 形式时，括号之间的所有字符构成命令；没有任何字符被特殊处理。

命令替换可以嵌套。使用旧形式嵌套时，内部反引号必须用反斜杠转义。

# 格式

```

`UNIX command`  # Old method with backquotes

```

```

$(UNIX command)  # New method

```

## 示例 13.73

（旧方法）

- 1. `$ echo "The hour is `date +%H`"`
  `The hour is 09`
- 2. `$ name=`awk -F: '{print $1}' database``
  `$ echo $name`
  `Ebenezer Scrooge`
- 3. `$ ls `ls /etc``
  `shutdown`
- 4. `$ set `date``
  `$ echo $*`
  `Wed Jul 14 09:35:21 PDT 2004`
- 5. `$ echo $2 $6`
  `Jul 2004`
- 6. `$ echo `basename \`pwd\``` 
  `ellie`

# 说明

- 1. `date` 命令的输出被替换到字符串中。
- 2. `awk` 命令的输出被赋值给变量 `name` 并显示。

# 说明（续）

3 用反引号括起来的 `ls` 命令输出是来自 `/etc` 目录的文件列表。这些文件名将作为第一个 `ls` 命令的参数。当前目录中与 `/etc` 中同名的所有文件都会被列出。（此目录中不匹配的文件会产生错误消息，例如 `ls: temicaps: No such file or directory`。）

4 `set` 命令将 `date` 命令的输出赋值给位置参数。空白将单词列表分隔为各自的参数。

5 `$*` 变量包含所有参数。`date` 命令的输出存储在 `$*` 变量中。每个参数由空白分隔。

6 打印第二个和第六个参数。

7 要将变量 `dirname` 设置为当前工作目录的名称（仅名称），需要嵌套命令替换。首先执行 `pwd` 命令，将当前工作目录的完整路径名作为参数传递给 UNIX 命令 `basename`。`basename` 命令会去掉路径名中除最后一个元素之外的所有部分。在反引号内嵌套命令时，内部命令的反引号必须用反斜杠转义。

`Bash` 中用于命令替换的反引号的替代形式如下面的示例 13.76 所示。

## 示例 13.76

（新方法）

```

1 $ d=$(date)
$ echo $d
Wed Jul 14 09:35:21 PDT 2004

```

```

2 $ lines = $(cat filex)
$ echo The time is $(date +%H)
The time is 09

```

```

4 $ machine=$(uname -n)
$ echo $machine
jody

```

```

5 $ pwd
/usr/local/bin
$ dirname="$(basename $(pwd))"   # Nesting commands
$ echo $dirname
bin

```

```

6 $ echo $(cal)
# Newlines are lost
July 2004 S M Tu W Th F S 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31

```

## 示例 13.76（续）

```

7 $ echo "$(cal)"
     2004年7月
日 一 二 三 四 五 六
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31

```

# 说明

- 1. `date` 命令被括在圆括号内。该命令的输出被替换到表达式中，然后赋值给变量 `d`，并显示出来。
- 2. `cat` 命令的输出被赋值给变量 `lines`。
- 3. `date` 命令同样被括在圆括号内。`date +%H` 的输出（当前小时）被替换到表达式中，并回显到屏幕。
- 4. 变量 `machine` 被赋值为 `uname -n` 的输出，即主机名。`machine` 变量的值被回显到屏幕。
- 5. `pwd` 命令（当前工作目录）的输出为 `/usr/local/bin`。变量 `dirname` 被赋值为命令替换的输出，其中命令替换是嵌套的。`$(pwd)` 是第一个要执行的命令替换。`pwd` 命令的输出被替换到表达式中，然后 `basename` 程序将使用该替换的结果 `/usr/local/bin` 作为其参数，得到 `basename /usr/local/bin`。
- 6. `cal`（当前月份）命令的输出被回显。执行命令替换时，末尾的换行符会被删除。
- 7. 当把整个命令替换表达式放在双引号中时，末尾的换行符会被保留，日历看起来就正常了。

## 13.13 算术展开

Shell 通过计算算术表达式并替换结果来执行算术展开。该表达式被视为位于双引号中，并且表达式可以嵌套。有关算术运算和算术求值的完整讨论，请参阅第 662 页的“算术运算符与 let 命令”。

计算算术表达式有两种格式：

# 格式

```

$[ expression ]
$(( expression ))

```

### 示例 13.77

```

echo $[ 5 + 4 - 2 ]
7
echo $[ 5 + 3 * 2 ]
11
echo $[(5 + 3) * 2]
16
echo $(( 5 + 4 ))
9
echo $(( 5 / 0 ))
bash: 5/0: division by 0 (error token is "0")
```
