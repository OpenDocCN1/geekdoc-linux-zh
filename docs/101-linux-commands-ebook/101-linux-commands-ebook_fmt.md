
# 101 条 Linux 命令电子书

# 101 个 Linux 命令 开源电子书

这是一本开源电子书，包含了每个人都应该的 101 个 Linux 命令。无论你是 DevOps/SysOps 工程师、开发者，还是仅仅是一个 Linux 爱好者，你可能在职业生涯的某个时刻需要使用终端。

# Hacktoberfest

本电子书的出版得益于 Hacktoberfest 和开源社区！

# 关于我

我叫 Bobby Iliev，自 2014 年以来我一直担任 Linux DevOps 工程师。我是一个狂热的 Linux 爱好者和开源运动哲学的支持者。我总是尝试那些我不会做的事情以便学习如何去做，并且我相信分享知识。

我认为始终保持专业素养、与优秀的人在一起、努力工作并对每个人友善是非常关重要的。你必须表现出持续高于他人的水平。这才是真正专业人士的标志。

更多信息，请访问我的博客 https://bobbyiliev.com，在 Twitter 上关注我 @bobbyiliev_ 并在 YouTube 上关注

# DigitalOcean

DigitalOcean 是一个云服务平台，为开发者提供喜爱的简单性和企业信任的赖，用于大规模运行生产应用程序。

它提供高可用、安全且可扩展的计算、存储和网络解决方案，帮助开发者更快地构建优秀的软件。

DigitalOcean 成立于 2012 年，办公室位于纽约和马萨诸塞州剑桥市，提供透明且实惠的定价、优雅的用户界面以及最大的开源资源库之一。

更多信息，请访问 https://www.digitalocean.com 或在 Twitter 上关注 @digitalocean。

如果你是 DigitalOcean 的新用户，可以通过此推荐链接获得 100 美元的免费额度并启动你的服务器：

DigitalOcean 100 美元免费额度

# DevDojo

DevDojo 是一个学习一切 Web 开发和网页设计的资源库。在午休时间学习，或者早晨醒后和我们一起喝杯咖啡学习新知识。

加入这个开发者社区，我们可以共同学习、共同构建、共同成长。

加入 DevDojo

欲了解更多，请访问 https://www.devdojo.com 或在 Twitter 上关注 @thedevdojo。

Ibis 是一个 PHP 工具，帮助你使用 markdown 编写电子书。

# ls 命令

`ls` 命令让你查看特定目录（默认是当前工作目录）内部的文件和目录。它通常按字母升序列出文件和目录。

## 示例：

- 1. 显示当前工作目录下的文件：

```
ls
```

- 2. 显示特定目录下的文件和目录：

```
ls {Directory_Path}
```

## 语法：

```
ls [-OPTION] [DIRECTORY_PATH]
```

## 交互式训练

在这个交互式教程中，你将学习使用 `ls` 命令的不同方法：

Tony 讲解的 `ls` 命令

## 附加标志及其功能：

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -l | - | 以长格式格式显示结果 |
| -S | - | 按文件大小排序结果 |
| -t | - | 按修改时间排序结果 |
| -r | --reverse | 反向显示文件和目录（字母降序） |
| -a | --all | 显示所有文件，包括隐藏文件（以点 `.` 开头的文件名） |
| -la | - | 显示包含隐藏文件的长格式文件和目录 |
| -lh | - | 以可读的大小列出长格式文件和目录 |
| -A | --almost-all | 显示所有 `-a` 但不显示 `.`（当前工作目录）和 `..`（父目录） |
| -d | --directory | 不列出目录内部的文件和目录，可以配合 `-l` 使用以显示长格式信息 |
| -F | --classify | 在每个列出的名称末尾添加指示字符，例如：在每个目录名后添加 `/` 字符 |
| -h | --human-readable | 类似 `-l` 但以易读单位而非字节显示文件大小 |

## 设置持久化选项：

使用 `alias` 命令可以为各种命令（包括 `ls`）设置持久化选项。此 `alias` 命令将颜色设置为自动，以长格式列出，并显示可读的文件大小。

```
alias ls="--color=auto -lh"
```

此别名仅在当前会话中有效直到其结束。要使此别名在所有新会话中生效，请将命令添加到用户的配置文件中，例如 bash 的：`~/.bashrc`

## cd 命令

`cd` 命令用于更改当前工作目录（即当前用户所在的目录）。"cd" 代表 "change directory"（更改目录），它是 Linux 终端中最常用的命令之一。

在导航系统时，`cd` 命令通常与 `ls` 命令结合使用（见第1章），不过你也可以按两次 `TAB` 键来列出你刚刚切换的新目录的内容。

## 使用示例：

- 1. 更改当前工作目录：

```
cd <specified_directory_path>
```

- 2. 将当前工作目录更改到主目录：

```
cd ~
```

或者

```
cd
```

- 3. 切换到上一个目录：

```
cd -
```

这将显示上一个目录的绝对路径。

- 4. 将当前工作目录更改到系统根目录：

```
cd /
```

## 快速提示

将 `. .` 作为目录将允许你从文件夹"向上"移动：

```
cd ..
```

这也可以多次执行！例如，向上移动三个文件夹：

```
cd ../../..
```

## 语法：

```
cd [OPTIONS] directory
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -L | | 跟踪符号链接。默认情况下，`cd` 的行为类似于指定了 `-L` 选项。 |
| -P | | 不跟踪符号链接。 |

## cat 命令

`cat` 命令允许我们创建单个或多个文件，查看文件内容或合并文件并将输出重定向到终端或文件。

"cat" 代表 "concatenate"（合并），它是 Linux 终端中最常用的命令之一。

## 使用示例：

- 1. 显示文件内容：

```
cat <specified_directory_path>
```

- 2. 在终端中合并文件：

```
cat file1 file2
```

- 3. 创建带有内容的文件：

```
cat > file1
```

- 4. 向文件追加内容：

```
cat file1 >> file2
```

- 5. 将输出重定向到文件：

```
cat file1 > file2
```

- 6. 带行号显示内容：

```
cat -n file1
```

## 语法：

```
cat [OPTION] [FILE]...
```

## 附加标志及其功能：

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -A | --show-all | 显示非打印字符 |
| -B | --show-nonblank | 在以换行符结束的行显示 `$` |
| -E | --show-ends | 在行尾显示 `$` |
| -n | --show-numbers | 生成行号 |
| -T | --show-tabs | 将制表显示为 `^` |
| -s | --squeeze-blank | 压缩多个空行 |

## tac 命令

`tac` 是 Linux 命令，允许你从最后一行逐行查看（`tac` 不会反转每行的内容，只反转行的显示顺序）。它是通过类 `cat` 命名的。

## 使用示例：

- 1. 反向显示文件内容：

```
tac <specified_directory_path>
```

- 2. 反向合并文件：

```
tac file1 file2
```

## 语法：

```
tac [OPTION]... [FILE]...
```

## head 命令

`head` 命令打印文件的前十行。

示例：

```
head filename.txt
```

语法：

```
head [OPTION] [FILENAME]
```

## 获取指定行数的行：

使用 `-n` 选项配合一个数字（应为整数）来指定显示的行数。

示例：

```
head -n 10 foo.txt
```

此命令将显示 `foo.txt` 文件的前十行。

语法：

```
head -n <number> foo.txt
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -c | --bytes=[-]NUM | 打印每个文件的前 `NUM` 字节；如果开头有 `-`，则打印每个文件除最后 `NUM` 字节以外的内容 |
| -n | --lines=[-]NUM | 打印前 `NUM` 行而不是前 10 行；打印每个文件除最后 `NUM` 行以外的所有行 |
| -q | --quiet, --silent | 永远不要包含文件名的头部信息 |
| -v | --verbose | 总是打印包含文件名的头部信息 |
| -z | --zero-terminated | 行分隔符为 `NUL`，而不是换行符 |
| --help | | 显示此帮助并退出 |
| --version | | 输出版本信息并退出 |

## tail 命令

`tail` 命令打印文件的最后十行。

示例：

```
tail filename.txt
```

语法：

```
tail [OPTION] [FILENAME]
```

## 使用 tail 获取指定行数的行：

使用 `-n` 选项配合一个数字（应为整数）来指定显示的行数。

示例：

```
tail -n 10 foo.txt
```

此命令将显示 `foo.txt` 文件的最后十行。

## 当文件有新条目时刷新输出

你可以 `tail` 输出你正在查看的文件中添加的任何新行。因此，如果文件中写入了新的一行，它将立即显示在你的输出中。这可以使用 `--follow` 或 `-f` 选项来实现。这对于监控日志文件特别有用。

示例：

```
tail -f foo.txt
```

语法：

```
tail -n <number> foo.txt
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -c | --bytes=[+]NUM | 输出最后 `NUM` 字节；或使用 `-c NUM` 从每个文件的第 `NUM` 字节开始输出 |
| -f | --follow={name\|descriptor} | 随着文件的增长输出追加数据；缺少选项参数意味着 `descriptor` |
| -F | | 等同于 `--follow=name--retry` |
| -n | --lines=[+]NUM | 输出最后 `NUM` 行，而不是最后 10 行；或使用 `-n +NUM` 在配合 `--follow=name` 时从第 `NUM` 行开始输出，如果文件在 `N`（默认 5）次迭代后大小未发生变化，则重新打开文件以检查其是否被解除链接或重命名（这是轮换日志常见情况）；如果配合 `notify`，此选项与 `-f` 配合很少用，在进程 `PID` 死亡后终止 |
| | --max-unchanged-stats=N | |
| | --pid=PID | |
| -q | --quiet, --silent | 永远不要输出包含文件名的头部信息 |
| | --retry | 如果文件不可访问，则继续尝试打开 |
| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -s | --sleep-interval=N | 使用 `-f` 时，每次迭代之间睡眠约 `N` 秒（默认 1.0）；配合 `inify` 和 `--pid=P` 时，每隔 `N` 秒检查一次进程 |
| -v | --verbose | 总是输出包含文件名的头部信息 |
| -z | --zero-terminated | 行分隔符为 `NUL`，而不是换行符 |
| | --help | 显示此帮助并退出 |
| | --version | 输出版本信息并退出 |

## pwd 命令

`pwd` 代表 Print Working Directory（打印工作目录）。它打印从根目录开始的当前工作目录路径。

示例：

```
pwd
```

输出将是你当前的目录：

```
/home/your_user/some_directory
```

语法：

```
pwd [OPTION]
```

提示：你也可以通过打印 `$PWD` 变量来检查：

```bash
echo $PWD
```

输出与 `pwd` 命令的结果相同。

## 选项：

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -L | --logical | 如果环境变量 `$PWD` 包含当前目录的绝对名称且不包含 `.` 或 `..` 组件，则输出这些内容，即使它们包含符号链接。否则，回到默认 (`-P`) 行为。 |
| -P | --physical | 打印当前目录的完全解析名称，名称的所有符号组件都是实际目录名而不是符号链接。 |
| | --help | 显示帮助消息并退出。 |
| | --version | 显示版本信息并退出。 |

默认情况下，`pwd` 的行为类似于指定了 `-L`。

## touch 命令

`touch` 命令修改文件的时间戳。如果指定的文件不存在，则会创建一个同名的空文件。

## 语法

```
touch [OPTION]... FILE...
```

## 选项

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -a | - | 仅更改访问时间。 |
| -c | --no-create | 不创建文件。 |
| -d STRING | --date=STRING | 解析 `STRING` 并使用它代替当前时间。（忽略）此选项不起作用，但被接受以与 BSD 版本的 `touch` 命令兼容。 |
| -f | - | 影响符号链接而不是引用文件（仅在可以的系统上有用） |
| -h | --no-dereference | 更改符号链接的时间戳。此选项隐含 `-c`，如果文件不存在则创建它。 |
| -m | - | 更改修改时间。 |
| -r=FILE | --reference=FILE | 使用此文件代替当前时间。 |
| -t STAMP | - | 使用数字时间代替当前时间。`STAMP` 的格式为 `[[CC][YY]]MMDDhhmm[.ss]`。 |
| | --time=WORD | 指定设置何种类型时间的替代方案（例如：访问、修改或更改）。 |

示例：

1. 如果 `file.txt` 存在，则将所有时间戳设置为当前时间。如果不存在，则创建一个同名的文件。

```
touch file.txt
```

2. 如果 `file.txt` 存在，则将其修改时间设置为当前时间。如果不存在，则创建一个同名的文件。

```
touch -m file.txt
```

3. 如果 `file.txt` 存在，则将其访问时间设置为当前时间。如果不存在，则创建一个同名的文件。

```
touch -a file.txt
```

4. 如果 `file.txt` 是符号链接，则更改链接本身的时间戳而不是引用文件。如果链接不存在，则无操作。

```
touch -h file.txt
```

5. 如果 `file.txt` 存在，则将其访问和修改时间更改为 `file.a`。如果 `file.txt` 不存在，则无操作。注意，在此情况下 `file.a` 必须已存在。

```
touch -cr file.a file.txt
```

6. 将 `file.txt` 的访问时间和修改时间设置为今年 2 月 1 日。更改时间将设置为当前时间。

```
touch -d "1 Feb" file.txt
```

## cal 命令

`cal` 命令在终端显示格式化的日历。如果没有选项，`cal` 显示当前月份并高亮今日。

语法：

```
cal [general options] [-jy] [[month] year]
```

选项：

| 选项 | 描述 |
| --- | --- |
| -h | 不高亮今日。 |
| -m month | 指定要显示的月份。月份指定符可以是全称（如 `February`）、至少三个字母的缩写（如 `Feb`）或数字（如 `2`）。如果你指定数字并在后面跟着字母 `f` 或 `p`，则分别显示明年或去年的月份。例如，`-m 2f` 显示明年的二月。 |
| -y year | 指定要显示的年份。例如，`-y 1970` 显示 1970 年全年日历。 |
| -3 | 显示上个月、本月和下个月。 |
| -1 | 仅显示本月。这是默认设置。 |
| -A num | 显示指定月份之后的 `num` 个月。例如，`-3 -A 3` 显示上个月、本月以及之后的四个月；`-y 1970 -A 2` 显示 1970 年的所有月份以及 1971 年的前两个月。 |
| -B num | 显示指定月份之前的 `num` 个月。例如，`-3 -B 2` 显示之前的三个月、本月和下个月。 |
| -d YYYY-MM | 按当前月份为 `YYYY` 年 `MM` 月操作。 |

## 示例：

- 1. 显示本月的日历，并高亮今天。

```
cal
```

- 2. 与上命令相同，但不高亮今天。

```
cal -h
```

- 3. 显示上个月、本月和下个月。

```
cal -3
```

- 4. 显示整年的日历。

```
cal -y
```

- 5. 显示 2000 年的完整日历。

```
cal -y 2000
```

- 6. 与上一个命令相同。

```
cal 2000
```

- 7. 显示今年 12 月的日历。

```
cal -m [December, Dec, or 12]
```

- 10. 显示 2000 年 12 月的日历。

```
cal 12 2000
```

## bc 命令

`bc` 命令提供了通过命令行执行数学计算的功能。

## 示例：

- 1. 算术：

```
Input : $ echo "11+5" | bc
Output : 16
```



# 2. 增量：`++`

- `var--`：后置增运算符，先使用变量的结果，然后变量加1。
- `++var`：前置增运算符，先增加变量，然后存储变量的结果。

```
Input: $ echo "var=3;++var" | bc
Output: 4
```

# 3. 减量：

- `var--`：后置减运算符，先使用变量的结果，然后变量减1。
- `--var`：前置减运算符，先减少变量，然后存储变量的结果。

```
Input: $ echo "var=3;--var" | bc
Output: 2
```

# 4. 赋值：

- `var = value`：将值赋给变量
- `var +=`：类似于 `var = var + value`
- `var -=`：类似于 `var = var - value`
- `var *=`：类似于 `var = var * value`
- `var /=`：类似于 `var = var / value`
- `var ^`：类似于 `var = var ^ value`
- `var %=`：类似于 `var = var % value`

```
Input: $ echo "var;var" | bc
Output: 4
```

# 5. 比较或关系：

- 如果比较为真，则结果为 1。否则（假）返回 0。
- `expr1<expr2`：如果 `expr1` 严格小于 `expr2`，结果为 1。
- `expr1<=expr2`：如果 `expr1` 小于或等于 `expr2`，结果为 1。
- `expr1>expr2`：如果 `expr1` 严格大于 `expr2`，结果为 1。
- `expr1>=expr2`：如果 `expr1` 大于或等于 `expr2`，结果为 1。
- `expr1==expr2`：如果 `expr1` 等于 `expr2`，结果为 1。
- `expr1!=expr2`：如果 `expr1` 不等于 `expr2`，结果为 1。

```
Input: $ echo "6<4" | bc
Output: 0
```

```
Input: $ echo "2==2" | bc
Output: 1
```

# 6. 逻辑或布尔：

- `expr1 && expr2`：如果两个表达式都非零，则结果为 1。
- `expr1 || expr2`：如果其中一个表达式非零，则结果为 1。
- `! expr`：如果 `expr` 为 0，则结果为 1。

```
Input: $ echo "! 1" | bc
Output: 0
```

```
Input: $ echo "10 && 5" | bc
Output: 1
```

# 语法：

```
bc [-hlswqv] [long-options] [ file ... ]
```

# 其他标志及其功能：

注意：此不包含选项的详尽列表。

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -i | --interactive | 强制进入交互模式 |
| -l | --mathlib | 使用预定义的数学例程 |
| -q | --quiet | 打开 bc 的交互模式但不打印页眉 |
| -s | --standard | 将非标准的 bc 结构视为错误 |
| -w | --warn | 使用非标准 bc 结构时提供警告 |

# 注意事项：

1. 在脚本中使用 `bc` 可以进一步体会其能力。除了基础算术运算外，`bc` 还支持增/减、复杂计算、逻辑比较等。
2. `bc` 的两个标志指的是非标准结构。例如如果你评估 `100>50 | bc`，将得到一个奇怪的警告。根据 `bc` 的 POSIX 页面，关系运算符仅在 `if`、`while` 或 `for` 语句中使用时才有效。

# df 命令

Linux/Unix 中的 `df` 命令用于显示磁盘使用情况和信息。`df` 是 "disk free"（磁盘可用）的缩写。

`df` 显示包含每个文件名参数的文件系统上可用的磁盘空间。如果没有给出文件名，则显示所有当前挂载文件系统的可用空间。

# 语法

```
df [OPTION]... [FILE]...
```

# 选项

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -a | --all | 包含所有文件系统 |
| -B | --block-size=SIZE | 块大小 |
| -h | --human-readable | 人类可读格式 |
| -H | --power-of-1024 | 以1024的幂打印 |
| -i | --inodes | 显示索引节点 |
| -l | --local | 仅限本地文件系统 |
| -m | --block-size=M | 以MB为单位 |
| -P | --portability | 使用标准格式 |
| -s | --total | 输出汇总 |
| -T | --type | 显示文件类型 |
| -x | --exclude=TYPE | 排除文件系统类型 |
| --help | | 显示帮助信息并退出 |
| --version | | 输出版本信息并退出 |

# 示例：

1. 显示磁盘空间
```
df
```

2. 以人类可读格式显示可用空间
```
df -h
```

3. 显示特定文件系统的可用空间
```
df -hT
```

4. 显示所有文件系统的索引节点
```
df -i
```

5. 显示所有文件系统的文件类型
```
df -T
```

6. 从输出中排除文件系统类型
```
df -x
```

# help 命令

`help` 命令显示关于内置命令的信息。显示内置命令的信息。

如果指定了 `PATTERN`，该命令将为匹配 `PATTERN` 的所有命令提供详细帮助，否则将打印主题列表。

# 语法

```
$ help [-dms] [PATTERN ...]
```

# 选项

**选项描述**

- `d`：为每个主题输出简短描述。
- `m`：以伪手册格式显示用法。
- `s`：为匹配指定 `PATTERN` 的每个主题输出简短用法摘要。

# 示例：

1. 获取 `cd` 命令的完整信息
```
$ help cd
```

2. 获取 `pwd` 命令的简短描述
```
$ help -d pwd
```

3. 获取 `cd` 命令的语法
```
$ help -s cd
```

# 示例

1. 打印质数的质因数。
```
$ factor 50
```

2. 打印非质数的质因数。
```
$ factor 75
```

# uname 命令

`uname` 命令允许您打印系统信息，并默认输出内核名称。

# 语法：

```
$ uname [OPTION]
```

# 示例

1. 输出所有系统信息。
```
$ uname -a
```

2. 输出内核版本。
```
$ uname -v
```

# 选项

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -a | --all | 打印所有信息，如果未知则跳过处理器和硬件平台信息。 |
| -s | --kernel-name | 打印内核名称。 |
| -n | --nodename | 打印网络节点主机名。 |
| -r | --kernel-release | 打印内核发布版本。 |
| -v | --kernel-version | 打印内核版本。 |
| -m | --machine | 打印机器硬件名称。 |
| -p | --processor | 打印处理器类型（不可移植）。 |
| -i | --hardware-platform | 打印硬件平台（不可移植）。 |
| -o | --operating-system | 打印操作系统。 |

# mkdir 命令

Linux/Unix 中的 `mkdir` 命令用于创建目录。

# 语法

```
$ mkdir [-m=mode] [-p] [-v] [-Z=context] directory [directory ...]
```

# 示例

1. 创建一个名为 `myfiles` 的目录。
```
$ mkdir myfiles
```

2. 在家目录下创建一个名为 `myfiles` 的目录：
```
$ mkdir ~/myfiles
```

3. 创建 `mydir` 目录，并设置其文件模式（`-m`），使得所有用户（`a`）均可以读取（`r`）、写入（`w`）和执行（`x`）该目录。
```
$ mkdir -m a=rwx mydir
```

您还可以创建目录的子目录。如果父目录不存在，它会先创建父目录。如果父目录已经存在，它将继续创建子目录，而不会产生错误信息。

对于目录来说，这意味着系统上的任何用户都可以查看（“读取”）并在目录中创建/修改/删除（“写入”）文件。任何用户还可以进入（“执行”）该目录，例如使用 `cd` 命令。

4. 创建目录 `/home/test/src/python`。如果任何父目录 `/home`、`/home/test` 或 `/home/test/src` 尚未存在，它们将被自动创建。
```
$ mkdir -p /home/test/src/python
```

# 选项

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -m | --mode=MODE | 设置文件模式（类似于 `chmod`），不是 `a=rwx - umask`。 |
| -p | --parents | 如果目录已存在时不报错，根据需要创建父目录。 |
| -v | --verbose | 为每个创建的目录打印信息。 |
| -Z | --context=CTX | 将每个创建目录的 SELinux 安全上下文设为 `CTX`。 |
| | --help | 显示帮助信息并退出。 |
| | --version | 输出版本信息并退出。 |

# gzip 命令

Linux/Unix 中的 `gzip` 命令用于压缩/解压数据。

# 使用

## 压缩文件

**操作：** --- 压缩文件

**详情：** --- 通过压缩减小文件大小

**命令：**

```
gzip file_name
```

## 解压文件

**操作：** --- 解压文件

**详情：** --- 在数据和大小上恢复文件的原始格式

**命令：**

```
gzip -d archive_01.gz
```

## 压缩多个文件：

**操作：** --- 压缩多个文件

**详情：** --- 将多个文件压缩成多个归档

**命令：**

```
gzip file_name_01 file_name_02
```

# 压缩文件：

**操作：** --- 压缩文件

**详情：** --- 通过压缩减小文件大小

**命令：**

```
gzip file_name
```

# 压缩多个文件：

**操作：** --- 压缩多个文件

**详情：** --- 将多个文件压缩成多个归档

**命令：**

```
gzip file_name_01 file_name_02
```

# 压缩文件：

**操作：** --- 压缩文件

**详情：** --- 通过压缩减小文件大小

**命令：**

```
gzip file_name
```

# 压缩文件：

**操作：** --- 压缩文件

**详情：** --- 通过压缩减小文件大小

**命令：**

```
gzip file_name
```

# 压缩多个文件：

**操作：** --- 压缩多个文件

**详情：** --- 将多个文件压缩成多个归档

**命令：**

```
gzip file_name_01 file_name_02
```

# 示例：

**top**

1. 显示运行进程的动态实时信息：
```
top
```

2. 按内部内存大小对进程进行排序（默认顺序 -进程 ID）：
```
top -o mem
```

3. 先按 CPU 排序，再按运行时间排序：
```
top -o cpu -o time
```

4. 仅显示指定用户拥有的进程：
```
top -user {user_name}
```

**htop**

1. 显示运行进程的动态实时信息。`top` 的增强版本。
```
htop
```

2. 显示特定用户拥有的进程：
```
htop --user {user_name}
```

3. 按指定的 `sort_item` 对进程进行排序，使用 `htop --sort help` 查看可用选项：
```
htop --sort {sort_item}
```

# 语法：

```
top [OPTIONS]
```

```
htop [OPTIONS]
```

# 附加标志及其功能：

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| -a | - | 按内存使用情况排序。 |
| -b | - | 批模式操作。以“批模式”启动 `top`，这有助于将 `top` 的输出发送到其他程序或文件。在此模式下，`top` 将不会接受输入并运行到你通过 `-n` 命令行选项设置的迭代限制或被杀死。 |
| -h | - | 帮助。 |
| -U | -user | 仅显示用户拥有的进程。 |
| -u | - | 这是等同于：`-o cpu -O time` 的别名。 |

# sl 命令

Linux 中的 `sl` 命令是一个幽默程序，它会在你的终端上运行一辆蒸汽机（sl）。

```
      (()) ( ) () ( ) () o o o o o
         )
      (oooo)
         )
      (eeee)
  D  ==---II===
  |  |  H  |  |  |  =====
  |  |  H  |  |  |         A
  |  |  H  |  |  |      =====
  |  |     [--] 0
  /| o |--- /--- /--- /---/  V
  /|-=-|=O==--O==--==O/ /__|_|___|/ /__|_|___|_
```

# 安装

在运行之前安装该包。

```
sudo apt install sl
```

# 语法

```
sl
```

# echo 命令

`echo` 命令允许你显示作为参数传递的文本行/字符串。

# 示例：

1. 显示作为参数传递的文本行或字符串：
```
echo Hello There
```

2. 类似于 `ls` 命令，显示所有文件/文件夹：
```
echo *
```

3. 将文本保存到名为 `foo.bar` 的文件中：
```
echo "Hello There" > foo.bar
```

4. 将文本追加到名为 `foo.bar` 的文件中：
```
echo "Hello There" >> foo.bar
```

# 语法：

```
echo [option] [string]
```

它通常用于 shell 脚本和批处理文件，用于向屏幕或文件输出状态文本。配合它使用的 `-e` 可以启用反斜杠转义的解释。

# 附加选项及其功能：

| 选项 | 描述 |
| --- | --- |
| \b | 删除文本中间所有的空格 |
| \c | 使用退格符解释器`-e`抑制末尾换行以继续执行而不产生新行。 |
| \n | 在使用处创建新行 |
| \t | 创建水平制表符 |
| \r | 使用退格符解释器`-e`创建回车，以便输出中产生指定的回车 |
| \v | 创建垂直制表符 |
| \a | 使用退格符解释器`-e`警报以产生声音警报 |
| \n | 忽略输出末尾换行。 |

# finger 命令

`finger` 显示有关系统用户的信息。

# 示例：

1. 查看特定用户的详细信息。
```
finger abc
```

输出：

```
Login: abc Name: (null)
Directory: /home/abc Shell: /bin/bash
 since Mon Nov 1 18:45 (IST) on :0 (messages for)
 since Mon Nov 1 18:46 (IST) on pts/0 from :0.0
New mail received Fri May 7 10:33 2013 (IST)
Unread since Sat Jun 7 12:59 2003 (IST)
No Plan.
```

2. 查看用户的登录详细信息和空闲状态：
```
finger -s root
```

输出：

| Login Name | Tty | Idle | Login Time |
|---|---|---|---|
| Office Office Phone | *1 | 19d | Wed 17:45 |
| root root | *2 | 3d | Fri 16:53 |
| root root | *3 | | Mon 20:20 |
| root root | *ta | 2d | Tue 15 |

# 语法：

```
finger [options] [user]
```

# 附加标志及其功能：



## `finger`我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。命令

`finger` 命令用于显示系统中用户的相关信息。

## 语法

`finger` 命令的语法为：

```
finger [options] [user]
```

## 选项

- `-l` | 长格式输出。
- `-m` | 匹配用户。
- `-p` | 仅打印详情。
- `-s` | 显示账户状态。

## 附加信息

## 默认格式

默认格式包括：

- 用户名
- 终端
- 空闲时间
- 登录时间

## 选项

- `-a`: 显示所有用户。
- `-d`: 删除用户的密码。
- `-e`: 立即使账户过期。
- `-h`: 显示帮助信息。
- `-i`: 禁用账户。
- `-l`: 锁定密码。
- `-q`: 静默模式。
- `-S`: 显示账户状态。

## `w` 命令

`w` 命令显示当前在机器上活跃的用户及其进程的信息。

## 示例

1. 不带参数运行`w`命令将显示登录用户及其进程的列表。

```
w
```

2. 显示名为`hope`的用户的信息。

```
w hope
```

## 语法

```
finger [-l] [-m] [-p] [-s] [username]
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-h` | `--no-header` | 不打印表头。 |
| `-u` | `--no-current` | 在计算当前进程和 CPU 时间时忽略用户名。（要查看示例，请通过`su`切换到 root 用户，然后运行`w -u`。） |
| `-s` | `--short` | 显示简短输出（不打印登录时间、CPU 或 PCU 时间）。 |

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-f` | `--from` | 切换是否打印来自（远程主机名）字段。发布时的默认设置是不打印“来自”字段，但系统维护者可能编译了默认显示“来自”字段的版本。 |
| `--help` | `-` | 显示帮助信息并退出。 |
| `-V` | `--version` | 显示版本信息并退出。 |
| `-o` | `--old-style` | 旧式输出（对于小于一分钟的空闲时间打印空格）。 |
| `user` | `-` | 仅显示指定用户的信息。 |

## 附加信息

输出表头显示（按此顺序）：当前时间、系统运行时间、当前登录的用户数，以及过去 1、5 和 15 分钟的系统负载平均值。

每个用户将显示以下条目：

- 登录名`tty`
- 姓名 远程地址
- 所在的主机
- 登录时长 登录时长的空闲时间
- 空闲时间`JCPU`
- `PCPU`
- 当前进程的命令行

`JCPU`时间是所有连接到该`tty`的进程所使用的时间。它不包括过去的后台作业，但包括当前正在运行的后台作业。

`PCPU`时间是“what”字段中指定的当前进程所使用的时间。

## `whoami` 命令

`whoami` 命令显示当前有效用户的用户名。换句话说，它在执行时仅打印当前登录用户的用户名。

要显示您的有效用户 ID，只需在终端中输入`whoami`：

```
manish@godsmack:~~$ whoami
```

## 输出

```
manish
```

## 语法

```
whoami [-OPTION]
```

只有两个选项可以传递给它：

- `--help`: 用于显示帮助并退出。

## 示例

```
whoami --help
```

## 输出

```
Usage: whoami [OPTION]...
打印与当前有效用户 ID 关联的用户名。
等同于 id -un。
  --help      显示此帮助并退出
  --version   输出版本信息并退出
```

- `--version`: 输出版本信息并退出。

## 示例

```
whoami --version
```

## 输出

```
whoami (GNU coreutils) 8.32
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later
<https://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute
it.
There is NO WARRANTY, to the extent permitted by law.
Written by Richard Mlynarik.
```

## `history` 命令

如果你输入`history`，将获得最后使用的 500 条命令的列表。这让你有机会复制和粘贴过去执行过的命令。

这与`grep`结合使用非常强大。因此你可以在命令历史中搜索命令。

## 示例

1. 如果你想在历史记录中搜索过去运行过的`artisan`命令。

```
history | grep artisan
```

2. 如果你只想显示最后 10 条命令。

```
history 10
```

## `login` 命令

`login` 命令启动用户会话。

## 语法

```
$ login [-p] [-h host] [-H] [-f username|username]
```

## 标志及其功能

| 短标志 | 描述 |
| --- | --- |
| `-f` | 用于跳过登录身份验证。此选项通常用于`getty(8)`的自动登录功能。 |
| `-h` | 用于其他服务器（如`telnetd(8)`）将远程主机名传递给`login`，以便将其置于`utmp`和`wtmp`中。仅允许超级用户使用此选项。 |
| `-p` | `getty(8)`通知`login`保留环境变量。 |
| `-H` | 用于其他服务器（例如`telnetd(8)`）告诉`login`在`login:`提示中抑制打印主机名。 |
| `--help` | 显示帮助文本并退出。 |
| `-v` | 显示版本信息并退出。 |

## 示例

以`abhishek`的身份登录系统，请遵循以下操作：

```
$ login
```

## `whoami` 命令

`whoami` 命令显示当前有效用户的用户名。

## `cp` 命令

## 语法

`cp` 命令的通用语法如下：

```
cp [OPTION] SOURCE DESTINATION
cp [OPTION] SOURCE DIRECTORY
cp [OPTION] SOURCE-1 SOURCE-2 SOURCE-3 SOURCE-n DIRECTORY
```

第一和第二语法用于将源文件复制到目标文件或目录。第三种语法用于将多个源（文件）复制到目录。

## 一些实用选项

- `-i`（交互式）`i`代表交互式复制。使用此选项，系统在覆盖目标文件之前会警告用户。`cp`会提示响应，如果你按下回车则覆盖文件，按下任何其他选项则留不复制。

```
$ cp -i file1.txt fileName2.txt
cp: overwrite 'file2.txt' y
```

- `-b`（备份）`-b`（备份）：使用此选项，命令会在相同文件夹中以不同的名称和格式创建目标文件的备份。

```
$ ls
a.txt b.txt

$ cp -b a.txt b.txt

$ ls
a.txt b.txt b.txt~
```

- `-f`（强制）如果系统因为用户对文件没有写入权限而无法打开目标文件进行写入操作，则通过`-f`使用`cp`命令选项时，会先删除目标文件，然后将内容从源文件复制到目标文件。

```
$ ls -l b.txt
-r-xr-xr-x+ 1 User User 3 Nov 24 08:45 b.txt
```

用户、组和其他用户没有写入权限。

如果没有`-f`选项，命令将不会被执行：

```
$ cp a.txt b.txt
cp: cannot create regular file 'b.txt': Permission denied
```

使用`-f`选项，命令将成功执行：

```
$ cp -f a.txt b.txt
```

## 附加选项及其功能

| 短选项 | 长选项 | 描述 |
| --- | --- | --- |
| `-i` | `--interactive` | 在覆盖前进行提示 |
| `-f` | `--force` | 如果无法打开已的目标文件，则将其删除并重试 |
| `-b` | | 在同一文件夹中创建一个与目标同名的备份文件，并使用不同的格式 |
| `-r` 或 `-R` | `--recursive` | `cp`命令通过递归复制整个目录来显示其递归行为 |
| `-n` | `--no-clobber` | 不覆盖现有文件（覆盖之前的`-i`） |
| `-p` | | 尽可能保留指定的属性（默认：模式、所有者、时间戳），如果可能还包括额外属性：上下文、链接、`xattr`、所有 |

## `mv` 命令

`mv`命令允许你像 UNIX 一样将一个或多个文件或目录从一个文件系统移动到另一个。它可以两个不同的功能：

- 重命名文件或文件夹。
- 将一组文件移动到不同的目录。

注意：重命名过程中不会消耗磁盘额外空间，且`mv`命令不会提供确认提示。

## 语法

```
mv [options] 源 (文件或目录) 目标
```

## 示例

1. 重命名名为`old_name.txt`的文件：

```
mv old_name.txt new_name.txt
```

2. 将名为`essay.txt`的文件从当前目录移动到`assignments`目录并重命名为`essay1.txt`：

```
mv essay.txt assignments/essay1.txt
```

3. 将名为`essay.txt`的文件从当前目录移动到`assignments`目录而不重命名：

```
mv essay.txt assignments
```

## 附加选项及其功能

| 短选项 | 长选项 | 描述 |
| --- | --- | --- |
| `-f` | `--force` | 强制覆盖目标文件进行移动，无需提示 |
| `-i` | `--interactive` | 在覆盖前进行交互式提示 |
| `-u` | `--update` | 仅当源文件比目标文件新或目标文件缺失时移动 |
| `-n` | `--no-clobber` | 不覆盖现有文件 |
| `-v` | `--verbose` | 打印源文件目标文件 |
| `-b` | `--backup` | 为现有目标文件创建备份 |

## `ps` 命令

`ps`命令用于识别系统上运行的程序和进程以及它们正在使用的资源。它经常与其他命令（如`grep`）配合管道使用以搜索程序/进程，或与`less`配合使用以便用户可以一次分析页输出。

假设你有一个程序，它在导出视频时因占用系统资源而闻名，你想关闭它，但 GUI 已经无响应了。

## 示例

1. 你想找到`openshot`的 PID 并杀死它。

```
ps aux | grep openshot
kill -openshot PID>
```

2. 显示所有运行的进程：

```
ps -A
```

## 语法

```
ps [options]
```

当不带任何选项运行时，它是没用的，并将打印：`CMD` - 正在运行的可执行进程/(程序)，`PID` - 进程 ID，`TTY` - 终端类型以及`Time` - 进程利用 CPU 或线程的时间。

## 常用选项

如果你只想从此页记住一件事，请记住这三个字母`aux`：`a` - 显示所有运行的进程，包括由其他用户运行的进程；`u` - 显示进程的有效用户，即使用该进程文件访问权限的人；`x` - 显示没有关联 TTY 的进程。

## 附加选项

| 选项 | 描述 |
| --- | --- |
| `a` | 显示所有带有终端 (`tty`) 的进程 |
| `-A` | 列出所有进程。与`-e`相同 |
| `-a` | 显示除会话领导和与终端关联进程之外的所有进程 |
| `-d` | 选择除会话领导以外的所有进程 |
| `--deselect` | 显示除符合指定条件以外的所有进程。与`-N`相同 |
| `-e` | 列出所有进程。与`-A`相同 |
| `-N` | 显示除符合指定条件以外的所有进程。与`--deselect`相同 |
| `T` | 选择所有与此终端关联的进程。与不带参数的`-t`选项相同 |
| `r` | 将选择限制为仅运行的进程 |
| `--help simple` | 显示基本选项 |
| `--help all` | 显示所有可用选项 |

另一个实用的命令是`top`，它每十秒提供一次进程及其资源的实时快照。

## `kill` 命令

Linux 中的`kill`命令（位于`/bin/kill`）是一个用于终止进程的内置命令。该命令向进程发送信号。如果没有指定信号，则发送`SIGTERM`。通常，`kill`命令通过知道进程名称或 PID 来杀死进程。

信号可以通过名称（例如`-HUP`或`-SIGHUP`）或数字（例如`-1`）或选项`-s`来指定。

## 语法

```
kill [options] PID 或 名称
```

## 示例

1. 列出所有可用的信号：

```bash
kill -l
```

2. 使用`SIGTERM`杀死所有匹配名称`conky`的进程：

```bash
kill conky
# OR
kill -SIGTERM conky
# OR
kill -15 conky
```

3. 通过名称杀死进程：

```bash
kill -f processky
```

4. 杀死特定的 PID：

```bash
kill 1234
```

## `killall` 命令

`killall`向运行的任何指定命令的**所有**进程发送信号。如果指定了信号名称，则发送`SIGTERM`。通常，`killall`命令通过知道进程的名称来杀死进程。

信号可以通过名称（例如`-HUP`或`-SIGHUP`）或数字（例如`-1`）或选项`-s`来指定。

如果命令不是正则表达式（选项`-r`）且包含斜杠 (`/`)，则执行该特定文件的进程将被选中杀死，与其名称无关。

如果每个列出的命令至少有一个进程被杀死，或者没有列出命令且至少有一个进程匹配`-u`和`-Z`则，则`killall`返回零状态码。否则返回非零状态码。

`killall`进程永远不会杀死自己（但可能会杀死其他的`killall`进程）。

## 示例

1. 使用`SIGTERM`杀死所有匹配名称`conky`的进程：

```
killall conky
# OR
killall -SIGTERM conky
# OR
killall -15 conky
```

我也能够杀死 Wine（在 Linux 上运行的 Windows exe 文件）应用程序。

```
killall TQ.exe
```

2. 列出所有支持的信号：

```bash
$ killall -l
HUP INT QUIT ILL TRAP ABRT BUS FPE KILL USR1 SEGV USR2 PIPE
ARM TERM STKFLT
CHLD CONT STOP TST TTIN TTOU URG CPU XFSZ VTALM PROF WINCH
POLL PWR SYS
```

关于数字：

```bash
$ for s in $(killall -l); do echo "$s " && kill -l $$; done
HUP 1
INT 2
QUIT 3
ILL 4
TRAP 5
ABRT 6
BUS 7
FPE 8
KILL 9
USR1 10
SEGV 11
USR2 12
PIPE 13
ALRM 14
TERM 15
STKFLT 16
CHLD 17
CONT 18
STOP 19
TSTP 20
TTIN 21
TTOU 22
URG 23
XCPU 24
XFSZ 25
VTALM 26
PROF 27
WINCH 28
POLL 29
PWR 30
SYS 31
```

3. 在杀死之前进行询问，以防止误杀：

```bash
$ killall -i conky
Kill conky(1685) ? (y/N)
```

4. 杀死所有进程并等待进程结束。

```bash
killall -w conky
```

5. 根据时间杀死：

```bash
## 杀死所有运行小于 2 分的 firefox
killall -y 2m firefox

## 杀死所有运行超过 2 小时的 firefox
killall -o 2h firefox
```

## 语法

```bash
killall [OPTION]... [-- NAME]...
killall -L, --list
killall -V, --version
```



##我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。附加标志及其功能

| 标志 | 长标志 | 描述 |
| - | - | - |
| `-e` | `--exact` | 对很长的名称要求精确匹配 |
| `-I` | `--ignore-case` | 忽略大小写的进程名匹配 |
| `-g` | `--process-group` | 杀死进程组而非单个进程 |
| `-y` | `--young-than` | 杀死运行小于 TIME 的进程 |
| `-o` | `--older-than` | 杀死运行超过 TIME 的进程 |
| `-i` | `--interactive` | 在杀死前请求确认 |
| `-l` | `--list` | 列出所有已知信号名称 |
| `-q` | `--quiet` | 不打印错误信息 |
| `-r` | `--regexp` | 将 NAME 解释为扩展正则表达式 |

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-s` | `--signal SIGNAL` | 发送此信号而非 `SIGTERM` |
| `-u` | `--user USER` | 只杀死以 USER 运行的进程 |
| `-v` | `--verbose` | 报告信号是否成功发送 |
| `-w` | `--wait` | 等待进程退出 |
| `-n` | `--ns PID` | 匹配与 PID 属于同一命名空间的进程 |
| `-Z` | `--context` | REGEXP 只杀死具有上下文的进程（必须在其他参数之前） |

## 相关命令

`kill`, `pidof`

## env 命令

Linux/Unix 中的 `env` 命令用于打印当前环境变量列表，或者在自定义环境中运行程序而不改变当前环境。

### 语法

```bash
env [OPTION]... [-] [NAME=VALUE]... [COMMAND [ARG]...]
```

### 用法

1. 打印当前设置的环境变量集

```bash
env
```

2. 在空环境运行命令

```bash
env -i command_name
```

3. 从环境中移除变量

```bash
env -u variable_name
```

4. 每个输出都以 NULL 结尾

```bash
env -0
```

## 选项完整列表

| 短标志 | 长标志 | 描述 |
| - | - | - |
| `-i` | `--ignore-environment` | 从空环境开始 |
| `-0` | `--null` | 每行输出以 `NUL` 结尾而非换行符 |
| `-u` | `--unset=NAME` | 从环境中移除变量 |
| `-C` | `--chdir=DIR` | 工作目录到 DIR |
| `-S` | `--split-string=S` | 将 S 处理并拆分为单独参数。用于 `shebang` 行中传递多个参数 |
| `-v` | `--debug` | 输出每个处理步骤的详细信息 |
| | `--help` | 打印帮助信息 |
| | `--version` | 输出版本信息 |

## printenv 命令

`printenv` 输出指定环境变量的值。如果指定了 `VARIABLE`，则打印它们所有的键值对。

### 示例

1. 显示所有环境变量的值

```bash
printenv
```

2. 显示当前用户的目录位置

```bash
printenv HOME
```

3. 使用 `--null` 命令行选项作为输出项之间的分隔符

```bash
printenv --null SHELL
```

注意：默认情况下，`printenv` 命令使用换行符作为输出项之间的分隔符。

### 语法

```bash
printenv [OPTION]... PATTERN...
```

4. 显示简短列表：

```bash
ifconfig -s
```

5. 显示特定网络接口（例如 `eth0`）的详情：

```bash
ifconfig eth0
```

6. 激活接口的驱动（例如 `eth0`）：

```bash
ifconfig eth0 up
```

7. 停用接口的驱动（例如 `eth0`）：

```bash
ifconfig eth0 down
```

8. 为网络接口分配特定的 IP 地址（例如 `eth0`）：

```bash
ifconfig eth0 10.10.1.23
```

9. 更改网络接口的 MAC（媒体访问控制）地址（例如 `eth0`）：

```bash
ifconfig eth0 hw ether AA:BB:CC:DD:EE:FF
```

10. 为网络接口定义子网掩码（例如 `eth0`）：

```bash
ifconfig eth0 netmask 255.255.255.252
```

11. 在网络接口上开启混杂模式（例如 `eth0`）：

```bash
ifconfig eth0 promisc
```

在普通模式下，当网卡接收到数据包时，它会验证该包是否属于自己。如果不是，则会正常丢弃该包。但在混杂模式下，它会接受所有通过网卡的数据包。

12. 在网络接口上禁用混杂模式（例如 `eth0`）：

```bash
ifconfig eth0 -promisc
```

13. 为网络接口设置最大传输单元（MTU）（例如 `eth0`）：

```bash
ifconfig eth0 mtu 1000
```

`MTU` 允许你设置在接口上传输的数据包限制。`MTU` 能够处理单次事务中发送接口的最大数量的字节。

14. 为网络接口添加额外的 IP 地址，你可以为该接口配置网络别名：

```bash
ifconfig eth0:0 10.10.1.24
```

请注意，别名地址与网络接口处于相同的子网掩码。例如，如果你的 `eth0` IP 地址是 `10.10.1.23`，那么别名 IP 地址可以是 `10.10.1.24`。无效的 IP 地址示例是 `10.10.2.24`，因为接口子网掩码是 `255.255.255.224`。

15. 删除网络别名：

```bash
ifconfig eth0:0 down
```

记住，对于每个范围（即相同的地址/子网掩码组合），如果你删除了第一个别名，所有的别名都会被删除。

## Help 命令

运行以下命令查看 `ifconfig` 命令的完整指南：

```bash
man ifconfig
```

## ip 命令

`ip` 命令存在于 `net-tools` 中，用于执行若干网络管理任务。IP 代表 Internet Protocol（网协议）。此命令用于显示或操作路由、设备和隧道。它可以执行诸如配置和修改默认及静态路由、设置 IP 隧道、列出 IP 地址和属性信息、修改接口状态、分配、删除和设置 IP 地址及路由等任务。

### 示例

1. 为特定接口（`eth1`）分配 IP 地址：

```bash
ip addr add 192.168.50.5 dev eth1
```

2. 显示关于网络接口的详细信息，如 IP 地址、MAC 地址信息等：

```bash
ip addr show
```

### 语法

```bash
ip [ OPTIONS ] OBJECT { COMMAND | help }
```

### 附加标志及其功能

| 标志 | 说明 |
| :--- | :--- |
| `-a` | 显示并修改 IP 地址 |
| `-l` | 显示并修改网络接口 |
| `-r` | 显示并更改路由表 |
| `-n` | 显示并操作节点对象 (ARP 表) |
| `-ru` | 路由策略数据库中的规则 |
| `-s` | 输出更多信息。如果选项出现两次或更多，信息量会增加 |
| `-f` | 指定要使用的协议族 |
| `-r` | 使用系统的名称解析器打印 DNS 名称而不是主机地址 |
| `-c` | 配置彩色输出 |

## clear 命令

在 linux 中，`clear` 命令用于清除终端屏幕。

### 示例

```bash
$ clear
```

执行前：

```bash
$ echo Hello World
Hello World
$ clear
```

执行 `clear` 命令后：

```bash
$
```

截图：

```bash
devdojo@bobbyiliev:~/101-linux-commands-ebook$ ls -l
total 20
-rw-r--r-- 1 devdojo devdojo 1068 Oct 13:31 LICENSE
-rw-r--r-- 1 devdojo devdojo 9806 Oct 13:31 README.md
drwxr-xr-x 3 devdojo devdojo 4096 Oct 13:31 ebook
devdojo@bobbyiliev:~/101-linux-commands-ebook$ clear
```

运行命令后，你的终端屏幕将是清的：

```bash
devdojo@bobbyiliev:~/101-linux-commands-ebook$
```

## 安装

`curl` 命令在大多数 Linux 发行版中都自带。但如果系统默认没有携带 `curl`，你需要手动安装。要安装 `curl`，请执行以下命令：

通过执行以下命令更新系统：

```bash
$ sudo apt update
$ sudo apt upgrade
```

现在，执行以下命令安装 `curl` 扩展：

```bash
$ sudo apt install curl
```

执行以下命令验证安装：

```bash
$ curl -version
```

上述命令将显示已安装的 `curl` 命令版本。

## yes 命令

linux 中的 `yes` 命令用于持续输出给定 STRING（字符串）的流。如果未指定 STRING，它将打印 `'y'`。它会重复输出字符串，直到被杀掉（使用类似 `ctrl + c` 的操作）。

### 示例

1. 在终端中无限打印 `hello world` 直到被杀死：

```bash
yes hello world
```

2. 一个更通用的命令：

```bash
yes [STRING]
```

### 选项

它接受以下选项：

- `--help`
  显示此帮助信息并退出
- `--version`
  输出版本信息并退出

## last 命令

此命令向你显示自 `var/log/wtmp` 文件创建以来所有登录和注出的用户列表。你还可以添加一些参数，它们可以显示例如某个用户何时登录以及登录了多久。

如果你想查看最后 5 条日志，只需在命令后添加 `-5`，如下所示：

```bash
last -5
```

如果你想查看最后 10 条，添加 `-10`。

另一个很酷的功能是，如果你添加 `-F`，你可以看到登录和注销时间，包括日期。

```bash
last -F
```

使用此命令可以查看很多内容。如果你需要更多关于此命令的信息，可以运行：

```bash
last --help
```

## locate 命令

`locate` 命令通过由 `updatedb` 命令生成的数据库文件，在文件系统中搜索名称与给定模式匹配的文件和目录。

### 示例

1. 运行 `locate` 命令来搜索名为 `.bashrc` 的文件：

```bash
locate .bashrc
```

输出：

```bash
/etc/bash.bashrc
/etc/sk/.bashrc
/home/linuxize/.bashrc
/usr/share/base-files/dot.bashrc
/usr/share/doc/adduser/examples/adduser.local.conf/examples/sh.bashrc
/usr/share/doc/adduser/examples/adduser.local.conf/examples/sk/dot.bashrc
```

`/root/.bashrc` 文件将不会显示，因为我们是以普通用户运行命令的，没有访问 `/root` 目录的权限。

如果结果列表很长，为了提高可读性，你可以将输出管道到 `less` 命令：

```bash
locate .bashrc | less
```

2. 搜索系统中所有的 `.md` 文件：

```bash
locate *.md
```

3. 搜索所有 `.py` 文件并仅显示 10 个结果：

```bash
locate -n 10 *.py
```

4. 执行不区分大小写的搜索：

```bash
locate -i readme.md
```

输出：

```bash
/home/linuxize/p1/readme.md
/home/linuxize/p2/README.md
/home/linuxize/p3/ReadMe.md
```

5. 返回文件名中所有包含 `.bashrc` 的文件总数：

```bash
locate -c .bashrc
```

输出：

```bash
6
```

6. 以下命令将仅返回文件系统中存在的 `.json` 文件：

```bash
locate -e *.json
```

7. 要执行更复杂的搜索，使用 `-r`（`--regexp`）选项。搜索你系统中所有的 `.mp4` 和 `.avi` 文件并忽略大小写：

```bash
locate --regex "(\.mp4|\.avi)"
```

### 语法

`locate [OPTION]... PATTERN...`

### 其他标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-A` | `--all` | 用于显示匹配所有 PATTERN 的条目，而不是只需其中一个匹配。 |
| `-b` | `--basename` | 用于匹配指定模式的基名。 |
| `-c` | `--count` | 用于在标准输出中写入条目数量。 |
| `-d` | `--database` | 用于替换默认数据库PATH。 |
| `-e` | `--existing` | 用于引用现有文件的条目。如果指定了 `--existing` 选项，将跳过符号链接。 |
| `-h` | `--help` | 用于显示帮助文档。 |
| `-i` | `--ignore-case` | 用于忽略模式的大小写敏感。 |
| `-p` | `--ignore-spaces` | 用于忽略匹配模式时的空格。 |
| `-t` | `--transliterate` | 用于忽略匹配模式时的重音符号。 |
| `-l` | `--limit` | 如果指定，命令在找到 LIMIT 条目后退出。 |
| `-m` | `--mmap` | 用于与 BSD 和 GNU 兼容。 |
| `-0` | `--null` | 使用 `NUL` 字符分隔输出的条目，而不是每个条目占一行。 |
| `-S` | `--statistics` | 用于搜索基本正则。 |
| `-r` | `--regexp` | 用于描述所有正则表达式。 |
| `-V` | `--version` | 用于显示版本和许可信息。 |
| `-w` | `--whename` | 用于匹配模式的完整路径。 |

## iostat 命令

Linux 中的 `iostat` 命令用于监控设备和分区的输入/输出统计信息。它通过观察设备相对于平均传输速率的时间来监控输入/输出。`iostat` 可用于平衡物理磁盘之间的输入/输出。`iostat` 包含在 `sysstat` 包中。如果没有它，你需要先安装。

### 语法

```bash
iostat [ -c ] [ -d ] [ -h ] [ -N ] [ -k ] [ -m ] [ -t ] [ -V ] [ -x ] [ -z ] [ -g group_name ] { device [...] } [ interval [ count ] ]
```

### 示例

1. 显示所有 CPU 和设备的自启动以来报告：

```bash
iostat -d
```

2. 每隔两秒显示一次连续设备报告：

```bash
iostat -d 2
```

3. 所有设备每隔两秒显示六次报告：

```bash
iostat -x sdb 2
```

4. `sda` 和 `sdb` 每隔两秒显示六次扩展报告：

```bash
iostat -p sda 2
```

### 其他标志及其功能

| 短标志 | 描述 |
| --- | --- |
| `-x` | 显示更详细的统计信息。 |
| `-c` | 仅显示 cpu 统计信息。 |
| `-d` | 仅显示设备报告。 |
| `-xd` | 仅显示设备的扩展 I/O 统计信息。 |
| `-k` | 以千字节或兆字节采集统计信息。 |
| `-k2` | 带延迟显示 cpu 和设备统计信息。 |
| `-j` | 显示持久性设备名称统计。 |
| `-p` | 显示块设备的统计信息。 |
| `-N` | 显示 lvm 统计信息。 |

## sudo 命令

`sudo`（"substitute user do" 或 "super user"）命令允许具有适当权限的用户以另一个用户（如超级用户）执行命令。这相当于 Windows 中的“以管理员身份运行”选项。`sudo` 命令允许你将用户账户提升到 `root` 权限。此外，`sudo` 中的 `root` 权限仅临时有效。一旦过期，你必须重新输入密码以重新获得 `root` 权限。警告：使用 `sudo` 命令时要非常小心。在 `root` 身份操作时可能会导致不可逆的灾难性变化！

### 语法

```bash
sudo [-OPTION] command
```



##我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。其他标志及其功能：

| 标志 | 描述 |
| :--- | :--- |
| `-V` (version) 选项导致 `sudo` 打印版本号并退出。如果调用者已经是 root，`-V` 选项将打印 `sudo` 编译时的默认列表以及机器的本地网络地址。 |
| `-l` (list) 选项打印当前主机上允许（和禁止）用户使用的命令。 |
| `-L` (list defaults) 选项列出 `Defaults` 行中的参数，每个参数带有简短描述。此选项与 `grep` 配合使用。 |
| `-h` (help) 选项调用 `sudo` 打印用法信息并退出。如果给出 `v` (validate) 选项，`sudo` 会更新用户的时间戳，必要时提示用户输入密码。这将 `sudo` 超时时间再延长 5 分钟（或 `sudoers` 中设置的超时时间），但不运行命令。 |
| `sudo` 的 `-K` (sure kill) 选项完全移除用户的时间戳。同样，此选项不需要密码。 |

## 参数描述

- `-u` (user) 选项导致 `sudo` 以 root 以外的用户身份运行指定的命令。要指定 uid 而不是用户名，请使用 `#uid`。
- `-s` (shell) 选项如果设置了 `SHELL` 环境变量，则运行该环境变量指定的 shell，否则运行 `passwd` 文件中指定的 shell。
- `--` 标志表示 `sudo` 应该停止处理命令行参数。它在与 `-s` 标志配合使用时最为有用。

## 示例

此命令将您的命令提示符切换为 root 用户身份的 BASH shell：

```
sudo bash
```

您的命令行应该会变为：

```
root@hostname:/home/[username]
```

向文件中添加文本字符串通常用于将软件存储库的名称添加到源文件中，而无需打开文件进行编辑。请结合 `echo`、`sudo` 和 `tee` 命令使用以下语法：

```
echo 'string-of-text' | sudo tee -a [path_to_file]
```

示例：

```
echo "deb http://nginx.org/packages/debian `lsb_release -cs` nginx" | sudo tee /etc/apt/sources.list.d/nginx.list
```

## apt 命令

`apt`（高级软件包系统）命令用于与 `dpkg`（debian 使用的软件包系统）交互。已经有一个 `dpkg` 命令来管理 `.deb` 包了。但 `apt` 是一种更用户友好且更高效的方法。

简单来说，`apt` 是一个用于在 debian Linux 上安装、删除和执行其他操作的命令。

您将主要在具有 `sudo` 权限的情况下使用 `apt` 命令。

## 安装软件包：

`install` 后跟 `package_name` 用于 `apt` 安装新软件包。

语法：

```
sudo apt install package_name
```

示例：

```
sudo apt install g++
```

此命令将在您的系统上安装 `g++`。

## 移除软件包：

`remove` 后跟 `package_name` 用于 `apt` 移除特定的软件包。

语法：

```
sudo apt remove package_name
```

示例：

```
sudo apt remove g++
```

此命令将从您的系统上移除 `g++`。

## 搜索软件包：

`search` 后跟 `package_name` 用于 `apt` 在所有存储库中搜索软件包。

语法：

```
apt search package_name
```

注意：不需要 `sudo`

示例：

```
apt search g++
```

## 移除未使用的软件包：

每当系统上安装依赖于其他软件包的新软件包时，软件包依赖项也会被安装。当软件包被移除时，依赖项将留在系统中。这些遗留的包不再被任何内容使用，可以被移除。

语法：

```
sudo apt autoremove
```

此命令将移除您系统中所有未使用的包。

## 更新软件包索引：

`apt` 软件包索引无非是一个数据库，存储了您系统中启用的可用软件包的记录。

语法：

```
sudo apt update
```

此命令将更新您系统上的软件包索引。

## 升级软件包：

如果您想为已安装的软件包安装最新更新，您可能想要运行此命令。

语法：

```
sudo apt upgrade
```

该命令不会升级任何需要移除已安装软件包的包。

如果您想升级单个软件包，请传递包名：

语法：

```
sudo apt upgrade package_name
```

此命令将您的软件包升级到最新版本。

## yum 命令

`yum` 是 Red Hat Enterprise Linux 中安装、更新、移除和管理软件包的主要软件包管理工具。它是 Yellow Dog Updater, Modified 的缩写。

`yum` 在安装、更新和移除软件包时会执行依赖解析。它可以管理来自系统已安装存储库的或来自 `.rpm` 包的软件包。

## 语法：

```
yum -option command
```

## 示例：

1. 查看过去事务中发生情况的概览：

```
yum history
```

2. 撤销之前的事务：

```
yum history undo <id>
```

3. 使用 'yes' 自动回答安装 firefox：

```
yum -y install
```

4. 将 mysql 更新到最新版本：

```
yum update mysql
```

## 常用使用的 yum 命令：

| 命令 | 描述 |
| :--- | :--- |
| `install` | 安装软件包 |
| `remove` | 移除软件包 |
| `search` | 搜索关键字 |
| `info` | 显示信息 |
| `update` | 更新指定的软件包 |
| `repolist` | 列出存储库 |
| `groupinstall` | 安装组 |
| `clean` | 清除缓存 |

## 附加标志及其功能：

| 短标志 | 长标志 | 描述 |
| :--- | :--- | :--- |
| `-C` | `--cacheonly` | 仅从缓存运行 |
| `-y` | `--assumes` | 对所有问题回答 yes |
|  | `--skip-broken` | 跳过损坏的包 |
| `-v` | `--verbose` | 详细模式 |

## zip 命令

`zip` 命令用于压缩文件并减小其大小。它输出包含一个或多个文件的归包。

## 示例

使用 `zip` 命令压缩单个文件的语法为：

```
zip zipFile.txt
```

这也适用于多个文件：

```
zip zipFile.zip file1.txt file2.txt
```

如果您压缩整个目录，请记得添加 `-r` 标志：

```
zip -r zipFolder.zip Folder/
```

## 语法：

```
zip [OPTION] zipFileName files
```

- `-d` 从 zip 包中删除文件。
- `-u` 更新 zip 包中的文件。此选项可更新指定的包列表。
- `-m` 压缩后删除原始文件。
- `-r` 递归压缩目录，它将递归压缩目录中的文件。
- `-x` 在创建 zip 时排除文件。
- `-v` 详细模式或打印诊断信息。

## unzip 命令

`unzip` 命令将归包中的所有文件提取到当前目录。

## 示例

为了提取文件，语法如下：

```
unzip myZipFile.zip
```

要将 ZIP 文件提取到与当前目录不同的目录，请记得添加 `-d` 标志：

```
unzip myZipFile.zip -d /path/to/directory
```

要解压 ZIP 文件并排除特定的文件或目录，请记得添加 `-x` 标志：

```
unzip myZipFile.zip -x file1.txt file2.txt
```

## 语法：

```
unzip zipFileName [OPTION] [PARAMS]
```

## 可能的选项：

| 标志 | 描述 | 参数 |
| :--- | :--- | :--- |
| `-d` | 将归包提取到不同的目录。 | `/path/to/directory` |

## 参数：

- `-x` 提取归包但不提取指定的文件。
- `-j` 如果压缩包包含文件夹结构，则不创建新的文件夹。
- `-l` 在不提取的情况下列出归包的内容。
- `-n` 不要覆盖现有文件；而是提供替代文件名。
- `-o` 覆盖文件。
- `-P` 提供密码来解压受保护的归包。| `password`
- `-q` 解压时不向标准输出写入状态消息。
- `-t` 测试归包文件是否有效。
- `-v` 在不提取的情况下显示归包的详细（verbose）信息。

## shutdown 命令

`shutdown` 命令允许你以一种安全的方式关闭系统。当执行 `shutdown` 时，系统将通知所有已登录的用户并阻止进一步登录。你可以选择立即关闭系统或在指定时间后关闭系统。

只有具有 root（或 sudo）权限的用户才能使用 `shutdown` 命令。

## 示例：

1. 立即关闭你的系统：

```
sudo shutdown now
```

2. 在 10 分钟后关闭系统：

```
sudo shutdown +10
```

3. 在 5 分钟后带消息关闭系统：

```
sudo shutdown +5 "System will shutdown in 5 minutes"
```

## 语法：

```
shutdown [OPTIONS] [TIME] [MESSAGE]
```

## 附加标志及其功能：

| 短标志 | 长标志 | 描述 |
| :--- | :--- | :--- |
| `-r` | `--reboot` | 重启系统 |
| `-c` | `--cancel` | 取消计划的关机 |

## dir 命令

`dir` 命令列出目录的内容（默认是当前目录）。它与 `ls` 命令的区别在于列出内容的格式。默认情况下，`dir` 命令按列列出文件和文件夹，并进行垂直排序，特殊字符用反斜杠转义序列表示。

## 语法：

```
dir [OPTIONS] [FILE]
```

## 示例：

1. 列出当前目录下的文件：

```
dir
```

2. 列出当前目录下的甚至是隐藏文件：

```
dir -a
```

3. 列出包含每个条目详细信息的内容：

```
dir -l
```

## 附加标志及其功能：

| 短标志 | 长标志 | 描述 |
| :--- | :--- | :--- |
| `-a` | `--all` | 显示所有隐藏文件（以 `.` 开头）以及由 `.` 和 `..` 表示的两个文件 |
| `-A` | `--almost-all` | 与 `-a` 选项类似，但不显示表示当前目录和上级目录的文件 |
| `-l` |  | 显示每个条目的详细信息 |
| `-s` | `--size` | 打印每个文件的分配大小（以块为单位） |
| `-h` | `--human-readable` | 与 `-l` 和 `-s` 配合使用，以人类可读的格式（如 1K, 2M 等）打印大小 |
| `-F` |  | 根据附加符号（`/`, `*`, `@`, `%`, `=`）对条目分类 |
| `-v` | `--verbose` | 在文件之前打印源文件和目标文件 |
|  | `--group-directories-first` | 将目录放在文件之前 |
| `-R` | `--recursive` | 递归列出子目录 |
| `-S` |  | 按文件大小排序，显示最大的文件 |

## reboot 命令

`reboot` 命令用于重启 Linux 系统。然而，它需要使用 `sudo` 命令获取高权限。通常在系统进行重大更新或网络更新后，需要使用此命令。

## 语法

```
reboot [OPTIONS...]
```

## 选项

- `help`: 此选项打印简短帮助文本并退出。
- `halt`: 此命令将停止机器。
- `w`, `-wtmp-only`: 此选项仅写入 `wtmp` 关机记录，实际上不会执行停止、关机或重启。

## 示例

1. 基础用法。主要用于在不带任何额外细节的情况下重启：

```
$ sudo reboot
```

然而，也可以使用带有 `-r` 选项的 `shutdown` 命令：

```
$ sudo shutdown -r now
```

**注意**：`reboot`、`halt` 和 `power off` 的语法和效果几乎相同。运行这些命令的每一个并配合 `-help` 查看详情。

2. `reboot` 命令的用法有限，通常使用 `shutdown` 命令代替 `reboot` 来满足许多高级的重启和关机需求。

## 使用 Flag

## Description

| Flag | Description |
| :--- | :--- |
| `-A` | 合并存档文件 |
| `-z` | zip，告诉 `tar` 命令使用 `gzip` 创建 `tar` 文件 |
| `-j` | 使用 `tbzip` 过滤存档 `tar` 文件 |
| `-w` | 验证存档文件 |
| `-r` | 在已存在的 `.tar` 文件中更新或添加文件或目录 |
| `-?` | 显示项目的简要摘要 |
| `-d` | 查找存档与文件系统之间的差异 |
| `--usage` | 显示所有可用的 `tar` 选项 |
| `--version` | 显示已安装的 `tar` 版本 |
| `--show-defaults` | 显示默认启用的选项 |

## 选项 Flag

## Description

| Flag | Description |
| :--- | :--- |
| `--check-device` | 在增量存档期间检查设备号 |
| `-g` | 用于兼容 GNU 格式的增量备份 |
| `--hole-detection` | 用于检测稀疏文件中的空洞 |
| `-G` | 用于兼容旧的 GNU 格式增量备份 |
| `--ignore-failed-read` | 文件错误时不退出程序 |
| `--level` | 设置存档的导出级别 |
| `-n` | 假设存档是可寻的 |
| `--no-check-device` | 创建存档时不检查设备号 |
| `--no-seek` | 假设存档是不可寻的 |
| `--occurrence=N` | 处理每个文件的第 N 次出现 |
| `--restrict` | 禁用潜在有害的选项 |
| `--sparse-version=MAJOR,MINOR` | 设置使用的稀疏格式版本 |
| `-S` | 高效处理稀疏文件。 |

## 覆盖控制 Flag

## Description

| Flag | Description |
| :--- | :--- |
| `-k` | 不替换现有文件 |
| `--keep-new-files` | 不替换比存档版本新的现有文件 |
| `--keep-directory-symlink` | 不替换现有符号链接 |
| `--no-overwrite-dir` | 保留现有目录的元数据 |
| `--one-top-level=DIR` | 将所有文件提取到 `DIR` 中 |
| `--overwrite` | 覆盖现有文件 |
| `--overwrite-dir` | 覆盖目录的元数据 |
| `--recursive-unlink` | 递归删除提取目录中的所有文件 |

## 覆盖控制 Flag

## Description

| Flag | Description |
| :--- | :--- |
| `--remove-files` | 将文件添加到目录后删除这些文件 |
| `--skip-old-files` | 提取时不替换现有文件 |
| `-u` | 在覆盖每个文件之前移除该文件 |
| `-w` | 在写入存档后验证存档 |

## gunzip 命令

`gunzip` 命令是 `gzip` 命令的反义词命令。换句话说，它解压缩由 `gunzip` 命令压缩的文件。

`gunzip` 接收命令行中的文件列表，并将每个以 `.gz`、`-gz`、`.z`、`-z`（忽略大小写）结尾且以正确的魔数数字开头的文件替换为不带原始扩展名的未压缩文件。`gunzip` 还认为特殊扩展名 `.tgz` 和 `.taz` 是 `.tar.gz` 和 `.tar.Z` 的缩写。

## 示例:

1. 解压缩文件

```
gunzip filename.gz
```

2. 递归解压缩目录内匹配 `gunzip` 接受的扩展名（后缀）压缩格式的内容：

```
gunzip -r directory_name/
```

3. 解压缩当前/工作目录下所有后缀匹配 `.tgz` 的文件：

```
gunzip -S .tgz *
```

4. 列出输入压缩文件的压缩大小、未压缩大小、压缩率和未压缩后的名称：

```
gunzip -l file_1 file_2
```

## 语法:

```
gunzip [ -acfhkLnNrtvV ] [-S suffix] [ name ... ]
```




# 关于 `gzip`、`gunzip` 和 `tar` 命令的视频教程

此视频展示了如何在 Unix shell 中进行压缩和解压缩。它使用 `gunzip` 作为解压缩命令。

# 其他 Flags 及其功能

| Short Flag | Long Flag | Description |
| :--- | :--- | :--- |
| `-c` | `--stdout` | 写到标准输出，保持原始文件不变 |
| `-h` | `--help` | 提供帮助信息 |
| `-k` | `--keep` | 保留（不删除）输入文件 |
| `-l` | `--list` | 列出压缩文件内容 |
| `-q` | `--quiet` | 抑制所有警告 |
| `-r` | `--recursive` | 对目录进行递归操作 |
| `-S` | `--suffix=SUF` | 对压缩文件使用后缀 `SUF` |
|  | `--synchronous` | 同步输出（系统崩溃时更安全，但速度较慢） |
| `-t` | `--test` | 测试压缩文件完整性 |
| `-v` | `--verbose` | 详细模式 |
| `-V` | `--version` | 显示版本号 |

## `hostnamectl` 命令

`hostnamectl command` 提供了一个适当 API，用于控制 Linux 系统主机名并更改相关设置。该命令还帮助更改主机名，而无需在系统中实际查找并编辑 `/etc/hostname` 文件。

### 语法

```bash
$ hostnamectl [OPTIONS...] COMMAND ...
```

其中 `COMMAND` 可以是以下任意一个：

- `status`：用于检查当前主机名设置
- `set-hostname NAME`：用于设置系统主机名
- `set-icon-name NAME`：用于设置主机图标名称

### 示例

1. 查看当前主机名的基本用法：

```bash
$ hostnamectl
```

或：

```bash
$ hostnamectl status
```

2. 将静态主机名更改为 `myhostname`。这可能需要或不需要 root 权限：

```bash
$ hostnamectl set-hostname myhostname
```

3. 将静态主机名更改为 `myhostname`。这可能需要或不需要 root 权限：

```bash
$ hostnamectl set-hostname myhostname
```

4. 将静态主机名更改为 `myhostname`。这可能需要或不需要 root 权限：

```bash
$ hostnamectl set-hostname myhostname
```

## `iptables` 命令

`iptables` 命令用于设置和维护 Linux 内核中的 IPv4 防火墙规则。

### 语法

```bash
iptables [table] [chain]
```

### 示例与解释

此命令向链追加追加：

```bash
iptables -t filter -A INPUT
```

此命令丢弃来自任何端口的流量：

```bash
iptables -t filter -A INPUT
```

### Flags 及其功能

| Flag | Description |
| :--- | :--- |
| `-C` | 检查规则是否存在于链中。如果存在返回 0，不存在返回 1。 |
| `-A` | 追加到链中。 |

## `netstat` 命令

`netstat` 术语代表 Network Statistics（网络统计）。通俗来说，`netstat` 显示当前的连接、网络协议统计以及各种接口。

检查你的 PC 上是否有 `netstat`：

```bash
netstat -v
```

如果你的 PC 上没有 `netstat`，可以使用以下命令进行安装：

```bash
sudo apt install net-tools
```

你可以在以下用例中使用 `netstat`：

- 带有 `-nr` 的 `netstat` 命令显示路由表详情。

```bash
netstat -nr
```

- 带有 `-i` 的 `netstat` 命令显示当前配置的网络接口的统计信息。此命令将显示文件的前 10 行。

```bash
netstat -i
```

- 带有 `-tunlp` 的 `netstat` 命令将给出网络列表、当前状态以及关联端口。

```bash
netstat -tunlp
```

- 你可以使用 `netstat -at` 获取所有 TCP 端口连接列表：

```bash
netstat -at
```

- 你可以使用 `netstat -au` 获取所有 UDP 端口连接列表：

```bash
netstat -au
```

- 你可以使用 `netstat -l` 获取所有活动连接列表：

```bash
netstat -l
```

## `lsof` 命令

`lsof` 命令显示运行中进程所打开的文件信息。它的名称也源于“列出打开的文件”（list open files > `lsof`）。

打开的文件可以是普通文件、目录、块设备文件、字符设备文件、执行文本引用、库、流或网络文件（Internet socket、NFS 文件或 UNIX 域套字）。可以通过路径选择特定文件或文件系统中的所有文件。

### 语法

```bash
lsof [-OPTION] [USER_NAME]
```

### 示例

1. 显示所有活动进程打开的文件：

```bash
lsof
```

2. 显示特定用户打开的文件：

```bash
lsof -u [USER_NAME]
```

3. 查看指定目录下打开了文件的进程：

```bash
lsof +d [PATH_TO_DIR]
```

### 选项及其功能

| 选项 | 附加选项 | 说明 |
| :--- | :--- | :--- |
| `+ - i` | `i tcp/ udp/ :port` | 列出所有运行的网络连接，此外，还可以针对 udp/tcp 或指定端口。 |
| `- i4` |  | 列出所有带有 ipv4 连接的进程。 |
| `- i6` |  | 列出所有带有 ipv6 连接的进程。 |
| `- c [PROCESS_NAME]` |  | 列出特定名称进程的所有文件。 |
| `- p [PROCESS_ID]` |  | 列出指定进程 ID 打开的所有文件。 |
| `- p ^[PROCESS_ID]` |  | 列出未由指定进程 ID 打开的文件。 |
| `- d [PATH]` |  | 列出在指定目录下打开了文件的进程。 |
| `- R` |  | 列出父进程 ID 打开的文件。 |

## 帮助命令

运行以下命令查看 `lsof` 命令的完整指南。

```bash
man lsof
```

## `bzip2` 命令

`bzip2` 命令允许你对文件进行压缩和解压缩，即它可以帮助将文件绑定到一个文件中，且占用的存储空间比原始文件更少。

### 语法

```bash
bzip2 [OPTIONS] filenames ...
```

注意：每个文件都会被其压缩后的版本替换，文件名为原始文件名加上扩展名 `.b2`。

### 选项及其功能

| 选项别名 | 说明 |
| :--- | :--- |
| `-d --decompress` | 解压缩压缩文件 |
| `-f --force` | 覆盖已有的输出文件 |
| `-h --help` | 显示帮助信息并退出 |
| `-k --keep` | 启用文件压缩，不删除原始文件 |
| `-L --license` | 显示许可条款和条件 |
| `-q --quiet` | 抑制非必要的警告信息 |
| `-t --test` | 检查指定的 `.bz2` 文件的完整性，但不进行解压缩 |
| `-v --verbose` | 显示每个压缩操作的详情 |
| `-V --version` | 显示软件版本 |
| `-z --compress` | 启用文件压缩，但会删除原始文件 |

默认情况下，当 `bzip2` 压缩文件时，它会删除原始（或输入）文件。然而，如果你不希望发生这种情况，请使用 `-k` 命令行选项。

### 示例

1. 强制压缩：

```bash
bzip2 -z input.txt
```

注意：此选项也会删除原始文件。

2. 强制压缩并保留原始输入文件：

```bash
bzip2 -k input.txt
```

3. 强制解压缩：

```bash
bzip2 -d input.txt.bz2
```

4. 测试压缩文件的完整性：

```bash
bzip2 -t input.txt.bz2
```

5. 显示每个已处理文件的压缩率：

```bash
bzip2 -v input.txt
```

## `service` 命令

`Service` 在尽可能可预测环境中运行 System V init 脚本，移除大多数环境变量并将当前工作目录设置为 `/`。

`SCRIPT` 参数指定一个 System V init 脚本，位于 `/etc/init.d/SCRIPT`。`COMMAND` 的可用值取决于所调用的服务，`service` 会原封不动地将 `COMMAND` 和 `OPTIONS` 传递给 init 脚本。所有脚本都应该至少支持 `start` 和 `stop` 命令。作为一种特殊情况，如果 `COMMAND` 是 `--full-restart`，则该脚本将运行两次，首先运行 `stop` 命令，然后运行 `start` 命令。

`COMMAND` 至少可以是 `start`、`stop`、`status` 和 `restart`。

`service --status-all` 按照字母顺序运行所有 init 脚本，并执行 `status` 命令。

### 示例

1. 检查所有运行中服务的状态：

```bash
service --status-all
```

2. 运行一个脚本：

```bash
service SCRIPT-Name start
```

3. 一个更通用的命令：

```bash
service [SCRIPT] [COMMAND] [OPTIONS]
```

## `vmstat` 命令

`vmstat` 命令允许你监控系统性能。它向你显示有关内存、磁盘、进程、CPU 调度、分页和块 I/O 的信息。该命令也被称为虚拟内存统计报告。

产生的第一份报告显示了自上次重启以来的平均细节，之后会生成其他随时间推移的报告。

```bash
vmstat
```

如你所见，这是一个非常实用的小命令。我们在上面看到的最重要的信息是 `free`（空闲），它显示了未使用的空闲空间；`si` 显示了每秒换入内存量（单位为 kB），`so` 显示了每秒换出的内存量（单位为 kB）。

```bash
vmstat -a
```

如果我们运行 `vmstat -a`，它将向我们显示系统的活跃和非活跃内存。

```bash
vmstat -d
```

`vmstat -d` 命令向我们显示所有的磁盘统计。

如你所见，这是一个非常实用的小命令。

## `mpstat` 命令

`mpstat` 命令用于报告 CPU 统计数据。它提供了关于处理器使用的详细信息。

### 语法

```bash
mpstat [OPTIONS] [interval] [count]
```

### 选项及其功能

| 选项 |  |
| :--- | :--- |
| `-a` | 报告自启动以来的所有 CPU |
| `-B` | 报告所有分页统计 |
| `-b` | 报告所有任务统计 |
| `-C` | 报告所有上下文统计 |
| `-E` | 报告所有扩展统计 |
| `-I` | 报告所有中断统计 |
| `-m` | 报告所有内存统计 |
| `-n` | 报告软中断统计 |
| `-p` | 报告进程统计 |
| `-P` | 报告指定处理器的统计 |
| `-q` | 报告所有队列统计 |
| `-T` | 报告所有时间相关统计 |
| `-U` | 报告所有用户级统计 |
| `-V` | 报告 `mpstat` 版本 |

### 示例

1. 报告一次 CPU 统计：

```bash
mpstat
```

2. 每秒报告一次 CPU 统计：

```bash
mpstat 1
```

3. 每隔 1 秒报告 5 次：

```bash
mpstat 1 5
```

4. 报告所有处理器的统计：

```bash
mpstat -P
```

## `ncdu` 命令

`ncdu`（NCurses Disk Usage）基于著名的 `du` 命令。它提供了一种查看哪些目录占用空间的快速方法。

### 示例

1. 静音模式：

```bash
ncdu -q
```

2. 排除挂载的文件系统：

```bash
ncdu -x
```

### 语法

```bash
ncdu [-hqvx] [--exclude PATTERN] [-X FILE] dir
```

### 附加标志及其功能

| 短标志 | 长标志 | same |
| :--- | :--- | :--- |
| `-h` |  | 显示简短的帮助信息。静音模式。在计算磁盘空间时，`ncdu` 默认更新屏幕 10 次，在静音模式下将降低为每 2 秒一次。在远程连接中使用此功能可以节省带宽。 |
| `-q` |  | 显示版本。 |
| `-v` |  | 排除与指定目录同一文件系统的文件和目录。 |
| `-x` | `--exclude PATTERN` | 排除匹配 `PATTERN` 的文件。可以多次添加此参数以添加更多模式。 |
| `-X` | `--exclude-from FILE` | 排除匹配 `FILE` 中任何模式的文件。模式应以换行符分隔。 |

```bash
uniq -f 2 kt.txt
```

为了在比较行唯一性时跳过 N 个字符，语法如下：

```bash
uniq -s 5 kt.txt
```

为了使比较不区分大小写，语法如下：

```bash
uniq -i [INPUT[OUTPUT]]
```

## 语法

## 可能的选项

| 标志 | 描述 | 参数 |
| :--- | :--- | :--- |
| `-c` | 它通过在行前显示数字，来告知该行重复了多少次。 |  |
| `-d` | 它只打印重复的行，不打印重复的行。 |  |
| `-i` | 默认情况下，比较是区分大小写的，但使用此选项可以进行不区分大小写的比较。 |  |
| `-f` | 它允许您在确定行的唯一性之前跳过 N 个字段（字段是一组由空白符分隔的字符）。 | `N` |
| `-S` | 在确定行的唯一性时，不比较每行的前 N 个字符。这类似于 `-f` 选项，但跳过的是单个字符而不是字段。 | `N` |
| `-u` | 它允许您只打印唯一的行。 |  |
| `-z` | 它将使行尾变为 0 字节（NULL），而不是换行符。 |  |
| `-w` | 它只比较行中的 N 个字符。 | `N` |
| `--help` | 显示帮助信息并退出。 |  |
| `--version` | 显示版本信息并退出。 |  |

## RPM 命令

`rpm` - RPM 软件包管理器

`rpm` 是一个强大的软件包管理器，用于构建、安装、查询、验证、更新和删除单个软件包。软件包由文件归档和用于安装、删除归档文件的元数据组成。元数据包括辅助脚本、文件属性以及关于软件包的描述性信息。软件包有两种类型：二进制包（用于封装要安装的软件）和源包（包含生成二进制包所需的源码和配方）。

必须选择以下基本模式之一：查询（Query）、验证（Verify）、签名检查（Signature Check）、安装/升级/刷新（Install/Upgrade/Freshen）、卸载（Uninstall）、初始化数据库（Initialize Database）、重建数据库（Rebuild Database）、重签名（Resign）、添加签名（Add Signature）、设置所有者/组（Set Owners/Groups）、显示查询标签（Show Querytags）和显示配置（Show Configuration）。

### 普通选项

这些选项可以在所有不同的模式下使用。

| 短标志 | 长标志 | 描述 |
| :--- | :--- | :--- |
| `-?` | `--help` | 打印比普通更详细的用法信息。 |
|  | `--version` | 打印包含正在使用的 rpm 版本的单行。 |
|  | `--quiet` | 尽可能少输出 - 通常只显示错误消息。 |
| `-v` |  | 打印详细信息 - 通常会显示例行进度消息。 |
| `-vv` |  | 打印大量的调试信息。 |
|  | `--rcfile FILELIST` | 按顺序读取由冒号分隔的 `FILELIST` 中的每个文件以获取配置信息。列表中的第一个文件必须存在，波号将扩展为 `$HOME` 的值。默认的 `FILELIST` 是 `/usr/lib/rpm/rpmrc:/usr/lib/redhat/rpmrc:/etc/.rpmrc`。 |
|  | `--pipe CMD` | 将 `rpm` 的输出通过到命令 `CMD`。 |
|  | `--dbpath DIRECTORY` | 使用 `DIRECTORY` 中的数据库而不是默认的 `/var/lib/rpm`。 |

| 短标志 | 长标志 | 描述 |
| :--- | :--- | :--- |
| `-` | `--root DIRECTORY` | 使用以 `DIRECTORY` 为根的文件系统树进行所有操作。请注意，这意味着 `DIRECTORY` 内的数据库将用于依赖检查，并且任何脚本（例如安装包时的 `%post`，或构建包时的 `%prep`）将在 `chroot(2)` 到 `DIRECTORY` 之后运行。 |
| `-D` | `--define='MACRO EXPR'` | 定义值为 `EXPR` 的 `MACRO`。 |
| `-E` | `--eval='EXPR'` | 打印 `EXPR` 的宏展开。 |

## 摘要

### 查询和验证软件包

```bash
rpm {-q|--query} [select-options] [query-options]

rpm {-V|--verify} [select-options] [verify-options]

rpm --import PUBKEY ...

rpm {-K|--checksig} [--signature] [--nodigest] PACKAGE_FILE ...
```

### 安装、升级和移除软件包

```bash
rpm {-i|--install} [install-options] PACKAGE_FILE ...
```




# rpm 命令

`rpm` 命令用于管理 RPM 软件包。以下是其各种用法和选项。

## 基本用法

```
rpm {-U|--upgrade} [install-options] PACKAGE_FILE ...
```

```
rpm {-F|--freshen} [install-options] PACKAGE_FILE ...
```

```
rpm {-e|--erase} [--allmatches] [--nodeps] [--noscripts] [--notnotrrigs] [--test] PACKAGE_NAME ...
```

## 杂项命令

```
rpm {--initdb|--rebuilddb}
```

```
rpm {--addsign|--resign} PACKAGE_FILE...
```

```
rpm {--querytags|--showcrc}
```

```
rpm {--setperms|--setugids} PACKAGE_NAME .
```

## query-options

```
[--changelog] [-c,--configfiles] [-d,--docfiles] [--dump]
[--filesbypkg] [-i,--info] [--last] [-l,--list]
[--provides] [--qf,--queryformat QUERYFMT]
[-R,--requires] [--requires]
```

## verify-options

```
rpm {-V|--verify} [select-options] [verify-options]
[--qf] [--queryformat]
```

## install-options

```
rpm {-i|--install} [install-options] PACKAGE_FILE ...
```

## query-options

```
rpm {-q|--query} [select-options] [query-options]
```

## verify-options

```
rpm {-V|--verify} [select-options] [verify-options]
```

## 通用选项

| 选项 | 描述 |
| --- | --- |
| `--version` | 打印包含正在使用的 `rpm` 版本的单行。 |
| `--quiet` | 尽可能少输出 - 通常只显示错误消息。 |

## upgrade-options

```
rpm {-U|--upgrade} [install-options] PACKAGE_FILE ...
```

## freshen-options

```
rpm {-F|--freshen} [install-options] PACKAGE_FILE ...
```

## erase-options

```
rpm {-e|--erase} [--allmatches] [--nodeps] [--noscripts] [--notnotrrigs] [--test] PACKAGE_NAME ...
```

## install-options

```
rpm {-i|--install} [install-options] PACKAGE_FILE ...
```

## checksig-options

```
rpm {-K|--checksig} [--signature] [--nodigest] PACKAGE_FILE ...
```

## import-options

```
rpm --import PUBKEY ...
```

## checksig-options

```
rpm {-K|--checksig} [--signature] [--nodigest] PACKAGE_FILE ...
```

## query-options

```
rpm {-q|--query} [select-options] [query-options]
```

## verify-options

```
rpm {-V|--verify} [select-options] [verify-options]
```

# sleep 命令

`sleep` 命令用于创建一个虚拟作业（dummy job）。虚拟作业有助于延迟执行。它默认以秒为单位，但可以在末尾添加小的后缀（`s`, `m`, `h`, `d`）以将其转换为任何其他格式。该命令将暂停执行由 `NUMBER` 定义的时间长度。

注意：如果你在 `sleep` 命令中定义了多个 `NUMBER`，则该命令将按这些值的总和进行延迟。

## 示例

- 1. 休眠 10 秒

```
sleep 10s
```

- 2. 一个更通用的命令：

```
sleep NUMBER[SUFFIX]...
```

## 选项

该命令接受以下选项：

- 1. `--help`
  显示此帮助信息并退出
- 2. `--version`
  输出版本信息并退出

# split 命令

Linux 中的 `split` 命令用于将文件拆分成多个小文件。

## 示例

- 1. 使用文件名将文件拆分为较小文件

```
split filename.txt
```

- 2. 将名为 `filename` 的文件拆分为每段 200 行的片段，前缀为 `file`

```
split -l 200 filename file
```

这将创建名为 `filea`, `fileab`, `fileac`, `filead` 等的每个 200 行的文件。

- 3. 将名为 `filename` 的文件拆分为每段 40 字节的片段，前缀为 `file`

```
split -b 40 filename file
```

这将创建名为 `filea`, `fileab`, `fileac`, `filead` 等的每个 40 字节的文件。

- 4. 使用 `--verbose` 模式查看正在创建的文件。

```
split filename.txt --verbose
```

## 语法

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-a` | `--suffix-length=N` | 生成长度为 `N` 的后缀（默认为 2） |
| | `--additional-suffix=SUFFIX` | 在文件名后附加额外的 `SUFFIX` |
| `-b` | `--bytes=SIZE` | 每个输出文件写入 `SIZE` 字节 |
| `-C` | `--line-bytes=SIZE` | 每个输出文件最多包含 `SIZE` 条记录 |
| `-d` | `--numeric-suffixes=[FROM]` | 使用从 0 开始的数字后缀，类似于 `-d`，但允许设置值 |
| `-x` | `--hex-suffixes=[FROM]` | 使用从 0 开始的十六进制字母数字数字后缀 |
| `-e` | `--elide-empty-files` | 与 `-x` 相同，但允许设置值 |
| | `--filter=COMMAND` | 不使用 `-n` 生成空输出文件 |
| `-l` | `--lines=NUMBER` | 写入 shell `COMMAND`；文件名为 `$FILE` |
| `-n` | `--number=CHUNKs` | 每个输出文件写入 `NUMBER` 行/记录 |
| `-t` | `--separator=SEP` | 生成 `CHUNKS` 文件；见下文解释 |
| `-u` | `--buffered` | 使用 `SEP` 代替换行符作为记录分隔符；`'\0'`（零）指定 `NUL` 字符 |
| | `--verbose` | 在打开输出文件之前打印诊断信息 |
| | `--help` | 显示此帮助信息并退出 |
| | `--version` | 输出版本信息并退出 |

`SIZE` 参数是一个整数和一个可选单位（例如：`10K` 是 `10*1024`）。单位有 `K,M,G,T,P,E,Z,Y`（1024 的幂）或 `KB,MB...`（1000 的幂）。

## CHUNKs 描述

- `N` 根据输入的大小拆分为 `N` 个文件
- `K/N` 将 `N` 个中的第 `K` 个输出到 `stdout`
- `l/N` 拆分为 `N` 个文件，且不拆分行/记录
- `l/K/N` 将 `N` 个中的第 `K` 个输出到 `stdout`，且不拆分行/记录
- `r/N` 类似于 `'l'` 但使用轮询算法分布
- `r/K/N` 同样，但仅将 `N` 个中的第 `K` 个输出到 `stdout`

# stat 命令

`stat` 命令允许你显示文件或文件状态。它为你提供了关于你所使用的文件（或目录）的有用信息。

## 示例

- 1. 基础命令用法

```
stat file.txt
```

- 2. 使用 `-c`（或 `--format`）参数仅显示你想看到的信息（这里是总大小，单位为字节）

```
stat file.txt -c %s
```

## 语法

```
stat [OPTION] [FILE]
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
|---|---|--|
| `-L` | | 跟随链接 |
| `-f` | `--file-system` | 显示文件系统状态而不是文件状态 |
| `-c` | `--format=FORMAT` | 指定格式（见下文） |
| `-t` | `--terse` | 以简术形式打印信息 |
| | `--cached=MODE` | 指定如何使用缓存属性。可以是：`always`, `never` 或 `default` |

## 短长标志描述

- `--printf=FORMAT` 类似于 `--format`，但会转义反斜杠转义 (`\n`, `\t`, ...)
- `--help` 显示帮助并退出
- `--version` 输出版本信息并退出

## 文件的有效格式序列示例

| 格式 | 描述 |
| --- | --- |
| `%a` | 八进制权限位 |
| `%A` | 人类可读的权限位 |
| `%d` | 十进制设备号 |
| `%D` | 十六进制设备号 |
| `%F` | 文件类型 |
| `%g` | 组 ID 用户 |
| `%G` | 组名 |
| `%h` | 数量 |
| `%i` | 节点号 |
| `%m` | 挂载点 |
| `%n` | 名称 |
| `%s` | 字节大小 |
| `%u` | 用户 ID |
| `%w` | 生日 |
| `%x` | 访问时间 |
| `%y` | 修改时间 |
| `%z` | 状态 |

# usermod 命令

`usermod` 命令允许通过命令行更改用户的属性。

## 语法

```
usermod [options] USER
```

注意：`root` 用户可以执行 `usermod` 命令。

## 选项及其功能

| 选项 | 描述 |
|---|--|
| `-a` | 添加到辅助组 |
| `-c` | 为用户添加注释 |
| `-d` | 修改现有用户的目录 |
| `-g` | 更改主组 |
| `-G` | 添加辅助组 |
| `-l` | 更改登录名 |
| `-L` | 锁定系统用户 |
| `-m` | 将现有目录的内容移动到新目录 |
| `-p` | 创建加密的密码 |
| `-s` | 为新用户指定 shell |
| `-u` | 分配 UID |
| `-U` | 解锁任何用户 |

## 示例

- 1. 为用户添加注释/描述：

```
sudo usermod -c "This is test user" test_user
```

- 2. 更改用户的主目录：

```
sudo usermod -d /home/sam test_user
```

- 3. 更改用户的过期日期：

```
sudo usermod -e 2021-10-05 test_user
```

- 4. 更改用户的组：

```
sudo usermod -g sam test_user
```

- 5. 更改用户登录名：

```
sudo usermod -l test_account test_user
```

- 6. 锁定用户：

```
sudo usermod -L test_user
```

- 7. 解锁用户：

```
sudo usermod -U test_user
```

- 8. 为用户设置未加密的密码：

```
sudo usermod -p test_password test_user
```

- 9. 为用户创建一个 shell：

```
sudo usermod -s /bin/sh test_user
```

- 10. 更改用户的 ID (UID)：

```
sudo usermod -u 1234 test_user
```

# useradd 命令

`useradd` 命令用于添加或更新用户账户。

## 示例

使用 `useradd` 命令添加用户的语法为：

```
useradd User
```

添加带有主目录的新用户，语法为：

```
useradd -d /home/User
```

添加带有特定 ID 的新用户，语法为：

```
useradd -u 1234 User
```

## 语法

```
useradd [OPTIONS] NameOfUser
```

## 选项

| 选项 | 描述 |
|---|--|
| `-d` | 修改现有用户的目录 |
| `-c` | 为用户账户添加注释 |
| `-e` | 过期日期（格式：`YYYY-MM-DD`） |
| `-g` | 更改主组 |
| `-G` | 添加辅助组 |
| `-h` | 硬链接数 |
| `-i` | 节点号 |
| `-m` | 挂载点 |
| `-n` | 名称 |
| `-s` | 为新用户指定 shell |
| `-u` | 分配 UID |
| `-U` | 解锁任何用户 |

# userdel 命令

`userdel` 命令用于删除用户账户及相关文件。

## 示例

使用 `userdel` 命令删除用户的语法为：

```
userdel User
```

即使用户已登录也强制删除用户账户，其语法为：

```
userdel -f User
```

删除用户及其主目录中的文件，其语法为：

```
userdel -r User
```

## 语法

```
userdel [OPTIONS] userName
```

## 可能的选项

| 选项 | 描述 |
|---|--|
| `-f` | 即使用户已登录也强制删除指定的用户账户 |
| `-r` | 删除用户主目录中的文件以及目录本身和用户的邮件池 |
| `-Z` | 移除用户的 SELinux 用户映射 |

# ionice 命令

`ionice` 命令用于设置或获取进程的 I/O 调度类和优先级。

如果不提供任何参数，`ionice` 将查询该进程当前的 I/O 调度类和优先级。

## 用法

```
ionice [options] -p <pid>
```

```
ionice [options] -P <pgid>
```

```
ionice [options] -u <uid>
```

```
ionice [options] <command>
```



# 进程调度类

进程可以分为三种调度类：

## Idle（空闲）

具有空闲 I/O 优先级的程序只有在没有其他程序在定义的宽限期请求磁盘 I/O 时，才能获得磁盘时间。

空闲进程对正常系统活动的影响应为零。

此调度类不接受优先级参数。

目前，此调度类允许普通用户使用（内核 2.6.25 起）。

## Best Effort（尽力而为）

这是未请求特定 I/O 优先级的进程的有效调度类。

此类接受 `0-7` 的优先级参数，数字越小优先级越高。

运行在相同尽力优先级的程序将以轮询方式提供服务。

注意，在内核 2.6.26 之前，未请求 I/O 优先级的进程形式上使用 `"None"` 作为调度类，但 I/O 调度器会将此类进程视为处于尽力类中。

尽力类内部的优先级将根据进程的 CPU nice 级别动态派生：对于 2.6.26 之后带有 CFQ I/O 调度器的内核，`io_priority = ( cpu_nice + 20 ) / 5`，未请求 I/O 优先级的进程继承 CPU 调度类。

> I/O 优先级派生自进程的 CPU nice 级别（与内核 2.6.26 之前相同）。

## Real Time（实时）

实时调度类将优先获得磁盘访问权限，无论系统中正在发生什么。

因此，实时类需要谨慎使用，因为它可能会饿死其他进程。

与尽力类一样，定义了 8 个优先级级别，表示给定进程在每个调度窗口将获得多大的时间片。

此调度类不允许普通用户使用（非 root）。

# 选项

| 选项 | 描述 |
| --- | --- |
| `-c, --class` | 调度类的名称或数字，`0: none, 1: realtime, 2: best-effort, 3: idle` |
| `-n, --classdata` | 指定调度类中的优先级 (`0..7`)，仅用于实时和尽力类 |
| `-p, --pid ...` | 作用这些正在运行的进程 |
| `-P, --pgid` | 于这些组中正在运行的进程 |
| `-t, --ignore` | 忽略失败 |
| `-u, --uid ...` | 作用这些用户拥有的进程 |
| `-h, --help` | 显示帮助 |
| `-V, --version` | 显示版本 |

更多详情请参见 `ionice(1)`。

# 示例

| 命令 | 输出 | 解释 |
| --- | --- | -- |
| `$ ionice` | `none: prio 4` | 单独运行 `ionice` 将提供当前进程的类和优先级 |
| `$ ionice -p 101` | `none: prio 4` | 获取由给定进程 ID 指定的进程的类和优先级 |
| `$ ionice -p 2` | `none: prio 4` | 检查 `pid` 为 2 的进程的类和优先级 |
| `$ ionice -c2 -n0 -p2` | `2 ( best-effort ) priority 0 process 2` | 现在让进程(`pid`) 2 作为一个具有最高优先级的尽力程序 |
| `$ ionice -p 2` | `best-effort: 0` | 现在如果检查进程 2，你可以看到更新后的优先级 |
| `$ ionice /bin/ls` | | 获取 `/bin/ls` 的优先级和类信息 |

# 从本地服务器传输文件到远程服务器

这是最常见的原因之一。本质上，这就是如何将文件从你所在的服务器（源服务器）复制到远程/目标服务器。

你需要做的是 SSH 登录存放文件的服务器，并进入你想要传输的目录：

```bash
cd /var/www/html
```

然后运行：

```bash
rsync -avz user@your-remote-server.com:/home/user/dir/
```

上述命令将从你服务器上当前文件夹中的所有文件和目录拷贝到远程服务器。

命令详解：

- `-a`: 用于指定你想要递归复制，并保留文件权限等。
- `-v`: 详细模式，它会增加传输过程中提供的信息量。
- `-z`: 该选项，`rsync` 在将文件数据发送到目标机器时对其进行压缩，从而减少传输的数据量——这在慢连接上非常有用。

我建议查看以下网站，它非常很好地解释了这些命令和参数：

`https://explainshell.com/explain?cmd=rsync+-avz`

如果远程服务器上的 SSH 服务没有运行在标准的 `22` 端口，你可以使用带有特殊 SSH 端口的 `rsync`：

```bash
rsync -avz -e 'ssh -p 1234' user@your-remote-server.com:/home/user/dir/
```

# 从远程服务器传输文件到本地

某些情况下，你可能想将文件从远程服务器传输到本地服务器，在这种情况下你需要使用以下语法：

```bash
rsync -avz your-user@your-remote-server.com:/home/user/dir/ /home/user/local-dir/
```

同样，如果你有一个非标准的 SSH 端口，可以使用命令：

```bash
rsync -avz -e 'ssh -p 2510' your-user@your-remote-server.com:/home/user/dir/ /home/user/local-dir/
```

# 仅传输缺失的文件

如果你只想传输缺失的文件，可以使用 `--ignore-existing` 标记。

这对于最终同步非常有用，可以确保在网站或服务器迁移后没有遗漏的文件。

基本上，命令除了追加了 `--ignore-existing` 标记外都是相同的：

```bash
rsync -avz --ignore-existing user@your-remote-server.com:/home/user/dir/
```

# 结论

使用 `rsync` 是一种通过 SSH 安全地从一台机器快速传输文件到另一台机器的好方法。

对于更多酷的 Linux 网络工具，我建议查看这里的教程：

[你应该知道的 15 个 Linux 网络工具]()

希望对你有所帮助！

最初发布于：[如何使用 rsync 从一台 Linux 服务器传输文件到另一台服务器]()

# dig 命令

`dig` - DNS 查找工具

`dig` 是一个查询 DNS 服务器的灵活工具。它执行 DNS 查询并显示从查询的服务器返回的答案。

## 示例

1. `dig` 是一个用于查询域名系统（DNS）的网络管理命令行工具。

```bash
dig google.com
```

2. 系统将列出它找到的所有 `google.com` DNS 记录以及 IP 地址。

```bash
dig google.com ANY
```

## 语法

```bash
dig [server] [name] [type] [q-type] [q-class] {q-opt} [global-d-opt] host [@local-server] {local-d-opt} [ host [@local-server] {local-d-opt} [...]]
```

## 附加标记及其功能

`domain` 位于域名系统中，`q-class` 是 `(in,hs,ch,...)` 之一 [默认: `in`]

`q-type` 是以下之一：
`(any,mx,ns,soa,hinfo,axfr,txt,...)` [默认:`a`]
(对于类型 `ixfr`，请使用 `ixfr=version`)

`q-opt` 是以下之一：
- `-4` (仅使用 IPv4 查询传输)
- `-6` (使用 IPv6 查询传输地址/端口)
- `-b address[#port]` (绑定到源)
- `-c class` (指定查询类)
- `-f filename` (批模式)
- `-k keyfile` (指定 tsig 密钥文件)
- `-m` (启用内存使用调试)
- `-p port` (指定端口号)
- `-q name` (指定查询名称)
- `-r` (不读取 `~/.digrc`)
- `-t type` (指定查询类型)
- `-u` (显示使用时间而非 (毫秒))
- `-x dot-notation` (反向查找快捷方式)
- `-y [hmac]:name:key` (指定的名称 base64)

`d-opt` 的格式为 `+keyword=[value]`，其中：
`+[no]aaflag` (在查询中设置 AA 标记)
`+[no]aaonly` (在查询中设置 AA 标记)
`+[no]additional` (控制显示)
`+[no]adflag` (在查询中设置 AD 标记)
`+[no]all` (设置或清除所有显示)
`+[no]answer` (控制显示)
`+[no]authority` (控制显示)
`+[no]badcookie` (重试 BADCOOKIE)
`+[no]besteffort` (尝试解析即使是非消息)
`+bufsize[###]` (设置 EDNS0 最大包大小 tsig key)

`keyword` 是：
`+[no]cdflag` (禁用检查)
`+[no]class` (控制类的显示)
`+[no]cmd` (控制命令行显示)
`+[no]comments` (控制头部和部分显示)
`+[no]cookie` (向请求添加 COOKIE 选项)
`+[no]crypto` (控制记录中加密字段的显示)
`+[no]defname` (使用列表 (`[no]search`))
`+[no]dnssec` (请求 DNSSEC 记录)
`+[no]dname` (设置默认域名)
`+[no]dscp` (设置 DSCP)
`+[no]edflags` (设置 EDNS 标记)
`+[no]edns` (设置 EDNS)
`+[no]edopt` (设置 edopt)
`+[no]expflags` (设置过期标记)
`+[no]expire` (设置过期)
`+[no]flags` (设置标记)
`+[no]hzone` (设置 HZONE)
`+[no]nsid` (设置 NSID)
`+[no]nskey` (设置 NSKEY)
`+[no]nsset` (设置 NSSET)
`+[no]opt` (设置 OPT)
`+[no]open` (设置 OPEN)
`+[no]query` (设置查询)
`+[no]rcode` (设置 RCODE)
`+[no]recursion` (设置递归可用)
`+[no]rnded` (设置 RNDED)
`+[no]rndset` (设置 RNDSET)
`+[no]search` (设置 SEARCH)
`+[no]sec` (设置 SEC)
`+[no]set` (设置 SET)
`+[no]server` (设置 SERVER)
`+[no]ttl` (设置 TTL)
`+[no]trace` (设置 TRACE)
`+[no]vc` (设置 VC)
`+[no]yaml` (设置 YAML)



`q-type`是以下之一：
`(any,mx,ns,soa,hinfo,axfr,txt,...)` [默认:`a`]
(对于类型`ixfr`，请使用`ixfr=version`)

`q-opt`是以下之一：
- `-4` (仅使用 IPv4 查询传输)
- `-6` (使用 IPv6 查询传输地址/端口)
- `-b address[#port]` (绑定到源)
- `-c class` (指定查询类)
- `-f filename` (批模式)
- `-k keyfile` (指定 tsig 密钥文件)
- `-m` (启用内存使用调试)
- `-p port` (指定端口号)
- `-q name` (指定查询名称)
- `-r` (不读取`~/.digrc`)
- `-t type` (指定查询类型)
- `-u` (显示使用时间而非 (毫秒))
- `-x dot-notation` (反向查找快捷方式)
- `-y [hmac]:name:key` (指定的名称 base64)

`d-opt`的格式为`+keyword=[value]`，其中：
- `+[no]aaflag` (在查询中设置 AA 标记)
- `+[no]aaonly` (在查询中设置 AA 标记)
- `+[no]additional` (控制显示)
- `+[no]adflag` (在查询中设置 AD 标记)
- `+[no]all` (设置或清除所有显示)
- `+[no]answer` (控制显示)
- `+[no]authority` (控制显示)
- `+[no]badcookie` (重试 BADCOOKIE)
- `+[no]besteffort` (尝试解析即使是非消息)
- `+bufsize[###]` (设置 EDNS0 最大包大小 tsig key)

`keyword`是：

| `+[no]cdflag` (禁用检查) | `+[no]class` (控制类的显示) |
| :--- | :--- |
| in records) | `+[no]cmd` (控制命令行显示) |
| `+[no]comments` (控制头部和部分显示) | comments) |
| `+[no]cookie` (向请求添加 COOKIE 选项) | `+[no]crypto` (控制记录中加密字段的显示) |
| `+[no]defname` 使用列表 (`[no]search`) | `+[no]dnssec` (请求 DNSSEC 记录) |
| `domain=###` (设置默认域名) | `+[no]dname` (设置默认域名) |
| in records) | `+[no]dscp` (设置 DSCP) |
| (`[no]search`) | `+[no]edflags` (设置 EDNS 标记) |
| `domain=###` (设置默认域名) | `+[no]edns` (设置 EDNS) |
| in records) | `+[no]edopt` (设置 edopt) |
| (`[no]search`) | `+[no]expflags` (设置过期标记) |
| `domain=###` (设置默认域名) | `+[no]expire` (设置过期) |
| in records) | `+[no]flags` (设置标记) |
| (`[no]search`) | `+[no]hzone` (设置 HZONE) |
| `domain=###` (设置默认域名) | `+[no]nsid` (设置 NSID) |
| in records) | `+[no]nskey` (设置 NSKEY) |
| (`[no]search`) | `+[no]nsset` (设置 NSSET) |
| `domain=###` (设置默认域名) | `+[no]opt` (设置 OPT) |
| in records) | `+[no]open` (设置 OPEN) |
| (`[no]search`) | `+[no]query` (设置查询) |
| `domain=###` (设置默认域名) | `+[no]rcode` (设置 RCODE) |
| in records) | `+[no]recursion` (设置递归可用) |
| (`[no]search`) | `+[no]rnded` (设置 RNDED) |
| `domain=###` (设置默认域名) | `+[no]rndset` (设置 RNDSET) |
| in records) | `+[no]search` (设置 SEARCH) |
| (`[no]search`) | `+[no]sec` (设置 SEC) |
| `domain=###` (设置默认域名) | `+[no]set` (设置 SET) |
| in records) | `+[no]server` (设置 SERVER) |
| (`[no]search`) | `+[no]ttl` (设置 TTL) |
| `domain=###` (设置默认域名) | `+[no]trace` (设置 TRACE) |
| in records) | `+[no]vc` (设置 VC) |
| (`[no]search`) | `+[no]yaml` (设置 YAML) |

## 附加标记及其功能：

| 标记 | 说明 |
| --- | --- |
| `-h HOST`, `--host` | 连接到 `HOST`。 |
| `-H` | 不显示某些注册表向你显示的法律免责声明。 |
| `-p`, `--port` | 连接到 `PORT`。 |
| `--verbose` | 开启详细模式。 |
| `--help` | 显示在线帮助。 |
| `--version` | 显示客户端版本信息。其他选项是`whos.ripe.net`以及其他类似 RIPE 的服务器所理解的标记。 |
| `-a` | 同时搜索所有镜像数据库。 |
| `-b` | 返回带有滥用联系方式的简短 IP 地址。 |
| `-B` | 禁用对象过滤（显示电子邮件地址）。 |
| `-c` | 返回带有 int 对象引用的最小 IP 地址。 |
| `-d` | 返回反向 DNS 委派工具。 |
| `-g SOURCE:FIRST-LAST` | 搜索 `FIRST` 和 `LAST` 序列号之间 `SOURCE` 数据库的更新。这对于获取近实时镜像流非常有用。 |
| `-G` | 禁用关联对象的分组。 |
| `-i ATTR,[ATTR]...` | 搜索具有关联属性的对象。属性值是位置相关的 `OBJECT` 参数。仅返回主键。异常是集合的 `members` 属性，它总是会被返回。另一个异常是 `organisation`、`person` 和 `role` 对象的属性，永远不会返回。 |
| `-l` | 返回特定层级对象。 |
| `-L` | 返回所有层级的特定对象。 |
| `-m` | 返回所有更具体的对象。 |
| `-M` | 返回所有层级的更具体的对象。 |
| `-q KEYWORD` | 返回服务器支持的关键词列表。`KEYWORD`可以是服务器版本的`version`、源列表的`sources`，或对象类型的`types`。 |
| `-r` | 禁用联系信息的递归查找。 |
| `-R` 禁用跟随引用，并强制从服务器的本地副本获取对象。 |
| `-s SOURCE[,SOURCE]...` | 请求服务器搜索从 `SOURCES` 镜像的对象。源用逗号分隔，且顺序很重要。使用`-q sources`选项获取有效源列表。 |
| `-t TYPE` 返回 `TYPE` 类型对象的模板。 |
| `-T TYPE[,TYPE]...` | 将搜索限制在 `TYPE` 类型对象上。多个类型用逗号分隔。 |
| `-v TYPE` 返回 `TYPE` 对象的详细模板。 |
| `-x` 仅对网络地址前缀进行精确匹配。 |
| `-1` | 强制 ssh 仅使用 SSH-1 协议。 |
| `-2` | 强制 ssh 仅使用 SSH-2 协议。 |
| `-4` | 允许 IPv4 地址。 |
| `-A` 启用身份代理连接转发。 |
| `-a` | 禁用身份代理连接转发。 |
| `-B bind_interface` | 在尝试连接到目标主机之前绑定到接口地址。这对于具有多个地址的系统非常有用。 |
| `-b bind_address` | 使用本地机器上的地址作为连接的源地址。这对于具有多个地址的系统非常有用。 |
| `-C` | 压缩所有数据（包括`stdin`、`stdout`、`stderr`以及转发的 `X11` 和 TCP 连接数据）以实现更快的数据传输。 |
| `-c cipher_spec` | 选择加密会话的密码规范。 |
| `-D [bind_address:]port` | 动态应用层端口转发。这会在本地侧分配一个套字来监听端口。当与该端口建立连接时，连接将通过安全通道转发，然后使用应用程序协议确定从远程机器连接的位置。 |
| `-E log_file` | 将调试日志追加到标准错误中。 |
| `-e escape_char` | 为带有 pty 的话设置转义字符（默认:`'~'`）。转义字符仅在行首被识别。转义字符后接点（`'.'`）将关闭连接；后接控制-Z 将挂起连接；后接自身将发送转义字符。设置为 `"none"` 将禁用任何转义。 |
| `-F configfile` 指定用户配置文件。默认的用户配置文件为`~/.ssh/config`。 |
| `-f` 请求 ssh 在执行命令前进入后台。 |
| `-G` 导致 ssh 在评估 `Host` 和 `Match` 块后打印配置并退出。 |
| `-g` 允许远程主机连接本地转发端口。 |
| `-I pkcs11` 指定 ssh 使用的与提供密钥的 PKCS#11 共享库通信。 |
| `-i identity_file` 用于读取公钥认证的身份密钥（私钥）的文件。 |
| `-J [user@]host[:port]` | 通过跳板机连接到目标。 |
| `-K` 启用基于 GSSAPI 的身份验证（委派）服务器。 |
| `-k` 禁用 GSSAPI 委派。 |
| `-l login_name` 指定登录的用户名。 |
| `-M` 逗号分隔的 MAC（消息认证）算法列表，按偏好顺序指定。 |
| `-m mac_spec` MAC 规范。 |
| `-N` 不执行远程命令。这对于仅转发端口有用。 |
| `-n` 防止从`stdin`读取。 |

## ssh 命令

Linux 中的 `ssh` 命令代表“Secure Shell”。它是一种用于安全连接到远程服务器/系统的协议。`ssh` 的安全性在于它在主机和客户端之间以加密形式传输数据，`ssh` 运行在 TCP/IP 端口 22。

## 示例：

1. 使用不同的端口进行 SSH 连接:

```
ssh test.server.com -p 3322
```

2. `-i` 使用私钥 ssh 到远程服务器?

```
ssh -i private.key user_name@host
```

3. `-l` 指定不同的用户名 ssh

```
ssh -l alternative-username sample.ssh.com
```

## 语法：

```bash
ssh user_name@host(IP/Domain_Name)
```

```bash
ssh -i private.key user_name@host
```

## 参数

## 描述

- `-R [bind_address:]port:host:hostport`,
- `-R [bind_address:]port:local_socket`,
- `-R remote_socket:host:hostport`,
- `-R remote_socket:local_socket`,
- `-R [bind_address:]port`

指定将到远程（服务器）主机上给定 TCP 端口或 Unix socket 的连接转发到本地 socket。

- `-S ctl_path`

指定用于连接共享的控制 socket 的位置，或使用字符串 `"none"` 来禁用连接共享。可用于请求在远程系统上的子系统。子系统有助于将 SSH 作为其他应用程序的安全传输工具（例如 `sftp(1)`）。子系统被指定为远程命令。

- `-T`

禁用伪终端分配。强制分配伪终端。这可以用于在远程机器上执行任意的屏幕程序，这非常有用，例如在实现菜单服务时。多个`-t`选项会强制 tty 分配，即使 ssh 没有本地 tty。

- `-t`

显示版本号。详细模式。它会在建立连接时回显它正在执行的所有操作。这在调试连接失败时非常有用。

- `-V`

请求将客户端的标准输入和输出通过安全通道转发到主机的端口。隐含了`-N`、`-T`、`ExitOnForwardFailure`和`ClearAllForwardings`，尽管可以在配置文件或使用`-o`命令行选项覆盖它们。

- `-W host:port`

- `-S`

## 参数

## 描述

```
-w local_tun[remote_tun]
```

请求在客户端（本地 `tun`）和服务器（远程 `tun`）之间使用指定的 `tun` 设备进行隧道设备转发。设备可以通过数字 ID 或关键字"any"来指定，后者将使用下一个可用的设备。如果没有指定远程 `tun`，则默认为"any"。如果未设置 `Tunnel` 指令，它将设置为默认隧道模式，即"点对点"。如果需要不同的 `Tunnel` 转发模式，则应在`-w`之前指定。

```
-X
```

启用 X11 转发（GUI 转发）。

```
-x
```

禁用 X11 转发（GUI 转发）。

```
-Y
```

启用可信的 X11 转发。

```
-y
```

使用 `syslog` 系统模块发送日志信息。默认情况下，这些信息被发送到 `stderr`。

## awk 命令

Awk 是一种专为高级文本处理设计的通用脚本语言。它主要用作报告和分析工具。

## 我们能用 awk 做什么？

1. AWK 操作：(a) 逐行扫描文件 (b) 将每行输入分成字段 (c) 将输入行/字段与模式比较 (d) 对匹配的行执行操作
2. 适用于：(a) 转换数据文件 (b) 生成格式化报告
3. 编程构造结构：(a) 格式化输出行 (b) 算术和字符串操作 (c) 条件和循环

## 语法

```
awk options 'selection _criteria {action}' input-file > output-file
```

## 示例

考虑以下文本文件作为下面示例的输入文件：

```
$cat > employee.txt
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
```

1. Awk 的默认行为：默认情况下，Awk 打印指定文件的每一行数据。

```
awk '{print}' employee.txt
```
```
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
```

2. 在上述示例中，awk 打印匹配模式的行。

```
awk '/manager/ {print}' employee.txt
```
```
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
```

3. 将行分成字段：默认情况下，awk 按空白字符拆分记录。

```
awk '{print $1,$2,$3}' employee.txt
```
```
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
```

## Awk 中的内置变量

Awk 的内置变量包括`$1`,`$2`,`$0`。
`NR`: NR 保持记录计数。
`NF`: NF 包含当前记录的字段数。
`FS`: FS 是字段分隔符。
`OFS`: OFS 是输出字段分隔符。
`RS`: RS 是记录分隔符。
`BEGIN`: BEGIN 在读取任何输入文件之前执行的块。
`END`: END 在处理所有输入文件后执行的块。

## crontab 命令

`crontab` 用于维护 `crontab` 文件。每个用户都有自己的 `crontab`，不能直接编辑，由 cron 守护进程维护。

## 语法：

```
crontab [-u user] [-i] {-e | -l | -r}
```

## 示例：

1. `-l` 选项在标准输出上显示 `crontab`。

```
crontab -l
```

2. `-r` 选项删除 `crontab`。

```
crontab -r
```

3. `-e` 选项使用指定的编辑器编辑当前表。退出编辑器后，修改的 `crontab` 将被安装。如果未定义这些环境变量，则使用默认编辑器`/bin/editor`。

```
crontab -e
```

4. 你可以指定要编辑的 `crontab` 的用户。假设你有一个 `www-data` 用户，它是 Apache 的默认运行。如果你想为该用户编辑 `crontab`，可以运行以下命令

```
crontab -u www-data -e
```

## 帮助命令

运行下面的命令查看 `crontab` 的完整指南。

```
man crontab
```

## xargs 命令

`xargs` 用于从标准输入构建并执行命令行。某些命令（如 `grep`）可以接受输入，但某些命令接受参数，这就是 `xargs` 出现的地方。

## 语法：

```
xargs [options] [command [initial-arguments]]
```

## 选项：

```
-0, --null
```

输入项以空字符而不是空白终止，且引号和反斜杠不是特殊的（每个字符都被字面对待）。禁用结束字符串，将其视为任何其他参数。当输入项可能包含空格、引号或反斜杠时有用。

```
-a file, --arg-file=file
```



从文件而不是标准输入读取项。如果使用此选项，在运行命令时 `stdin` 将保持不变。否则，`stdin` 将重定向到 `/dev/null`。

### `-o`, `--open-tty`

在执行命令之前，将 `stdin` 重新打开为 `/dev/tty`。如果希望 `xargs` 运行交互式应用程序，这非常有用。

### `--delimiter=delim`, `-d delim`

输入项由指定的字符终止。指定的分隔符可以是单个字符、C 风格的转义字符（如 `\n`），或八进制或十六进制转义代码。八进制和十六进制转义代码被视为 `printf` 命令处理。

不支持多字节字符。在处理输入时，引号和反斜杠不是特殊字符：输入中的每个字符都被视为字面量。`-d` 选项会禁用任何文件结束字符串，该字符串被视为与其他参数相同。

当输入仅由换行符分隔的项组成时，可以使用此选项，尽管在可能的情况下，设计程序使用 `-null` 总是更好。

### `-p`, `--interactive`

提示用户是否运行每条命令行并从终端读取一行。只有当响应以 `y` 或 `Y` 开头时才执行该命令行。隐含 `-p`。

## 示例

```bash
find /tmp -name core -type f -print | xargs /bin/rm -f
```

在 `/tmp` 目录或其子目录下查找名为 `core` 的文件并删除它们。请注意，如果文件名包含换行符或空格，此操作将无法工作。

```bash
find /tmp -name core -type f -print0 | xargs -0 /bin/rm -f
```

在 `/tmp` 目录或其子目录下查找名为 `core` 的文件并删除它们，处理文件名的方式可以正确处理包含空格或换行的目录名。

```bash
find /tmp -depth -name core -type f -delete
```

在 `/tmp` 目录或其子目录下查找名为 `core` 的文件并删除它们，但比之前的示例更高效，因为避免了使用 `fork(2)` 和 `exec(2)` 来启动 `rm`，并且不需要额外的 `xargs` 进程。

```bash
cut -d: -f1 < /etc/passwd | sort | xargs echo
```

生成系统上所有用户的紧凑列表。

## 帮助命令

运行以下命令查看 `xargs` 命令的完整指南。

```bash
man xargs
```

## `nohup` 命令

当 shell 退出（可能是在退出 SSH 会话时），HUP（挂断）信号会被发送给它的所有子进程，导致它们终止。

如果需要一个长时间运行的进程在退出 shell 后继续运行，则需要使用 `nohup` 命令。在任何命令前加上 `nohup` 会导致该命令对 HUP 信号免疫。

此外，`STDIN` 将被忽略，所有输出将重定向到本地文件 `./nohup.out`。

### 示例

1. 将 `nohup` 应用于长时间运行的 Debian 升级：

```bash
nohup apt-get -y upgrade
```

### 语法

```bash
nohup COMMAND [ARG]...
nohup OPTION
```

## `pstree` 命令

`pstree` 命令类似于 `ps`，但它不是列出正在运行的进程，而是以树的形式显示它们。

树形格式有时是显示进程层次更好的方法，这是可视化运行进程的一种更简单的方法。树的根是 `init` 或具有给定 `pid` 的进程。

### 示例

1. 显示所有运行进程的层级树结构：

```bash
pstree
```

2. 以指定的进程作为树的根显示树结构：

```bash
pstree [pid]
```

3. 仅显示由用户启动的进程：

```bash
pstree [USER]
```

4. 显示给定进程的父进程：

```bash
pstree -s [PID]
```

5. 每次分页查看输出，将其传输给 `less` 命令：

```bash
pstree | less
```

## 语法

```bash
ps [OPTIONS] [USER or PID]
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-a` | `--arguments` | 显示命令行参数 |
| `-A` | `--ascii` | 使用 ASCII 绘图字符 |
| `-c` | `--compact` | 不对相同的子树进行紧凑处理 |
| `-h` | `--highlight-all` | 高亮当前进程及其祖先 |
| `-H PID` | `--highlight-pid=PID` | 高亮此进程及其祖先 |
| `-g` | `--show-pgids` | 显示进程组 ID；隐含 `-c` |
| `-G` | `--vt100` | 使用 VT100 绘图字符 |
| `-l` | `--long` | 不截断长行 |
| `-n` | `--numeric-sort` | 按 PID 排序输出 |
| `-N type` | `--ns-sort=type` | 按命名空间类型排序（`cgroup`、`ipc`、`mnt`、`net`、`user`、`uds`） |
| `-p` | `--show-pids` | 显示 PIDs；隐含 `-c` |
| `-s` | `--show-parents` | 显示所选进程的父进程 |
| `-S` | `--ns-changes` | 显示命名空间转换 |
| `-t` | `--thread-names` | 显示完整的线程名称 |
| `-T` | `--hide-threads` | 隐藏线程，仅显示进程 |
| `-u` | `--uid-changes` | 显示 uid 转换 |
| `-U` | `--unicode` | 使用 UTF-8（Unicode）绘图字符 |
| `-V` | `--version` | 显示版本信息 |
| `-Z` | `--security-context` | 显示 SELinux 安全上下文 |

## `tree` 命令

Linux 中的 `tree` 命令递归地列出目录。

### 示例

1. 将 `nohup` 应用于长时间运行的 Debian 升级：

```bash
nohup apt-get -y upgrade
```

版本信息和退出。`-h`：显示帮助并退出。

## `printf` 命令

此命令允许你通过规则格式化变量来打印变量的值。它与 C 语言中的 `printf` 非常相似。

### 语法

```bash
$printf [-v variable_name] format [arguments]
```

### 选项

| 选项 | 描述 |
| --- | --- |
| `FORMAT` | `FORMAT` 控制输出，并定义 `ARGUMENTS` 在输出中的表示方式 |
| `ARGUMENT` | `ARGUMENT` 将根据 `FORMAT` 的定义插入到格式化后的输出中 |
| `--help` | 显示帮助并退出 |
| `--version` | 输出版本信息并退出 |

### 格式

`FORMAT` 字符串的结构可以提取为三个不同的部分：

- **普通字符**：将与原始输出完全相同的字符精确复制到输出中。
- **解释性字符序列**：使用反斜杠（`\`）进行转义。
- **转换规范**：这定义了 `ARGUMENTS` 作为输出部分的表示方式。

你可以在这个示例中看到这些部分：

```bash
printf " %s is where over %d million developers shape \"the future of software.\" Github 65
```

输出：

```text
Github is where over 65 million developers shape "the future of software."
```

有两个转换规范 `%s` 和 `%d`，并且有两个转义字符，即包裹 `future of software` 单词的起始和结束双引号。除此之外，都是普通字符。

## 转换规范

每个转换规范都以 `%` 开头，并以转换字符结束。在 `%` 和转换字符之间，按顺序可以存在：

- 一个负号，用于左对齐参数的转换结果。
- 一个整数，指定字段宽度；在至少有该数字个字符宽的字段中打印 `ARGUMENT` 数字的转换结果。如有必要，它将在左侧（如果调用了左对齐，则在右侧）填充以达到字段宽度。
- 一个点，将字段宽度与精度隔开。
- 一个整数，即精度，指定从字符串中打印的最大字符数，或者浮点数值小数点后的数字位数，或者整数的最小位数。
- 这些用于分别区分短整数和长整数，通常仅用于计算机编程。

`h` 或 `l`

`printf` 的转换字符决定打印什么种类的参数，如下：

| 转换字符 | 参数类型 |
| --- | --- |
| `s` | 字符串 |
| `c` | 整数，表示为对应 ASCII 值的字符 |
| `d, i` | 十进制形式的整数 |
| `o` | 无符号八进制整数 |
| `x, X` | 无符号十六进制整数 |
| `u` | 无符号十进制整数 |

| 转换字符 | 参数类型 |
| --- | --- |
| `f` | 默认精度为 6 的浮点数 |
| `e, E` | 科学计数法浮点数 |
| `p` | 内存地址指针 |
| `%` | 不进行转换 |

这里是 `printf` 输出 `ARGUMENT` 的示例列表。我们可以放置任何单词，但在本例中，我们放置了 `"linuxcommand"` 并用引号括起来，以便更容易看到与空格相关的位置。

| `FORMAT` 字符串 | 参数字符串 | 输出字符串 |
| --- | --- | --- |
| `%5s` | `"linuxcommand"` | `"linuxcommand"` |
| `%5s` | `"linuxcommand"` | `"linuxcommand"` |
| `%-.5s` | `"linuxcommand"` | `"linux"` |
| `%-8s` | `"linuxcommand"` | `"linuxcommand"` |
| `%-15s` | `"linuxcommand"` | `"linuxcommand "` |
| `%12.5s` | `"linuxcommand"` | `"linux"` |
| `%-12.5s` | `"linuxcommand"` | `"linux "` |
| `%-12.4` | `"linuxcommand"` | `"linu "` |

### 说明

- `printf` 要求转换字符串的数量与 `ARGUMENT` 的数量匹配。
- `printf` 将转换字符串一对一映射，并期望为每个转换字符串找到正好一个 `ARGUMENT`。
- 转换字符串始终从左到右解释。

### 示例

输入：

```bash
printf "We know %f is %s %d" 12.07 "larger than" 12
```

输出：

```text
We know 12.070000 is 3 larger than 12
```

上面的示例显示了 3 个参数：`12.07`、`larger than` 和 `12`。它们每一个都从左到右与给定的 3 个转换字符串（`%f`、`%d`、`%s`）一一对应。

## 被 `printf` 解释为特殊字符的序列

| 转义字符 | 描述 |
| --- | --- |
| `\a` | 发出警报（播放铃声）。通常是 ASCII BEL 字符 |
| `\b` | 打印退格 |
| `\c` | 指示 `printf` 不再产生输出 |
| `\e` | 打印转义字符（ASCII 27） |
| `\f` | 打印分页 |
| `\n` | 打印换行 |
| `\r` | 打印回车 |
| `\t` | 打印制表符 |
| `\v` | 打印垂直制表符 |
| `"` | 打印双引号（`"`） |
| `\` | 打印反斜杠（`\`） |
| `\NNN` | 用八进制打印字节 |
| `\xNN` | 用十六进制打印字节 |
| `\uNNNN` | 用 Unicode 打印字符 |

输出：

```text
Github is where over 65 million developers shape "the future of software."
```

有两个转换规范 `%s` 和 `%d`，并且有两个转义字符，即包裹 `future of software` 单词的起始和结束双引号。除此之外，都是普通字符。

| 转换字符 | 参数类型 |
| --- | --- |
| `f` | 默认精度为 6 的浮点数 |
| `e, E` | 科学计数法浮点数 |
| `p` | 内存地址指针 |
| `%` | 不进行转换 |

| `FORMAT` 字符串 | 参数字符串 | 输出字符串 |
| --- | --- | --- |
| `%5s` | `"linuxcommand"` | `"linuxcommand"` |
| `%5s` | `"linuxcommand"` | `"linuxcommand"` |
| `%-.5s` | `"linuxcommand"` | `"linux"` |
| `%-8s` | `"linuxcommand"` | `"linuxcommand"` |
| `%-15s` | `"linuxcommand"` | `"linuxcommand "` |
| `%12.5s` | `"linuxcommand"` | `"linux"` |
| `%-12.5s` | `"linuxcommand"` | `"linux "` |
| `%-12.4` | `"linuxcommand"` | `"linu "` |

## `cut` 命令

`cut` 命令允许你从文件的每行中删除部分。将每个文件的选定部分打印到标准输出。如果没有文件，或文件为 `-`，则读取标准输入。

### 用法示例

1. 在文件中选择特定字段：

```bash
cut -d "delimiter" -f (字段编号) file.txt
```

2. 选择特定字符：

```bash
cut -c [(k)-(n)/(k,(n)/(n)] filename
```

在这里，如果 `k` 和 `n` 用 `-` 分隔，`k` 表示每行字符的起始位置，`n` 表示结束位置；否则它们仅为输入文件中每行中字符的位置。

3. 选择特定字节：

```bash
cut -b 1,2,3 filename               # 选择字节 1,2
                                   # 和 3

cut -b 1-4 filename                # 选择字节 1
                                   # 到 4

cut -b 1- filename                 # 选择字节 1 到文件末尾

cut -b -4 filename                 # 选择从开始到第 4 个字节
```

制表符和退格被视为 1 字节的字符。

### 语法

```bash
cut OPTION... [FILE]...
```

### 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-b` | `--bytes=LIST` | 仅选择这些字节 |
| `-c` | `--characters=LIST` | 仅选择这些字符 |
| `-d` | `--delimiter=DELIM` | 使用 `DELIM` 代替 TAB 作为字段分隔符 |
| `-f` | `--fields` | 仅选择这些字段；打印任何不包含分隔符的行，除非指定了 `-s` |
| `-s` | `--only-delimited` | 不打印不包含分隔符的行 |
| `-z` | `--zero-terminated` | 行分隔符为 NUL，而不是换行符 |

## `sed` 命令

`sed` 命令代表流编辑器（stream editor）。流编辑器用于对输入流（文件或来自管道的输入）执行基础文本转换。

例如，它可以对文件执行许多功能，如搜索、查找并替换、插入或删除。虽然它在某些方面与允许脚本化编辑的编辑器（如 `ed`）相似，但 `sed` 的工作方式是对输入仅进行一次扫描，因此是高效的。`sed` 在管道中过滤文本的能力使其特别从其他类型的编辑器中脱颖出来。

`sed` 命令最常用的用法是替换或查找并替换。通过使用 `sed` 可以在不打开文件的情况下编辑文件，这是在文件中查找和替换某些内容的快得多的方法。

它支持基本和扩展表达式，允许你匹配复杂模式。大多数 Linux 发行版都附带 GNU，并且默认预装了 `sed`。

### 示例

1. 使用 `sed` 查找并替换字符串：

```bash
sed -i 's/{search_regex}/{replace_value}/g' input-file
```

2. 递归查找并替换（配合 `find` 使用）：

有时你可能想递归搜索目录中包含某个字符串的文件，并替换所有文件中的该字符串。可以使用 `find` 等命令递归搜索目录中的文件并将文件名传递给 `sed`。

以下命令将递归搜索当前工作目录下的文件并将文件名传递给 `sed`。它将递归搜索当前工作目录下的文件并将文件名传递给 `sed`。

```bash
find . -type f -exec sed -i 's/{search_regex}/{replace_value}/g' {} +
```

### 语法

```bash
sed [OPTION]... {script-if-no-other-script} [INPUT-FILE]...
```




- `OPTION` - `sed` 原地编辑、静默、跟踪符号链接、行长度、空数据……等。
- `{script-if-no-other-script}` - 如果可用，将脚本添加到命令中。
- `INPUT-File` - 输入流，一个文件或来自管道的输入。

如果没有提供输入，则第一个非选项参数被视为要解释的 `sed` 脚本。所有剩余都是输入文件的名称；如果未指定输入文件，则标准输入为 `sed`。

GNU `sed`我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。主页：http://www.gnu.org/software/sed/

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-i[SUFFIX]` | `--in-place=[SUFFIX]` | 原地编辑文件（根据提供的 `SUFFIX` 制作备份）。 |
| `-n` | `--quiet,--silent` | 抑制模式空间的自动打印。 |
| `-e` | `--expression=script` | 将脚本添加到要执行的命令中。 |
| `-f script-file` | `--file=script-file` | 将 `script-file` 的内容添加到要执行的命令中。 |
| `-l N` | `--line-length=N` | 指定命令所需的行换行长度。 |
| `-r` | `--regexp-extended` | 在脚本中使用扩展正则表达式。 |
| `-s` | `--separate` | 将文件视为单独的文件，而不是单个长流。从输入文件中加载最少的数据并频繁地刷新输出缓冲区。 |
| `-z` | `--null-data` | 使用 NULL 字符分隔行。 |

# 在开始之前

起初可能看起来很复杂，但使用 `sed` 在文件中搜索和替换文本非常简单。

了解更多信息：https://www.gnu.org/software/sed/manual/sed.html

# `vim` 命令

`vim` 是一个用于 Unix 的文本编辑器，随 Linux、BSD 和 macOS 一起提供。它以快速强大而闻名，部分是因为是一个可以在终端运行的小型程序（尽管它有图形界面）。`vim` 文本编辑器由 Bram Moolenaar 开发。它支持大多数文件类型，`vim` 编辑器也被称为程序员的编辑器。这主要是因为完全完全可以使用键盘进行管理，无需菜单或鼠标。

注意：不要将 `vim` 与 `vi` 混淆。`vi` 代表 "Visual"，是 Bill Joy 在 1976 年开发的文本编辑器。`vim` 代表 "Improved"，是 `vim` 编辑器的改进版克隆。

## 关于 `vim` 搜索最多的问题

### 如何退出 `vim` 编辑器？

关于 `vim` 编辑器搜索最多的问题看起来非常滑稽，但新用户在使用 `vim` 编辑器时在刚开始就卡住确实是真的。

保存文件并退出 `vim` 编辑器的命令：`:wq`

在不保存文件的情况下退出 `vim` 编辑器的命令：`:q!`

## 趣味阅读

这里有一个针对同一个问题的调查，看看这个，不要想着退出 `vim` 编辑器。

## 安装

首先检查是否安装了 `vim`，运行以下命令：

```bash
vim --version
```

在 Ubuntu/Debian 上：

```bash
sudo apt-get install
```

在 CentOS/Fedura 上：

```bash
sudo yum install
```

## 语法

```bash
vim [DIRECTORY_PATH]
```

## 示例

1. 在当前打开名为 `demo.txt` 的文件：

   ```bash
   vim demo.txt
   ```

2. 打开特定路径的文件：

   ```bash
   vim path/filename
   ```

3. 从指定行号打开文件：

   ```bash
   vim filename +NUMBER
   ```

## `vim` 编辑器的模式

`vim` 有一些模式，但可能使用的模式是命令模式和插入模式。

## `vim` 编辑器的工作流

- 使用 `vim` 打开新文件或现有文件。
- 输入 `i` 切换到插入模式以便编辑文件。
- 完成后，按 Esc 键退出插入模式返回命令模式。
- 输入 `:w` 或 `:wq` 分别保存文件。

## 交互式训练

在这些交互式教程中，你将学习使用 `vim` 命令的不同方法：

打开教程

## 附加标志及其功能

| 标志/选项 | 描述 |
|---|---|
| `-e` | 进入 Ex 模式 (Ex-mode) |
| `-R` | 进入只读模式 |
| `-R` | 进入只读模式 |
| `-g` | 启动 GUI |
| `-eg` | 以 Ex 模式启动 GUI |
| `-Z` | 类似于 `vim`，但在受限模式下 |
| `-d` | 进入差异模式 (diff-mode) |
| `-h` | 显示用法（帮助）信息并退出 |
| `+NUMBER` | 打开文件并将光标置于指定的行号 |

## 了解更多关于 `vim`

`vim` 无法在一天内学会，要在日常任务中使用它来上手。

要了解更多关于 `vim` 的信息请参考文章：

作者 Daniel Miessler

# `chown` 命令

`chown` 命令使得更改文件或目录的所有权成为可能。用户和组在 Linux 中是基础，通过 `chown` 可以更改文件或目录的所有者。也可以递归地更改所有权。

## 示例

1. 更改文件的所有者：

   ```bash
   chown user file.txt
   ```

2. 更改文件的组：

   ```bash
   chown :group file.txt
   ```

3. 在同一行中更改用户和组：

   ```bash
   chown user:group file.txt
   ```

4. 递归地更改文件夹的所有权：

   ```bash
   chown -R user:group folder
   ```

# `find` 命令

`find` 命令允许你在目录层次结构中搜索文件。

- 搜索具有特定名称的文件。
- 按模式搜索文件。
- 搜索空文件和空目录。

## 示例

1. 搜索特定名称的文件：

   ```bash
   find ./directory1 -name sample.txt
   ```

2. 按模式搜索文件：

   ```bash
   find ./directory1 -name '*.txt'
   ```

3. 在 `/` 目录下查找所有名称为 `test` 的目录：

   ```bash
   find / -type d -name test
   ```

4. 搜索当前目录下的空文件：

   ```bash
   find . -size 0k
   ```

## 语法

```bash
find [options] [paths] [expression]
```

## 简单来说

```text
find [从何处开始搜索]

[expression 决定要查找的内容] [-options] [要查找的内容]
```

## 附加标志及其功能

常用的主表达式包括：

- `-name` 模式 - 测试文件名是否匹配给定的 shell 通配符模式。
- `-type` 类型 - 测试文件是否为给定类型。接受的 Unix 文件类型包括：

| options | 描述 |
| --- | --- |
| `b` | 块设备（缓冲） |
| `d` | 目录 |
| `f` | 普通文件 |
| `l` | 符号链接 |
| `-print` | 始终返回真；将当前文件名加换行符打印到标准输出。 |
| `-mtime n` | 查找 `n` 天前修改的所有文件。 |
| `-atime n` | 查找 5 天前访问的所有文件。 |
| `-cmin n` | 查找过去 1 小时内修改的所有文件。 |
| `-newer file` | 查找比指定文件修改更晚的文件。 |
| `-size n` | 文件使用空间单位，并向上取整。 |

## 帮助命令

运行以下命令查看 `find` 命令的完整指南，或点击此处。

```bash
man find
```

# `rmdir` 命令

`rmdir` 命令用于从 Linux 文件系统中删除空目录。只有当命令行中指定的目录都为空时，`rmdir` 命令才会删除每一个目录。

## 使用方法与示例

1. 删除目录及其父目录：

   ```bash
   rmdir -p a/b/c              // 类似于 'rmdir a/b/c a/b a'
   ```

2. 删除多个目录：

   ```bash
   rmdir a b c                   // 删除空目录 a、b 和 c
   ```

## 语法

```bash
rmdir [OPTION]... DIRECTORY...
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-` | `--ignore-fail-on-empty` | 忽略仅因目录非空导致的每个失败 |
| `-p` | `--parents` | 删除 `DIRECTORY` 及其父目录 |
| `-d` | `--delimiter=DELIM` | 使用 `DELIM` 代替 TAB 作为字段分隔符 |
| `-v` | `--verbose` | 为处理的每个目录输出诊断 |

# `lsblk` 命令

## 总结

`lsblk` 命令显示系统上的块设备和循环设备。当你想要格式化磁盘、写入文件系统、检查文件系统并知道设备的挂载点时，它非常有用。

## 示例

1. 基本用法非常简单 - 直接执行 `lsblk` 而不带任何选项。

   ```bash
   lsblk
   ```

2. 让 `lsblk` 显示空设备：

   ```bash
   lsblk -a
   ```

3. 让 `lsblk` 以字节为单位打印大小信息：

   ```bash
   lsblk -b
   ```

4. 让 `lsblk` 为每个设备打印区域模型：

   ```bash
   lsblk -z
   ```

5. 让 `lsblk` 跳过从条目：

   ```bash
   lsblk -d
   ```

6. 让 `lsblk` 使用 ASCII 字符进行树形格式化：

   ```bash
   lsblk -i
   ```

7. 让 `lsblk` 显示关于设备所有者、组和模式的信息：

   ```bash
   lsblk -m
   ```

8. 让 `lsblk` 输出指定的列：

   ```bash
   lsblk -o NAME,SIZE
   ```

## 语法

```bash
lsblk [options] [<device> ...]
```

## 读取 `lsblk` 提供的信息

在不带标志或命令行参数的情况下运行 `lsblk` 时，它会将通用磁盘信息写入标准输出（STDOUT）。以下是解释这些信息的表格：

| 列名 | 含义 | 解释 |
| --- | --- | --- |
| `NAME` | 设备名称。 | 显示设备名称。 |
| `RM` | 可移动。 | 如果设备是可移动的显示 1，否则显示 0。 |
| `SIZE` | 设备大小。 | 显示设备大小。 |
| `RO` | 只读。 | 如果是只读的显示 1，否则显示 0。 |
| `TYPE` | 块或循环设备的类型。 | 整个磁盘显示 disk，分区显示 part。 |
| `MOUNTPOINTS` | 设备挂载位置。 | 显示设备挂载的位置。如果未挂载则显示为空。 |

## 读取特定设备的信息

在不带标志或命令行参数的情况下运行 `lsblk` 时，它会将通用磁盘信息写入标准输出（STDOUT）。以下是解释这些信息的表格：

```bash
lsblk /dev/sda
```

## `lsblk` 的常用标志

是一些标志的表格：

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-` | `--ignore-fail-on-empty` | 忽略仅因目录非空导致的每个失败 |
| `-p` | `--parents` | 删除 `DIRECTORY` 及其父目录 |
| `-d` | `--delimiter=DELIM` | 使用 `DELIM` 代替 TAB 作为字段分隔符 |
| `-v` | `--verbose` | 为处理的每个目录输出诊断 |
| `-a` | `--all` | 显示所有设备 |
| `-b` | `--bytes` | 以字节打印大小 |
| `-d` | `--device` | 仅显示设备 |
| `-D` | `--discard` | 显示丢弃能力 |
| `-E` | `--exclude` | 排除设备 |
| `-f` | `--fs` | 显示文件系统 |
| `-h` | `--help` | 显示帮助 |
| `-l` | `--list` | 列出设备 |
| `-j` | `--json` | 输出 JSON 格式 |
| `-L` | `--list` | 列出设备 |
| `-m` | `--perms` | 显示所有者、组和模式 |
| `-M` | `--merge` | 合并列 |
| `-n` | `--noheadings` | 不打印标题头 |
| `-o` | `--output` | 指定列 |
| `-P` | `--paths` | 显示路径 |
| `-r` | `--raw` | 原始输出 |
| `-S` | `--sort` | 排序 |
| `-t` | `--tree` | 显示树形结构 |
| `-V` | `--version` | 显示版本 |
| `-w` | `--width` | 设置宽度 |
| `-x` | `--sort` | 排序 |
| `-z` | `--zoned` | 显示模型 |

# `chmod` 命令

`chmod` 命令允许你使用符号模式、数字模式或引用文件来更改文件的权限。

## 示例

1. 使用符号模式更改文件的权限：

   ```bash
   chmod u=rwx,g=rx,o=r myfile
   ```

上述命令意味着：

- 用户可以读取、写入、执行 `myfile`
- 组用户可以读取、执行 `myfile`
- 其他用户可以读取 `myfile`

2. 使用数字模式更改文件的权限：

   ```bash
   chmod 754 myfile user:group file.txt
   ```

上述命令意味着：

- 用户可以读取、写入、执行 `myfile`
- 组用户可以读取、执行 `myfile`
- 其他用户可以读取 `myfile`

3. 递归地更改文件夹的权限：

   ```bash
   chmod -R 754 folder
   ```

## 语法

```bash
chmod [OPTIONS] MODE FILE(s)
```

- `[OPTIONS]`：
  - `-R`：递归，意味着处理目录内的所有文件。
- `MODE`：设置权限的不同方式：
  - 符号模式说明：
    - `u`：用户 (user)
    - `g`：组 (group)
    - `o`：其他 (other)
    - `=`：设置权限
    - `r`：读取 (read)
    - `w`：写入 (write)
    - `x`：执行 (execute)
    - 示例 `u=rwx` 意味着用户可以读取、写入和执行。
  - 数字模式说明：

数字模式基于用户、组和其他权限的二进制表示。欲需更多信息，请参考 Digital Ocean 社区部分的此解释：

- 4 代表“读取”；
- 2 代表“写入”；
- 1 代表“执行”，以及
- 0 代表“无权限”。
- 示例 7 表示读取 + 写入 + 执行。

# `grep` 命令

`grep` 过滤器在文件中搜索特定的字符模式，并显示所有包含该模式的行。`grep` 是 globally search for regular expression and print out（全局搜索正则表达式并输出）的缩写。文件中搜索模式被称为正则表达式。

## 示例

1. 在不区分大小的情况下搜索 `destination.txt` 文件中的字符串 ("KeY")：

   ```bash
   grep -i "KeY" destination.txt
   ```

2. 显示匹配项的数量：

   ```bash
   grep -c "key" destination.txt
   ```

3. 我们可以搜索多个文件并仅显示包含给定字符串/模式的文件：

   ```bash
   grep -l "key" destination1.txt destination2.txt destination3.xt destination4.txt
   ```

4. 显示文件中与匹配行的行号：

   ```bash
   grep -n "key" destination.txt
   ```

5. 如果你想 `grep` 正在监控的日志文件，可以添加 `--line-buffered` 来实时搜索它们。

## 语法

`grep` 命令的通用语法如下：

```bash
grep [options] pattern [files]
```




## 附加标志及其功能：

| 短标志 | 长标志 | 描述 |
|---|---|---|
| `-c` | `--count` | 打印每个输入文件的匹配行数计数 |
| `-h` | `--no-filename` | 显示匹配行，但不显示文件名 |
| `-i` | `--ignore-case` | 忽略匹配时的大小写 |
| `-l` | `--files-with-matches` | 仅显示文件名列表。 |
| `-n` | `--line-number` | 显示匹配行及其行号。 |
| `-v` | `--invert-match` | 打印所有不匹配模式的行 |
| `-e` | `--regexp=` | 使用此选项指定表达式。可以使用多次。 |
| `-f` | `--file=` | 从文件中读取模式，每行一个。 |
| `-F` | `--fixed-strings=` | 将模式解释为固定字符串，而非正则表达式。 |
| `-E` | `--extended-regexp` | 将模式视为扩展正则表达式 (ERE) |
| `-w` | `--word-regexp` | 匹配整个单词 |
| `-o` | `--only-matching` | 仅打印匹配行中的匹配部分，每个部分单独占一个输出行。 |
| | `--line-buffered` | 强制输出为行缓冲模式 |

# screen 命令

`screen` - 使用 `screen`，你可以启动一个 `screen` 会话，然后在该会话中打开任意数量的窗口（虚拟终端）。在 `screen` 中运行的即使在断开连接且窗口不可见也会继续运行。这对于运行长时间的会话（例如运行时间很长的 `bash` 脚本）非常有用。

要启动 `screen` 会话，你输入 `screen`，这将打开一个带有打开虚拟终端的新 `screen` 会话。

以下是管理 Linux `screen` 窗口的一些常用命令：

| 命令 | 描述 |
|---|---|
| `Ctrl+a+ c` | 创建新窗口（带 shell）。 |
| `Ctrl+a+"` | 列出所有窗口。 |
| `Ctrl+a+0` | 切换到窗口 0（通过数字）。 |
| `Ctrl+a+A` | 重命名当前窗口。 |
| `Ctrl+a+S` | 将当前区域水平拆分为两个区域。 |
| `Ctrl+a+'` | 将当前区域垂直拆分为两个区域。 |
| `Ctrl+a+ tab` | 将输入焦点切换到下一个区域。 |
| `Ctrl+a+ Ctrl+a` | 在当前和之前的窗口之间切换 |
| `Ctrl+a+ Q` | 关闭当前区域外的所有区域。 |

## 恢复 Linux Screen

要恢复到 `screen` 会话，你输入 `screen -r`。如果你有多个打开的 `screen` 会话，必须在命令中添加会话 ID 以连接到正确的会话。

## 列出所有打开的 screen 会话

要找到会话 ID，可以列出运行中的会话：

```
screen -ls
```

有屏幕 (Detached):
...

如果你想恢复会话，可以输入以下命令：

```
screen -r
```

# nc 命令

`nc`（或 `netcat`）命令用于执行涉及 TCP（传输控制协议，面向连接）、UDP（用户数据报协议，无连接，不保证数据交付）或 Unix socket 的操作。它可以被视为瑞士军刀。

## 语法：

```
nc [options] host [port]
```

## 示例：

- 1. 打开 `host` 的 TCP 连接：

```
nc -zv host.ip 80
```

- 2. 使用 UDP 代替 TCP：

```
nc -u host.ip
```

- 3. 使用 Unix socket：

```
nc -U /tmp/socket
```

- 4. 创建监听服务器：

```
nc -l 1234
```

- 5. 构建数据传输：

```
nc -l 1234 > filename.out
```

- 6. 与服务器通信：

```
printf "GET / HTTP/1.0\r\n\r\n" | nc host.ip 80
```

- 7. 端口扫描：

```
nc -zv host.ip 20-2000
```

## 标志及其功能：

| 短标志 | 描述 |
|---|---|
| `-4` | 强制 `nc` 使用 IPv4 地址 |
| `-6` | 强制 `nc` 使用 IPv6 地址 |
| `-b` | 允许广播 |
| `-D` | 开启套调试 |
| `-i` | 指定行与接收行之间的时间间隔 |
... (其余标志)

# make 命令

`make` 命令用于在特定的目录结构中自动重复多个命令。

一个示例是在 Azure 中更改不同订阅时，使用 `terraform init`、`terraform plan` 和 `terraform validate`。这通常通过以下步骤完成：

```
az account set --subscription "Subscription - Name"
terraform init
```

`make` 命令可以帮助我们的地方在于它可以一次性自动完成所有操作：`make tf-init`

## 语法：

```
make [ -f makefile ] [ options ] ... [ targets ] ...
```

## 使用示例（指南）：

- 1. 在你的指南目录创建 `Makefile`

- 2. 在你的 `Makefile` 中包含以下内容：

```
hello-world:
  echo "Hello, World!"

hello-bobby:
  echo "Hello, Bobby!"

touch-letter:
  echo "This is a text that is being inputted into our
  letter!" > letter.txt

clean-letter:
  rm letter.txt
```

- 3. 执行 `make hello-world` - 这会在我们的终端中输出 "Hello, World"。

- 4. 执行 `make hello-bobby` - 这会在我们的终端中输出 "Hello, Bobby!"。

- 5. 执行 `make touch-letter` - 这创建一个名为 `letter.txt` 的文本文件并在其中填充一行。

- 6. 执行 `make clean-letter`

# 详细且内容更丰富的教程参考：

[linoxide - linux make 命令示例](https://linoxide.com/linux-make-command-examples/) [makefiletutorial.com - 名字本身就说明了一切](https://makefiletutorial.com/)

# basename 命令

`basename` 是一个命令行实用程序，用于从给文件名中剥离目录。可选。它还可以移除任何尾部后缀。它是一个简单的命令，只接受几个选项。

## 示例

最基本的示例是打印去除了前导目录的文件名：

```
basename /etc/bar/foo.txt
```

输出将包含文件名：

```
foo.txt
```

如果你在指向目录的路径字符串上运行 `basename`，你将获得路径的最后一段。在这个示例中，`/etc/bar` 是一个目录。

```
basename /etc/bar
```

输出

```
bar
```

`basename` 命令移除任何尾部的 `/` 字符：

```
basename /etc/bar/foo.txt/
```

输出

```
foo.txt
```

## 选项

- 1. 默认情况下，每行输出都以换行符结束。要用 `\NUL` 结束行，请使用 `-z` (`-zero`) 选项。

```
$ basename -z /etc/bar/foo.txt
foo.txt$
```

- 2. `basename` 命令可以接受多个名称作为参数。要这样做，请使用 `-a` (`-multiple`) 选项调用它，后跟着用空格分隔的文件列表。例如，要获取 `/etc/bar/foo.txt` 和 `/etc/spam/eggs.docx` 的文件名，你需要运行：

```
basename -a /etc/bar/foo.txt /etc/spam/eggs.docx
```

```
foo.txt
eggs.docx
```

## 语法

`basename` 命令支持两种语法格式：

```
basename NAME [SUFFIX]
basename OPTION... NAME...
```

## 附加功能

移除尾部后缀：要移除文件名中的任何尾部后缀，请将后缀作为第二个参数传递：

```
basename /etc/hostname name
host
```

通常，此功能用于剥离文件扩展名

## 帮助命令

运行以下命令查看 `basename` 命令的完整指南。

```
man basename
```

# banner 命令

`banner` 命令以大字母将 ASCII 字符字符串写入标准输出。输出中的每行长度最多可达 10 个大写或小写字符。输出时，所有字符均以大写形式显示，小写的输入字符比大写的输入字符小。

注意：如果你在 `sleep` 命令中定义了多个数字，则该命令将延迟这些值之和。

## 示例：

- 1. 在工作站上显示 `banner`，请输入：

```
banner LINUX!
```

- 2. 要在一行中显示多个单词，请用引号将文本括起来，如下：

```
banner "Intro to" Linux
```

这将 `Intro to` 显示在一行，`Linux` 显示在下一行

- 3. 用大字母打印 "101LinuxCommands"。

```
banner 101LinuxCommands
```

它将只会打印 `101LinuxCo`，因为 `banner` 的默认容量为 10

# alias 命令

`alias` 命令允许你为命令创建快捷方式或定义你自己的命令。这主要用于避免输入长命令。

## 示例：

- 1. 以 `alias NAME=VALUE` 的重用形式显示所有定义的别名列表：

```
alias -p
```

- 2. 为 `ls -A` 创建快捷方式：

```
alias la='ls -A'
```

## 语法：

```
alias [-p] [name[=value]]
```

## 设置持久选项：

与大多数 Linux 终端自定义设置一样，你定义的任何别名仅适用于当前打开的终端会话。

要让任何别名在所有新会话中生效，你需要将该命令添加到你的文件中，以便在每个新终端启动时执行。此文件如下：

- **Bash**: `~/.bashrc`
- **ZSH**: `~/.zshrc`
- **Fish**: `~/.config/fish/config.fish`

你可以使用你喜欢的编辑器按如下方式打开该文件：

```
vim ~/.bashrc
```

每行输入你的命令，然后保存文件并退出。命令将在下次会话中自动生效。

如果你要在当前会话中生效，请运行以下命令：

```
source ~/.bashrc
```

## 反向命令：

要移除预定义的别名，你可以如下 Go 使用 `unalias` 命令：

```
unalias alias_name
```

移除所有别名

```
unalias -a
```

# date 命令

`date` 命令用于打印当前日期。

`date` 命令也用于设置日期、时间。

## 在 UTC 中显示日期和时间

- `-u` 在协调世界时区中显示日期和时间：

```
date -u
```

- 1. 显示任何给定的日期字符串：

```
date --date="2/02/2010"
date --date="2 years ago"
```

## 语法：

```
date [OPTION]... [+FORMAT]
date [-u|--universal] [MMDD[[CC]YY][.ss]]
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
|---|---|---|
| `-d` | `--date=STRING` | 将提供的字符串转换为格式化的日期 |
| `-f` | `--file=DATE` | 类似于 `--date`，但用于文件 |
| `-I[FMT]` | `--iso-8601[FMT]` | 以 ISO-8601 格式显示日期和时间 |
| `-r` | `--reference=FILE` | 显示 `FILE` 的最后修改时间 |
| `-s` | `--set=STRING` | 将时间设置为 `STRING` 描述的时间 |
| `-u` | `--universal` | 在 UTC（协调世界时）时区显示日期和时间 |
| `-R` | `--rfc-email` | 以 RFC 3339 格式显示日期和时间 |
| | `rfc-3339=FMT` | 通常配合 `--date` 使用，用于标记解析日期并向 `stderr` 警告可疑用法 |

## 控制输出：

你可以使用格式指定符来控制输出的日期和时间。

## 示例：

| 命令 | 输出 |
|---|---|
| `$ date "+%D"` | 10/22/21 |
| `$ date "+%D %T"` | 10/22/21 05:33:51 |
| `$ date "+%A %B %d %T %y"` | Friday October 22 05:34:47 21 |

## 语法：

```
date "+[format-options ...]"
```

## 控制输出的格式指定符列表：

| 指定符 | 描述 |
|---|---|
| `%a` | 简写的星期几名称（例如 Sun） |

## 标识符描述

- `%A` 完整的星期几名称（例如：Sunday）
- `%b` 月份缩写（例如：Jan）
- `%B` 完整的月份名称（例如：January）
- `%c` 日期和时间（例如：Thu 3 23:05:25 2005）
- `%C` 世纪；与 `%Y` 相似，但省略最后两位数字（例如：20）
- `%d` 月份几号（例如：01）
- `%D` 日期；与 `%m/%d/%y` 相同
- `%e` 月份几号，空格填充；与 `%d` 相同
- `%F` 完整日期；与 `%Y-%m-%d` 相同
- `%g` ISO周数的最后两位（与 `%G` 相同）
- `%G` ISO周年份（与 `%V` 相同）；通常与 `%V` 配合
- `%h` 与 `%b` 相同
- `%H` 小时（00..23）
- `%I` 小时（01..12）
- `%j` 年中的第几天（001..366）
- `%k` 小时，空格填充（0..23）；与 `%H` 相同
- `%l` 小时，空格填充（1..12）；与 `%I` 相同
- `%m` 月份（01..12）
- `%M` 分（00..59）
- `%n` 换行
- `%N` 纳秒（000000000.999999999）
- `%p` 语言区域的 AM 或 PM；若未知则为空
- `%P` 与 `%p` 相同但小写
- `%q` 季度（1..4）
- `%r` 语言区域的12小时制时间（例如：11:10:04）
- `%R` 24小时制的小时分钟；与 `%H:%M` 相同
- `%s` 自 1970-01-01 00:00:00 UTC 以来的秒数
- `%S` 秒（00..60）
- `%t` 制表符
- `%T` 时间；与 `%H:%M:%S` 相同
- `%u` 星期几（1..7）；1 是周一
- `%U` 年周数，以周日为周的第一天（00..53）
- `%V` ISO周数，以周一为周的第一天（01..53）
- `%w` 星期几（00..6）；0 是周日
- `%W` 年周数，以周一为周的第一天（00..53）
- `%x` 语言区域的日期表示（例如：12/31/99）
- `%X` 语言区域的时间表示（例如：23:13:48）
- `%y` 年份的最后两位（00..99）
- `%Y` 年
- `%z` +hhmm 数字时区（例如：-0400）
- `%:z` +hh:mm:ss 数字时区（例如：-04:00:00）
- `%::z` 带有必要精度的数字时区（例如：-04, +05:30）
- `%Z` 字母时区缩写（例如：EDT）

# mount 命令

`mount` 命令用于挂载“附加”文件系统，使其可以通过现有的目录树结构访问。

## 示例：

1. 显示版本信息：

```
mount -V
```

2. 将设备上找到的为 `type` 文件系统挂载到目录 `dir`：

```
mount -t type device dir
```

## 语法：

```
mount [-lhV]
```

```
mount -a [-Fnrsvw] [-t vfstype] [-o optlist]
```

```
mount [-fnrvw] [-t fstype] [-o options] device dir
```

## 附加标志及其功能：

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-h` | `--help` | 显示帮助信息并退出 |
| `-n` | `--no-mtab` | 挂载时不写入 `/etc/mtab` |
| `-a` | `--all` | 挂载 `fstab` 中提到的所有（指定类型的）文件系统 |
| `-r` | `--read-only` | 以只读模式挂载文件系统 |
| `-w` | `--rw` | 以读写模式挂载文件系统 |
| `-M` | `--move` | 将子树移动到其他地方。 |
| `-B` | `--bind` | 重新挂载子树到其他地方（使其内容在两个地方都可用）。 |

# nice/renice 命令

`nice`/`renice` 命令用于修改要执行程序的优先级。优先级范围在 -20 到 19 之间，其中 19 最低。

## 示例：

1. 以比默认低的优先级（较慢）在后台运行 `cc` 命令：

```
nice -n 15 cc -c *.c &
```

2. 增加 "test" 组所有进程的优先级：

```
renice --20 -g test
```

## 语法：

```
nice [ -Increment| -n Increment ] Command [ Argument ... ]
```




## 标志

| 短标志 | 长标志描述 |
| --- | --- |
| `-Increment` | `Increment` 是你想要分配的优先级值。 |
| `-n Increment` | 与 `-Increment` 相同 |

# `wc` 命令

`wc` 命令代表 word count（单词计数）。它用于统计行数、单词和字节数。

## 示例

1. 统计文件的行、单词和字节：

```bash
wc file
```

2. 仅统计行数：

```bash
wc -l file
```

3. 仅统计单词数：

```bash
wc -w file
```

4. 仅统计字节数：

```bash
wc -c file
```

## 语法

```bash
wc [option...] [file...]
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
| --- | --- | --- |
| `-c` | `--bytes` | 打印字节数 |
| `-L` | `--chars` | 打印字符数 |
| `-l` | `--lines` | 打印行数 |
| `-w` | `--words` | 打印单词数 |
| `-m` | `--max-chars` | 打印最大字符数 |

# `zcat` 命令

`zcat` 允许你查看压缩文件。

## 示例

1. 查看压缩文件的内容：

```bash
~$ zcat test.txt.gz
Hello World
```

2. 它也可以与多个文件一起工作：

```bash
~$ zcat test2.txt.gz test.txt.gz
hello
Hello world
```

## 语法

`zcat` 命令的一般语法如下：

```bash
zcat [ -n ] [ -V ] [ File ... ]
```

# `fold` 命令

Linux 中的 `fold` 命令会将输入文件中的每行折叠，以适应指定的宽度，并将其打印到标准输出。

默认情况下，它会在最大 80 列处进行折行，但这是可以配置的。

要使用 `fold` 命令折叠输入，请将文件或标准输入传递给该命令。

## 语法

```bash
fold [OPTION]... [FILE]...
```

## 选项

`-w`：在 `fold` 命令中使用此选项，我们可以通过列数来限制宽度。

通过使用此命令，我们将列宽从默认的 80 更改。语法：

```bash
fold -w[n] [FILE]
```

示例：将 `file1.txt` 的行折叠为 60 列的宽度：

```bash
fold -w60 file1.txt
```

`-b`：`fold` 命令的此选项用于通过字节数而不是列数来限制输出宽度。

通过使用此选项，我们可以强制输出宽度为字节数。

```bash
fold -b[n] [FILE]
```

示例：将文件的输出宽度限制为 40 字节，命令将在 40 字节处断开输出。

```bash
fold -b40 file1.txt
```

`-s`：此选项用于在空格处断行，以确保单词不被切断。

如果行的段落在第一个宽度列位置内包含空白字符，则在满足宽度限制的最后一个此类空白字符后断行。

```bash
fold -w[n] -s [FILE]
```

# `quota` 命令

`quota` 显示磁盘使用情况和限制。

## 安装

你可以直接通过运行以下命令在 Ubuntu 系统上安装 `quota`：

```bash
sudo apt-get install quota
```

对于 Debian，使用不带 `sudo` 的安装命令：

```bash
apt-get install quota
```

## 语法

`quota` 命令的一般语法如下：

```bash
quota [ -u [ User ] ] [ -g [ Group ] ] [ -v | -q ]
```

# `aplay` 命令

`aplay` 是一个用于 ALSA（高级 Linux 声音架构）声卡驱动的命令行音频播放器。它支持多种文件格式和带有多个设备的多个声卡。它基本上用于命令行界面播放音频。`aplay` 与 `arecord` 非常相似，只是它播放而不是录制。对于支持的音频文件格式，采样率、位深度等可以从音频文件头自动确定。

## 语法

```bash
$ aplay [flags] [filename [filename]] ...
```

## 选项

- `-h, -help`：显示帮助信息。
- `-d, -duration=#`：在 `#` 秒后中断。
- `-r, -rate=#`：以赫兹为单位的采样率。默认率为 8000 兹。
- `-version`：打印当前版本。
- `-l, -list-devices`：列出所有声卡和数字音频设备。
- `-L, -list-pcms`：列出所有定义的 PCM（脉冲编码调制）。
- `-D, -device=NAME`：通过名称选择 PCM。

注意：此命令包含我们通常不需要的各种选项。如果你想了解更多信息，可以只需在终端上运行以下命令：

```bash
aplay --help
```

## 示例

1. 以 2500hz 的频率播放 10 秒音频：

```bash
$ aplay -d 10 -r 2500hz sample.mp3
```

以 2500hz 频率播放 `sample.mp3` 文件持续 10 秒。

2. 以 2500hz 的频率播放完整音频段：

```bash
$ aplay -r 2500hz sample.mp3
```

以 2500hz 频率播放 `sample.mp3` 文件。

3. 显示版本信息：

```bash
$ aplay --version
```

显示版本信息。对我来说它显示的是 `aplay: version 1.1.0`。

# `spd-say` 命令

`spd-say` 将文本转语音输出请求发送到 `speech-dispatcher` 进程，该进程处理它并在理想情况下将结果输出到音频系统。

## 语法

```bash
$ spd-say [options] "some text"
```

## 选项

- `-r, --rate`：设置语音速率（-100 到 +100 之间，默认：0）。
- `-p, --pitch`：设置语音音调（-100 到 +100 之间，默认：0）。
- `-i, --volume`：设置语音音量（强度）（-100 到 +100 之间，默认：0）。
- `-o, --output-module`：设置输出模块。
- `-l, --language`：设置语言（ISO 代码）。
- `-t, --voice-type`：设置首选的语音类型（`male1, male2, male3, female1, female2, female3, child_male, child_female`）。
- `-m, --punctuation-mode`：设置标点模式（`none, some, all`）。
- `-s, --spelling`：拼写消息。
- `-x, --ssml`：开启 SSML 模式（默认：0）。
- `-e, --pipe-mode`：从 stdin 管道到 stdout 并加上 Speech Dispatcher。
- `-P, --priority`：设置消息优先级（`important, message, text, notification, progress`；默认：`text`）。
- `-N, --application-name`：设置用于建立连接到特定字符串值的应用程序名称（默认：`spd-say`）。
- `-n, --connection-name`：等待消息。
- `-w, --wait`：等待消息。
- `-S, --stop`：停止消息。
- `-v, --version`：打印当前版本。
- `-h, --help`：打印此帮助。

# `xeyes` 命令

`xeyes` 是一个图形化程序，可创建一组跟随光标的眼睛。它在显示器上非常有用。

## 语法

```bash
xeyes
```

## `xeyes` 的作用是什么？

`xeyes` 是一个创建一组跟随光标的眼睛的图形化程序。它在显示器上非常有用。

# `parted` 命令

`parted` 命令用于管理硬盘分区。它可以用于添加、删除、缩小和扩展文件系统。需要 root 权限。

## 示例

1. 显示所有块设备的分区布局：

```bash
sudo parted -l
```

2. 显示默认选择磁盘的分区表：

```bash
sudo parted print
```

3. 为特定磁盘创建新的 `label-type` 类型：

```bash
sudo parted mklabel label-type
```

`label-type` 可以取 `"aix"`、`"amiga"`、`"bsd"`、`"dvh"`、`"gpt"`、`"loop"`、`"mac"`、`"msdos"`、`"pc98"` 或 `"sun"`。

4. 在特定磁盘上创建类型、文件系统和大小的分区：

```bash
sudo parted mkpart type fs-type 1 size
```

`type` 取 `"primary"`、`"logical"`、`"extended"`。`fs-type` 可选。它可以取 `"btrfs"`、`"ext2"`、`"ext3"`、`"ext4"`、`"fat16"`、`"fat32"`、`"hfs"`、`"hfs+"`、`"linux-swap"`、`"nfs"`、`"reisers"`、`"udf"` 或 `"xfs"`。`size` 是磁盘的总大小。要创建一个大小为 50Mb 的分区，将取值为 50。

5. `parted` 也可以以交互格式运行。可以通过交互会话中的适当命令执行对分区的操作。交互会话中的 `help` 命令将显示所有可能的磁盘操作。

```text
$ sudo parted
GNU Parted 3.3
Using /dev/sda
Welcome to GNU Parted! 输入 'help' 查看命令列表。

(parted) print # 输出默认选择磁盘的分区表 - /dev/sda
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sda: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:
Number Start End Size Type File system Flags
1 1049KB 53.7GB 53.7GB primary ext4 boot

(parted) select /dev/sdb # 更改操作的磁盘
Using /dev/sdb

(parted) quit # 退出交互会话
```

## 语法形式

```bash
parted [options] [device [command [options...]]]
```

## 选项

| Short Flag | Long Flag Description |
| :--- | :--- |
| `-h` | `--help`：显示出所有可能的命令[选项]的帮助信息 |
| `-l` | `--list`：列出所有块设备上的分区布局 |
| `-m` | `--machine`：显示机器可解析的输出 |
| `-v` | `--version`：显示版本 |
| `-a` | `--align`：为新创建的分区设置对齐类型。它可以接受以下值：<br>`none`：使用磁盘类型允许的最小对齐<br>`cylinder`：将分区对齐到磁柱<br>`minimal`：使用磁盘拓扑信息提供的最小对齐<br>`optimal`：使用磁盘拓扑信息提供的最佳对齐 |

# `nl` 命令

`nl` 命令对文件中的行进行编号。作为查看文件内容的另一种方式，`nl` 命令对许多任务都非常有用。

## 语法

```bash
nl [ -b Type ] [ -f Type ] [ -h Type ] [ -l Number ] [ -d Delimiter ] [ -i Number ] [ -n Format ] [ -v Number ] [ -w Number ] [ -p ] [ -s Separator ] [ File ]
```

## 示例

1. 为所有行编号：

```bash
nl -ba chap1
```

2. 显示所有文本行：

```text
[server@ssh ~]$ nl states
1 Alabama
2 Alaska
3 Arizona
4 Arkansas
5 California
6 Colorado
7 Connecticut.
8 Delaware
```

3. 指定不同的行号格式：

```bash
nl -il0 -nrz -s:: -v10 -w4 chap1
```

你可以在命令行上只指定一个文件。你可以以任何顺序列出标志和文件名。

# `pidof` 命令

`pidof` 是一个命令行实用工具，允许你找到正在运行程序的进程 ID（PID）。

## 语法

```bash
pidof [OPTIONS] PROGRAM_NAME
```

要查看该命令的帮助信息和所有选项：

```text
[user@home ~]$ pidof -h
-c    返回具有相同根目录的 PID
-d <sep>  使用提供的字符作为输出分隔符
-h      显示此帮助文本
-n      避免在网络共享上使用 stat 系统函数
-o <pid>  忽略结果为给定 PID
-q      静默模式。不显示输出
-s      只返回一个 PID
-x      返回运行匹配名称脚本的 shell PID
-z      列出僵尸进程和 I/O 等待进程。可能会导致挂起。
```

## 示例

要找到 SSH 服务器的 PID，你可以运行：

```bash
pidof sshd
```

如果存在与 `sshd` 名称匹配的运行进程，它们的 PID 将显示在屏幕上。如果没有找到匹配项，输出将为空。

```text
# Output
4382 4368 811
```

当至少有一个运行的程序与请求的名称匹配时，`pidof` 返回 0。否则，退出码为 1。这在编写 shell 脚本时非常有用。

为了确保只显示你搜索的程序的 PID，请使用程序的完整路径作为参数。例如，如果你在两个不同的目录下运行了两个同名的程序，`pidof` 将显示这两个运行程序的 PID。

默认情况下，会显示所有匹配的运行程序的 PID。使用 `-s` 选项强制 `pidof` 只显示一个 PID：

```bash
pidof -s program_name
```

`-o` 选项允许你从命令输出中排除给定 PID 的进程：

```bash
pidof -o pid program_name
```

当使用 `-o` 选项调用 `pidof` 时，你可以使用名为 `%PPID` 的特殊 PID，它代表调用的 shell 或 shell 脚本。

要仅返回在相同根目录运行的进程 PID，请使用 `-c` 选项。该选项仅在 `pidof` 作为 root 或 sudo 用户运行时有效：

```bash
pidof -c pid program_name
```

## 结论

`pidof` 命令用于查找特定运行程序的 PID。

`pidof` 是一个简单的命令，没有很多选项。通常，你只会使用要搜索的程序名称来调用 `pidof`。

# `shuf` 命令

Linux 中的 `shuf` 命令将输入行的随机排列写入标准输出。它以与洗牌相同的方式对输入进行伪随机化处理。它是 GNU Coreutils 的一部分，不是 POSIX 的一部分。该命令在 bash 中可以从文件或标准输入读取，对这些输入行进行随机处理并显示输出。

## 语法

```bash
# 文件排序
shuf [OPTION] [FILE]

# 列表排序
shuf -e [OPTION]... [ARG]

# 范围排序
shuf -i LO-HI [OPTION]
```

和其他 Linux 命令一样，`shuf` 命令带有 `--help` 选项：

```text
[user@home]$ shuf --help
Usage: shuf [OPTION]... [FILE]
or: shuf -e [OPTION]... [ARG]
or: shuf -i LO-HI [OPTION]...
```

写入输入行的随机排列。

- `-e, --echo=ARG...`
- `-i, --range=LO-HI`
- `-n, --count=COUNT`
- `-o, --output=FILE`
- `-r, --repeat`
- `-s, --delimiter=DELIM`
- `-z, --shuffle-only`

## 示例

1. 为所有行编号：

```bash
nl -ba chap1
```

2. 显示所有文本行：

```text
[server@ssh ~]$ nl states
1 Alabama
2 Alaska
3 Arizona
4 Arkansas
5 California
6 Colorado
7 Connecticut.
8 Delaware
```

3. 指定不同的行号格式：

```bash
nl -il0 -nrz -s:: -v10 -w4 chap1
```

你可以在命令行上只指定一个文件。你可以以任何顺序列出标志和文件名。

## `less` 命令选项

一些常用的选项标志包括：

```text
-E less 在到达文件末尾时自动退出。

-f 强制 less 打开非普通文件（目录或设备特殊文件）。

-F 如果整个文件可以在第一个屏幕显示，则退出。

-g 高亮上次通过搜索找到的字符串。默认情况下，less 会高亮所有匹配上一次搜索命令的字符串。

-G 移除所有搜索到的字符串上的高亮。
```

要查看完整的选项列表，请运行以下命令查看 `less` 帮助文件：

```bash
less --help
```

## 示例

1. 打开文本文件：

```bash
less /etc/updatedb.conf
```

2. 显示行号：

```bash
less -N /etc/init/mysql.conf
```




# 使用模式搜索打开文件

```
less -pERROR /etc/init/mysql.conf
```

# 移除多个空行

```
less welcome.txt
```

在这里我向你展示了如何在 Linux 中使用 `less` 命令。虽然还有其他终端分页器（如 `most` 和 `more`），但 `less` 可能是一个更好的选择，因为它是一个几乎存在于每个系统中的强大工具。

更多详情：
https://phoenixnap.com/kb/less-command-in-linux#:~:text=The%20less%20command%20is%20a,resulting%20in%20fast%20loading%20speeds.

# nslookup 命令

`nslookup` 命令是一个网络管理命令行工具，用于查询域名命名系统（DNS）以获取域名与 IP 地址的映射或任何其他特定的 DNS 记录。

## 语法

```
nslookup [options] [host]
```

## 选项

一些常用的选项标志包括：

- `-domain=[domain-name]` 更改默认 DNS 名称。
- `-debug` 显示调试信息。
- `-port=[port-number]` 为查询指定端口。默认端口号为 53。
- `-timeout=[seconds]` 指定服务器响应允许的时间。
- `-type=a` 查看 DNS A 记录记录的信息。
- `-type=any` 查看所有可用的记录。
- `-type=hinfo` 查看关于主机的硬件信息。
- `-type=mx` 查看邮件交换服务器信息。
- `-type=ns` 查看名称服务器记录。
- `-type=ptr` 查看指针记录。用于反向 DNS 查询。
- `-type=soa` 查看起始起始记录（Start of Authority）。

## 示例

### 1. 查询 DNS 服务器

```
nslookup www.google.com
```

### 2. 为查询指定端口

```
nslookup -port=53 www.google.com
```

### 3. 获取 MX 记录

```
nslookup -type=mx google.com
```

在这里我向你展示了如何在 Linux 中使用 `nslookup` 命令。虽然还有其他 DNS 查询工具（如 `dig`），但 `nslookup` 可能是一个更好的选择，因为它是一个几乎存在于每个系统中的强大工具。

更多详情：Wikipedia 上的 `nslookup`

# cmp 命令

`cmp` 命令用于逐字节地比较两个文件。

## 语法

```
cmp [option] File1 File2
```

## 示例

### 1. 两个文件的比较

对两个文件进行简单比较，检查它们之间是否存在差异。

```
cmp File1 File2
```

### 2. 跳过指定字节数后比较文件

在跳过某些字节数后比较两个文件。

```
cmp -i 2 list.txt list2.txt
```

在这里“INT”代表要跳过的字节数。

### 3. 在输出中显示文件中差异的字节

```
cmp -b list.txt list1.txt
```

### 4. 在输出中显示文件的字节数和差异的字节值

```
cmp -l list.txt list1.txt
```

### 5. 比较文件的前 “n” 个字节

```
cmp -n 10 list.txt list2.txt
```

## 附加标志及其功能

| 短标志 | 长标志 | 描述 |
|---|---|---|
| `-b` | `--print-bytes` | 打印差异字节 |
| `-i` | `--ignore-initial=SKIP` | 跳过两个输入的前 `SKIP` 字节 |
| `-i` | `--ignore-initial=SKIP1:SKIP2` | 跳过 `FILE1` 的前 `SKIP1` 字节和 `FILE2` 的前 `SKIP2` 字节 |
| `-l` | `--verbose` | 输出字节数和差异字节值 |
| `-n` | `--bytes=LIMIT` | 最多比较 `LIMIT` 字节 |
| `-s` | `--quiet`, `--silent` | 禁止所有正常输出 |
| `v` | `--version` | 输出版本信息并退出 |
| | `--help` | 显示此帮助并退出 |

# expr 命令

`expr` 命令计算给定的表达式并显示其相应的输出。它用于整数的基本操作（如加、减、乘、除和取模）以及评估正则表达式、字符串操作（如子字符串、字符串长度等）。

## 语法

```
expr expression
```

## 示例

### 1. 使用 `expr` 命令执行基础算术运算

```
expr 7 + 14
expr 7 * 8
```

### 2. 比较两个表达式

```
x=10
y=20
res=`expr x = $y`
echo res
```

### 3. 匹配两个字符串中的字符数

```
expr alphabet : alpha
```

### 4. 寻找模值

```
expr 20 % 30
```

### 5. 提取字符串

```
a=HelloWorld
b=`expr substr $a 6 10`
echo $b
```

## 附加标志及其功能

| 标志 | 描述 |
|---|---|
| `--version` | 输出版本信息并退出 |
| `--help` | 显示此帮助并退出 |

更多详情：Wikipedia 上的 `Expr`

999-wrap-up.md
