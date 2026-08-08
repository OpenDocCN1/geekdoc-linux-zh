# Unix & Linux shell 脚本入门指南






![](img/84a50f94dfcd1da09f623b014d3ee18c_0_0.png)




![](img/84a50f94dfcd1da09f623b014d3ee18c_1_0.png)




这是一本关于学习使用 Unix shell 的 Bourne Shell 编程/脚本教程。

- 请在 Facebook 上加入我们的小组：http://facebook.com/shellscript
- 在 https://www.shellscript.sh/tips/ 关注技巧与提示
- 访问本书书的 Amazon 页面：http://amzn.com/dp/B00C2EGNSA





#!//sh

# 1. 引言

## 本教程的目的

本教程旨在帮助人们理解 Unix shell，并介绍一些简单但强大的 Bourne 脚本。

## 目标读者

本教程假设读者具备以下背景：

- 交互式 shell 的经验
- 对变量、函数的简单编程知识
- 对常用 Unix 命令的了解，以及任何编程语言（如 ruby, perl, python, C 或 BASIC）的基础知识

## Bourne shell 的简要史

Bourne shell 出于贝尔实验室。其他 shell 包括 Korn Shell (ksh)、C Shell (csh) 以及 tcsh。本教程并不涵盖这些 shell。

## 本教程使用的排版规范

首次提到的重要词汇将使用*斜体*。代码段和脚本输出将使用等宽字体。命令行输入将以美元符号（$）开头。如果你的提示符不同，请输入：

```
PS1="$ "
```

那么你输入的内容将以**粗体**显示。

```
$ echo '#!/sh' > my-script.sh
$ echo 'echo Hello World' >> my-script.sh
$ chmod 755 my-script.sh
$ ./my-script.sh
Hello World
$
```整个脚本都可以从 https://steve-parker.org/shell/download 下载。建议现在下载以备后之用。

```
first.sh¹

# 这是一个注释
echo Hello World
# 这也是一个注释！
```

注意，要使一个文件可执行，必须设置执行权限；对于 shell 脚本，还必须设置读取权限：

```
$ chmod a+rx first.sh
```

```
$ ./first.sh
```

在开始之前，你可以从 https://steve-parker.org/shell/download 下载所有脚本。

脚注会在页面底部出现，引导你查看相应的脚本。

¹ first.sh.txt

# 2. 哲学

shell 编程在某些 Unix 系统管理员中评价并不高。这通常由于以下两个原因引起：

- 解释型程序与 C 程序、甚至是解释型 Perl 程序相比的运行速度。
- 由于编写简单的批处理类型 shell 脚本很容易，因此有很多低质量的脚本。

部分由于如此，创建*优秀*的 shell 脚本带有一种男子主义。例如，可以作为 CGI 程序使用的脚本，如果以速度为唯一标准，它们可能都会输给 C。

许多因素可以有助于良好的、简洁、快速的 shell 脚本：

- 最重要的标准必须是清晰、易读的布局。
- 其次是避免不命令。

清晰的布局使得 shell 脚本从“黑魔法”变得易于维护和理解。你可能会认为对于简单的脚本，这



这不是什么严重的问题，但这里有两点值得记住。

- 1. 首先，一个简单的脚本往往比预期更频繁地成长为大型且复杂的脚本。
- 2. 其次，如果没有其他人理解它是如何工作的，你余生都得由自己来维护它！

Shell 脚本的某些特性似乎使得它们特别容易出现缩进错误，而且由于主要的控制结构是 if/then/else 和循环，缩进对于理解脚本在做什么至关重要。

许多 shell 脚本的主要弱点之一是如下行：

```
cat /tmp/myfile | grep "mystring"
```

这种写法的运行速度会快得多：

```
grep "mystring" /tmp/myfile
```

你可能觉得没什么大不了；但请考虑，操作系统必须加载 /bin/grep 可执行文件（在我的系统上它相当小只有 75600 字节），在内存中打开一个管道进行传输，加载并运行 /bin/cat 可执行文件（在我的系统上更小，只有 9528 字节），将其附加管道的输入端并让其运行。

当然，这种操作正是操作系统的用武之地，而且它在处理此类任务时通常高效。但如果这个命令在一个循环中运行多次，那么省去定位和加载 cat 可执行文件、设置和释放管道的时间就可以产生差异，特别是在比如 CGI 环境中，那里有足够的其他因素减慢速度，而脚本本身并不是太大阻碍。某些 Unix 在处理它们所谓的“构建和销毁进程”（即加载、执行并再次清理它们）方面比其他系统更高效。但无论你使用的 Unix 版本在这方面做得有多好，它都希望根本不需要执行这一步。

结果，你可能会在 comp.unix.shell 新闻组中偶尔听到“无用处 的 Cat 奖”（UUoC）的提及，这在某些圈子里也称为**在严肃 Shell 脚本中极度刻意使用单词 Cat 的奖**。这纯粹是同伴之间互相监督的一种方式，确保事情被正确完成。

这很好地引出了我的另一个话题：*永远*不要对自己的 shell 脚本感到过于亲近；从本质上说，源代码无法隐藏的。如果你给客户提供一个 shell 脚本，他/她可以很容易地检查它。因此，你也接受任何你交给的人都会检查它；利用 GPL² 的这一优势吧——鼓励人们免费为你提供反馈和错误修复！


Shell 脚本教程
第 11 页

## 3. 第一个脚本

对于我们的第一个 shell 脚本，我们将写一个输出“Hello World”的脚本。然后我们将尝试从一个 Hello World 程序中获得比你读过的任何教程都更多的收获 :-) 
创建一个如下所示的文件 (first.sh)：

first.sh

```bash
#!/bin/sh
# 这是一个注释！
echo Hello World      # 这也是一个注释！
```

第一行告诉 Unix 该文件将由 /bin/sh 执行。这几乎是每个 Unix 系统上 Bourne shell 的标准位置。如果你使用的是 GNU/Linux，/bin/sh 通常是指向 bash（或者最近的 dash）的符号链接。

第二行以特殊符号 # 开头。这标记该行是一行注释，shell 会完全忽略它。唯一的例外是当文件的极第一行以 #! 开头时——正如我们的脚本中所示。这是一个 Unix 特殊处理的特殊指令。这意味着即使你使用 csh、ksh 或任何其他作为交互式 shell，随后的内容也应该由 Bourne shell 解释。

同样，一个 Perl 脚本可能以行 #!usr/bin/perl 开始

- 3 first.sh.txt

告诉你的交互式 shell 随后的程序应该由 Perl 执行。对于 Bourne shell 编程，我们将坚持使用 #!/bin/sh。

第三行运行了一个命令：echo，带有两个参数（或参数）。
注意 echo 会自动在它的参数之间放置一个空格。
# 符号仍然标记注释；# 之后的任何内容都会被 shell 忽略。

现在运行 `chmod 755 first.sh` 使该文本文件变为可执行，然后运行 `./first.sh`。
你的屏幕看起来应该是这样的：

```
$ chmod 755 first.sh
$ ./first.sh
Hello World
$
```

你可能已经预到了这！你甚至可以直接运行：

```bash
$ echo Hello World
Hello World
$
```

现在让我们做一些更改。
首先，注意 echo 在其参数之间只留**一个**空格。在 "Hello" 和 "World" 之间多放几个空格。你预期输出是什么？在它们之间放一个 TAB 字符又如何？
一如 shell 编程的常态，试一试。
输出完全相同！我们是在带两个参数调用 echo 程序；它对参数之间的间隙并不像 cp 那样没那么不在乎。现在再次修改代码：

```bash
#!/bin/sh
# 这是一个注释
```

```bash
echo "Hello World" # 这也是一个注释！
```

这次起作用了。如果你有其他编程语言的经验，你可能也预到了这一点。但理解更复杂的命令和 shell 脚本正在发生什么的关键，在于理解并能够解释：为什么？echo 现在调用时只带了一个参数——字符串 "Hello World"。它会原封不动地打印出来。
这里需要理解的点是，shell 在将参数传递给被调用的程序之前会对它们进行解析。在这种情况下，它去掉了引号但将字符串作为单个参数传递。
作为最后一个例子，输入以下脚本。尝试在运行它之前预测结果：

first2.sh

```bash
#!/bin/sh
# 这是一个注释！
echo "Hello World" # 这也是一个注释！即使echo "Hello World"
echo "Hello World * World"
echo Hello * World
echo Hello World
echo "Hello" " World
echo Hello " " World
echo "Hello \*\" World"
echo hello` world
echo 'hello' world
```

一切都如你预期的那样吗？如果没有，不要担心！这些只是我们将在本教程中涵盖的内容……而且是的，我们将使用比 echo 更强强大的命令！

- 4 first2.sh.txt

## 4. 变量 - 第一部分

几乎每种存在的编程语言都有变量的概念，它是某块内存的符号名称，我们可以对其赋值、读取并操纵其内容。Bourne shell 也不例外，本节引入了这一概念。在“变量 - 第二部分”中将进一步讨论，那里将研究环境为我们设置的变量。

让我们回到第一个 Hello World 示例。可以使用变量来实现（尽管这个例子如此简单，以至于没必要这样做！）

注意，等号符号周围不能有空格：VAR=value 有效；VAR = value 无效。在第一情况下

如果你想一想，这是很合理的——否则你如何告诉它运行命令 VAR，其第一个参数是 "="，第二个参数是 "value" 呢？

将以下代码输入 var.sh：

```bash
var.sh
#!/bin/sh
MY_MESSAGE="Hello World"
echo $MY_MESSAGE
```

- 5 var.sh.txt

将字符串 "Hello World" 赋值给变量 MY_MESSAGE，然后打印变量的值。
注意我们在 Hello World 周围需要引号。虽然 echo Hello World 可以接受任意数量的参数，变量只能包含一个值，因此带空格的字符串必须加引号以便 shell 知道将其视为整体。否则，shell 会在赋值 MY_MESSAGE=Hello 后尝试执行命令 World。

shell 不关心变量类型；它们可以存储字符串、整数、实数——任何你喜欢的。
习惯 Perl 的人对此很满意；如果你在 C、Pascal 或者更糟糕的 Ada 环境中长大，这可能看起来很奇怪。事实上，这些都存储为字符串，但期望数字的例程可以将其视为数字。
如果你给变量赋值一个字符串并尝试对其加 1，你将无法成功：

```bash
$ x="hello"
$ expr $x + 1
expr: non-numeric argument
$
```

这是因为外部程序 expr 只期望数字。但在语法上，以下内容之间没有区别：

```bash
MY_MESSAGE="Hello World"
MY_SHORT MESSAGE=hi
MY_NUMBER=1
MY_PI=3.142
MY_OTHER_PI="3.142"
MY_MIXED=123abc
```

但注意，特殊字符必须正确转义以避免被 shell 解析。
这将在第 6 章“转义字符”中进一步讨论。




我们通过 `read` 命令交互式地设置变量名；以下脚本会询问你的名字，然后向你进行个人问候：

var2.sh

```
#!/bin/sh
echo "What is your name?"
read MY_NAME
echo "Hello $MY_NAME - hope you're well."
```

Mario Bacinsky 友好地指出，我最初在第 3 行漏掉了双引号，这导致单词 "you're" 中的单引号没有成对匹配，导致了错误。正是这种小细节会让 shell 程序员抓狂的，所以请务必注意！

这里使用的是 shell 内置命令 `read`，它从标准输入读取一行并存入提供的变量中。
请注意，如果你输入全名且在 `echo` 命令周围没有使用双引号，它仍然能正确输出。这是如何做到的？在之前处理 `MY_MESSAGE` 变量时，我们必须在它周围加上双引号来设置它。
发生的是，`read` 命令会自动在其输入周围加上引号，这样空格就能被正确处理。（当然，你仍然对输出加引号——例如 `echo "$MY_MESSAGE"`）。

## 变量作用域

Bourne shell 中的变量不需要像 C 等语言那样进行声明。但如果你尝试读取一个未声明的变量，结果将是空字符串。你不会收到任何警告或错误。这可能会导致一些细微的 bug——如果你赋值 `MY_OBFUSCATED_VARIABLE=Hello` 然后执行

`echo $OBFUSCATED_VARIABLE`

那么你什么也得不到（因为第二个 `OBFUSCATED` 拼写错误）。

有一个名为 `export` 的命令，它对变量的作用域有根本性的影响。为了真正了解你的变量发生了什么，你需要了解一些它是如何使用的。

创建一个短小的 shell 脚本 `myvar2.sh`：

myvar2.sh

```
#!/bin/sh
echo "MYVAR is: $MYVAR"
MYVAR="hi there"
echo "MYVAR is: $MYVAR"
```

现在运行脚本：

```bash
$ ./myvar2.sh
MYVAR is:
MYVAR is: hi there
```

MYVAR 还没有被赋予任何值，所以它是空的。然后我们给它一个值，它就有了预期的结果。
现在运行：

```bash
$ MYVAR=hello
$ ./myvar2.sh
MYVAR is:
MYVAR is: hi there
```

它还没有被设置！到底是怎么了？！
当你从交互式 shell 调用 `myvar2.sh` 时，会启动一个新的 shell 来运行该脚本。这部分部分是因为脚本开头的 `#!/bin/sh` 行，我们之前讨论过它。

我们需要导出该变量，它才能被另一个程序（包括 shell 脚本）继承：

```bash
$ export MYVAR
$ ./var2.sh
MYVAR is: hello
MYVAR is: hi there
```

现在看脚本的第 3 行：这正在改变 MYVAR 的值。但没有办法将这个值传回给你的交互式 shell。尝试读取 MYVAR 的值：

```bash
$ echo $MYVAR
hello
$
```

一旦 shell 脚本退出，它的环境就会被销毁。但 MYVAR 在你的交互式 shell 中保留其 `hello` 的值。为了从脚本接收环境变化，我们必须 `source` 脚本——这实际上是在我们自己的交互式 shell 中运行该脚本，而不是启动另一个 shell 来运行它。我们可以通过 `.` (点) 命令来 source 脚本：

```bash
$ MYVAR=hello
$ echo $MYVAR
hello
$ ./var2.sh
MYVAR is: hello
MYVAR is: hi there
$ echo $MYVAR
hi there
```

变化现在再次作用于我们的 shell 了！例如，你的 `.profile` 或 `.bash_profile` 文件就是这样工作的。请注意，在这种情况下，我们不需要 `export MYVAR`。感谢 sway 指出我最初在上面写的是 `echo MYVAR` 而不是应该的 `echo $MYVAR`。这是另一个在 shell 脚本中容易犯的简单错误。关于变量，这里还有一点值得提到，即考虑以下 shell 脚本：

```bash
#!/bin/sh
echo "What is your name?"
read USER_NAME
echo "Hello $USER_NAME"
echo "I will create you a file called $USER_NAME_file"
touch $USER_NAME_file
```

思考你预期的结果是什么。例如，如果你输入 "steve" 作为 `USER_NAME`，脚本应该创建 `steve_file` 吗？
实际上，不会。除非有一个名为 `USER_NAME_file` 的变量，否则会导致错误。shell 并不知道变量在哪里结束，其他部分在哪里开始。我们如何定义？
答案是将变量本身括在*大括号*中：

```bash
user.sh
#!/bin/sh
echo "What is your name?"
read USER_NAME
echo "Hello $USER_NAME"
echo "I will create you a file called ${USER_NAME}_file"
touch "${USER_NAME}_file"
```

shell 现在知道我们引用的是变量 `USER_NAME`，并且我们希望它后面加上后缀 `_file`。这个 `user.sh.txt` 可能是许多新手 shell 脚本程序员的噩梦，因为问题的源头很难追踪。

另外注意 `"${USER_NAME}_file"` 周围的引号——如果用户输入 "Steve Parker"（注意空格），如果没有引号，传递给 `touch` 的参数将是 `Steve` 和 `Parker_file`——也就是说，我们实际上是在说 `touch Steve Parker_file`，这是两个要处理的文件，而不是一个。引号避免了这一点。感谢 Chris 强调了这一点。

## 5. 通配符

如果你以前用过 Unix，那么通配符并不是什么新鲜事。不过，它们在 shell 脚本中的用处并不显而易见。这一部分实际上只是为了让大脑思考在 shell 脚本中事物看起来是什么样——预测使用不同语法的效果。这在以后会被用到，特别是在循环（Loops）部分。

首先思考你会如何将所有文件从 `/tmp/a` 复制到 `/tmp/b`。所有的 `.txt` 文件？所有的 `.html` 文件？希望你已经想出了：

```bash
$ cp /tmp/a/* /tmp/b/
$ cp /tmp/a*.txt /tmp/b/
$ cp /tmp/a*.html /tmp/b/
```

现在，如何在不使用 `ls /tmp/a/` 的情况下列出 `/tmp/a/` 下的文件？
`echo /tmp/a/*` 怎么样？这与 `ls` 输出之间有什么关键区别？这有什么用？或者有什么阻碍？
如何将所有 `.txt` 文件重命名为 `.bak`？请注意

```bash
$ mv *.txt *.bak
```

将不会产生预期的效果；思考一下 shell 在传递给 `mv` 之前是如何展开它的。如果有帮助，试着用 `echo` 代替 `mv` 试试。

我们以后会深入探讨这一点，因为它涉及到一些尚未涵盖的概念。

## 6. 转义字符

某些字符对 shell 具有特殊意义；例如，我们已经看到双引号（""）的使用会影响空格和 TAB 字符的处理，例如：

```bash
$ echo Hello World
Hello World
$ echo "World"
Hello World World
```

那么我们如何显示 "World"：

```bash
$ echo "World"
```
等一下，让我重新检查 OCR。OCR 那里的内容有点乱码。原文是：
```bash
$ echo Hello World
Hello World
$ echo "World"
Hello World World
```
实际上，`echo "World"` 的结果是 `World`。OCR 可能会因为噪声打印出 `Hello World World`。让我们看看逻辑。

那么我们如何显示 "World"：

```bash
$ echo "World"
```
等等，OCR 说：
```
$ echo Hello World
Hello World
$ echo "World"
Hello World World
```
这看起来像是源文本中的 OCR 错误。我会将其清理为逻辑输出。

那么我们如何显示 "World"：

```bash
$ echo "World"
```
实际上，看文本："So how do we display "World":"` 然后文本继续了。

反斜杠 (\) 是特殊的，因为它本身被用来标记其他字符的；为了一个完整的 shell，我们需要以下选项：

```bash
$ echo "This is \\ a backslash"
This is \ a backslash
$ echo "This is \" a quote and this is \\ a backslash"
This is \" a quote and this is \ a backslash
```

所以反斜杠本身必须被转义，以显示它是按字面意思的。另一个特殊字符反引号（backtick）将在第 12 章“外部程序”中讨论。



## 7. 循环

大多数语言都有循环的概念：如果我们想重复某项任务二十次，我们不希望手动输入二十次代码，而且每次只进行细微的修改。因此，在 Bourne shell 中我们有了 `for` 和 `while` 循环。与其它语言相比，这些功能要少一些，但没有人声称 shell 编程拥有 C 语言那样的威力。

### For 循环

`for` 循环遍历一组值，直到列表耗尽为止：

```bash
for.sh
#!/bin/sh
for i in 1 2 3 4 5
do
echo "Looping ... number $i"
done
```

尝试这段代码并看看它的作用。请注意，这些值可以是任何内容：

```bash
for2.sh

#!/bin/sh
for i in hello 1 * 2 goodbye
do
echo "Looping ... i is set to $i"
done
```

这非常值得尝试。确保你理解了这里发生了什么。尝试在不带 `*` 的情况下运行并掌握该概念，重新阅读“通配符（Wildcards）”章节，然后在带上 `*` 的情况下再次尝试。也尝试在不同的目录下运行，以及给 `*` 加上双引号，或者在它前面加上反斜杠 (`\*`) 尝试。

如果你目前无法访问 shell（在阅读本教程时手头有一个 shell 是非常有用的），上述两个脚本的结果如下：

- Looping .... number 1
- Looping .... number 2
- Looping .... number 3
- Looping .... number 4
- Looping .... number 5

而对于第二个示例：

- Looping ... i is set to hello
- Looping ... i is set to 1
- Looping ... i is set to (当前目录下第一个文件的文件名)
- ... 等等 ...
- Looping ... i is set to (当前目录下最后一个文件名)
- Looping ... i is set to 2
- Looping ... i is set to goodbye

所以，正如你所见，`for` 循环简单地遍历它接收到的任何输入，直到输入耗尽。

### While 循环

`while` 循环可以有趣得多！（取决于你对趣味的理解，以及你离开出门的频率……）

```bash
while.sh
#!/bin/sh
INPUT_STRING=hello
while [ "$INPUT_STRING" != "bye" ]
do
echo "Please type something in (bye to quit)"
read INPUT_STRING
echo "You typed: $INPUT_STRING"
done
```

这里发生的是 `echo` 和 `read` 语句将无限运行，直到你在提示时输入 "bye"。回顾“变量 - 第一部分”（第 4 章）来了解为什么我们在测试之前使用 `INPUT_STRING=hello`。这使得它成为重复循环，而不是传统的 `while` 循环。

冒号 (`:`) 始终求值为真；虽然有时使用它可能是必要的，但通常认为使用真实的退出条件更好。比较退出上面的循环和下面的循环；看看哪一个更优雅。也考虑在某些情况下，哪一种会比另一种更有用：

```bash
while2.sh

#!/bin/sh
while :
do
    echo "Please type something in (Ctrl+C to quit)"
    read INPUT_STRING
    echo "You typed: $INPUT_STRING"
done
```

另一个实用的技巧是 `while read f` 循环。这个示例使用了 `case` 语句，我们稍后会介绍。它从文件 `myfile` 读取内容，对于每一行，它都会告诉你它认为使用的是哪种语言。每行必须以 LF（换行符）结束 - 如果 `cat myfile` 不以空行结尾，那么最后一行将不会被处理。

```bash
while3a.sh

#!/bin/sh
while read f
do
    case $f in
        hello)      echo English ;
        howdy)      echo American ;
        gday)       echo Australian ;
        bonjour)     echo French ;
        "guten tag")  echo German ;
        *)          echo Unknown Language: $f
    esac
done < myfile
```

- 11 while2.sh.txt
- 12 while3a.sh.txt

在许多 Unix 系统上，也可以这样做：

```bash
while3b.sh

#!/bin/sh
while f=`line`
do
  .. process f ..
done < myfile
```

但由于 `while read f` 适用于任何 *nix 系统，且不依赖于外部程序 `line`，因此前者更优。查看“外部程序（External Programs）”（第 12 章）以了解为什么这种方法使用了反引号（`` ``）。如果我在上面引用了 `$i`（而不是 `f`），那么即使 `$i` 没有被声明或定义，也不会有警告或错误。例如：

```bash
$ i=THIS_IS_A_BUG
$ export i
$ ./while3.sh something
Unknown Language: THIS_IS_A_BUG
$ 
```

所以请确保你避免拼写错误。这也是使用 `${x}` 而不仅仅是 `$x` 的另一个良好理由 - 如果 `x="A"` 且你想说 "A1"，你需要执行 `echo ${x}1`，因为 `echo $x1` 将尝试使用变量 `x1`，而该变量可能不存在，或者被设置为“B2”，或其他任何意想不到的内容。

我最近在 Usenet 上发现了一个我参与过的旧帖子，我在那里实际上学到了更多……Google 在这里记录。

- 13 while3b.sh.txt

## 我从 Linux From Scratch 项目中学到的实用 Bash（但不是 Bourne Shell）小技巧是：

```bash
mkdir rc{0,1,2,3,4,5,S}.d
```

而不是繁琐的

for runlevel in 0 1 2 3 4 5 6 S
do
  mkdir rc${runlevel}.d
done
```

这也可以递归完成：

```bash
$ cd /
$ ls -ld {usr,usr/local}/{bin,sbin,lib}
drwxr-xr-x 2 root root 4096 Oct 26 01:00 /bin
drwxr-xr-x 6 root root 4096 Jan 16 17:19 /usr/bin
drwxr-xr-x 2 root root 4096 Oct 27 00:02 /sbin
drwxr-xr-x 2 root root 40960 Jan 16 19:35 /usr/bin
drwxr-xr-x 83 root root 49152 Jan 16 17:23 /usr/lib
drwxr-xr-x 2 root root 4096 Jan 16 22:22 /usr/local/bin
```



```bash
[ "$X" = "0" ] && \
echo X is the string or number "0"
[ "$X = "hello" ] && \
echo X matches the string "hello"
[ "$X != "hello" ] && \
echo X is not the string "hello"
[ -n "$X" ] && \
echo X is of nonzero length
[ -f "$X" ] && \
echo X is the path of a real file || \
echo No such file: $X"
[ -x "$X" ] && \
echo X is the path of an executable file
[ "$X" -nt /etc/passwd ] && \
echo X is a file which is newer than /etc/passwd
```

注意，我们可以使用分号（;)将两行连接在一起。这通常是为了在简单的 if 语句中节省空间。反斜杠（\）告诉 shell 这并不是行的结束，而是应该将两行（或多行）被视为整体。这对于可读性很有帮助。习惯上会对下一行进行缩进。

从这些示例中看到，test 可以对数字、字符串和文件名进行许多测试。

感谢 Aaron 指出 -a、-e（均表示“文件存在”）、-s（文件是 Socket）、-nt（文件较新）、-ot（文件较旧）、-ef（路径指向同一个文件）和 -0（文件不属于该用户）在传统的 Bourne shell（例如，Solaris、AIX、HPUX 等上的 /bin/sh）中是不可用的。

编写 if 语句有一种更简单的方法：`&& || ||` 命令分别在结果为真或假运行时执行代码。

```bash
#!/bin/sh
[ $X -ne 0 ] && echo "X isn't zero" || echo "X is zero"
[ -f $X ] && echo "X is a file" || echo "X is not a file"
[ -n $X ] && echo "X is of non-zero length" || \
echo "X is of zero length"
```

这种语法之所以可行，是因为有一个名为 `[` 的文件（或 shell 内置命令），它链接到 test。不过，使用这种结构时要小心，因为过度使用会导致代码非常难以阅读。`if...then...else...` 结构要可读得多。建议在循环和不希望过度分散读者注意力的简单健康检查（sanity checks）中使用 `[...]` 结构。

注意，当你将 X 设置为非数值值时，前几次比较会产生以下消息：

```
test.sh: [: integer expression expected before -lt
test.sh: [: integer expression expected before -gt
test.sh: [: integer expression expected before -le
test.sh: [: integer expression expected before -ge
```

这是因为 -lt、-gt、-le 和 -ge 比较仅为整数设计，不作用于字符串。字符串比较（如 `!=`）会很乐意将 "5" 视为字符串，但没有合理的方法将 "Hello" 视为整数，因此整数比较会报错。如果你想让 shell 脚本运行得更优雅，你必须在测试之前检查变量的内容——可能像这样所示：

```bash
echo -en "Please guess the magic number: " 
read X 
echo $X | grep "[0-9]" > /dev/null 2>&1 
if [ "$?" -eq "0" ]; then 
  # 如果 grep 找到了除了 0-9 以外的内容 
  # 那么它不是整数。
  echo "Sorry, wanted a number" 
else 
  # grep 只找到了 0-9，所以它是整数。
  # 我们可以安全地对其进行测试。
  if [ "$X" = "7" ]; then 
    echo "You entered the magic number!"
  fi 
fi
```

通过这种方式你可以向用户输出更有意义的消息并优雅地退出。`$?` 变量在“Variables - Shell Scripting Tutorial II”（第 10 章）中有所解释，而 grep 是一个复杂的家伙，所以如下：`grep [0-9]` 查找包含数字 (0-9) 以及可能的其他字符的行，因此 `grep [0-9]` 中的脱字符 (`^`) 仅查找那些不完全由数字组成的行。我们然后可以相反的操作（通过处理失败而非成功来实现）。好吗？`>/dev/null 2>&1` 将任何输出或错误重定向到特殊的“null”设备，而不是到用户的屏幕。感谢 Schermerhorn 纠正我——这一页曾声称 `grep -v [0-9]` 可以工作，但这显然太简单了。

我们可以像这样在 while 循环中使用 test：

```bash
# test2.sh¹⁷
#!/bin/sh
X=0
while [ -n "$X" ]
do
  echo "Enter some text (RETURN to quit"
  read X
  echo "You said: $X"
done
```

这段代码将一直请求输入，直到你按下 RETURN 键（此时 X 的长度为 0）。感谢 Justin Heath 指出脚本不起作用——我漏掉了 `while [ -n "$X" ]` 中 $X 周围的引号。如果没有这些引号，当 $X 为空时，没有任何可测试的内容。Alexander Weber 指出运行此脚本将结束得并不整洁：

```bash
$ ./test2.sh
Enter some text (RETURN to quit)
fred
You said: fred
Enter some text (RETURN to quit)
wilma
You said: wilma
Enter some text (RETURN to quit)

You said:
$
```

可以通过循环内的另一个测试来清理它：

```bash
#!/bin/sh

X=0
while [ -n "$X" ]
do
echo "Enter some text (RETURN to quit)"
read X
if [ -n "$X" ]; then
echo "You said: $X"
fi
done
```

另外注意我在这一页上使用了两种不同的 if 语句语法。它们是：

```bash
if [ "$X" -lt "0" 
then
echo "X is less than zero"
fi
```

以及 ........

```bash
if [ -n "$X" ]; then
echo "You said: $X"
fi
```

你必须在 if 语句和 then 结构之间有一个分隔符（break）。这可以是分号也可以是换行，哪种都行，但在 if 和 then 之间必须有其中之一。如果能直接写成就好了：

```bash
if [ ! -n "$X" ]
  echo "You said: $X"
```

但 `then` 和 `fi` 是绝对必须的。

## 9. Case

case 语句避免了遍历整组 `if .. then .. else` 语句。它的语法非常简单：

talk.sh¹⁸

```bash
#!/bin/sh
echo "Please talk to me ..."
while :
  read INPUT_STRING
  case $INPUT_STRING in
    hello)
      echo "Hello yourself!"
      ;;
    bye)
      echo "See you again!"
      break
      ;;
    *)
      echo "Sorry, I don't understand"
      ;;
  esac
done
echo
echo "That's all folks!"
```
¹⁸ talk.sh.txt

好了，它并不是世界上最棒的聊天者；它只是一个例子！尝试运行并检查它是如何工作的……

```bash
$ ./talk.sh
Please talk to me ...
hello
Hello yourself!
What do you think?
Sorry, I don't understand
bye
See again!

That's all folks!
$
```

语法非常简单：`case` 行本身意味着我们正在测试变量 `INPUT_STRING` 的值。我们理解的选项列出并跟着一个右括号，`hello)` 和 `bye)`。这意味着如果 `INPUT_STRING` 匹配 `hello`，则执行相应的代码，直到双分号。如果 `INPUT_STRING` 匹配 `bye`，则打印“再见”消息并退出循环。第三个选项 `*` 是默认的通配条件；它不是必须的，但对调试很有用。

整个 `case` 语句以 `esac` 结束（case 反过来！）然后我们用 `done` 结束循环。case 条件已经足够复杂了，但它们是一个非常有用且强大的工具。它们通常用于解析传递给 shell 脚本的参数，其他如此。

## 10. Variables - Part II

有一组已经设置好的变量，其中大多数不能被赋值。这些变量可以包含有用信息，脚本可以利用它们来了解其运行的环境。

我们将查看的第一组变量是 `$0 .. $9` 和 `$#`。变量 `$0` 是调用时的程序基名。`$1 .. $9` 是调用脚本时的前 9 个额外参数。变量 `$@` 是所有参数 `$1 ..` 无论什么。变量 `$*` 类似，但它不会保留任何空格和引号，因此 "File with spaces" 会变成 "File" 和 "spaces"。这与我们在“第一个脚本”中看到的 echo 内容相似。作为一条通用规则，使用 `$@` 并避免使用 `$$`。`$#` 是调用脚本时的参数个数。让我们来看一个示例脚本：

```bash
var3.sh
#!/bin/sh
echo "I was called with $# parameters"
echo "My name is $0"
echo "My first parameter is $1"
echo "My second parameter is $2"
echo "All parameters are $@"
```




让我们来运行这段代码并查看输出：

```
$ /home/steve/var3.sh
I was called with 0 parameters
My name is /home/steve/var3.sh
My first parameter is
My second parameter is
All parameters are
$
 ./var3.sh hello world earth
I was called with 3 parameters
My name is ./var3.sh
My first parameter is hello
My second parameter is world
All parameters are hello world earth
```

注意，$0 的值取决于你是如何调用脚本的。外部实用程序 `basename` 可以帮助整理这些内容：

```
echo "My name is `basename $0`"
```

$# 和 $1 .. $2 是由 shell 自动设置的。我们可以通过 `shift` 命令来获取 9 个以上的参数；请看下方的脚本：

```
var4.sh

!/bin/sh
while [ "$#" -gt "0" ]
do
  echo "\$1 is $1"
  shift
done
```

此脚本会持续使用 `shift` 直到 $# 减为零，此时列表为空。

另一个特殊的变量是 $?。它包含了上一次运行命令的退出值。因此，代码：

```
#!/bin/sh
/usr/local/bin/my-command
if [ "$?" -ne "0" ]; then
echo "Sorry, we had a problem there!"
fi
```

将尝试运行 /usr/local/bin/my-command，如果一切顺利它应该以零值退出，如果失败则返回非零值。我们随后可以在调用命令后检查 $? 的值来处理这种情况。这有助于让脚本更加健壮、更智能。良好的应用程序在成功时应该返回零。因此有句名言：

> “罗马帝国灭落的主要原因之一是由于缺乏零，他们没有办法指示他们的 C 程序的成功终止。” (Robert Firth)

环境为你设置的另外两个主要变量是 $$ 和 $。它们都是进程号。$$ 变量是当前运行的 shell 的 PID（进程标识符）。这对于创建临时文件非常有用，例如 /tmp/my-script.$$，如果同时运行多个脚本实例，且它们都需要自己的临时文件，这就会很有用。$! 变量是上一次运行的后台进程的 PID。这有助于在进程执行任务时跟踪它。

另一个有趣的变量是 IFS。它是内部字段分隔符。默认值是空格 制表符 换行符，但如果你要更改它，最好先取一个副本，所示：

# var5.sh21

```
#!/bin/sh
old IFS="$IFS"
IFS=
echo "Please input some data separated by colons ..."
read x y z
IFS=$old IFS
echo "x is $x y is $y z is $z"
```

此脚本运行方式如下：

```
$ ./ifs.sh
Please input some data separated by colons ...
hello:how are you:today
x is hello y is how are you z is today
```

```
$ ./ifs.sh
Please input some data separated by colons ...
hello:how are you:today:my:friend
x is hello y is how are you z is today:my:friend
```

在处理 IFS（特别是任何你无法完全控制的变量）时，意识到它可能包含空格、换行符和其他“不可控”的字符非常重要。因此，在它周围使用双引号是一个非常好的主意，例如使用 old_IFS="$IFS" 而不是 old_IFS=$IFS。

# #!/ch/11

## 11. 变量 - 第三部分

正如我们在第 4 章（“变量 - 第一部分”）中提到的，变量周围的大大括号可以避免混淆：

```
foo=sun
echo $fooshine      # $fooshine 未定义
echo ${foo}shine     # 显示单词 "sunshine"
```

但这并不是全部——这些花括号还有另一个更强大的用途。我们可以处理变量未定义或为空的问题（在 shell 中，未定义和空没有太大区别）。

## 使用默认值

考虑以下代码段，它会提示用户输入，但接受默认值：

```
#!/bin/sh
echo -en "What is your name [ `whoami` ] "
read myname
if [ -z "$myname" ]; then
  myname=`whoami`
fi
echo "Your name is : $myname"
```

向 echo 传递 "-en" 告诉它不要添加换行（适用于 bash 和 csh）。对于 Dash、Bourne 以及其他符合标准的 shell，你需要在行尾使用 \c。Ksh 理解这两种形式。

如果你通过按“回车”接受默认值，此脚本运行如下：

```
steve$ ./name.sh
What is your name [ steve ] RETURN
Your name is : steve
```

... 或者，带有用户输入：

```
steve$ ./name.sh
What is your name [ steve ] foo
Your name is : foo
```

使用 shell 变量功能可以更好地实现。通过使用大括号和特殊的 `:-\` 用法，你可以指定在变量未设置时使用的默认值：

```
echo -en "What is your name [ `whoami` ]"
read myname
echo "Your name is : ${myname:-`whoami`}"
```

这可以被视为特殊情况——我们正在使用 whoami 命令的输出，该命令打印你的登录名（UID）。更典型的示例是使用固定文本，如下：

```
echo "Your name is : ${myname:-John Doe}"
```

与其他使用反引号的情况一样，`whoami` 在子 shell 中运行，因此在反引号内执行的任何 `cd` 命令或设置任何其他变量都不会影响当前正在运行的 shell。

## 使用和设置默认值

另一种语法是 ":="，它在变量未定义时将其设置为默认值：

```
echo "Your name is : ${myname=John Doe}"
```

2. 外部程序

外部程序通常用于 shell 脚本；有一些内置命令（echo, which 和 test 都是内置的），但许多有用的命令实际上是工具，如 tr, grep 和 cut。

反引号也与命令关联。正正如此，我们将首先讨论反引号。反引号可以捕获我们选择的命令或命令集的标准输出：

```bash
$ grep "${USER}" /etc/passwd | cut -d:f5
Steve Parker
```

我们可以将其输出到一个变量中以便更方便地进行处理：

```bash
$ MYNAME=`grep "${USER}" /etc/passwd | cut -d:f5`
$ echo $MYNAME
Steve Parker
```

我们看到反引号可以捕获任何命令或命令集的输出。如果你想运行一个缓慢的命令或命令集并解析它的部分输出：

```bash
#!/bin/sh
find -name "*.html" -print | grep "/index.html$"
find -name "*.html" -print | grep "/contents.html$"
```

这段代码可能运行很长时间，而且我们运行了两次！更好的解决方案是：

```bash
#!/bin/sh
HTML_FILES=`find -name "*.html" -print`
echo "$HTML_FILES" | grep "/index.html$"
echo "$HTML_FILES" | grep "/contents.html$"
```

注意：$HTML_FILES 周围的引号对于保留文件之间的换行符至关重要。否则 grep 将看到巨大的文本，而不是每个文件一行。

通过这种方式，我们只运行一次缓慢的 find 命令，大约缩短了脚本的执行时间。




- 使用 `return` 命令结束函数，并将提供的值返回给 shell 的调用部分
- 将 `echo` 输出到标准输出（stdout），这会被调用者捕获，就像 `c=`expr a + $b`` 一样

这类似于 C 语言，因为 `exit` 会停止程序，而 `return` 将控制权交给调用者。区别在于 shell 函数不能更改其参数，但它可以更改全局参数。

一个使用函数的简单脚本如下：

function.sh²²

```sh
#!/bin/sh
## 一个带有函数的简单脚本...
add_a_user()
{
    USER=$1
    PASSWORD=$2
    shift; shift;
    # 移动两次后，剩余部分现在是注释 ... 
    COMMENTS=$@
    echo "Adding user $USER .."
    echo useradd -c "$COMMENTS" $USER
    echo echo passwd $USER $PASSWORD
    echo "Added user $USER ($COMMENTS) with pass $PASSWORD"
}
###
## 脚本主体从这里开始
###
echo "Start of script..."
add_a_user bob letmein Holness the presenter
add_a_user fred badpassword Fred Durst the singer
add_a_user bilko worseorsepassword Sgt. Bilko the role model
echo "End of script..."
```

22 function.sh.txt

第 4 行通过以 `()` 结尾来标识自身为函数声明。其后是 `{`，匹配的 `}` 之前的所有内容都被视为该函数的代码。这些代码在函数被调用之前不会执行。函数会被读取，但在实际被调用之前基本上会被忽略。

请注意，对于此示例，`userid` 和 `passwd` 命令被加上了 `echo -` 这是一个非常有用的调试技术，用于检查是否会执行正确的命令。这意味着你可以在没有 root 权限或向系统添加可疑账户的情况下运行脚本！

我们习惯了 shell 脚本是顺序执行的。但函数并非如此。在这种情况下，函数 `add_a_user` 被读取并检查语法，但在被显式调用之前不会执行。执行从 `echo` 语句 "Start of script..." 开始。下一行 `add_a_user bob letmein Bob Holness` 被识别为函数调用——进入了 `add_a_user` 函数，并在环境带有某些新增的情况下开始执行：

```
$1=bob
$2=letmein
$3=Bob
$4=Holness
$5=the
$6=presenter
```

因此，在该函数内部，$1` 被设置为 `bob`，无论函数外的 `$1` 被设置为什么。所以如果我们想在函数内部引用“原始”的 `$1`，我们必须给它分配一个名称——例如在调用函数之前设置 `A=$1`。然后在函数内部，我们可以引用 `$A`。我们再次使用 `shift` 命令将 `$3` 及以后的参数放入 `$@`。然后函数添加用户并设置其密码。它输出了相应的注释，并将控制权返回给主代码的下一行。

## 变量作用域

习惯于其他语言的程序员可能会对 shell 函数的作用域规则感到惊讶。基本上，除了参数（`$1`, `$2`, `$@` 等）外没有作用域。取以下简单的代码段：

```sh
#!/bin/sh

myfunc()
{
    echo "I was called as : $@"
    x=2
}

### 主脚本从这里开始

echo "Script was called with $@"
x=1
echo "x is $x"
myfunc 1 2 3
echo "x is $x"
```

当通过 `scope.sh a b c` 调用脚本时，给出如下输出：

```
Script was called with a b c
x is 1
I was called as : 1 2 3
x is 2
```

`$@` 参数在函数内部被更改，以反映函数是如何调用的。然而，变量 `x` 实际上是一个全局变量——`myfunc` 修改了它，而该更改仍然

如果函数的输出被管道到其他地方，则它将在子 shell 中调用——也就是说，“myfunc 1 2 3 | tee out.log" 第二次执行仍然显示 "x is 1"。这是因为调用了一个新的 shell 进程来处理 `myfunc()`。这会让调试变得非常沮丧；Astrid 曾有一个脚本突然失败，结果证明就是因为这个。





## 退出码 (Exit Codes)

退出码是一个 0 到 255 之间的数字，当任何 Unix 命令将控制权交还给父进程时返回。可以使用其他数字，但它们会被视为模 256 的结果，因此 exit 10 等于 exit 246，而 exit 257 等于 exit 1。

这些代码可以在 Shell 脚本中使用，根据所执行的命令的成功或失败来改变执行流。这在第 10 章“变量 - 第二部分”中简要介绍过。在这里，我们将更详细地查看退出码的各种解释。

传统上用 exit 0 表示成功；失败用非零退出码表示。此值可以表示失败的不同原因。例如，GNU grep 在成功时返回 0，在未找到匹配项时返回 1，在其他错误（语法错误、输入文件不存在等）时返回 2。

我们将查看检查错误状态的三种方法，并讨论每种方法的优缺点。

首先是简单的方法：

```bash
#!/bin/sh
## 第一次检查返回值的尝试
USERNAME=`grep "^${1}:" /etc/passwd|cut -d:" -f1`
if [ "$?" -ne "0" ]; then
  echo "Sorry, cannot find user ${1} in /etc/passwd"
  exit 1
fi
NAME=`grep "^${1}:" /etc/passwd|cut -d:" -f5`
HOMEDIR=`grep "^${1}:" /etc/passwd|cut -d:" -f6`

echo "USERNAME:$USERNAME"
echo "NAME: $NAME"
echo "HOMEDIR:$HOMEDIR"
```

如果你在 /etc/passwd 中提供了一个有效的用户名，这个脚本运行良好良好。然而，如果你输入了一个无效的代码，它的表现不像你最初预期的那样的 - 它会继续运行，并显示：

USERNAME:
NAME:
HOMEDIR:

为什么会这样？如前所述，$? 变量被设置为上一次执行命令的返回码。在这种情况下，命令是 `cut`。它没有遇到任何它认为需要报告的问题 - 从我通过测试和重新阅读文档来看，`cut` 无论发生什么都会返回！它接收了一个空字符串并完成了工作 - 返回了它输入的第一个字段，而该字段恰好是空字符串。那么我们该怎么办？如果这里发生了错误，是 `grep` 会报告，而不是 `cut`。因此，我们必须测试 `grep` 的返回码，而不是 `cut` 的。

```bash
#!/bin/sh
## 第二次检查返回值的尝试
grep "^${1}:" /etc/passwd > /dev/null 2>&1
if [ "$?" -ne "0" ]; then
  echo "Sorry, cannot find user ${1} in /etc/passwd"
  exit 1
fi
USERNAME=`grep "^${1}:" /etc/passwd|cut -d:" -f1`
NAME=`grep "^${1}:" /etc/passwd|cut -d:" -f5`
HOMEDIR=`grep "^${1}:" /etc/passwd|cut -d:" -f6`

echo "USERNAME: $USERNAME"
echo "NAME: $NAME"
echo "HOMEDIR: $HOMEDIR"
```

这为我们解决了问题，尽管代价是代码稍微长了。这是教科书中可能会向你展示的基本方法，但远不是 Shell 脚本中检查状态的全部。这种方法可能不适用于你特定的命令序列，或者可能难以维护。下面，我们将研究两种替代方法。

作为第二种方法，我们可以通过将测试放入单独的函数中来稍微整理一下，而不是在代码中充斥着大量的 4 行测试：

```bash
#!/bin/sh
## 一种整洁的方法

check_errs() {
  # 函数。参数 1 是失败时显示的文本。
  if [ "${1}" -ne "0" ]; then
    echo "ERROR #${1} : ${2}"
    # 额外奖励，让我们的脚本以正确的错误码退出。
    exit ${1}
  fi
}
```

### 主脚本从这里开始 ###
grep "^${1}:" /etc/passwd > /dev/null 2>&1
check_errs $? "User ${1} not found in /etc/passwd"
USERNAME=`grep "^${1}:" /etc/passwd|cut -d:" -f1`
check_errs $? "Cut returned an error"
echo "USERNAME: $USERNAME"
check_errs $? "echo returned an error - very strange!"

这允许我们测试 3 次错误，带有自定义的错误信息，而无需编写 3 个独立的测试。通过编写一次测试程序，我们可以根据需要调用任意次数，创建一个更智能的脚本，而对程序员的开销极小。Perl 程序员会识别出这类似于 Perl 中的 `die` 命令。

作为第三种方法，我们将查看一种更简单、更粗暴的方法。我倾向于构建 Linux 内核 - 简单的自动化，如果运行顺利，应该直接继续进行；但当出现问题时，往往需要操作人员做一些智能操作（即脚本无法做到的）：

```bash
#!/bin/sh
cd /usr/src/linux && make modules && \
make dep && make bzImage && make modules && \
make modules install && \
cp arch/i386/boot/bzImage /boot/my-new-kernel && \
cp System.map /boot && \
echo "Your new kernel awaits, m'lord."
```

这个脚本运行构建 Linux 内核涉及的任务（可能需要一段时间时间），并使用 `&&` 运算符检查成功与。使用 `if` 实现将涉及：

```bash
#!/bin/sh
cd /usr/src/linux
if [ "$?" -eq "0" ]; then
  make dep
  if [ "$?" -eq "0" ]; then
    make bzImage
    if [ "$?" -eq "0" ]; then
      make modules
      if [ "$?" -eq "0" ]; then
        make modules install
        if [ "$?" -eq "0" ]; then
          cp arch/i386/boot/bzImage /boot/my-new-kernel
          if [ "$?" -eq "0" ]; then
            cp System.map /boot/
            echo "Your new kernel awaits, m'lord."
          fi
        fi
      fi
    fi
  fi
fi
```

... 这，我个人觉得这种写法很难跟随。

`&&` 和 `||` 运算符是 Shell 中 AND 和 OR 的等价物。它们可以像上面那样组合：

```bash
#!/bin/sh
cp /foo/bar && echo Success || echo Failed
```

这段代码取决于 `cp` 命令是否成功来输出 Success 或 Failed。仔细看这个结构，是：

```bash
command && command-to-execute-on-success
|| command-to-execute-on-failure
```

这种方法适用于简单的成功/失败场景，但如果你想检查命令本身的状态，很容易混淆哪个 && 对应哪个。它也很难以维护。因此，这种结构只建议用于命令的序列。在较早的版本中，我建议可以使用子 shell 来根据 `cp` 命令的成功或失败来执行多个命令：

```bash
cp /foo/bar && \
  ( echo Success ; echo Success part II ) || \
  ( echo Failed ; echo Failed part II )
```

但实际上，Marcel 发现这并不有效。子 shell 的语法是：

```
( command1 ; command2; command3 )
```

子 shell 的返回码是最后一个命令（示例中的 command3）的返回码。该返回码会影响整体命令。

## 简单的替代替代品

这里有一个 expect 的简单替代品。许多人询问这是如何实现的，受我在 Hints and Tips 中展示的 Sun 示例（用于 Sun Microsystems 的 Explorer 工具）的启发，这里有一个非常简单的版本。

expect.txt 的语法非常简单：

```
S command E[delay] expected_text
```

因此，命令以 "S"（代表 Send）开头，预期结果用 "E" 标记。由于某些命令可能需要一段时间才能完成，可以在预期结果之前指定延迟：“E10 \$” 将在等待美元提示符之前等待 10 秒。如果未找到预期结果，脚本将等待一秒，重试，然后等待两秒，然后


三秒，直到找到预期的文本或达到由 `MAX_WAITS` 定义的最大值。延迟是的，因此 "E $" 将立即等待提示符。

注意，如果 `MAX_WAITS=5`，最大延迟不是五秒，而是 1+2+3+4+5=15秒。

```sh
#!/bin/sh
## expect.sh | telnet > file1
host=127.0.0.1
port=23
file1=file1
MAX_WAITS=5

echo open ${host} ${port}

while read l
do
  c=`echo ${l}|cut -c1`
  if [ "${c}" = "E" ]; then
    expected=`echo ${l}|cut -d " " -f2-`
    delay=`echo ${l}|cut -d " " -f1|cut -c2-`
    if [ -z "${delay}" ]; then
      sleep ${delay}
    fi
    res=1
    i=0
    while [ "${res}" -ne "0" ]
    do
      tail -1 "${file}" 2>/dev/null | grep "${expected}"
      res=$?
      sleep ${i}
      i=`expr ${i} + 1``
      if [ "${i}" -gt "${MAX_WAITS}" ]; then
        echo "ERROR : Waiting for ${expected}" >> ${file}
        exit 1
      fi
    done
  else
    echo ${l}|cut -d " " -f2-
  fi
done < expect.txt
```

其运行方式如下：
$ expect.sh | telnet > file1

这将创建一个名为 `file1` 的文件，其中包含会话记录。在这种情况下，它将是登录过程、`/tmp` 的 ls 输出以及 `cal` 的输出。例如：

```
telnet> Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character '^'.

declan login: steve
Password:
Last login: Thu May 30 23:52:50 +0100 on pts/3 from localhost.
No mail.
steve:-$ ls /tmp
API.txt cgihtml-1.69.tar.gz orbit-root
cal
a.txt cmd.txt orbit-steve
apache-1.3.23.tar.gz defaults.cgi parser.c
b.txt diary.c patchdiag.xref
background.jpg drops.jpg sh-thd-1013541438
blocks.jpg fortune-mod-9708.tar.gz stone-dark.jpg
blue3.jpg grey2.jpg water.jpg
c.txt
steve:-$ cal
jpsock.131.1249
May 2002
Su Mo Tu Th Fr Sa
1 2 3 4
5 6 7 8 9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31

steve:-$ exit
logout
```

## Trap

Trap 是一个简单但非常有用的工具。如果你的脚本创建了临时文件（例如这个简单的脚本，它会将当前目录下所有文件中的 FOO 替换为 BAR），当脚本退出时，`/tmp` 是干净的。但是，如果它在执行过程中被中断，`/tmp` 中可能会残留文件：

```sh
#!/bin/sh

trap cleanup 1 2 3 6

cleanup()
{
    echo "Caught Signal ... cleaning up."
    rm -rf /tmp/temp.*$$
    echo "Done cleanup ... quitting"
    exit 1
}
```

```sh
### main script
for i in *
do
    sed s/FOO/BAR/g $i > /tmp/temp_${i}.$ && mv /tmp/temp_${i}.$ $i
done
```

`trap` 语句告诉脚本在触发信号 1、2、3 或 6 时运行 `cleanup()`。最常用的信号（CTRL-C）是信号 2 (SIGINT)。它也可以用于一些非常有趣的用途：

```sh
#!/bin/sh

trap 'increment' 2

increment()
{
    echo "Caught SIGINT ..."
    X=`expr ${X} + 500
    if [ "\${X}" -gt "2000" ]
    then
        echo "Okay, I'll quit ..."
        exit 1
    fi
}
```

```sh
### main script
X=0
while
do
    echo "X=$X"
    X=`expr ${X} + 1`
    sleep 1
done
```

上面的脚本非常有趣——它捕获了 CTRL-C 并不退出，而是改变了运行方式。这对于产生积极或负面影响可能有什么用，留给读者思考 :) 这个特定的例子在 4 次中断后（或 2000 秒后）会退出。请注意，任何进程都会被 `kill -9<PID>` 强制杀死，而没有机会处理信号。

以下是一些常见中断信号的表格：

| 数字 | SIG | 含义 |
|---|---|---|
| 0 | | 在 shell 退出时 |
| 1 | SIGHUP | 清理工作 |
| 2 | SIGINT | 中断 |
| 3 | SIGQUIT | 退出 |
| 6 | SIGABRT | 终止 |
| 9 | SIGKILL | 立即死亡（无法被捕获） |
| 14 | SIGALRM | 闹钟 |
| 15 | SIGTERM | 终止 |

注意，如果你的脚本启动在一个本身忽略信号的环境中（例如在 `nohup` 控制下），该脚本也将忽略这些信号。

# echo : -n \c

正如你现在可能注意到的，当你使用 `echo` 语句时，命令末尾会添加一个换行符。对此有一个解决方法……更准确地说，有两种解决方法。

某些 Unix 系统使用 `echo -n message` 来告诉 `echo` 不要追加换行符；另一些系统使用 `echo message \c` 实现相同的功能：

```sh
echo -n "Enter your name:"read name
echo "Hello, $name"
```

这在某些系统上有效，显示如下：

Enter your name: Steve
Hello, Steve

然而，在其他系统上，你需要这样写代码：

```sh
echo "Enter your name: \c"read name
echo "Hello, $name"
```

这在那些系统上将产生相同的结果。

嗯，这真麻烦。这里有一个适用于两种系统的变通方案：

```sh
if [ "echo -n" = "-n" ]; then
n=""
c="\c"
else
n="-n"
c=""
fi
```

```sh
echo $n Enter your name: $cread name
echo "Hello, $name"
```

如果 `echo -n` 没有被正确解析，它将直接输出文本 `-n`，在这种情况下 `$n` 被设置为空字符串，而 `$c` 被设置为 `\c`。否则，执行相反操作，将 `$n` 设置为 `-n`，而 `$c` 设置为空字符串。

我们在上面已经展示了简单但有效的 `cut` 命令的用法。我们在这里将讨论一些更常用的外部程序的示例。

`grep` 是 shell 脚本程序员一个极其有用的工具。`grep` 的示例如下：

```sh
#!/bin/sh
grep "pattern" file
```

`sed s/eth0/eth1/g file1 > file2` 将 file1 中所有的 eth0 更改为 eth1。如果我们只更改一个单独字符，`tr` 会是更合适的工具，因为它体积更小，加载速度更快。`tr` 无法做的另一件事是：从文件中删除字符：

```
echo ${SOMETHING} | sed s/"bad word"//g
```

这会从变量 ${SOMETHING} 中删除短语 "bad word"。你可能会想：“但是 grep 也能做到这一点！”——`grep` 只处理整行。请考虑以下文件：

This line is okay.
This line contains a bad word. Treat with care.
This line is fine, too.

`grep` 会删除整个第二行，只留下一个两行的文件；而 `sed` 则会将文件内容更改为：

This line is okay.
This line contains a . Treat with care.
This line is fine, too.

## Telnet 提示

这是我从 Sun 的 Explorer 工具中学会的一个实用技巧。虽然服务器上不再使用 telnet，但某些网络设备（如终端集中器等）仍在使用它。通过创建一个像这样的脚本（你自己的脚本，或从命令行），你可以运行：

```
$ ./telnet.sh | telnet
```

我曾几个人问过我这个问题，我倾向于引导他们使用 `expect` 代码包，那套代码非常复杂且臃肿；这段代码在不同系统之间具有很好的移植性（只要它们支持 `egrep`）。如果它在你的系统上不起作用，请尝试使用带有 `-q` 参数的 `grep`，或者使用特定的 `grep` 并重定向到 `/dev/null`。尽管这比安装 `expect` 要简单得多。

## telnet1.sh²⁸

```bash
#!/bin/sh
host=127.0.0.1
port=23
login=steve
asswd=hellothere
cmd="ls /tmp"

echo ${host} ${port}
sleep 1
echo ${login}
sleep 1
echo ${passwd}
sleep 1
echo ${cmd}
sleep 1
echo exit
```

然而，Sun 添加了一些巧妙的错误检查代码（注意：你可以从当前的 shell 或脚本中设置并导出变量，以避免将密码存储在明文文件中）：

```
$ ./telnet2.sh | telnet > file
```

## telnet2.sh²⁹

- 28 telnet1.txt
- 29 telnet2.txt

```bash
#!/bin/sh
## telnet2.sh | telnet > FILE1
host=127.0.0.1
port=23
login=steve
passwd=hellothere
cmd="ls /tmp"
timeout=3
file=file1
prompt="$"
```

```bash
echo open ${host} ${port}
sleep 1
tout=${timeout} 2
while [ "${tout}" -ge 0 ]
do
  if tail -1 "${file}" 2>/dev/null | \
    egrep -e "${login}" > /dev/null
    then
      echo "${login}"
      sleep 1
      tout=-5
      continue
  else
    sleep 1
    tout=`expr ${tout} - 1`
  fi
done
```

```bash
if [ "${tout}" -ne "-5" ]; then
  exit 1
fi

out=${timeout}
while [ "${tout}" -ge 0 ]
do
  if tail -1 "${file}" 2>/dev/null | \
    egrep -e "Password:" > /dev/null
    then
      echo "${password}"
      sleep 1
      tout=-5
      continue
  else
if tail -1 "${file}" 2>/dev/null | \
eegrep -e "${prompt}" > /dev/null
then
    tout=-5
else
    sleep 1
    tout=`expr ${tout} - 1`
fi
done

if [ "${tout}" -ne "5" ]; then
    exit 1
fi

> ${file}
echo ${cmd}
sleep 1
echo exit
```

注意，在这个版本中，输出被捕获到 file1 中，并且脚本实际上使用了该文件来检查进度。我添加了 `> ${file}`，以便进入文件的输出仅为命令的输出，而不包含登录过程。

## 15. 快速参考

这是一个关于某些不太容易猜的命令和代码含义的快速参考指南。

| 命令 / 变量 / 语法结构 | 说明 | 示例 |
| --- | --- | --- |
| & | 在后台运行上一个命令 | ls & |
| && | 逻辑与 | if [ "$foo" -ge "0" ] && [ "$foo" -le "9" ] |
| \| | 逻辑或 | if [ "$foo" -lt "0" ] \| [ "$foo" -gt "9" ] (在 Bourne shell 中不支持) |
| ^ | 行首 | grep "^foo" |
| $ | 行尾 | grep "foo$" |
| = | 字符串相等（对比 -eq） | if [ "$foo" = "bar" ] |

| 命令 / 变量 / 语法结构 | 说明 | 示例 |
| --- | --- | --- |
| ! | 逻辑非 | if [ "$foo" != = "bar" ] |
| $$ | 当前 shell 的进程 ID (PID) | echo "my PID = $$" |
| |$ | 上一个后台命令的 PID | ls & echo "PID of ls = \$!" |
| $? | 上一个命令的退出状态 | ls ; echo "ls returned code \$?" |
| $0 | 当前命令的名称（按调用方式） | echo "I am \$0" |
| $1 | 当前命令的第一个参数 | echo "My first argument is \$1" |
| $9 | 当前命令的第九个参数 | echo "My ninth argument is \$9" |
| $@ | 当前命令的所有参数（保留空格） | echo "My arguments are \$@" |

| 命令 / 变量 / 语法结构 | 说明 | 示例 |
| --- | --- | --- |
| * | 引用) | | |
| $* | 当前命令的所有参数（不保留空格和引号） | echo "My arguments are $*" |
| -eq | 数值相等 | if [ "$foo" -eq "9" ] |
| -ne | 数值不相等 | if [ "$foo" -ne "9" ] |
| -lt | 小于 | if [ "$foo" -lt "9" ] |
| -le | 小于或等于 | if [ "$foo" -le "9" ] |
| -gt | 大于 | if [ "$foo" -gt "9" ] |
| -ge | 大于或等于 | if [ "$foo" -ge "9" ] |
| -z | 字符串为空 | if [ -z "$foo" ] |
| -n | 字符串不空 | if [ -n "$foo" ] |

## 16. 交互式 Shell

这里是关于交互式使用的一些快速提示。我个人在大多数情况下推荐 bash shell。你可以通过添加历史记录来让 ksh 更好用，可以使用 vi 或 emacs。有多种方法可以实现，取决于具体情况：set -o vi、ksh -o vi，或者 exec ksh -o vi（如果你更喜欢 emacs 模式，可以将 "vi" 替换为 "emacs"）。

如果你想从另一个交互式 shell 启动 ksh，可以像这样调用 ksh：

```
csh% # 噢，那是 csh！
csh% ksh
ksh$ 噢，那好多了
ksh$ # 在 ksh 下操作
ksh$ # 回到 csh 提示符：
ksh$ exit
```

这将启动一个新的 ksh 会话，你可以退出并返回到之前的 shell。或者，你可以使用 exec 命令将 csh（或任何 shell）替换为 ksh shell：

```csh% # 噢，那是 csh！
csh% exec ksh
ksh$ # 在 ksh 下操作
ksh$ exit
```

这里的区别在于你无法找回 csh 会话。

好用的地方是历史记录：

```
csh% ksh
ksh$ set -o vi
ksh$ # 现在你可以用 vi 编辑历史记录了
```

如果你按下 ESC 然后按 k，通过重复按 k 就可以回溯命令历史。你可以使用 vi 命令模式和输入模式命令来编辑命令，例如：

```
ksh$ touch foo
ESC-k (进入 vi 模式，显示上一个命令)
w (跳到下一个单词，从 "touch" 跳到 "foo")nww (修改单词)bar (将 "foo" 改为 "bar")
ksh$ touch bar
```




## 17. 练习

我认为这个简单的练习可能对衡量你的 Shell 脚本编写水平很有帮助……

- 通讯录
- 目录遍历

## 通讯录

好了，虽然这看起来很无聊，但这是你今天的练习题：使用 bourne 或 bourne-again shell 创建一个通讯录程序。它应该使用函数来执行所需的任务。该程序应该是基于菜单的，允许提供以下选项：

- 搜索通讯录
- 添加条目
- 删除 / 编辑条目

你还需要一个“显示”函数，在选择时显示单条或多条记录。

## 搜索

当用户搜索“Smith”时，脚本应该识别并显示所有包含“Smith”的记录。搜索是仅针对姓氏还是整条记录，由你决定。

## 添加

输入数据（姓名、姓氏、电子邮件、电话等）。如果看起来是重复的，为了获得加分，可以提供编辑现有记录get。在用户确认后将记录保存到数据文件中。

## 删除

输入搜索标准，将其缩小到一条，确认，然后删除该记录。

## 编辑

操作与删除相似，但使用现有记录作为默认输入。例如，如果你只想更改 John Smith 的电话号码，界面可能像这样：

```
Name [ John Smith ]
Phone [ 12345 ] 54321
Email [ joe@smith.org.uk ]
```

删除旧记录并添加新记录。或者，直接编辑现有记录，尽管这可能更困难。

## 加分项

- 允许取消选项（使用“特殊”条目如 `^d`, `CR`, `^c` 等）
- 添加“确认”选项。
- 提供交互式/非交互式模式（即基于菜单的版本和基于命令行 (CLI)的版本）。
- 在 CLI 版本中尝试 `getopt`。

## 提示 / 需要思考的问题

我提供了一个答案在下方；除非你卡住了否则不要看！主文件：`addressbook/addr.sh.txt` 库文件：`addressbook/addr_libs.sh.txt`

## 目录遍历

创建一个 Shell 脚本来遍历文件系统树。

示例答案在此：

directories

Shell 脚本教程
第 95 页

## 其他资源链接

这些是互联网上可以找到的许多有用资源中的极少数：

Steve Bourne 的《Unix Shell 简介》。
https://steve-parker.org/sh/bourne.shtml

关于引号和转义字符的非常权威文档
http://www.mpi-inf.mpg.de/departments/rg1/teaching/unixffb-ss98/quoting-guide.html

编写可移植 Shell 脚本时需要注意什么。
http://archive09.linux.com/articles/34658

Unix 罗塔石：
http://bhami.com/rosetta.html

## 感谢！

感谢你购买这本书并一直读到最后！我希望这本书对你是有用的、信息丰富的且有帮助的。

书籍需要评价来让潜在读者了解他们将获得什么。请考虑花五秒钟在 Amazon 上为本电子书打分，甚至撰写一段评论——无论长短随意，一句话或几个段落都可以。

你可能想提到的点：

- 这本书适合什么人群，
- 你从书中收获了什么，
- 你觉得写作风格如何，
- 你预计未来会再次重阅书的某些部分，
- 这对你来说是否是有效的时间利用，

http://amzn.com/B0C2EGNSA – 或直接在 Amazon 上搜索“Shell Scripting Tutorial”

## 600 页的书

本教程的作者 Steve Parker 编写编写了一本完整的书；由 Wrox 出版，书籍《Shell Scripting: Expert Recipes for Linux, Bash and more》在所有优质零售商处买到。ISBN 1118024486。建议零售价 $49.99。Kindle 同样可用：

http://steve-parker.org/book/ 包含详情；书籍可以在在线和实体店购买。

Steve Parker 还写了《How to Build a LAMP Server》，详细介绍了 LAMP 栈的安装以及在其之上构建运行的应用程序，包括 MySQL 配置、phpMyAdmin 的使用和 PHP 开发。该书目前仅在 Amazon 以电子书形式出售；搜索“B00DAI6IATO”或“How to Build a LAMP Server”。

请访问 http://steve-parker.org/publications/ 获取最新信息。

这是一门学习使用 Unix shell 的 Bourne Shell 编程/脚本教程。通过示例结合理论来学习 Linux / Unix shell 脚本。我们将让你很快掌握 Unix shell 脚本编写！

这本详尽且实用的教程贯穿了示例，是根据该内数百名学生和专业人士的广泛反馈编写的，无论他们是否具有 Unix 或 Linux 背景。

![](img/84a50f94dfcd1da09f623b014d3ee18c_103_0.png)

