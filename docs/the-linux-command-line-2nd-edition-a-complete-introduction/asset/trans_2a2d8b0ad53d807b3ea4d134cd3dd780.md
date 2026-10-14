

tions:
http://tldp.org/LDP/abs/html/testbranch.html

## 32 – 位置参数

我们程序中一直缺少的一个功能是接受和处理命令行选项和参数的能力。在本章中，我们将研究 shell 的特性，这些特性允许我们的程序访问命令行内容。

### 访问命令行

shell 提供了一组称为位置参数的变量，其中包含命令行上的各个单词。变量命名为 0 到 9。它们可以这样演示：

```bash
#!/bin/bash

# posit-param: script to view command line parameters
echo "
\$0 = $0
\$1 = $1
\$2 = $2
\$3 = $3
\$4 = $4
\$5 = $5
\$6 = $6
\$7 = $7
\$8 = $8
\$9 = $9
"
```

一个非常简单的脚本，用于显示变量 $0-$9 的值。执行时不带命令行参数：

```text
[me@linuxbox ~]$ posit-param

$0 = /home/me/bin/posit-param
$1 =
$2 =
$3 =
$4 =
$5 =
$6 =
$7 =
$8 =
$9 =
```

即使不提供参数，$0 也始终包含出现在命令行上的第一项，即正在执行的程序的路径名。当提供参数时，我们看到结果：

```text
[me@linuxbox ~]$ posit-param a b c d

$0 = /home/me/bin/posit-param
$1 = a
$2 = b
$3 = c
$4 = d
$5 =
$6 =
$7 =
$8 =
$9 =
```

> 注：你实际上可以使用参数扩展访问超过九个参数。要指定大于九的数字，请用大括号括住该数字。例如 ${10}、${55}、${211} 等。

### 确定参数数量

shell 还提供了一个变量 $#，它给出命令行上的参数数量：

```bash
#!/bin/bash

# posit-param: script to view command line parameters

echo "
```

```bash
$8 = Desktop
$9 = dirlist-bin.txt
```

在这个示例系统中，通配符 * 展开为 82 个参数。我们如何处理这么多？shell 提供了一种方法，尽管有点笨拙，可以做到这一点。shift 命令每次执行时都会使所有参数“向下移动一位”。事实上，通过使用 shift，只需一个参数（加上永远不变的 $0）即可：

```bash
#!/bin/bash

# posit-param2: script to display all arguments

count=1

while [[ $# -gt 0 ]]; do
    echo "Argument $count = $1"
    count=$((count + 1))
    shift
done
```

每次执行 shift 时，$2 的值会移动到 $1，$3 的值会移动到 $2，依此类推。$# 的值也会减少一。

在 posit-param2 程序中，我们创建一个循环来评估剩余参数的数量，只要至少有一个参数就继续。我们显示当前参数，用 count 变量在每次循环迭代时递增以提供已处理参数的运行计数，最后执行 shift 以将下一个参数加载到 $1 中。以下是程序运行情况：

```text
[me@linuxbox ~]$ posit-param2 a b c d
Argument 1 = a
Argument 2 = b
Argument 3 = c
Argument 4 = d
```

### 简单应用

即使没有 shift，也可以使用位置参数编写有用的应用程序。举例来说，这里有一个简单的文件信息程序：

```bash
#!/bin/bash

# file_info: simple file information program

PROGNAME=$(basename $0)

if [[ -e $1 ]]; then
    echo -e "\nFile Type:"
    file $1
    echo -e "\nFile Status:"
    stat $1
else
    echo "$PROGNAME: usage: $PROGNAME file" >&2
    exit 1
fi
```

此程序显示指定文件的类型（由 file 命令确定）和文件状态（来自 stat 命令）。该程序的一个有趣特性是 PROGNAME 变量。它被赋予 basename $0 命令的结果值。basename 命令删除路径名的前导部分，只留下文件的基本名称。在我们的示例中，basename 删除了 $0 参数中包含的路径名的前导部分，即我们示例程序的完整路径名。此值在构建诸如程序末尾的用法消息之类的消息时很有用。通过这种方式编码，脚本可以重命名，消息会自动调整为包含程序的名称。

### 使用位置参数与 shell 函数

正如位置参数用于向 shell 脚本传递参数一样，它们也可以用于向 shell 函数传递参数。为了演示，我们将 file_info 脚本转换为 shell 函数：

```bash
file_info () {

    # file_info: function to display file information

    if [[ -e $1 ]]; then
        echo -e "\nFile Type:"
        file $1
        echo -e "\nFile Status:"
        stat $1
    else
        echo "$FUNCNAME: usage: $FUNCNAME file" >&2
        return 1
```
