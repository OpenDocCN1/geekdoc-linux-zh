
| | `cat program 2>> errors` | `cat` 文件 `program` 到标准输出，并将错误追加到文件 `errors`。 |

| | `find / -name "*.c" -print > cprograms 2> errors` | `find` 系统中所有以 `*.c` 结尾的文件，将文件列表放入当前工作目录中的 `cprograms` 文件，并将所有错误（文件描述符 2）发送到当前工作目录中的 `errors` 文件。 |

| | `find / -name "*.c" -print > cprograms 2>&1` | `find` 系统中所有以 `*.c` 结尾的文件，将文件列表放入当前工作目录中的 `cprograms` 文件，并将所有错误（文件描述符 2）发送到与文件描述符 1（`cprograms`）相同的位置。 |

使用表 3-4 中显示的符号，你可以从`标准输入`和`标准输出`进行重定向。例如，你可以不将输出显示在屏幕上，而是将其发送到文件。我们将在接下来的示例中使用其中一些重定向形式。

### 使用 cat, more, pg, head 和 tail 查看文件

![](img/75f39fc91296b889c0653851accdfd46_173_0.png)

首先，让我们看一个长文件。事实上，让我们看一个非常长的文件，长到如果将其内容打印到屏幕上，屏幕无法完整显示。

`cat` 命令（concatenate 的缩写）正是如此，它将文件打印到你的屏幕上。然而，如果文件很长，你在屏幕上只能看到文件的末尾。还记得本书前面提到的用户 `denise` 吗？她的目录里有很多文件。让我们列出她目录中的文件，并使用以下命令将输出重定向到一个名为 `listing` 的文件：

![](img/75f39fc91296b889c0653851accdfd46_173_1.png)

```
$ ls -a /home/denise > listing
```

当我们 `cat listing` 到屏幕上时，我们只看到其末尾，如图 3-18 所示。我们知道这是文件的末尾，因为我对 `cat` 使用了包含行号的 `-n` 选项。行号表明这不是文件的开头。

```
106  rclock.exe
107  rkhelp.exe
108  sb.txt
109  shellupd.exe
110  smsup2.exe
111  softinit.remotesoft.cm
112  srvpr.exe
113  tabndi.exe
114  target.exe
115  tcp41a.exe
116  tnds2.exe
117  trace.TRC1
118  trace.TRC1.Z.uae
119  upgrae.exe
120  uue.syntax
121  v103.txt
122  whoon
123  win95app.exe
124  wsdrv1.exe
125  wsos21.exe
126  wsos22.exe
127  wsos23.exe
128  xferp110.zip
$
```

![](img/75f39fc91296b889c0653851accdfd46_174_0.png)

只看到这个文件的末尾并不是我们想要的结果。使用 `pg`（代表分页），我们将逐屏查看，如图 3-19 所示：

![](img/75f39fc91296b889c0653851accdfd46_174_1.png)

![](img/75f39fc91296b889c0653851accdfd46_175_0.png)

图 3-19 `pg` 命令

![](img/75f39fc91296b889c0653851accdfd46_175_1.png)

`more` 命令产生的输出与 `pg` 相同，如图 3-20 所示。

![](img/75f39fc91296b889c0653851accdfd46_175_2.png)

![](img/75f39fc91296b889c0653851accdfd46_176_0.png)

图 3-20 `more` 命令

这就好多了；现在我们可以使用 `pg` 和 `more` 逐屏滚动。然而，有时你只想查看文件的开头或结尾。你可以使用 `head` 命令查看文件的开头，使用 `tail` 命令查看文件的底部。下面的 `head` 和 `tail` 两个示例（见图 3-21 和 3-22）分别展示了查看 listing 的前 20 行和后 20 行。

![](img/75f39fc91296b889c0653851accdfd46_176_1.png)

![](img/75f39fc91296b889c0653851accdfd46_176_2.png)

![](img/75f39fc91296b889c0653851accdfd46_176_3.png)

![](img/75f39fc91296b889c0653851accdfd46_176_4.png)

```
$ head -20 listing
.
..
.CbtOptSet
.Xauthority
.cshrc
.cshrc.orig
.cim
.exrc
.fmrc
.fmrc.orig
.glanercrc
.gpmlp
.history
.login
.lrom
.mailrc
.netscape-bookmarks.html
.netscape-cache
.netscape-history
.netscape-newsgroups=news.spry.com
$
```

图 3-21 head 命令

```
$ tail -20 listing
shellupd.exe
smsup2.exe
softinit.remotesoft.cm
srvpr.exe
tabndi.exe
target.exe
tcp41a.exe
tnds2.exe
trace.TRC1
trace.TRC1.Z.uae
upgrade.exe
uue.syntax
v103.txt
whoon
win95app.exe
wsdrv1.exe
wsos21.exe
wsos22.exe
wsos23.exe
xferp110.zip
$
```

图 3-22 tail 命令

你使用的命令取决于你希望显示的信息。我个人偏好，无论是查看大文件的内容还是长长的文件列表，都使用 `more`。我并没有很好的理由，我只能说我们是习惯的动物，而且我一直都在使用 `more`。以下是 `cat`、`pg`、`more`、`head` 和 `tail` 的命令摘要。我列出了这些命令最常使用的一些选项。由于这些命令都不难使用，我建议你尝试每个命令，看看哪一个比其他的更适合你的需求。

以下是 `cat`、`pg`、`more`、`head` 和 `tail` 命令的摘要。

- `-` 当你想使用键盘作为标准输入时，用作指定文件名的替代。
- `-n` 在输出行的旁边显示行号。
- `-p` 将多个连续的空白行替换为单个空白行。
- `-s` 这是静默模式，抑制关于不存在文件的信息。
- `-u` 输出是无缓冲的，这意味着它是按字符处理的。
- `-v` 可见地打印大多数非打印字符。
- `-number` 你想显示的行数。
- `-p string` 使用 `string` 指定提示符。
- `-c` 在显示文件的下一页之前清除屏幕。

![](img/75f39fc91296b889c0653851accdfd46_178_0.png)

![](img/75f39fc91296b889c0653851accdfd46_178_1.png)

![](img/75f39fc91296b889c0653851accdfd46_178_2.png)

![](img/75f39fc91296b889c0653851accdfd46_178_3.png)

### -f

不要换行显示正在显示的文本。

### -n

只要输入了命令字母，命令就会立即发出，而不需要输入新的换行字符。

### `more`

一次显示一屏或显示文件的一部分。

**选项**

- `-c`: 在显示文件的下一页之前清屏。
- `-d`: 在屏幕底部显示带有简短说明的提示。
- `-f`: 将文本折行以适配屏幕，并据此判断页长。
- `-n`: 将显示窗口中的行数设置为 n。
- `-s`: 将多个连续的空白行压缩为一个空白行。

### `head`

仅提供文件的前几行。

**选项**

- `-c`: 输出指定字节数。
- `-l`: 输出指定行数。这是默认选项。
- `-n count`: 指定字节数或行数由 `count` 决定。您也可以使用 `-count` 来指定字节数或行数，如下例所示。默认 `count` 为 10。

#### tail

提供文件的最后几行。

**选项**
