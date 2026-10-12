
除了使用 `case` 结构根据命令行参数数量进行分支外，`safedit` 脚本还引入了其他几个特性。首先，在脚本开头，将 `PATH` 变量设置为搜索 `/bin` 和 `/usr/bin`。以这种方式设置 `PATH` 可确保脚本执行的命令是标准实用程序，这些实用程序保存在这些目录中。通过在脚本内部设置 `PATH`，你可以避免以下问题：用户将 `PATH` 设置为优先搜索他们自己的目录，并且拥有与脚本调用的实用程序同名的脚本或程序。你也可以在脚本中包含绝对路径名以实现此目的，但这种做法可能会降低脚本的可移植性。

## 程序名称

在第二个 `safedit` 特性中，以下行创建一个名为 `script` 的变量，并将脚本的简单文件名赋值给它：

```bash
script=$(basename $0)
```

`basename` 实用程序将其参数的简单文件名片段发送到标准输出，该输出通过命令替换被赋值给 `script` 变量。`$0` 保存调用脚本时使用的命令（第 931 页）。无论用户使用以下哪个命令调用脚本，`basename` 的输出都是简单文件名 `safedit`：

```bash
$ /home/alex/bin/safedit memo
$ ./safedit memo
$ safedit memo
```

设置 `script` 变量后，它会替换用法和错误消息中的脚本文件名。通过使用从调用脚本的命令中推导出的变量，而不是硬编码到脚本中的文件名，你可以创建

通过链接或重命名来命名临时文件，其使用方法和错误消息仍会提供准确的信息。

`safedit` 的第三个重要特性与在临时文件名称中使用 `$$` 变量有关。`esac` 语句之后的语句创建并给 *tempfile* 变量赋值。该变量包含存储在 `/tmp` 目录中的临时文件的名称，许多临时文件都存储在此处。临时文件名以 shell 的 PID 号开头，并以脚本名称结尾。PID 号的使用确保了文件名的唯一性，并且 `safedit` 不会尝试覆盖现有文件（如果两个人同时使用 `safedit`，这种情况可能会发生）。附加脚本名称的目的是，如果文件因某种原因滞留在 `/tmp` 中，你可以弄清楚它是从哪里来的。

在文件名中，PID 号被放在 `$script` 之前而不是之后，这是因为某些旧版本的 UNIX 对文件名施加了 14 个字符的限制。Linux 系统没有此限制。由于 PID 号确保了文件名的唯一性，因此将其放在最前面，以防止其被截断。（即使 `$script` 部分被截断，文件名仍然是唯一的。）基于同样的原因，当在脚本下方几行处的 *if* 控制结构中创建备份文件时，文件名由字符串 `bak` 加上正在编辑的文件编号组成。在旧系统上，如果将 `bak` 用作后缀而不是前缀，并且原始文件名长度为 14 个字符，`.bak` 可能会丢失，从而导致原始文件被覆盖。`basename` 实用程序在 `$edfile` 被加上 `bak` 前缀之前，提取其简单文件名。

第四，`safedit` 在 *if* 结构中使用了一个不寻常的 *test-command*：`vim $edfile`。*test-command* 调用 `vim` 来编辑 `$edfile`。当你完成文件编辑并从 `vim` 退出时，`vim` 返回一个退出代码。*if* 控制结构使用该退出代码来确定执行哪个分支。如果编辑会话成功完成，`vim` 返回 0，并执行 *then* 语句之后的语句。如果 `vim` 未正常终止（例如，如果用户杀掉了 `vim` 进程），`vim` 返回非零退出状态，脚本则执行 `else` 之后的语句。

## 选择

`select` 控制结构基于 Korn Shell 中的结构。它显示一个菜单，根据用户对项的选择为变量赋值，并执行一系列命令。`select` 控制结构具有如下语法：

```bash
select varname [in arg ...]
do
    commands
done
```

`select` 结构显示 *arg* 项的菜单。如果省略关键字 *in* 和参数列表，`select` 将使用位置参数代替 *arg* 项。菜单格式为在每个项前加上数字。例如，以以下开头的 `select` 结构：

```bash
select fruit in apple banana blueberry kiwi orange watermelon STOP
```

显示以下菜单：

```text
1) apple  3) blueberry  5) orange  7) STOP
2) banana  4) kiwi     6) watermelon
```

`select` 结构使用 `LINES` 和 `COLUMNS` 变量的值来确定显示大小。（`LINES` 的默认值为 24；`COLUMNS` 的默认值为 80。）当 `COLUMNS` 设置为 20 时，菜单看起来像这样：

```text
1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP
```

`PS3` 在显示菜单后，`select` 显示 `PS3` 的值，即特殊的选择提示符。`PS3` 的默认值为 `#`，但你通常会将 `PS3` 设置为更有意义的值。当你在 `PS3` 提示符后输入一个有效数字（菜单范围内的数字）时，`select` 将 *varname* 设置为你输入的数字对应的参数。如果你进行了无效输入，*varname* 被设置为 null。无论哪种情况，`select` 都会将你的响应存储在变量 `REPLY` 中，然后执行 `do` 和 `done` 之间的 *commands*。如果你按 `RETURN` 而未输入选择，shell 将重新显示菜单和 `PS3` 提示符。

`select` 结构持续发出 `PS3` 提示符并执行 *commands*，直到有某些操作使其退出——通常是 `break` 或 `exit` 语句。`break` 语句退出循环，`exit` 语句退出脚本。

以下脚本说明了 *select* 的用法：

```bash
$ cat fruit2
#!/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select FRUIT in apple banana blueberry kiwi orange watermelon STOP
do
if [ "$FRUIT" == "" ]; then
echo -e "Invalid entry.\n"
continue
elif [ "$FRUIT" = STOP ]; then
echo "Thanks for playing!"
break
fi
echo "You choose $FRUIT as your favorite."
echo -e "That is choice number $REPLY.\n"
done
```

```text
$ fruit2
1) apple  3) blueberry  5) orange  7) STOP
2) banana 4) kiwi  6) watermelon
Choose your favorite fruit from these possibilities: 3
You chose blueberry as your favorite.
That is choice number 3.

Choose your favorite fruit from these possibilities: 99
Invalid entry.

Choose your favorite fruit from these possibilities: 7
Thanks for playing!
```

在设置 `PS3` 提示符并使用 `select` 语句建立菜单后，`fruit2` 执行 `do` 和 `done` 之间的 `commands`。如果用户进行了无效输入，shell 将 *varname*（`$FRUIT`）设置为 null 值，因此 `fruit2` 首先测试 `$FRUIT` 是否为 null。如果是，`echo` 显示一个**错误**，`continue` 使 shell 重新显示 `PS3` 提示符。如果输入有效，脚本测试用户是否想停止。如果是，`echo` 显示一条消息，`break` 退出 `select` 结构（以及脚本）。如果用户输入了有效响应且不想停止，脚本显示用户响应的名称和编号。（有关 `echo` 的 `-e` 选项的信息，请参见第 914 页。）

## 此处文档

此处文档允许你从 shell 脚本内部将输入重定向到 shell 脚本。此处文档之所以如此命名，是因为它就在*此处*——在 shell 脚本中可立即访问——而不是在*彼处*，也许在另一个文件中。
