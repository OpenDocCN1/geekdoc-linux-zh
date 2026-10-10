
`IFS=` 如果你想从文件中读取内容时保留所有空白字符，这非常有用（循环和 `read` 命令将在后续章节中介绍）。

```bash
while IFS= read -r
  line=$REPLY
  echo "$REPLY"
done < somefile
```

另一个示例是将 `IFS` 设置为冒号，这通常用于分隔电子表格中的列。三个连续的小于号被称为“此处处字符串”（here string），将在指南的末尾附近介绍。

```bash
IFS=: read -r column1 column2
<<<'Budget:6000'; echo 'Column1 - Column2'
Budget - 6000
```

逗号也是常见的分隔符。在这里，`IFS` 值被这样设置。

```bash
set | grep '^IFS='
IFS=$' | grep IFS
IFS=
s set | grep IFS
```

注意看你在设置 `IFS` 后，`IFS` 值是如何被永久修改的？这通常是有用的。在大多数情况下，你可能只想为单个命令（例如读取输入）更改 `IFS` 值，但在脚本的剩余部分保留其默认值；否则，你的脚本行为将变得很奇怪，因为单词拆分将不再以你预期的方式进行。

一种方法是使用当前的 `IFS` 值设置一个变量，稍后将其还原。

```bash
$ORIG_IFS=$IFS
$IFS=
# perform your commands here
$IFS=$ORIG_IFS
```

第二种方法是通过双引号包围 `IFS` 来临时设置一个新的 `IFS` 值。

```bash
$ set | grep ^IFS
IFS=$'\t'
$IFS='' read r column1 column2
<<<Budget,6000; echo 'Column1 --- Column2'
Budget -- 6000
$ set | grep ^IFS
IFS=$'\t'
```

看到 `IFS` 值只在那个单个命令中发生了变化了吗？这正是我们想要的。

注意，`IFS` 值对应于它的值，且仅对应它的值。因此，如果遇到两个分隔符，它对应于两者之间的一个空字段。

```bash
$ IFS='-' read -r column1 column2 column3
<<< 'Budget --6000'; echo 'Col1:$column1 Col2:$column2 Col3:$column3'
Col1:Budget Col2:1013 Col3:6000
```

通过以下命令可以将 `IFS` 恢复到默认值：

`IFS=$IFS`

## IFS

本节利用了本指南后续章节介绍的许多概念。建议你跳过此部分，在完成本指南后再回来。现在，只需知道 `IFS` 代表“内部字段分隔符”（Internal Field Separator）。它的作用是根据分隔符列表确定在何时以及如何进行单词拆分。默认的 `IFS` 值（分隔符）是空格 (`' '`)、水平制表符 (`'\t'`) 和换行符 (`'\n'`)。

有几种方法可以检查 `IFS` 设置。第一种使用 `printf`，第二种使用 `od`，第三种使用 `set`。

```bash
$ printf %q 'IFS'
$ '\t'
$ echo -n 'IFS' | od -abc
000000 50 ht 72
      040 011 012
        116 04

$ set | grep 'IFS'
IFS=$' '\t'
```

设置 `IFS` 值的方法是将你想要作为分隔符的特殊字符传递给 `IFS`。在这里，`IFS` 值被设置为空字符串。

`IFS=` 如果你想从文件中读取内容时保留所有空白字符，这非常有用（循环和 `read` 命令将在后续章节中介绍）。

```bash
while IFS= read -r
  line=$REPLY
  echo "$REPLY"
done < somefile
```

另一个示例是将 `IFS` 设置为冒号，这通常用于分隔电子表格中的列。三个连续的小于号被称为“此处处字符串”（here string），将在指南的末尾附近介绍。

```bash
IFS=: read -r column1 column2
<<<'Budget:6000'; echo 'Column1 - Column2'
Budget - 6000
```

逗号也是常见的分隔符。在这里，`IFS` 值被这样设置。

```bash
set | grep '^IFS='
IFS=$' | grep IFS
IFS=
s set | grep IFS
```

注意看你在设置 `IFS` 后，`IFS` 值是如何被永久修改的？这通常是有用的。在大多数情况下，你可能只想为单个命令（例如读取输入）更改 `IFS` 值，但在脚本的剩余部分保留其默认值；否则，你的脚本行为将变得很奇怪，因为单词拆分将不再以你预期的方式进行。

一种方法是使用当前的 `IFS` 值设置一个变量，稍后将其还原。

```bash
$ORIG_IFS=$IFS
$IFS=
# perform your commands here
$IFS=$ORIG_IFS
```

第二种方法是通过双引号包围 `IFS` 来临时设置一个新的 `IFS` 值。

```bash
$ set | grep ^IFS
IFS=$'\t'
$IFS='' read r column1 column2
<<<Budget,6000; echo 'Column1 --- Column2'
Budget -- 6000
$ set | grep ^IFS
IFS=$'\t'
```

看到 `IFS` 值只在那个单个命令中发生了变化了吗？这正是我们想要的。

注意，`IFS` 值对应于它的值，且仅对应它的值。因此，如果遇到两个分隔符，它对应于两者之间的一个空字段。

```bash
$ IFS='-' read -r column1 column2 column3
<<< 'Budget --6000'; echo 'Col1:$column1 Col2:$column2 Col3:$column3'
Col1:Budget Col2:1013 Col3:6000
```

通过以下命令可以将 `IFS` 恢复到默认值：

`IFS=$IFS`

目录（因为你的当前工作目录可能不在 `$PATH` 变量中，对吧？）。

`./your_script`

# 别名 (Aliases)

别名是简短的命令。仅此而已。没有任何花哨或特殊。别名仅仅是在需要反复输入长命令时节省时间的方法，让你免于记忆长命令所需的所有开关和参数。在不带任何参数的情况下运行 `alias` 会列出当前用户定义的别名。

```bash
$ alias The same command also defines new aliases.
alias upgrade='sudo apt-get update && sudo apt-get upgrade'
```

现在，当在终端输入 `upgrade` 时，Bash 将字符串 `upgrade` 替换为字符串“sudo apt-get update && sudo apt-get upgrade”。就是如此。以下是一些（可能）有用的别名。

## 标准别名

```bash
$ alias egrep='egrep --color=auto'
$ alias fgrep='fgrep --color=auto'
$ alias grep='grep --color=auto'
$ alias l='ls -CF'
$ alias la='ls -la -A'
$ alias ll='ls -la --color=auto'
$ alias ls='ls --color=auto --color-directories'
```

## 更新与升级

```bash
$ alias uu='sudo apt-get update && sudo apt-get upgrade'
```

## 安装软件包

```bash
$ alias ins='sudo apt-get install'
```

## 软件包

```bash
$ alias rem='sudo apt-get remove'
```

## 切换到父级目录

```bash
$ alias ..='cd ..'
$ alias ...='cd ../..'
$ alias ....='cd ../../'
$ alias.....='cd ../../..'
```

## 使用 rsync 备份

```bash
$ alias backup='sudo rsync -av --exclude-from=/home/aries/rsync-excludes / /mnt/ext4/backup'
```

请注意，如果你使用 `rsync`，你应该排除临时文件系统、可移动式存储设备等（`/proc`, `/run`, `/sys`, `/dev`, `/media`, `/mnt` 和 `/tmp`）。

## 使用 tar 备份

```bash
$ alias backup='sudo tar cvpft \
backup.tar.gz --exclude=/backup.tar.gz \
--exclude=/proc --exclude=/sys \
--exclude=/dev/ --exclude=/run \
--exclude=/media/ --exclude=/*'
```

## SSH

```bash
$ alias connect='ssh -X -c blowfish -C \
username@domain.net'
```

## 关机

```bash
$ alias sd='sudo shutdown -h now'
```

## 重启

```bash
$ alias rb='sudo reboot'
```

# 函数 (Functions)

函数基本上就是微型脚本。它们可以处理变量、命令、参数等更多内容。随着你 Bash 编码技能的提高，你的脚本通常会呈现出一系列岛屿（函数）的形态，每个岛屿都有供从大陆（脚本本身）起飞和降落的美优小跑道，用于交付、检索和对包（数据）执行任务。在介绍完脚本基础后，将介绍函数。

# 标准流 (Standard streams)

三个标准流，每个流都有特定且独特的用途。`Stdin` 是第一个，代表“标准输入”。默认情况下，它指的是来自键盘的输入。在运行 Bash 的终端内部，所有输入的命令都是通过键盘输入的，因此通过标准输入进入。标准输入的文件描述符（关于此主题将在稍后介绍）是 0（零）。

本指南的后续章节将介绍其他输入模式，例如从文件、进程或上一个命令的输出中读取。虽然它们不是通过键盘输入的，但通过使用特殊字符 (`|`) 或多个小于符号 (`<`, `<<`, `<<<`) 被重定向到标准输入。

`Stdout` 是第二个流，代表“标准输出”。默认情况下，它输出到运行 Bash 的终端。标准输出的文件描述符是 1（一）。

与 `stdin` 类似，`stdout` 可以通过使用特殊字符（如管道 `|` 或一个或多个大于号 `>`, `>>`））重定向到另一个进程或文件。

`Stderr` 意味着“标准错误”。每当程序产生错误（无论是由于误用、错误甚至是故意为之），任何所有的错误代码或消息都会写入标准错误。需要注意的是，除非显式告知，否则标准错误和标准输出并不总是输出到同一个位置。

# 变量 (Variables)

变量是存储值的存储位置。在 Bash 中，变量用于存储稍后使用的信息。变量有很多类型，包括字符串、整数和数组。

## 字符串 (Strings)

字符串是字符序列。在 Bash 中，字符串通常在双引号中以允许变量扩展和命令替换。如果不使用引号，Bash 可能会对字符串进行分词。

```bash
$ name="hello world"
$ echo $name
hello world
```

## 整数 (Integers)

整数是整数。在 Bash 中，整数可以用于算术运算。

```bash
$ count=10
$ echo $((count + 1))
11
```

## 数组 (Arrays)

数组是值的集合。在 Bash 中，可以使用括号定义数组。

```bash
$ fruits=("apple" "banana" "cherry")
$ echo ${fruits[0]}
apple
```

## 赋值 (Assignment)

为变量赋值使用等号 (`=`)。等号周围不能有空格。

```bash
$ variable="value"
$ echo $variable
value
```

访问变量的值在名称前使用美元符号 (`$`)。

```bash
$ name="Alice"
$ echo $name
Alice
```

## 作用域 (Scope)

变量具有作用域，定义了它们的可访问范围。主要的作用域：局部和全局。

全局变量在整个脚本中都是可用的。局部变量仅在定义它们的函数内可用。

```bash
function my_function() {
  local local_var="local"
  global_var="global"
  echo $local_var
  echo $global_var
}

my_function
echo $local_var # 这将产生错误
echo $global_var # 这将正常工作
```

## 整数 (Integers)

整数变量是 Bash 中你能够遇到字符串以外内容的少数情况之一。相反，它们几乎从不使用，因为算术扩展（后文将详细介绍）要易用且易读得多。

要一个整数变量，你必须使用 `declare -i` 显式将其设置为整数。

```bash
$ declare -i varname
```

要删除一个整数变量，你可以使用 `unset`。

```bash
$ unset varname
```

下面是一个声明并设置整数变量、回显变量以及随后将其删除的单行示例：

```bash
$ declare -i x=10; echo "$x"; unset x
10
```

记住，你必须显式声明整数变量。如果你不这样做，你将得到一个字符串！

```bash
$ x=10; $x=5; echo "$x"; unset $x
105
```

让我们再试一次，这次我们正确地声明它，然后给整数加 5（`+=5` 部分）。

```bash
$ declare -i x=10; $x=5; echo "$x"; unset x
15
```

好多了！`let` 同样有效。

```bash
$ x=10; let $x+=5; echo "$x"; unset $x
15
```

然而，反过来操作是不行的。

```bash
$ let x=10; $x+=5; echo "$x"; unset $x
105
```

除非你在 `let` 语句内部执行加法。

```bash
$ declare -i x=10+5; echo "$x"; unset $x
15
$ let $x=10+5; echo "$x"; unset $x
15
```

一旦你开始多个整数变量，情况就会变得更加繁琐。

```bash
$ declare -i x=10; declare -i y=5; \
z="$x+$y"; echo "$z"; unset $x; unset $y; \
10+5
$ declare -i x=10; declare -i y=5; \
declare -i z="$x+$y"; echo "$z"; \
unset $x; unset $y; unset $z
15
```

你是否彻底困惑了？我知道我很困惑。不要太担心；这就是为什么整数变量在 Bash 中很少被使用。我们稍后会介绍算术扩展，它编写、读取和使用起来要简单得多。

## 只读 (Read only)

只读变量与普通变量完全相同，但正如其所示，它们是只读的。你通过向 `declare` 传递 `-r` 标志来设置只读变量。

```bash
$ declare -r varname
```

在这里我们设置了理想的天气条件：

```bash
$ declare -r weather='sunny'; echo $weather
sunny
```

一旦设置，只读变量就是永久的。这意味着 `unset` 无效。只读变量会一直存在，直到 shell 进程退出或被杀死。

```bash
$ unset weather
bash: unset: weather: cannot unset: readonly variable
$ echo "$weather"
sunny
```

要用新的 Bash 实例替换当前的实例并丢弃只读变量，你可以执行以下命令：

```bash
$ exec bash
```

## Shell 变量 (Shell variables)

除了设置“普通”变量外，Bash 还提供了一些特殊变量以供你方便。并不是所有的 shell 变量都列在这里，但最常用的都在。

| 常见的 shell 变量 | 说明 |
| :--- | :--- |
| `$BASH` | Bash 二进制文件的路径。 |
| `$BASH_VERSION` | Bash 的版本。 |
| `$BASH_VERSINFO` | Bash 的主版本。 |
| `$EDITOR` | 环境的默认编辑器。 |
| `$UID` | 当前用户的有效用户 ID。 |
| `$HOME` | 当前用户的家目录路径。 |
| `$HOSTNAME` | 机器主机名。 |
