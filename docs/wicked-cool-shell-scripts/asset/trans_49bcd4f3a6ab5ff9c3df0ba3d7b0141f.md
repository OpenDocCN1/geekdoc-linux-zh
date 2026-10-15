

因为此脚本会在用户的主目录中秘密创建一个目录①，所以它需要确保那里面的文件不会因为 umask 值设置不当而突然被他人读取。（umask 值定义了新创建文件或目录的默认权限。）为了避免这种过度共享，脚本在②处使用 chmod 来确保该目录对用户具有读/写/执行权限，而对其他人则完全关闭。最后在③处，脚本使用 basename 去除文件路径中的目录信息，并为每个被删除的文件添加日期和时间戳，格式为 second.minute.hour.day.month.filename：

```
newname="$archivedir/$(date "+%S.%M.%H.%d.%m").$(basename "$arg")"
```

注意在同一个替换中使用了多个 $( ) 元素。虽然可能有点复杂，但它非常有帮助。请记住，$( 和 ) 之间的任何内容都会被送入子 shell，而整个表达式随后会被该命令的结果替换。那么为什么还要费心使用时间戳呢？为了支持存储具有相同名称的多个被删除文件。一旦文件被归档，脚本就不会区分 /home/oops.txt 和 /home/subdir/oops.txt，除了它们被删除的时间之外。如果在同一时间（或同一秒内）删除了多个同名文件，先归档的文件将被覆盖。解决此问题的办法之一是在归档文件名中添加原始文件的绝对路径。

## 运行脚本

要安装此脚本，请添加一个别名，这样当你输入 rm 时，实际运行的是此脚本，而不是 /bin/rm 命令。bash 或 ksh 别名看起来像这样：

```
alias rm=yourpath/newrm
```

## 结果

运行此脚本的结果按设计是隐藏的（如清单 2-6 所示），因此让我们在过程中留意 .deleted-files 目录。

```
$ ls ~/.deleted-files
ls: /Users/taylor/.deleted-files/: No such file or directory
$ newrm file-to-keep-forever
$ ls ~/.deleted-files/
51.36.16.25.03.file-to-keep-forever
```

清单 2-6：测试 newrm shell 脚本

完全正确。虽然文件已从本地目录中删除，但它的副本已被秘密地藏在 .deleted-files 目录中。时间戳允许具有相同名称的其他被删除文件存储在同一目录中而不互相覆盖。

## Hacking the Script

一个有用的调整是更改时间戳，使其按逆时间顺序排列，以便 ls 的文件列表按时间顺序显示。以下是修改脚本的行：

```
newname="$archivedir/$(date '+%S.%M.%H.%d.%m')_$(basename "$arg")"
```

你可以反转该格式化请求中标记的顺序，使原始文件名排在备份文件名中靠前，日期排在第二位。然而，由于我们的时间粒度是秒，你可能会在同一秒内删除多个同名版本的副本（例如，rm test testdir/test），导致出现两个同名文件。因此，另一个有用的修改是将文件的位置纳入归档副本中。这将产生例如 timestamp.test 和 timestamp.testdir.test，显然是两个不同的文件。

## #16 Working with the Removed File Archive

现在用户主目录中隐藏了一个已删除文件的目录，一个让用户在不同版本的已删除文件之间选择的脚本将很有用。然而，要处理所有可能的情况是一项相当大的任务，从根本找不到指定文件到找到多个匹配给定条件的已删除文件不等。例如，在有多于一个匹配项的情况下，脚本是否应自动选择最新的文件进行恢复？抛出错误指示匹配项的数量？还是列出不同版本让用户选择？让我们看看清单 2-7 中详细说明的 unrm shell 脚本能做什么。

## 代码

```
#!/bin/bash

# unrm~Searches the deleted files archive for the specified file or
# directory. If there is more than one matching result, it shows a list
# of results ordered by timestamp and lets the user specify which one
# to restore.

archivedir="$HOME/.deleted-files"
realrm="$(which rm)"
move="$(which mv)"

dest=$(pwd)

if [ ! -d $archivedir ] ; then
echo "$0: No deleted files directory: nothing to unrm" >&2
exit 1
fi
```
