
The name `sed` is short for stream editor. It performs text editing on a stream of text, either a set of specified files or standard input. `sed` is a powerful and somewhat complex program (there are entire books about it), so we will not cover it completely here.

In general, the way `sed` works is that it is given either a single editing command (on the command line) or the name of a script file containing multiple commands, and it then performs these commands upon each line in the stream of text. Here is a very simple example of `sed` in action:

```
[me@linuxbox ~]$ echo "front" | sed 's/front/back/'
back
```

In this example, we produce a one-word stream of text using `echo` and pipe it into `sed`. `sed`, in turn, carries out the instruction `s/front/back/` upon the text in the stream and produces the output “back” as a result. We can also recognize this command as resembling the “substitution” (search-and-replace) command in `vi`.

Commands in `sed` begin with a single letter. In the example above, the substitution command is represented by the letter `s` and is followed by the search-and-replace strings, separated by the slash character as a delimiter. The choice of the delimiter character is arbitrary. By convention, the slash character is often used, but `sed` will accept any character that immediately follows the command as the delimiter. We could perform the same command this way:

```
[me@linuxbox ~]$ echo "front" | sed 's_front_back_'
back
```

By using the underscore character immediately after the command, it becomes the delimiter. The ability to set the delimiter can be used to make commands more readable, as we shall see.

Most commands in `sed` may be preceded by an address, which specifies which line(s) of the input stream will be edited. If the address is omitted, then the editing command is carried out on every line in the input stream. The simplest form of address is a line number. We can add one to our example:

```
[me@linuxbox ~]$ echo "front" | sed '1s/front/back/'
back
```

Adding the address `1` to our command causes our substitution to be performed on the first line of our single-line input stream. 如果我们指定另一个数字：

```
[me@linuxbox ~]$ echo "front" | sed '2s/front/back/'
front
```

可以看到编辑没有执行，因为我们的输入流中没有第 2 行。

地址可以用多种方式表达。以下是最常见的几种：

### 表 20-7: `sed` 地址表示法

| 地址 | 描述 |
|---|---|
| `n` | 行号，其中 `n` 是正整数。 |
| `$` | 最后一行。 |
| `/regexp/` | 匹配 POSIX 基本正则表达式的行。注意，正则表达式由斜杠字符分隔。也可以使用替代字符来分隔正则表达式，通过指定 `\cregexpc` 形式，其中 `c` 是替代字符。 |
| `addr1,addr2` | 从 `addr1` 到 `addr2` 的范围行，包含两端。地址可以是上面任何单地址形式。 |
| `first~step` | 匹配由数字 `first` 表示的行，然后按 `step` 的间隔匹配后续每一行。例如，`1~2` 表示每个奇数行，`5~5` 表示第 5 行以及其后每隔 5 行的行。 |
| `addr1,+n` | 匹配 `addr1` 及其后的 `n` 行。 |
| `addr!` | 匹配除 `addr` 之外的所有行，`addr` 可以是上述任何形式。 |

我们将使用本章前面的 `distros.txt` 文件来演示不同种类的地址。首先是行号范围：

```
[me@linuxbox ~]$ sed -n '1,5p' distros.txt
SUSE      10.2  12/07/2006
Fedora    10    11/25/2008
SUSE      11.0  06/19/2008
Ubuntu    8.04  04/24/2008
Fedora 8 11/08/2007
```

在这个例子中，我们打印一个行范围，从第 1 行开始一直到第 5 行。为此，我们使用了 `p` 命令，它只是让匹配的行被打印出来。但为了使其生效，我们必须包含选项 `-n`（即关闭自动打印选项），以阻止 `sed` 默认打印每一行。

接下来，我们尝试一个正则表达式：

```
[me@linuxbox ~]$ sed -n '/SUSE/p' distros.txt
SUSE 10.2 12/07/2006
SUSE 11.0 06/19/2008
SUSE 10.3 10/04/2007
SUSE 10.1 05/11/2006
```

通过包含用斜杠分隔的正则表达式 `/SUSE/`，我们能够像 `grep` 一样隔离包含它的行。

最后，我们通过在地址上添加感叹号（`!`）来尝试取反：

```
[me@linuxbox ~]$ sed -n '/SUSE/!p' distros.txt
Fedora 10 11/25/2008
Ubuntu 8.04 04/24/2008
Fedora 8 11/08/2007
Ubuntu 6.10 10/26/2006
Fedora 7 05/31/2007
Ubuntu 7.10 10/18/2007
Ubuntu 7.04 04/19/2007
Fedora 6 10/24/2006
Fedora 9 05/13/2008
Ubuntu 6.06 06/01/2006
Ubuntu 8.10 10/30/2008
Fedora 5 03/20/2006
```

这里我们看到了预期结果：文件中除了被正则表达式匹配的行之外的所有行。

到目前为止，我们已经了解了 `sed` 的两种编辑命令，`s` 和 `p`。下面是基本编辑命令的更完整列表：

### 表 20-8: `sed` 基本编辑命令

| 命令 | 描述 |
|---|---|
| `=` | 输出当前行号。 |
| `a` | 在当前行之后追加文本。 |
| `d` | 删除当前行。 |
| `i` | 在当前行之前插入文本。 |
| `p` | 打印当前行。默认情况下，`sed` 会打印每一行，并且只编辑文件中匹配指定地址的行。可以通过指定 `-n` 选项来覆盖默认行为。 |
| `q` | 退出 `sed`，不再处理更多行。如果未指定 `-n` 选项，则输出当前行。 |
| `Q` | 退出 `sed`，不再处理更多行。 |
