
你也可以通过在脚本开头放置以下 `set x` 命令来设置运行脚本的 shell 的 `-x` 选项：

set -x

在脚本中任何位置放置 `set -x` 即可开启调试模式。使用加号来关闭调试：

set +x

`set -o xtrace` 和 `+o xtrace` 命令的作用分别与 `set -x` 和 `set +x` 相同。

## for...in

for...in 结构结构具有以下语法：

+   for loop-index in argument-list
  do
    commands
  done

![](img/45ff4cd21497435daa35084a84b95d07_1017_0.png)

图 27-4 一个 for...in 流程图

for...in 结构（图 27-4，上页）将 argument-list 中第一个参数的值赋值给 loop-index，并执行 `do` 和 `done` 语句之间的命令。`do` 和 `done` 语句标记了循环的开始和结束。

在将控制权传递给 `done` 语句后，该结构将 argument-list 中第二个参数的值赋值给 loop-index 并重复执行命令。它会 argument-list 中的每个参数重复执行一次 `do` 和 `done` 语句之间的命令。当该结构耗尽 argument-list 时，它会将控制权传递给 `done` 之后的语句。

下面的 for...in 结构将 apples 赋值给用户创建的变量 fruit，并显示 `fruit` 的值（即 apples）。接下来，该结构将 oranges 赋值给 `fruit` 并重复该过程。当耗尽列表时，该结构将控制权转移到 `done` 之后的语句，该语句会显示消息。

+   $ cat fruit
for fruit in apples pears bananas

```
do
echo "$fruit"
done
echo "Task complete."
```

+   $ ./fruit
apples
oranges
pears
bananas
Task complete.

下一个脚本通过遍历工作目录中的文件并使用 `test` 判断哪些是目录文件，从而列出工作目录中的目录文件名：

+   $ cat dirfiles

```
for i in *
do
if [ -d "$i" ];
then
echo "$i"
done
```

歧义的文件引用字符 `*` 匹配工作目录中的所有文件名（隐藏文件除外）。在执行 for 循环之前，shell 会展开 `*` 并使用生成的列表为索引变量 `i` 赋值分配连续的值。

for 控制结构具有以下语法：

```
for loop-index
do
commands
done
```

## 控制结构 969

在 for 结构中，loop-index 会逐个获取命令行参数的值。for 结构与 for...in 结构（图 27-4，第 967 页）相同，区别在于它获取 loop-index 取值的方式。for 结构执行一系列命令，通常按轮流涉及每个参数。

下面的 shell 脚本显示了输出每个命令行参数的 for 结构。脚本的第一行 `for arg` 意味着 `for arg in "$@"`，shell 将 `"$@"` 扩展为带引号的命令行参数列表 `"$1"` `"$2"` `"$3"` 等。脚本的其余部分与 for...in 结构对应。

```
$ cat for_test
for arg
do
  echo "$arg"
done
$ for_test candy gum chocolate
  candy
  gum
  chocolate
```

## 可选 whos 脚本

下面的名为 `whos` 的脚本演示了 for 结构中隐含的 `"$@"` 的用。你向 `whos` 提供一个或多个用户的全名或用户名作为参数，whos 会显示关于用户的信息。whos 脚本从 `/etc/passwd` 文件的第一字段和第五字段获取信息。第一字段包含用户名，第五字段通常包含用户的全名。你可以提供用户名作为 `whos` 的参数来识别用户名，或提供姓名作为参数来识别用户名。whos 脚本类似于 `finger` 工具，尽管 whos 提供的信息较少。

```
$ whos
!/bin/bash

if [ $# -eq 0 ];
then
  echo "Usage: whos id..." 1>&2
  exit 1
fi
for id
do
  awk -F: '{print $1, $5}' /etc/passwd |
  grep -i "$id"
done
```

在下一个示例中，whos 识别出用户名是 chas，用户名为 Marilou Smith：

```
$ ./whos chas "Marilou Smith"
chas Charles Casey
smith Marilou Smith
```

使用 "$@" 脚本使用 `for` 语句循环遍历命令行参数。在此脚本中，for 循环中隐含的 `"$@"` 用法特别有益，因为它导致循环将包含空格（SPACE）的参数视为单个参数。这会将 Marilou Smith 包裹在引号中，导致 shell 将其作为单个参数传递给脚本。`for` 语句中隐含的 `"$@"` 导致 shell 重新生成带引号的参数 Marilou Smith，以便其被视为单个参数。

awk 对于每个命令行参数，它都会搜索 `/etc/passwd` 文件。在 for 循环内部，awk 工具从 `/etc/passwd` 的每行提取第一个 ($1) 和第五个 ($5) 字段。`-F` 选项导致 awk 在读取 `/etc/passwd` 时使用冒号 (:) 作为字段分隔符，允许它将每行拆分为字段。awk 命令设置了后续

## while

while 控制结构具有以下语法：

+   while test-command
  do
    commands
  done

只要 `test-command` 返回真（true），该结构就会执行 `do` 和 `done` 语句之间的命令。当 `test-command` 的退出状态为假（false）时，该结构将控制权传递给 `done` 之后的语句。

## 控制结构 971

![](img/45ff4cd21497435daa35084a84b95d07_1021_0.png)

执行 `do` 和 `done` 语句之间的命令。有关内置命令 `test` 的信息请参见第 955 页。

```
$ cat count
!/bin/bash
number=0
while [ "$number" -lt 10 ]
  do
    echo -n "$number"
    ((number +=1))
  done
$ ./count
0123456789
$
```
