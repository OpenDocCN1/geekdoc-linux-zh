

注意该命令的结构：

```
alias name='string'
```

在“alias”命令之后，我们给别名一个名称，紧接着（不允许有空白）是一个等号，然后紧接着是一个包含要赋予该名称含义的引号字符串。定义别名后，它可以在 shell 期望命令的任何地方使用。我们来试试：

```
[me@linuxbox ~]$ foo
bin  games  kerberos  lib64  local  share  tmp
etc  include  lib  libexec  sbin  src
/home/me
[me@linuxbox ~]$
```

我们也可以再次使用 type 命令来查看我们的别名：

```
[me@linuxbox ~]$ type foo
foo is aliased to 'cd /usr; ls ; cd -'
```

要删除别名，使用 unalias 命令，如下所示：

```
[me@linuxbox ~]$ unalias foo
[me@linuxbox ~]$ type foo
bash: type: foo: not found
```

虽然我们有意避免使用已存在的命令名称来命名别名，但这样做并不少见。这通常是为了对常用命令的每次调用应用一个常用的期望选项。例如，我们之前看到 ls 命令经常被别名化以添加颜色支持：

```
[me@linuxbox ~]$ type ls
ls is aliased to 'ls --color=tty'
```

要查看环境中定义的所有别名，请不带参数使用 alias 命令。以下是 Fedora 系统默认定义的一些别名。试着弄清楚它们都做了什么：

```
[me@linuxbox ~]$ alias
alias l='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
```

在命令行上定义别名有一个小问题。它们会在你的 shell 会话结束时消失。在后面的章节中，我们将看到如何将我们自己的别名添加到每次登录时建立环境的那些文件中，但现在，请享受我们已经迈出进入 shell 编程世界的第一步，尽管这一步很小！

## 重温老朋友

现在我们已经学会了如何查找命令的文档，去查找我们迄今为止遇到的所有命令的文档。研究有哪些额外的选项可用并尝试使用它们！

## 进一步阅读

Linux 和命令行有许多在线文档来源。以下是一些最好的：

- *Bash 参考手册* 是对 `bash` shell 的参考指南。它仍然是一部参考著作，但包含示例，比 `bash` 手册页更容易阅读。
  http://www.gnu.org/software/bash/manual/bashref.html
- *Bash FAQ* 包含有关 `bash` 的常见问题的答案。该列表面向中级到高级用户，但包含大量有用的信息。
  http://mywiki.wooledg.org/BashFAQ
- GNU 项目为其程序提供了广泛的文档，这些程序构成了 Linux 命令行体验的核心。你可以在这里看到完整列表：
  http://www.gnu.org/manual/manual.html
- Wikipedia 上有一篇关于手册页的有趣文章：
  http://en.wikipedia.org/wiki/Man_page

I/O 重定向允许我们更改输出去向和输入来源。通常，输出发送到屏幕，输入来自键盘，但使用 I/O 重定向，我们可以更改这一点。

## 重定向标准输出

I/O 重定向允许我们重新定义标准输出去向。要将标准输出重定向到屏幕之外的另一个文件，我们使用“>”重定向运算符，后跟文件名称。为什么我们要这样做？将命令的输出存储在文件中通常很有用。例如，我们可以告诉 shell 将 ls 命令的输出发送到文件 ls-output.txt 而不是屏幕：

```
[me@linuxbox ~]$ ls -l /usr/bin > ls-output.txt
```

在这里，我们创建了 /usr/bin 目录的长列表，并将结果发送到文件 ls-output.txt。让我们检查一下命令的重定向输出：

```
[me@linuxbox ~]$ ls -l ls-output.txt
-rw-rw-r-- 1 me me 167878 2008-02-01 15:07 ls-output.txt
```

很好；一个漂亮的大文本文件。如果我们用 less 查看该文件，我们会看到文件 ls-output.txt 确实包含了我们 ls 命令的结果：

```
[me@linuxbox ~]$ less ls-output.txt
```

现在，让我们重复重定向测试，但这次稍作改变。我们将目录名称改为一个不存在的名称：

```
[me@linuxbox ~]$ ls -l /bin/usr > ls-output.txt
ls: cannot access /bin/usr: No such file or directory
```

我们收到了一个错误消息。这是有道理的，因为我们指定了不存在的目录 /bin/usr，但为什么错误消息显示在屏幕上而不是被重定向到文件 ls-output.txt 呢？答案是 ls 程序不会将其错误消息发送到标准输出。相反，像大多数编写良好的 Unix 程序一样，它会将错误消息发送到标准错误。由于我们只重定向了标准输出而没有重定向标准错误，因此错误消息仍然发送到屏幕。我们将看到

