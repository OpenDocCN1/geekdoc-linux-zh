

# xargs

将一个命令的标准输出转换为另一个命令的参数

xargs [options] [command]

xargs 实用程序是一种方便且高效的方法，可以将一个命令的标准输出转换为另一个命令的参数。该工具从标准输入读取内容，并跟踪允许的最大命令行长度，并在必要时通过重复执行命令来避免超过该限制。

参数 你提供给 xargs 的命令行被作为 `command` 参数。如果 `command` 的任何参数应该在来自标准输入的参数之前出现，则它们必须包含在 `command` 中。默认情况下，xargs 假设输入将附加到 `command` 之后形成一个完整的命令行。如果你省略了 `command`，它默认为 `echo`。

# 参数

- --interactive -p 在执行命令前提示用户。
- --max-args=maxargs
- -n maxargs 针对输入行中的每 `maxargs` 个参数执行一次命令。
- --max-lines=[maxlines]
- -1 [maxlines] 为每 `maxlines` 行输入执行一次命令。如果省略 `maxlines`，默认值为 1。
- --max-procs=maxprocs 允许 xargs 同时运行最多 `maxprocs` 个命令实例。（默认是顺序执行。）如果你在多处理器系统上运行 GNU/Linux，这可能会提高吞吐量。
- --no-run-if-empty -r 通常情况下，即使输入为空，xargs 也会执行一次命令。此选项告诉 xargs 如果输入为空则不执行命令。
- --replace=[marker]
- -i [marker] 允许你将标准输入中的参数放置在命令中的任何位置。命令中 `marker` 的所有出现处都会被 xargs 从标准输入生成的参数替换。如果你省略 `marker`，默认使用字符串 `{}`，这与第一个命令的 `-exec` 选项使用的语法匹配。使用此选项时，每行输入都会执行一次命令。使用 `--replace` 时会忽略 `--max-lines` 选项。

# 17 xargs

# 讨论

xargs 实用程序从标准输入读取命令的参数，将每个由空白分隔的字符串解释为独立的参数。xargs 实用程序根据 `command` 和一系列参数构建命令行。当添加另一个参数将导致超过最大命令行长度时，xargs 会运行它已构建的命令行。如果有更多输入，xargs 将重复构建命令行并运行它的过程。此过程一直持续到所有输入都被读取完毕。

# 注意事项

xargs 最常用的用法是 `find` 的 `-exec` 选项的高效替代方案（参见第 1167 页的“exec command \;”）。如果你使用 `-exec` 选项调用 `find` 来运行命令，它会为处理的每个文件单独运行一次。这通常是低效的，因为每次执行命令都需要一个新进程。通过尽可能累积多个参数，xargs 可以大幅减少所需的进程数量。第一个示例显示了如何将 xargs 与 find 使用：

- 使用 xargs 比使用命令替换——`$(command)` 或 ‘command’——更安全。当你使用命令替换为另一个命令构建参数列表时，可能会超过 GNU/Linux 施的命令长度限制。当你超过此限制时，GNU/Linux 会发出错误消息且不运行命令。xargs 通过拆分参数列表并根据需要重复执行命令来避免这种限制，你可以确保 GNU/Linux 始终运行命令。
- --replace 选项更改了 xargs 处理标准输入中空白的方式。如果没有此选项，xargs 将连续的空格、制表符和换行符视为等同。使用此选项，xargs 会特殊处理换行符。在使用 --replace 选项时，如果在标准输入中遇到换行符，xargs 将使用到为止参数列表运行命令。

# 示例

如果你想从目录及其子目录查找并删除所有以 .o 结尾的文件，可以使用 `find` 的 `-exec` 选项：

```
$ find -name \*.o -exec rm --force { \;}
```

这种方法为 find 找到的每个 .o 文件调用一次 `rm` 实用程序。每次调用 `rm` 都需要一个新进程。有很多 .o 文件，将花费大量时间在创建、启动和清理这些进程上。你可以允许 xargs 在调用 `rm` 之前尽可能累积文件名来减少进程数量：

```
$ find -name \*.o -print | xargs rm --force
```

在下一个示例中，将在所有 *.txt 文件中搜索包含单词 `login` 的行。grep 将显示所有包含 `login` 的文件名：

```
$ find -name \*.txt -print | xargs grep -w -1 login
```

下一个示例显示了如何使用 --replace 选项让 xargs 将标准输入嵌入命令中，而不是附加到命令之后。此选项也会在标准输入中遇到每个换行符时执行一次命令；--max-lines 选项无法覆盖此行为：

```
$ cat names
Tom,
Dick,
and Harry
$ xargs echo "Hello, " <names
Hello, Tom, Dick, and Harry
$ xargs --replace echo "Hello {}. Join for lunch?" <names
Hello Tom., Join me for lunch?
Hello Dick., Join me for lunch?
Hello and Harry.
```

最后一个示例使用了与上一个相同的输入文件，并使用了 --max-args 和 --max-lines 选项：

```
$ xargs echo "Hi there" <names
Hi there Tom, Dick, and Harry
$ xargs --max-args=1 echo "Hi there" <names
Hi there Tom,
Hi there Dick,
Hi there and
Hi there Harry
$ xargs --max-lines=2 echo "Hi there" <names
Hi there Tom, Dick,
```
