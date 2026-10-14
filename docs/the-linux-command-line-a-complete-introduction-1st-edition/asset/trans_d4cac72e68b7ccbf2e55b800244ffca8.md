

## 使用 alias 创建自己的命令

现在让我们来体验第一次编程！我们将使用 alias 命令创建一个属于自己的命令。但在开始之前，我们需要揭晓一个小命令行技巧。可以将多个命令放在同一行，只需用分号字符分隔每个命令即可。用法如下：

```
command1; command2; command3...
```

下面是我们将使用的示例：

```
[me@linuxbox ~]$ cd /usr; ls; cd -
bin games kerberos lib64 local share tmp
etc include lib libexec sbin src
/home/me
[me@linuxbox ~]$
```

如我们所见，我们将三个命令组合在一行中。首先我们将目录更改为 /usr，然后列出该目录，最后我们返回到原始目录（使用 cd -），这样我们就回到了起点。现在让我们使用 alias 将这个序列变成一个新命令。首先要做的是为我们的新命令想一个名字。让我们试试 test。在此之前，最好先弄清楚名字 test 是否已经被使用。要查找，可以再次使用 type 命令：

```
[me@linuxbox ~]$ type test
test is a shell builtin
```

糟糕！名字 test 已经被人用了。让我们试试 foo：

```
[me@linuxbox ~]$ type foo
bash: type: foo: not found
```

太好了！foo 还没有被占用。所以让我们创建我们的别名：

```
[me@linuxbox ~]$ alias foo='cd /usr; ls; cd -'
```

注意这个命令的结构：

```
alias name='string'
```

在 alias 命令之后，我们为别名指定一个名字，然后紧接着（不允许有空白）是一个等号，等号后紧跟一个引号字符串，其中包含要赋予该名字的含义。在我们定义别名后，它可以在 shell 期望命令的任何地方使用。

让我们试试：

```
[me@linuxbox ~]$ foo
bin games kerberos lib64 local share tmp
etc include lib libexec sbin src
/home/me
[me@linuxbox ~]$
```

我们也可以再次使用 type 命令来查看我们的别名：

```
[me@linuxbox ~]$ type foo
foo is aliased to `cd /usr; ls ; cd -`
```

要删除别名，使用 unalias 命令，如下所示：

```
[me@linuxbox ~]$ unalias foo
[me@linuxbox ~]$ type foo
bash: type: foo: not found
```

虽然我们特意避免使用已存在的命令名来命名我们的别名，但有时这样做是可取的。这通常是为了为常用命令的每次调用应用一个常用的期望选项。例如，我们之前看到 ls 命令经常被别名化以添加颜色支持：

```
[me@linuxbox ~]$ type ls
ls is aliased to `ls --color=tty`
```

要查看环境中定义的所有别名，使用不带参数的 alias 命令。以下是 Fedora 系统默认定义的一些别名。试着弄清楚它们各自的作用：

```
[me@linuxbox ~]$ alias
alias l='ls -d .*'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
```

在命令行上定义别名有一个小问题。它们会在你的 shell 会话结束时消失。在后面的章节中，我们将看到如何将自己的别名添加到每次登录时建立环境的配置文件中，但现在，享受我们已经迈出进入 shell 编程世界的第一步，尽管很小！

## 重温老朋友

现在我们已经学会了如何查找命令的文档，去查阅我们迄今为止遇到的所有命令的文档吧。研究有哪些额外的选项可用并尝试它们！

## 6 重定向

在本课中，我们将释放命令行可能最酷的功能：I/O 重定向。I/O 代表输入/输出，通过此功能你可以将命令的输入和输出重定向到文件，以及连接多个命令以创建强大的命令管道。为了展示此功能，我们将介绍以下命令：

- cat—连接文件。
- sort—对文本行进行排序。
- uniq—报告或省略重复行。
- wc—打印每个文件的换行符、单词和字节计数。
- grep—打印匹配模式的行。
- head—输出文件的前部。
- tail—输出文件的后部。
- tee—从标准输入读取并写入标准输出和文件。

