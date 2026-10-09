
# 第 9 章 TC SHELL

## 表 9-6 `who` 格式序列

| 序列 | 显示内容 |
| :--- | :--- |
| `%n` | 用户名 |
| `%a` | 用户执行的操作 |
| `%l` | 执行操作的终端 |
| `%M` | 执行操作所在主机的完整主机名（若无则显示 `local`） |
| `%m` | 不带域名的主机名 |

当 `who` 未设置时，用于 `watch` 消息的默认字符串为 `"%n has %a %l from %m"`，它会生成以下行：

```
jenny has logged on tty2 from local
```

就像在 `bash` 中一样，该变量包含当前 shell 的 PID 号；请将其作为 `$$$` 使用。

## 作为开关的 SHELL 变量

以下 shell 变量充当开关；它们的值并不重要。如果变量已声明，shell 就会执行指定的动作。如果未执行该操作或操作被否定，你可以在 `~/.tshrc` 启动文件、shell 脚本或从命令行中设置这些变量。

- `autocorrect` 导致 shell 在每次尝试补全之前自动尝试进行拼写检查。

- `dunique` 正常情况下会将新的工作目录推入目录栈，这意味着该栈上可能会出现许多重复条目。设置 `dunique` 可导致 shell 查找并删除任何与其即将推入的内容重复的条目。

- `echo` 导致 shell 在执行每个命令之前显示该命令。通过调用带 `-x` 选项的 `tsh` 或使用 `set` 来设置 `echo`。

- `file` 在运行 `tsh` 时（且 `csh` 链接到 `tsh` 时）启用文件名（见第 350 页）。

- `histlist` 按照用户输入的原始格式精确显示历史列表中的命令，而不经过 shell 的解释（第 346 页）。

- `ignoreof` 防止你使用 `CONTROL-D` 退出 shell，这样你就不会无意中注销了。当此变量被禁用时，你必须使用 `exit` 或 `logout` 来退出 shell。

- `listjobs` 导致 shell 在作业挂起时列出所有作业。

- `listlinks` 导致内置命令 `ls -F` 显示每个符号链接指向的类型，而不是用 `@` 符号标记符号链接。

- `login` 如果当前 shell 是作为登录 shell 运行，则由 shell 设置。

- `nobeep` 禁用 shell 发出的所有哔哔声。

- `noclobber` 防止你在重定向输出时无意覆盖文件，并防止在尝试向不存在的文件追加输出时创建文件（见表 9-7）。要覆盖 `noclobber`，请在你用于重定向或追加输出的符号后加一个感叹号（例如 `>!` 和 `>>!`）。欲了解信息请参阅第 119 页。

## 表 9-7 `noclobber` 的工作原理

| 命令 | `noclobber` 未声明 | `noclobber` 已声明 |
| :--- | :--- | :--- |
| `> fileout` | 将进程的标准输出重定向到 `fileout`。如果 `fileout` 存在，则覆盖它。 | 将进程的标准输出重定向到 `fileout`。shell 显示错误信息“`fileout` 已存在”且不覆盖该文件。 |
| `>> fileout` | 将进程的标准输出重定向到 `fileout`。如果 `fileout` 存在，则将新输出追加到 `fileout` 的末尾。如果不存在，则创建 `fileout`。 | 将进程的标准输出重定向到 `fileout`。如果 `fileout` 存在，则将新输出追加到 `fileout` 的末尾。shell 显示错误信息“`fileout` 不存在”且不创建该文件。 |

- `noglob` 防止 shell 扩展歧义的文件名。所有情况下都允许你在命令行或脚本中使用 `*`、`~` 和 `[]` 而无需加引号。

- `nonmatch` 导致 shell 将一个不匹配任何文件名的歧义文件引用传递给正在调用的命令。shell 不会扩展该文件引用。当你不设置 `nonmatch` 时，`tcsh` 不生成错误信息也不执行命令。

```
tcsh $ cat questions?
cat: No match
tcsh $ set nonmatch
tcsh $ cat questions?
cat: questions?: No such file
```

- `notify` 导致 shell 在作业完成时向屏幕发送消息。

- `pushd` 导致 shell 切换到目录并将当前目录推入目录栈。

- `popd` 导致 shell 从目录栈中弹出目录并切换。

- `cd` 导致 shell 切换目录。

- `pwd` 导致 shell 显示当前工作目录。

- `ls` 导致 shell 列出目录内容。

- `clear` 导致 shell 清空屏幕内容。

- `history` 导致 shell 记录命令历史。

- `exit` 导致 shell 退出。

## `goto`

`goto` 语句具有如下语法：

```
goto label
```

`goto` 内置命令会将控制权转移到以 `label:` 开头的语句。下面的脚本片段演示了 `goto` 的用法：

```
tcsh $ cat goto_1
#!/bin/tcsh
#
# 检查是否有 2 个参数
#
if ($argv == 2) goto goodargs
echo "Usage: goto_1 arg1 arg2"
exit 1
goodargs:
  ..
```

当调用 `goto_1` 脚本时提供的参数多于或少于两个，它会显示用法信息（第 440 页）。

## 中断处理

当中断 shell 脚本时，`onintr` 语句会转移控制权。`onintr` 语句的格式为：

```
onintr label
```

在执行 shell 脚本期间按下中断键时，shell 将控制权转移到以 `label:` 开头的语句。该语句允许你在脚本被中断时优雅地终止。你可以使用它来确保在中断 shell 脚本时，脚本在返回控制权给父 shell 之前删除临时文件。

下面的脚本演示了 `onintr`。它会持续循环直到按下中断键，此时它会显示一条消息并将控制权返回给 shell：

```
tcsh $ cat onintr_1
#!/bin/tcsh
# onintr 演示
onintr close
while ( 1 )
  echo "Program is running."
  sleep 2
end
close:
echo "End of program."
```

如果脚本创建了临时文件，你可以使用 `onintr` 来删除它们。

```
close:
  rm -f /tmp/$$*
```

模糊的文件引用 `/tmp/$$` 匹配 `/tmp/` 下所有以当前 shell 的 PID 号开头的文件。请参阅第 478 页关于这种临时文件命名技术的描述。

## `if...then...else`

`if...then...else` 控制结构有三种形式。第一种是简单 `if` 结构的扩展，当表达式为真时，它执行更复杂的命令或系列命令。这种形式仍然是单向分支。

```
if (expression) then
  commands
endif
```

第二种形式是双向分支。如果表达式为真，则执行第一组命令。如果为假，则执行 `else` 之后的命令集。

```
if (expression) then
  commands
else
  commands
endif
```

第三种形式与 `if...then...elif` 结构（第 442 页）类似。它执行测试直到找到一个为真的表达式，然后执行对应的命令。

```
if (expression) then
  commands
else if (expression) then
  commands
  ...
else
  commands
endif
```

下面的程序根据第一个命令行参数的值为变量 `class` 赋值 0、1、2 或 3。程序在开头声明了变量 `class` 以保持清晰起见；你不需要在第一次使用之前声明它。同样为了清晰起见，脚本将第一个命令行参数的值赋值给 `number`。

```
tcsh $ cat if_else_1
#!/bin/tcsh
# 对第一个命令行
# 参数进行分类的程序

set class =

set number = $argv[1]

#

if ($number < 0) then
  @ class = 0
else if (0 <= $number && $number < 100) then
  @ class = 1
else if (100 <= $number && $number < 200) then
  @ class = 2
else
  @ class = 3
endif

#

echo "The number is in class ${class}"
```

第一个 `if` 语句测试 `number` 是否小于 0。如果是，脚本将 0 赋值给 `class` 并将控制权转移到 `endif` 之后的语句。如果不是，第二个 `if` 测试 `number` 是否在 0 到 100 之间。`&&` 是布尔逻辑与（AND）运算符。如果表达式为真，则执行对应的命令。如果为假，则执行 `else` 之后的命令集。

## `break` 和 `continue`

你可以使用 `break` 或 `continue` 语句中断 `foreach` 或 `while` 结构。这些语句在转移控制权之前会执行行内的剩余命令。`break` 语句将控制权转移到 `end` 语句之后的语句，终止循环执行。`continue` 语句将控制权转移到 `end` 语句，继续执行循环。

## `switch`

`switch` 结构类似于 `bash` 的 `case` 结构（第 459 页）：

```
switch (test-string)
case pattern:
  commands
  breaksw
case pattern:
  commands
  breaksw
...
default:
  commands
  breaksw
endsw
```
