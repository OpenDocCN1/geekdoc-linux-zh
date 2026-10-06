
一个简单的 `echo` 和 `read` 语句可以处理屏幕暂停，直到用户按下回车键，这样就可以查看任何消息或命令输出。我们还需要清除屏幕。使用 `tput` 命令应该可以做到（我们稍后会讨论 `tput`），但如果不行，请尝试使用 `clear` 命令。这就是我们需要的，这里是脚本：

```bash
$ pg menu

#!/bin/sh

# menu

# 设置日期、用户和主机名

MYDATE=$(date +%d/%m/%Y)

THIS_HOST=$(hostname -s)

USER=whoami

# 无限循环！

while

do

# 清除屏幕

tput clear

# 此处开始文档

cat <<MAYDAY

| User:$USER Host:$THIS_HOST Date:$MYDATE |

| 1 : 列出当前目录文件 |

| 2 : 使用 vi 编辑器 |

| 3 : 查看谁正在使用系统 |

| H : 帮助屏幕 |

| Q : 退出菜单 |

MAYDAY

# 此处文档结束

echo -en "\tYour Choice [1,2,3,H,Q]"

read CHOICE

case $CHOICE in

1) ls

;;

2) vi

;;

3) who

;;

H|h)

```
290 控制流结构

```bash
# 使用此在此文档创建帮助屏幕

cat <<MAYDAY

这是帮助屏幕，目前还没有可以帮你的！

MAYDAY

  ;

  Q(q) exit 0

  ;

*) echo -e "\t007unknown user response"

  ;

esac

echo -e -n "\t按回车键继续"

read DUMMY

```

done

## 18.10 结论

任何合理脚本的核心都是某种形式的流程控制。如果你想让脚本具有智能性，它们必须能够做出决策。

在本章中，你学习了流程控制如何让一个普通的脚本与一个健壮的脚本产生区别，你还学习了如何处理列表或循环直到条件为真或假。

## 第 19 章

## Shell 函数

书中到目前为止的所有脚本代码都是从上到下执行的。这种方法是可以的，但你可能已经注意到，我们在示例中涵盖的某些代码段在同一个脚本的后面重复出现。
Shell 允许你将一组命令或语句分组成一个可重用的块。这些块被称为 Shell 函数。

在本章中，我们将涵盖：

- 定义函数；
- 在脚本内部使用函数；
- 从函数文件中使用函数；以及
- 函数示例。

一个函数由两部分组成：

- 函数标签（label）
- 函数体（body）

标签是函数名，体是函数内部的命令。标签名称应该是唯一的；否则你将得到混乱的结果，因为脚本在查看你的调用脚本之前，会先在 shell 中寻找该函数。
以下是定义函数的格式：

```bash
function_name()
{
  command1
  ...
}
```

292 Shell 函数

或者

```bash
function_name() {
  command1
  ...
}
```

两种方法都是接受的。如果你愿意，也可以在 `function_name` 之前加上 `function`，这取决于你。

```bash
function function_name() {
  ... 
}
```

你可以将函数看作脚本中的某种脚本，但有一个主要区别。当你执行一个函数时，它留在当前 shell 中并留在内存中。另一方面，如果你在脚本内部执行或调用另一个脚本，将创建一个独立的 shell，从而清除你在之前的脚本中声明的所有变量。

函数可以存放在与脚本相同的文件中，也可以放在只包含函数的独立文件中。函数并不一定要包含许多语句或命令——它可以只包含一个 `echo` 语句，这取决于你。

## 19.1 在脚本中声明函数

这是一个简单的函数：

```bash
hello () {
  echo "Hello there today's date is `date`"
}
```

所有函数在在使用之前必须声明。这意味着你必须将所有函数放在脚本的顶部。在 shell 解释器看到它之前，你无法引用它。要调用函数，只需通过其名称调用即可。在上面的示例中，函数名是 'hello'；其函数体包含一个包含今天日期的 `echo` 语句。

## 19.2 在脚本中使用函数

现在我们创建了函数，看看它在脚本中是如何使用的。

```bash
$ pg funcl

#!/bin/sh

# func1

hello () {
echo "Hello there today's date is `date`"
}

echo "now going to the function hello"
hello
echo "back from the function"
```

## 19.8 源文件 (Souring the file)

源格式为：

- `. /pathname/filename`

现在文件已经创建，让我们将文件加载到 shell 中（源）。输入以下内容：

```bash
$ functions.main
```

如果上述命令返回“file not found”（未找到文件），请尝试以下：

```bash
$ /functions.main
```

那是一个 `<点><空格><正斜杠><文件名>`。现在文件应该已经加载到 shell 中。如果你仍然收到错误，请确保提供该文件的完整路径。

## 19.9 检查已加载的函数

要确保函数已成功加载，请使用 `set` 命令，它将显示 shell 可用的所有已加载函数。

```bash
$ set
USER=dave
findit()
{
 if [ $ -lt 1 ]; then
  echo "usage :findit file"
  return 1;
fi
find / -name $1 -print
...
```

## 19.10 执行 shell 函数

要执行函数，只需输入函数名（此处为 `findit`）并带上参数，该参数应该是位于系统某处的一个文件。

```bash
$ findit groups
usr/bin/groups
usr/local/backups/groups.bak
```

### 19.10.1 删除 shell 函数

现在让我们对函数进行一些小更改。首先删除该函数，使其不再在 shell 中可用。使用 `unset` 命令来实现。删除函数时使用 `unset` 命令的格式为：

```bash
unset function_name
unset findit
```

如果你现在输入 `set`，你会发现该函数不再显示。

### 19.10.2 编辑 shell 函数

现在编辑 `functions.main` 文件并函数中添加一个循环，以便脚本从命令行读取多个参数。现在函数看起来像这样：

```bash
$ pg functions.main
!/bin/sh
findit()
{
  # findit
  if [ $# -lt 1 ]; then
    echo "usage :findit file"
    return 1
  fi
for loop in "$@"
do
    find -name $loop -print
done
}
```

再次源该文件：

```bash
$ ./functions.main
```

使用 `set` 命令查看其确实已加载，你会注意到 shell 已正确解释了 `for` 循环以接收所有参数。

```bash
$ set
findit=()
{
  if [ $# -lt 1 ]; then
    echo "usage:`basename $0` file"
    return 1;
  fi;
for loop in "$@";
do
  find / -name $loop -print;
done
...
```

现在执行更改后的 `findit` 函数。提供几个文件进行查找：

```bash
$ findit LPSO.doc passwd
/usr/local/accounts/LPSO.doc
/etc/passwd
...
```

### 19.10.3 函数示例

现在你已经掌握了函数，让我们看看如何让它们为你工作。一旦你有了函数，它可以节省大量的编码时间，因为函数是可重用的。

## 验证输入

这是一个小型脚本，它询问名然后询问姓：

```bash
$ pg func2
!/bin/sh
# func2
echo -n "What is your first name : "
read F_NAME
echo -n "What is your surname : "
read S_NAME
```

任务是确保两个变量中输入的字符只包含字母。为了在不重复代码的情况下测试是否仅包含字符，我们可以使用 `awk`。这里是测试是否获取大写或小写字母的函数。

```bash
char_name()
{
# char_name
# 调用：char_name string
# 将参数赋值给新变量
LETTERS_ONLY=$1
# 使用 awk 测试是否仅包含字母！
LETTERS_ONLY=$(echo $1|awk '{if($0~/[^a-zA-Z]/) print "1"}')
if [ "$LETTERS_ONLY" != "" ]
then
# 哦，错误
return 1
else
# 仅包含字符
return 0
}
```

我们首先将 `$1` 变量赋值给一个更有意义的名字。使用 `awk` 来测试整个记录是否只包含字母。该命令的输出结果（非字母为 1，OK 则为空）存储在变量 `_LETTERS_ONLY` 中。

对该变量进行测试。如果它包含任何值，则说明是 OK。然后根据此测试执行返回码。使用返回码使得脚本在调用脚本的部分对函数进行测试时，代码看起来更整洁。

要测试函数的输出，我们可以使用所需的 `if` 语句格式：

```bash
if char_name $F_NAME; then
  echo "OK"
else
  echo "ERRORS"
fi
```

如果发生错误，我们可以创建另一个函数将错误打印到屏幕上：

```bash
name_error()
# name_error
# 显示错误消息
{
  echo $@ contains errors, it must contain only letters
}
```

函数 `name_error` 将用于回显所有错误，忽略任何无效输入。使用特殊变量 `$` 允许所有参数被回显。在这种情况下，它是 `F_NAME` 或 `S_NAME` 的值。以下是使用函数后完成的脚本样式：

```bash
$ pg func2
!/bin/sh
char_name()
{
# 调用：char_name string
# 检查 $1 是否仅包含字母 a-z,A-Z
{
  # 将参数赋值给新变量
  LETTERS_ONLY=$1
}
LETTERS_ONLY=$(echo $1|awk '{if($0~/[^a-zA-Z]/) print "1"}')
if [ "$LETTERS_ONLY" != "" ]
then
  # 哦，错误
  return 1
else
  # 仅包含字符
  return 0
fi
}
name_error()
# 显示错误消息
{
  echo " $@ contains errors, it must contain only letters"
}
while :
do
  echo -n "What is your first name :"
  read F_NAME
  # (其余脚本逻辑)
```

`dd` 命令主要用于转换以及查询磁带上的数据问题或普通的磁带存档任务，但它也可以用于创建固定长度的文件。以下命令创建一个名为 `myfile` 的 1 兆字节文件。

```
dd if=/dev/zero of=myfile count=52 bs=2048
```

`dd` 命令可以解释来自键盘的输入，并可以用于接收许多字符。在这种情况下，我们只需要一个字符。`dd` 命令需要切掉换行；当用户按下回车键时，会附加这个控制字符。`dd` 也只会发送一个字符。在发生这些操作之前，必须使用 `stty` 命令将终端设置为原始模式（raw mode）。我们在调用 `dd` 之前保存设置，并在 `dd` 完成后恢复它们。

这是该函数：

```
read_a_char()
# read_a_char
{
# 保存设置
SAVEDTTY=`stty -g`
# 设置终端为原始模式
stty cbreak
# 读取并输出单个字符
dd if=/dev/tty bs=1 count=1 > /dev/null
# 恢复终端并恢复 stty
stty -cbreak
stty $SAVEDTTY
}
```

要调用该函数并返回输入的字符，请使用命令替换。这是一个示例。

```
echo -n "Hit Any Key To Continue"
character=`read_a_char`
echo "In case you are wondering pressed $character"
```

## 测试目录是否存在

在移动文件时，测试目录是否存在是一个很常见的任务。此函数将测试传递给函数的参数以判断是否为目录。由于我们使用了带有成功或失败值的 `return` 命令，`if` 语句成为测试结果的最明显选择。

这是该函数：

```bash
is_it_a_directory()
{
# is_it_a_directory
# 调用方法：is_it_a_directory directory_name
```

# 304 Shell 函数

```bash
if [ $ -lt 1 ]; then
  echo "is_it_a_directory: I need an argument"
  return 1
fi
# 判断是否为目录
DIRECTORY_NAME=$1
if [ ! -d $DIRECTORY_NAME ]; then
  # 不是
  return 1
else
  # 是
  return 0
fi
```

要调用并测试结果，我们可以使用：

```bash
echo -n "enter destination directory :"
read DIRE
if is_it_a_directory $DIREC
then
  :
else
  echo "$DIREC does not exist, create it now? [y..n]"
  # 在此处编写创建目录或退出的命令
  ...
fi
```

## 提示 Y 或 N

许多脚本在继续执行进程之前会提示用户做出响应。提示可能是执行以下操作之一：

- 创建目录
- 你现在想删除此备份文件吗？
- 运行记录
- 确认保存记录

列表可能很长。以下函数是一个通用的提示函数。你提供要显示的消息以及默认答案。如果用户在提示时直接按回车键，将使用默认答案。`case` 语句用于捕获答案。

```bash
continue_prompt()
# continue_prompt
# 调用方法：continue_prompt "要显示的字符串" 默认答案
{
  STR=$1
  _DEFAULT=$2
# 检查参数是否正确
  if [ $# -lt 1 ]; then
    echo "continue-prompt: I need a string to display"
    return 1
  fi
  # 无限循环
  while; do
    echo -n "$$STR [Y..N] [$DEFAULT]:"
    read _ANS
    # 如果用户按回车，则设置默认值并确定返回值，
    # 这是一个冒号，然后是空格，然后是 s$
    : ${ANS:=$DEFAULT}
    if [ "$ANS" = "" ]; then
      case $ANS in
        Y) return 0 ;;
        N) return 1 ;;
      esac
    fi
    # 用户选择了内容
    case $ANS in
      y|Y|Yes|YES)
        return 0
        ;;
      n|N|No|NO)
        return 1
        ;;
      *) echo "Answer either Y or N, default is $DEFAULT"
        ;;
    esac
    echo $ANS
  done
}
```

要调用上面的函数，你可以用双引号提供要显示的消息，或者带参数调用 $1，或者使用包含字符串的变量。还必须传递一个 Y 或 N 形式的默认答案。以下是调用 `continue_prompt` 函数的方法。

```bash
if continue_prompt "Do you want to delete the var filesystem" "N"; then
  echo "Are you nuts!"
else
  echo "Phew !, what a good answer"
fi
```
