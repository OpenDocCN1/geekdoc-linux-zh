
```
$ echo three extra parameters
three extra parameters
$ echo UID
UID
```

显然，由于对 shell 变量的名称（上例中的 UID）使用 echo 只会显示变量的名称而不是其内容，必须有其他方法来访问内容。

每当你想从 shell 变量中提取值时，需要在其名称前加上美元符号（$）。美元符号是一个特殊符号，其含义由 shell 解释。这也意味着，如果你需要将美元符号作为参数传递给另一个命令，它需要被引用。请注意，只有反斜杠和单引号的引用机制才适用于美元符号。如果你需要关于 shell 引用机制的提醒，请参考第 4.1 节。UID 变量的值可以按如下方式显示：

```
$ echo the value of UID is $UID
the value of UID is 500
```

echo 命令在 shell 脚本中非常有用，因为它能够显示文本消息和 shell 变量的值。

shell 变量可以用以下语法为其分配新值：

```
variable=value
```

以下序列会更改 PS1 的值，从而 shell 的主提示符字符串也会改变：

```
$ PS1='hello: '
hello: echo prompt is now $PS1
prompt is now hello:
```

请注意，在实际更改变量值的那一行，变量名称前面没有美元符号。美元符号表示法仅在从变量中提取值时使用，而不是在分配值时使用。另请注意，在赋值中，等号（=）符号两侧没有空格。如果你在这两个位置加上空格，shell 将无法识别该行为变量赋值，并可能会生成错误消息。

除了标准的一组 shell 变量之外，你可以自由创建自己的变量并为其分配值。如果尝试访问尚未分配的变量的值，shell 不会抱怨。shell 只会将空字符串作为值返回：

```
$ echo $sn flowers are pretty
flowers are pretty
$ sn=sun
$ echo $sn flowers are pretty
sun flowers are pretty
```

如果你希望之前的输出为 sunflowers are pretty，那么你需要消除变量 sn 的值与单词 flowers 之间的空格。如以下示例所示，解决此问题的明显方法不起作用：

```
$ echo $snflowers are pretty
are pretty
```

仅在命令行上删除空格会导致 shell 将新单词 snflowers 视为变量名，而该变量目前没有值。解决此问题的标准方法是使用一对花括号括住所需的变量名，从而将名称与后面的单词分隔开，但两者之间没有空格：

```
$ echo ${sn}flowers are pretty
sunflowers are pretty
```

通常，仅仅通过重新为其分配新值来更改现有变量的值是可以接受的：

```
$ sn=`all kinds of `
$ echo ${sn}flowers are pretty
all kinds of flowers are pretty
```

在此示例中，对分配给变量 sn 的字符串使用引号是必要的，因为该字符串包含空格。通常，shell 会使用空格作为分隔点将输入行拆分为单独的单词。在此示例中，需要将包括其空格在内的所有字符字符串都分配给 shell 变量。

有时你可能想要声明一个变量，将其设置为特定值，然后防止该值被更改。这可以通过在初始值分配后将变量设置为只读来实现：

```
$ readonly sn
$ sn=sun
bash: sn: read-only variable
$ echo ${sn}flowers are pretty
all kinds of flowers are pretty
```

作为另一个示例，还有一个你已经见过的标准 shell 变量，它也被设置为只读——UID 变量。这显然需要是只读的，因为它的值是在用户登录时从密码文件中的用户 UID 设置的，而这不是可以随意更改的值。

每当你创建一个变量时，它仅限于当前 shell。这意味着你的本地 shell 变量的值不能被从你的 shell 运行的其他命令或脚本看到。经常会希望这些值对 shell 执行的命令可用。这可以通过 export 命令完成。在前面的示例中，变量 sn 是一个本地变量，可以按如下方式使其可供后续命令使用：

```
$ export sn
```

对变量的 export 操作也可以在为其分配值的同时执行，作为一行命令：

```
$ export sn=sun
```

## 6.3 Shell 脚本参数

我们之前编写的 dirsize shell 脚本有一个主要问题：它只能给出 /usr/bin 目录中文件的数量，因为该路径名已内置在脚本中。如果能够指定要使用的目录的路径名，那就更有用了，这样你就可以找到任何给定目录中的文件数。理想情况下，你希望能够给出如下命令：

```
$ dirsize /etc
```

并让 dirsize 计算该目录中的文件数而不是。

事实上，这很容易，因为 shell 会自动将你输入的任何命令行拆分为单独的单词，然后将这些单词分配给一组特殊变量，其值可以在 shell 脚本内部读取。这些特殊变量的值可以通过 $0、$1、$2 等表示法访问。$0 中的值将是该行上的第一个单词（即命令名），$1 中的值将是第一个命令行参数，$2 将是第二个命令行参数，依此类推。从 $1、$2 等开始的值称为位置参数。例如，如果名为 test1 的 shell 脚本按如下方式执行：

```
$ test1 param1 param2
```

那么在 shell 脚本内部，特殊变量的值将为：

```
$0 = test1
$1 = param1
$2 = param2
```

鉴于此信息，现在修改 dirsize 以按要求执行就很简单了：

```
$ cat >dirsize
ls $1 | wc -w
Ctrl-d
$ chmod 700 dirsize
$ dirsize /etc
```

如你所见，当 shell 脚本运行时，参数（/etc）会被替换到管道中的 ls 命令中，替换 $1 的位置。这种替换由 shell 完成，而 ls 命令并不知道发生了替换。

为了让你在目录层次结构中的任何位置都能访问此新命令，你需要确保包含该命令的目录列在你的 PATH 变量中。下一个示例在你的主目录下创建一个 bin 目录，将 dirsize 命令移入其中，并将此 bin 目录添加到 PATH 的开头，以便 shell 在你输入命令名时自动搜索该目录。示例中使用了 shell 变量 HOME 的值，因为它包含你的主目录的路径名：

```
$ echo $PATH
/bin:/usr/bin:.
$ mkdir $HOME/bin
$ mv dirsize $HOME/bin
$ PATH=$HOME/bin:$PATH
$ echo $PATH
/usr1/pc/bin:/bin:/usr/bin:.
```

请记住，PATH 变量中包含的目录列表由冒号分隔。PATH 的初始内容显示，将搜索三个目录以查找你输入的任何命令：首先是 /bin，然后是 /usr/bin，最后是点号，即当前目录。然后命令序列通过在 PATH 前面添加 /usr1/pc/bin: 来修改 PATH 的值，以便在输入命令时始终先搜索该目录，然后再搜索其他三个目录。

当你想引用主目录时，可以使用波浪号（~）符号作为 $HOME 的替代表示法。使用这种表示法，$HOME/bin 与 ~/bin 相同。波浪号表示法也可以通过在其后加上另一个用户的登录名来扩展。在这种情况下，表示法会扩展为指定用户的主目录的路径名。例如：

```
$ ls ~carey/bin
```

将列出用户 carey 主目录下 bin 的内容，前提是我有权限读取该目录的内容。

## 6.4 登录脚本

执行诸如更改 PS1 shell 提示符之类的操作可能很有趣。并且向 PATH 内容添加个人额外项也非常有用。然而，当你每次登录前都必须执行这些操作才能使其生效时，很快就会变得相当乏味。

解决此问题的办法是创建一个个人登录脚本，shell 在你登录时会为你自动读取并执行该脚本。个人登录脚本
