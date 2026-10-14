

```
# Requires a user name and database table name on the
# command line
#
if [ $# -ne 2 ];
then
    echo You must provide a user name and a database table name.
    exit
fi
# Begin processing:
# Store command line parameters in shell variables
DB_USER=$1
DB_TABLE=$2
```

如果查看 `/etc/rc.d/init.d` 中的脚本，你会看到使用多个环境变量的复杂测试表达式。研究这些脚本是学习 shell 脚本编写的好方法，尽管你可能不会立刻理解所看到的一切。参考 bash 手册页以了解 shell 脚本可用的更高级的测试类型。

尽管每个测试只能返回真或假，但你通常需要确定一个变量或文件名的取值，而该取值可能有若干种可能的值。你可以使用多个 if-then-else 语句来检查不同的值，如下所示。当你使用 if-then-else 语句并且 else 块中的第一个命令是另一个 if-then-else 语句时，可以使用 elif 关键字代替 else，如下所示：

```
if [ $# = 4 ] ; then
echo "Ready to process four files."
elif [ $# = 3 ] ; then
echo "Ready to process three files."
elif [ $# = 2 ] ; then
echo "Ready to process two files ."
elif [ $# = 1 ] ; then
echo "Ready to process one file."
else
echo "No filenames to process."
fi
```

case 语句是更优雅的做法。case 语句允许你为一个变量指定若干可能的值，并为每个匹配的值提供一个要执行的语句块。在 case 语句的所有语句块中，只有一个会被执行。之前的代码可以用 case 语句重写如下：

```
case $# in
4)
echo "Ready to process four files." ;;
3)
echo "Ready to process three files." ;;
2)
echo "Ready to process two files." ;;
1)
echo "Ready to process one file." ;;
```

```
echo "Invalid number of filenames provided." ;;
esac
```

在上面的示例中，如果 `$#` 变量与之前的任何 case（4、3、2 或 1）都不匹配，则执行跟在 `*)` case 之后的语句块。双分号表示每个 case 的语句块结束。esac 关键字（“case”倒写）用于表示 case 语句的结束。在执行了 case 语句中的一个语句块之一（例如 `echo "Ready to process four files."`）之后，执行的下一条语句是 esac 关键字之后的那一行。

`/etc/rc.d/init.d` 中的脚本是查看 case 语句示例的好地方。

## 为脚本添加循环

选择语句用于确定计算机程序的某部分是否应该被执行。循环语句用于确定计算机程序的某部分是否应该被执行多次。循环语句包含几个部分：

- 一个计数变量，每次循环重复时被赋予不同的值；计数变量通常称为循环的索引，因为它跟踪循环已执行语句列表的次数
- 应赋给计数变量的值列表
- 每次循环时要执行的语句列表

循环语句使一组命令重复执行一定次数或直到满足条件为止。你可以在 bash shell 脚本中定义几种类型的循环。

for 命令创建 for 循环，它对列表中的每个项目重复执行一次语句块。你可以在编写脚本时包含项目列表，也可设计循环以便在脚本执行时从命令行提供列表项。for 命令的语法如下所示。关键字 for、in、do 和 done 都是 for 循环的一部分：

```
for <counting variable> in <list of items>
do
    <statement block>
done
```

`<statement block>` 会对 `<list of items>` 中的每个项目执行一次。每次通过循环称为一次迭代。每次执行 `<statement block>` 时，`<counting variable>` 都会被赋予 `<list of items>` 中下一个项目的值——每次迭代。do 和 done 命令是用于开始和结束 for 循环中语句块的关键字（也在其他地方使用，如你将看到的）。

`<list of items>` 可以是以下内容中的任意一种（为每种情况展示 for 循环的第一行示例）：

- 数字：for COUNT in 1 2 3 4 5 6 7
- 单词：for NAME in george ali maria rupert kim
- 用于匹配文件名的正则表达式：for db_filename in *html
- 下面描述的特殊变量 $@：for db_filename in $@

当你使用正则表达式（例如 *c）作为 for 循环中的 `<list of items>` 时，shell 会用所有匹配的文件名替换该正则表达式。以 *html 为例，shell 会用当前目录中以字母 “html” 结尾的所有文件名进行替换。此替换在 shell 执行 for 循环之前发生。

for 循环中使用的一个特殊变量是 $@。该变量包含在执行脚本时命令行上包含的所有参数。如果你在命令行上包含正则表达式，例如 *txt 或 *html，shell 会找到所有匹配的文件名，并在脚本执行时将它们作为 $@ 的一部分包含在内。通过将 $@ 用作 for 循环中的 `<list of items>`，你会自动包含命令行上的所有项目。

下面的示例脚本展示了一个 for 循环，对命令行给出的每个文件名进行压缩：

```
#!/bin/bash
# Author:      dave lambert, dave@xyz.org
# Date:        12 October 2005
# Description: Compress each filename given on the command line
#
for counter in $@
do
    gzip $counter
done
```

假设上面的脚本存储在名为 squash 的文件中，并且你使用以下命令行启动脚本：
./squash phoebe.tif charon.tif europa.tif

for 循环将执行 do 和 done 之间的命令（本例中的 gzip 命令）三次，对应命令行上的每个文件名。计数变量 counter 在 do 和 done 包围的语句块的三次迭代中依次取三个文件名的值。

```
while <test>
do
    <statement block>
done
```

while 循环使用与 if-then 语句相同的测试。例如，考虑以下 while 循环：

```
DB_FILE=""
while [ ! -f $DB_FILE ] ;
do
    echo Please enter the database file to archive:
    read DB_FILE
done
```

首先，DB_FILE 变量被初始化为空字符串。这可以防止在第一次测试变量时 while 循环出现意外行为。然后循环开始测试由 DB_FILE 定义的文件名是否存在。此测试使用 -f 运算符来测试文件是否存在，并使用 ! 字符来反转测试结果。你可以把这个测试读作“当 DB_FILE 不存在时”，或“只要存储在 DB_FILE 中的文件名不存在”。只要满足此条件，do 和 done 之间的语句块就会被执行，要求用户输入文件名。

使用此循环的原因是确保用户在脚本继续并尝试使用该文件之前输入有效的文件名。循环将无限重复语句块，直到用户输入有效的文件名。

![](img/43f64015de86d989e30eff5bb284fb96_680_0.png)

你通常可以通过按 Ctrl+c 退出任何 shell 脚本。

当你使用 for 或 while 创建循环时，有时希望在语句块中间而不是其末尾退出循环。其他时候，你可能希望返回到循环顶部（执行循环的下一次迭代或再次运行 while 测试），而不执行语句块中的其余语句。break 和 continue 命令可以让你做到这一点。

例如，假设你想处理命令行提供的若干文件名。你需要在处理文件之前测试每个文件名是否有效。如果名称有效，你想处理该文件，否则，你想跳到下一个文件名。下面的 continue 命令会导致如果文件名无效，脚本执行 for 循环的下一次迭代。

```
for NEXTFILE in $@
do
if [ ! -f '$NEXTFILE' ] ; then
echo "$NEXTFILE cannot be found!"
continue
```

