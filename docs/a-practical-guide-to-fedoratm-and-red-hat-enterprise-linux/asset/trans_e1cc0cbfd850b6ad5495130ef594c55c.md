

```bash
$ cat ~/.bash_profile
if [ -f ~/.bashrc ]; then
    . ~/.bashrc                          # 如果本地启动文件存在，则读取它
fi
PATH=$PATH:/usr/local/bin               # 将 /usr/local/bin 添加到 PATH
export PS1='\h \w \u\$'
```

在上述 **.bash_profile** 文件中，第一条命令如果在用户的主目录中存在 .bashrc 文件，则执行该文件中的命令。下一条命令将路径添加到 PATH 变量中（第 359 页）。通常 PATH 是在 /etc/profile 中设置并导出的，因此无需在用户的启动文件中再次导出。最后一条命令设置并导出 PS1（第 361 页），该变量用于控制用户提示符。

在下文所示的 .bashrc 文件中，第一条命令如果在 /etc/bashrc 文件存在的情况下，则执行该文件中的命令。接着该文件设置了 noclobber（第 156 页），取消设置 MAILCHECK（第 361 页），导出 LANG（第 366 页）和 viminit（用于 Vim 初始化），并定义了几个别名。最后一条命令定义了一个函数（第 396 页），该函数用于交换两个文件的名称。

```bash
$ cat ~/.bashrc
if [ -f /etc/bashrc ]; then
    source /etc/bashrc                  # 如果全局启动文件存在，则读取它
fi

set -o noclobber                        # 防止覆盖文件
unset MAILCHECK                         # 关闭“你有新邮件”通知
export LANG=C                           # 设置 LANG 变量
export viminit='set ai aw'              # 设置 vim 选项
alias df='df -h'                        # 设置别名
alias rm='rm -i'                       # 始终执行交互式 rm 操作
alias lt='ls -ltrh | tail'
alias hw='history | tail'
alias ch='chmod 755 '

function switch() {                     # 一个交换两个文件名称的函数
    local tmp=$$switch
    mv "$1" $tmp
    mv "$2" "$1"
    mv $tmp "$2"
}
```

![](img/243613168ac865b539f12460d966088e_388_0.png)

# . (点) 或 source：在当前 Shell 中运行启动文件

编辑完 .bashrc 等启动文件后，你不需要注销并重新登录即可使更改生效。相反，你可以使用 . (点) 或 source 内置命令来运行启动文件（它们是同一个命令）。与其他命令一样，在命令行中 . 后面必须跟一个空格。使用 . 或 source 类似于运行 shell 脚本，区别在于这些命令在当前进程中运行脚本。因此，当你使用 . 或 source 运行脚本时，你在脚本内部对变量所做的更改会影响你运行脚本的那个 shell。如果你将启动文件作为普通的 shell 脚本运行，而没有使用 . 或 *source* 内置命令，那么启动文件中创建的变量只在运行脚本的子 shell 中生效，而不会在你运行脚本的 shell 中生效。你可以使用 . 或 *source* 命令运行任何 shell 脚本，不仅仅是启动文件，但可能会产生不良的副作用（例如更改你依赖的 shell 变量的值）。更多信息请参阅第 1032 页的“环境、环境变量和继承”。

在以下示例中，*.bashrc* 设置了几个变量，并将 *PS1*（*bash* 提示符）设置为主机名。. 内置命令使新值生效。

```
$ cat ./.bashrc
export TERM=xterm              # 设置终端类型
export PS1="`hostname -f` : "   # 设置提示字符串
export CDPATH=:$HOME          # 将 HOME 添加到 CDPATH 字符串
stty kill '^Au'               # 将删除行设置为 control-u
$ . ./.bashrc

Guava:
```

## 作为符号的命令

Bourne Again Shell 以多种方式使用符号 (, ), [, ], 和 $。为了减少混淆，表 9-1 列出了这些符号中最常见的用法及其讨论所在的页码。

**表 9-1 作为符号的内置命令**

| 符号 | 命令 |
| :--- | :--- |
| `( )` | 子 shell（第 344 页） |
| `$( )` | 命令替换（第 410 页） |
| `(( ))` | 算术求值；*let* 的同义词（当包含的值包含等号时使用；第 1056 页） |
| `$(( ))` | 算术扩展（不用于包含等号的情况；第 408 页） |
| `[ ]` | *test* 命令（第 983 页和第 986 页） |
| `[[ ]]` | 条件表达式；类似于 `[ ]`，但增加了字符串比较（第 1057 页） |

# 重定向标准错误

第 5 章介绍了标准输出的概念，并解释了如何重定向命令的标准输出。除了标准输出外，命令还可以将输出发送到 *标准错误*。命令可能会将错误消息发送到标准错误，以防止它们与发送到标准输出的信息混淆。

与处理标准输出一样，默认情况下 shell 将标准错误定向到屏幕。除非你重定向其中某一个，否则你可能无法区分命令发送到标准输出的输出和发送到标准错误的输出。一个区别是，系统会对标准输出进行缓冲，但不对标准错误进行缓冲。本节描述了 bash 用于重定向标准错误以及区分标准输出和标准错误的语法。

### 文件描述符

文件描述符是程序发送输出和获取输入的地方。当你执行一个程序时，shell 为该程序打开三个文件描述符：0（标准输入）、1（标准输出）和 2（标准错误）。重定向输出符号（第 154 页）是 1> 的简写，它告诉 shell 重定向标准输出。同样，<（第 155 页）是 0< 的简写，用于重定向标准输入。符号 2> 用于重定向标准错误。更多信息请参阅第 1016 页的“文件描述符”。

以下示例演示了如何将标准输出和标准错误重定向到不同的文件以及同一个文件。当你运行 cat 工具并传入一个不存在的文件和一个存在的文件时，cat 会将错误消息发送到标准错误，并将存在的文件复制到标准输出。除非你重定向它们，否则两条消息都会显示在屏幕上。

```
$ cat y
This is y.
$ cat x
cat: x: No such file or directory

$ cat x y
cat: x: No such file or directory
This is y.
```

当你重定向命令的标准输出时，发送到标准错误的输出不受影响，仍然显示在屏幕上。

```
$ cat x y > hold
cat: x: No such file or directory
$ cat hold
This is y.
```

同样，当通过管道发送标准输出时，标准错误不受影响。以下示例将 cat 的标准输出通过管道发送到 tr，在此示例中 tr 将小写字母转换为大写字母。（有关更多信息，请参见 tr 的信息页。）cat 发送到标准错误的文本不会被转换，因为它直接发送到屏幕而不是通过管道。

```
$ cat x y | tr "[a-z]" "[A-Z]"
cat: x: No such file or directory
THIS IS Y.
```

以下示例将标准输出和标准错误重定向到不同的文件。shell 将标准输出（文件描述符 1）重定向到 1> 后面的文件名。你可以用 > 代替 1>。shell 将标准错误（文件描述符 2）重定向到 2> 后面的文件名。

```
$ cat x y 1> hold1 2> hold2
$ cat hold1
This is y.
$ cat hold2
cat: x: No such file or directory
```

### 合并标准输出和标准错误

在下一个示例中，`&>` 令牌将标准输出和标准错误重定向到单个文件：

```
$ cat x y &> hold
$ cat hold
cat: x: No such file or directory
This is y.
```

### 复制文件描述符

在下一个示例中，首先 `1>` 将标准输出重定向到 `hold`，然后 `2>&1` 声明文件描述符 2 是文件描述符 1 的副本。结果是，标准输出和标准错误都重定向到 `hold`。

```
$ cat x y 1> hold 2>&1
$ cat hold
cat: x: No such file or directory
This is y.
```

在这种情况下，`1> hold` 先于 `2>&1`。如果它们的顺序相反，标准错误将在标准输出重定向到 `hold` 之前被设为标准输出的副本。在那种情况下，只有标准输出会被重定向到 `hold`。

### 通过管道发送错误

下一个示例声明文件描述符 2 是文件描述符 1 的副本，并将文件描述符 1（以及文件描述符 2）的输出通过管道发送到 `tr` 命令。

```
$ cat x y 2>&1 | tr "[a-z]" "[A-Z]"
CAT: X: NO SUCH FILE OR DIRECTORY
THIS IS Y.
```

令牌 `&1` 是 `2>&1` 的简写：

```
$ cat x y 1& tr "[a-z]" "[A-Z]"
CAT: X: NO SUCH FILE OR DIRECTORY
THIS IS Y.
```

### 将错误发送到标准错误

你可以使用 `1>&2`（或简单地使用 `>&2`；不需要 1）将命令的标准输出重定向到标准错误。Shell 脚本使用这种技术将 `echo` 的输出发送到标准错误。在下面的脚本中，第一个 `echo` 的标准输出被重定向到标准错误：

```
$ cat message_demo
echo This is an error message. 1>&2
echo This is not an error message.
```

