
# Shell 循环与函数

## for 循环

- 数字：`for COUNT in 1 2 3 4 5 6 7`
- 单词：`for NAME in george ali maria rupert kim`
- 用于匹配文件名的正则表达式：`for db_filename in *html`
- 下面描述的特殊变量 `$@`：`for db_filename in $@`

当你使用正则表达式（例如 `*c`）作为 `for` 循环中的 `<list of items>` 时，shell 会用所有匹配的文件名替换该正则表达式。以 `*html` 为例，shell 会用当前目录中以字母 “html” 结尾的所有文件名进行替换。此替换在 shell 执行 `for` 循环之前发生。

`for` 循环中使用的一个特殊变量是 `$@`。该变量包含在执行脚本时命令行上包含的所有参数。如果你在命令行上包含正则表达式，例如 `*txt` 或 `*html`，shell 会找到所有匹配的文件名，并在脚本执行时将它们作为 `$@` 的一部分包含在内。通过将 `$@` 用作 `for` 循环中的 `<list of items>`，你会自动包含命令行上的所有项目。

下面的示例脚本展示了一个 `for` 循环，对命令行给出的每个文件名进行压缩：

```
#!/bin/bash
## Author:      dave lambert, dave@xyz.org
## Date:        12 October 2005
## Description: Compress each filename given on the command line
#
for counter in $@
do
    gzip $counter
done
```

假设上面的脚本存储在名为 `squash` 的文件中，并且你使用以下命令行启动脚本：

`./squash phoebe.tif charon.tif europa.tif`

`for` 循环将执行 `do` 和 `done` 之间的命令（本例中的 `gzip` 命令）三次，对应命令行上的每个文件名。计数变量 `counter` 在 `do` 和 `done` 包围的语句块的三次迭代中依次取三个文件名的值。

## while 循环

```
while <test>
do
    <statement block>
done
```

`while` 循环使用与 `if-then` 语句相同的测试。例如，考虑以下 `while` 循环：

```
DB_FILE=""
while [ ! -f $DB_FILE ] ;
do
    echo Please enter the database file to archive:
    read DB_FILE
done
```

首先，`DB_FILE` 变量被初始化为空字符串。这可以防止在第一次测试变量时 `while` 循环出现意外行为。然后循环开始测试由 `DB_FILE` 定义的文件名是否存在。此测试使用 `-f` 运算符来测试文件是否存在，并使用 `!` 字符来反转测试结果。你可以把这个测试读作“当 `DB_FILE` 不存在时”，或“只要存储在 `DB_FILE` 中的文件名不存在”。只要满足此条件，`do` 和 `done` 之间的语句块就会被执行，要求用户输入文件名。

使用此循环的原因是确保用户在脚本继续并尝试使用该文件之前输入有效的文件名。循环将无限重复语句块，直到用户输入有效的文件名。

![](img/43f64015de86d989e30eff5bb284fb96_680_0.png)

你通常可以通过按 `Ctrl+c` 退出任何 shell 脚本。

当你使用 `for` 或 `while` 创建循环时，有时希望在语句块中间而不是其末尾退出循环。其他时候，你可能希望返回到循环顶部（执行循环的下一次迭代或再次运行 `while` 测试），而不执行语句块中的其余语句。`break` 和 `continue` 命令可以让你做到这一点。

例如，假设你想处理命令行提供的若干文件名。你需要在处理文件之前测试每个文件名是否有效。如果名称有效，你想处理该文件，否则，你想跳到下一个文件名。下面的 `continue` 命令会导致如果文件名无效，脚本执行 `for` 循环的下一次迭代。

```
for NEXTFILE in $@
do
if [ ! -f '$NEXTFILE' ] ; then
echo "$NEXTFILE cannot be found!"
continue
```

```
fi
## Everything looks OK for the current file name.
## Begin processing it
done
```

![](img/43f64015de86d989e30eff5bb284fb96_681_0.png)

本节中的脚本是嵌套控制结构的示例，例如包含 `if-then` 语句的 `for` 循环，或包含 `case` 语句的 `while` 循环。

类似地，你可以使用 `break` 命令完全退出循环。此处的示例使用了一个没有任何测试的 `while` 循环。这创建了一个无限循环——不存在的测试永远不会失败，因此循环会一直继续，直到用户按下 `Ctrl+c` 或执行 `break` 命令为止。请注意，在下面的脚本片段中，用户无需按下 `Ctrl+c` 即可退出脚本。脚本不会基于 `while` 语句中测试的值而退出，但如果用户输入 `q` 或 `Q`，则会因 `case` 语句中的 `break` 命令而退出。

```
while :
do
echo "Enter a file to see how many lines it contains (q to quit):"
read NEXTFILE
case $NEXTFILE in
[qQ]) break ;;
*) wc -l $NEXTFILE ;;
esac
done
```

## 脚本中使用函数

如果你编写了许多 shell 脚本（作为系统管理员，这很可能就是这种情况），你会发现需要反复执行相同的任务。通过创建函数，你可以创建一个小型 shell 脚本，给它命名，然后从其他位置引用该脚本。例如，假设你经常编写操作一组数据库文件的脚本。在这些脚本中，你希望设置用于引用数据库文件的某些变量。你可以创建一个设置这些变量的函数，然后将该函数包含在每个脚本中。该函数可能如下所示：

```
init_db_files() {
DB_FILE="/data/newport/users.db"
ADMIN="nwells"
SQL_MODE="standard"
}
```

要定义一个函数，你可以像变量一样选择任意名称，但在名称后加上 `()`（圆括号）以表示这是一个函数。用大括号 `{ }` 括起来的所有语句都被视为函数的一部分。如果你已在脚本开头包含上述函数，你就可以在脚本后面的位置通过名称引用它。此时，构成该函数的全部命令都会被执行。使用函数有以下几个优点：

- 你可以将函数从一个脚本复制到另一个脚本，并确切知道它会做什么，并且它已经编写正确（没有错误），因为你之前使用过它。
- 你可以在单个脚本中多次调用同一个函数，因此无需一遍又一遍地重写和重新测试相同的命令。
- 你可以将脚本的操作分成组，使脚本更易读，如下一个示例所示。

以之前的函数为例，脚本的第一部分可能如下所示：

```
#!/bin/bash
## Author:        dave lambert, dave@xyz.org
## Date:          12 October 2005
## Description:   Database analysis, main script
#
init_db_files() {
DB_FILE="/data/newport/users.db"
ADMIN="nwells"
SQL_MODE="standard"
}
## Main part of script
## First, initialize the database variables
init_db_files
## Now, let’s begin reading data from the database file and
## making calculations
```

## SHELL 脚本调试

当你使用本章中的示例脚本时，很容易定位出现的任何问题——脚本很短，设计也很简单。当你创建或检查更长的脚本时，你会发现很难快速发现语法错误或逻辑问题。语法错误是指语句输入方式的错误——shell 无法理解你的意思，因为你拼错了关键字、漏掉了分号或做了类似的事情。逻辑错误指的是命令试图完成的工作。例如，你的脚本有一个删除临时文件的命令，该文件由变量名引用，但你从未设置该变量的值，因此删除命令无法正确运行。

为了查找和修复这两种类型的错误，你可以使用 shell 的调试功能。请回忆，当你输入脚本名称时，会启动 shell 的另一个副本并运行该脚本。你也可以自己启动 shell 的另一个副本，包含调试选项并提供要调试的脚本名称。例如，假设你创建了一个名为 `startnet` 的长脚本。你可以使用以下命令启动该脚本：

```
$ bash ./startnet
```

在执行任何你编写的大型脚本之前，你应该检查脚本是否不包含语法错误。这些错误 shell 本身很容易识别。通过检查语法错误，你可以在脚本执行前修复它们。为此，在启动脚本时使用 `-n` 选项：

```
$ bash -n ./startnet
```
