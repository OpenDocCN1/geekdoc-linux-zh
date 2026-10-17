
-rwx--xr-x 1 root root     7292 2011-05-04 17:43 aainfo

将光标移动到第三行，然后输入以下 `ex` 命令：

```
:r foo.txt
```

`:r` 命令（read 的缩写）会将指定文件插入到光标位置之前。现在我们的屏幕应该看起来像这样：

```
total 343700

-rwx--xr-x 1 root root    31316 2011-12-05 08:58 [

-rwx--xr-x 1 root root    8240 2011-12-09 13:39 411toppm

The quick brown fox jumped over the lazy dog. It was cool.

Line 2

Line 3

Line 4

Line 5

-rwx--xr-x 1 root root   111276 2012-01-31 13:36 a2p

-rwx--xr-x 1 root root    25368 2010-10-06 20:16 a52dec

-rwx--xr-x 1 root root    11532 2011-05-04 17:43 aafire

-rwx--xr-x 1 root root     7292 2011-05-04 17:43 aainfo
```

## 保存我们的工作

与 `vi` 中的其他所有操作一样，有几种方法可以保存我们编辑过的文件。我们已经介绍了 `ex` 命令 `:w`，但还有一些其他命令可能也很有用。

在命令模式下，输入 `ZZ` 将保存当前文件并退出 `vi`。同样，`ex` 命令 `:wq` 将 `:w` 和 `:q` 命令组合为一个命令，既可以保存文件，也可以退出。

`:w` 命令还可以指定一个可选的文件名。这相当于“另存为”命令。例如，如果我们正在编辑 `foo.txt`，并想保存一个名为 `foo1.txt` 的替代版本，我们可以输入以下命令：

```
:w foo1.txt
```

注意：虽然这会以新名称保存文件，但不会改变你正在编辑的文件名。当你继续编辑时，你仍然在编辑 `foo.txt`，而不是 `foo1.txt`。

## 13

## 自定义提示符

在本章中，我们将研究一个看似微不足道的细节：我们的 shell 提示符。通过这种检查，我们将揭示 shell 本身以及终端仿真程序的一些内部工作原理。

就像 Linux 中的许多事物一样，shell 提示符高度可配置，虽然我们几乎理所当然地使用它，但一旦学会如何控制它，提示符就是一个非常有用的设备。

### 提示符的构成

我们的默认提示符看起来像这样：

```
[me@linuxbox ~]$
```

请注意，它包含我们的用户名、主机名和当前工作目录，但它是如何变成这样的呢？非常简单。提示符由一个名为 `PS1` 的环境变量定义（prompt string 1 的缩写）。我们可以使用 `echo` 命令查看 `PS1` 的内容：

```
[me@linuxbox ~]$ echo $PS1
\u@\h \W\$
```

> 注意：如果你的结果与上面的示例不完全相同，不用担心。每个 Linux 发行版都会以略有不同的方式定义提示符字符串，有些甚至非常奇特。

从结果中，我们可以看到 `PS1` 包含我们在提示符中看到的一些字符，例如方括号、@ 符号和美元符号，但其余的则是个谜。细心的读者会认识到这些是反斜杠转义的特殊字符，就像我们在表 7-2 中看到的那样。表 13-1 是 shell 在提示符字符串中特殊处理的字符的部分列表。

#### 表 13-1：Shell 提示符中使用的转义代码

| 序列 | 显示的值 |
|---|---|
| `\a` | ASCII 铃声。遇到时会使计算机发出蜂鸣声。 |
| `\d` | 当前日期，格式为星期几、月份、日期；例如 'Mon May 26' |
| `\h` | 本地机器的主机名，不含尾部的域名 |
| `\H` | 完整的主机名 |
| `\j` | 当前 shell 会话中运行的作业数 |
| `\l` | 当前终端设备的名称 |
| `\n` | 一个换行字符 |
| `\r` | 一个回车 |
| `\s` | shell 程序的名称 |
| `\t` | 当前时间，24 小时制，小时:分钟::秒格式 |
| `\T` | 当前时间，12 小时制格式 |
| `\@` | 当前时间，12 小时制，AM/PM 格式 |
| `\A` | 当前时间，24 小时制，小时:分钟格式 |
| `\u` | 当前用户的用户名 |
| `\v` | shell 的版本号 |
| `\V` | shell 的版本和发行号 |
| `\w` | 当前工作目录的名称 |

#### 表 13-1（续）

| 序列 | 显示的值 |
|---|---|
| `\w` | 当前工作目录名称的最后一部分 |
| `\!` | 当前命令的历史编号 |
| `\#` | 本次 shell 会话中输入的命令数 |
| `\$` | 如果你没有超级用户权限，则显示“$”字符。如果有超级用户权限，则显示“#”代替。 |
| `\[` | 这表示一个或多个非打印字符的开始。它用于嵌入操纵终端仿真器的非打印控制字符，例如移动光标或更改文本颜色。 |
| `\]` | 这表示非打印字符序列的结束。 |

### 尝试一些替代的提示符设计

有了这个特殊字符列表，我们就可以更改提示符以查看效果。首先，我们将备份现有的字符串，以便以后可以恢复。为此，我们将把现有字符串复制到我们自己创建的另一个 shell 变量中：

```
[me@linuxbox ~]$ PS1_old="$PS1"
```

我们创建一个名为 `PS1_old` 的新变量，并将 `PS1` 的值赋给它。我们可以使用 `echo` 命令验证字符串是否已复制：

```
[me@linuxbox ~]$ echo $PS1_old
[\u@\h \W\$]
```

在终端会话期间的任何时候，我们都可以通过简单地反转该过程来恢复原始提示符：

```
[me@linuxbox ~]$ PS1="$PS1_old"
```

现在我们准备继续，让我们看看如果提示符字符串为空会发生什么：

```
[me@linuxbox ~]$ PS1=
```

如果我们不对提示符字符串进行赋值，我们将得到空。完全没有提示符字符串！提示符仍然在那里，但显示为空，正如我们要求的那样。由于这样看起来有点令人不安，我们将用一个最小的提示符替换它：

```
PS1="^$ "
```

That’s better. At least now we can see what we are doing. Notice the trailing space within the double quotes. This provides the space between the dollar sign and the cursor when the prompt is displayed.

Let’s add a bell to our prompt:

```
$ PS1="\a$ "
```

Now we should hear a beep each time the prompt is displayed. This could get annoying, but it might be useful if we needed notification when an especially long-running command has been executed.

Next, let’s try to make an informative prompt with some hostname and time-of-day information:

```
$ PS1="\A \h $ "
17:33 linuxbox $
```

Adding time-of-day to our prompt will be useful if we need to keep track of when we perform certain tasks. Finally, we’ll make a new prompt that is similar to our original:

```
17:37 linuxbox $ PS1="\u@\h \W\$ "
<cme@linuxbox ~>$
```
