
B. Display Disk Space

C. Display Home Space Utilization

Q. Quit"

`read -p "Enter selection [A, B, C or Q] "`

`case $REPLY in`

  `q|Q) echo "Program terminated."`

    `exit`

    `;;`

```

```bash
a|A) echo "Hostname: $HOSTNAME"

   uptime

   ;;
b|B) df -h

   ;;
c|C) if [[ $(id -u) -eq 0 ]]; then

       echo "Home Space Utilization (All Users)"

       du -sh /home/*

   else

       echo "Home Space Utilization ($USER)"

       du -sh $HOME

   fi

   ;;
*) echo "Invalid entry" >&2

   exit 1

   ;;
esac
```

在这里，我们修改了 `case-menu` 程序，用字母代替了数字。注意，新模式允许输入大写和小写字母。

## 结语

`case` 命令是我们工具箱中一个非常实用的补充。正如我们在下一章中看到的，它是处理某些类型问题的完美工具。

# 32

## POSITIONAL PARAMETERS（位置参数）

我们的程序缺少的一个功能是接受并处理命令行选项。在本章中，我们将检查允许程序访问命令行的 shell 特性。

## 命令行

shell 提供了一组*位置参数*，包含命令行上的单个单词。变量命名为 `$0` 到 `$9`。它们可以通过这种方式演示：

```bash
#!/bin/bash

# posit-param: 查看参数的脚本

echo ""

$0 = 0

$1 = 1

$2 = 2

$3 = 3

$4 = 4

$5 = 5

$6 = 6

$7 = 7

$8 = 8

$9 = 9
```

这个简单的脚本显示变量 `$0` 到 `$9` 的值。在没有命令行参数的情况下执行时：

```bash
$ posit-param

$0 = /home/me/posit-param

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

即使没有提供参数，`$0` 也会始终包含命令行上的第一个项，即程序的路径名。当提供了参数时：

```bash
$ posit-param a b c d

$0 = /home/me/posit-param

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

可以使用参数扩展访问多九的参数。要指定大于九的数字，请将数字括起来，例如 `${10}`、` ${11}` 等。

### 确定参数数量

shell 还提供了一个变量 `#`，它产生命令行上的参数数量：

```bash
#!/bin/bash

# posit-param: 查看参数的脚本

echo "Number of arguments: #"

$0 = 0

$1 = 1

$2 = 2

$3 = 3

$4 = 4

$5 = 5

$6 = 6

$7 = 7

$8 = 8

$9 = 9
```

```bash
$ posit-param a b c d

Number of arguments: 4

$0 = /home/me/posit-param

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

### shift——获取大量参数

但当我们给程序大量的参数时会发生什么：

```bash
$ posit-param *

Number of arguments: 82

$0 = /home/me/posit-param

$1 = addresses.list

$2 = bin

$3 = bookmarks.html

$4 = debian-500-i386-netinst.iso

$5 = debian-500-i386-netinst.jigdo

$6 = debian-500-i386-netinst.template

$7 = debian-cd_info.tar.gz

$8 = Desktop

$9 = dirlist.txt
```

在这个示例中，通配符 `*` 展开为 82 个参数。我们如何处理那么多参数？shell 提供了一个笨拙的方法。`shift` 命令每次执行都会导致每个参数“向下移动”。实际上，通过使用 `shift`，可以每次获取一个参数（除了从不改变的 `$0` 之外）。

```bash
#!/bin/bash

# posit-param2: 显示所有参数的脚本

while [[ $# -gt 0 ]]; do

  echo "Argument $count = $1"

  count=$((count + 1))

  shift
```

每次执行 `shift`，`$2` 的值就会移动到 `$1`，`$3` 的值就会移动到 `$2`，以此此类推。`#` 的值也会减 1。

在 `posit-param` 程序中，我们创建一个循环，评估剩余参数的数量，只要至少有一个参数就继续。我们显示当前参数，在循环的每次迭代中增加计数以提供已处理参数数量的运行计数，最后执行 `shift` 将下一个参数加载到 `$1` 中。

```bash
$ posit-param2 a b c d

Argument 1 = a

Argument 2 = b

Argument 3 = c

Argument 4 = d
```

### 简单应用程序

即使没有 `shift`，也可以使用位置参数编写实用的应用程序。例如，这里有一个简单的文件信息程序：

```bash
#!/bin/bash

# file-info: 简单的文件信息程序

PRONAME=$(basename $0)

if [[ -e $1 ]]; then

  echo -e "\nFile Type:"

  file $1

  echo -e "\nFile Status:"

  stat $1

else

  echo "$PRONAME: usage: $PRONAME file" >&2

  exit 1

fi
```

该程序显示指定文件的类型（由 `file` 命令确定）和文件状态（来自 `stat` 命令）。该程序的一个有趣特性是 `PRONAME` 变量。它被赋予了 `basename $0` 命令产生的值。`basename` 命令删除了

路径的头部部分，只保留文件的基名。在我们的示例中，basename 删除了包含 `$0` 参数中包含的路径头部部分，即我们示例程序的完整路径。该值在构建此类消息（例如程序末尾的消息）时非常有用。如果以这种方式编码，脚本就可以被重命名，而消息会自动调整以包含程序的名称。

### 在 Shell 函数中使用位置参数

正如位置参数用于向 Shell 脚本传递参数一样，它们也可以用于向 Shell 函数传递参数。为了演示这一点点，我们将 `file_info` 脚本转换为一个 Shell 函数：

```
file_info () {

    # file_info: 用于显示文件信息的函数

    if [[ -e $1 ]]; then

        echo -e "\nType:"

        file $1

        echo -e "\nStatus:"

        stat $1

    else

        echo "$FUNNAME: $FILENAME file" >&2

        return 1

    fi

}
```
