
第八行执行小写字母到大写字母的转写。注意，与命令不同，`sed` 不支持字符范围（例如 `[a-z]`），不支持 POSIX 字符类。同样，由于 `y` 命令前面没有地址，它适用于输入中的每一行。

# 喜欢 `sed` 的人也喜欢...

`sed` 是一个非常强大的程序，能够对文本流执行相当复杂的编辑任务。它主要用于简单的单行任务，而不是长脚本。许多用户在较大任务中倾向于使用其他工具。其中最流行的是 `awk` 和 `perl`。它们超越了这里涵盖的简单程序，扩展到了完整编程语言领域。特别是 `perl`，经常被用于替代 shell 脚本执行许多系统管理和管理任务，也是一种非常流行的 Web 开发媒介。它有点专门。它的特定优势在于处理表格数据的能力。它类似于 `sed` 的之处在于，`awk` 通常按行处理文本文件，使用的方案类似于 `sed` 的“地址后跟操作”的理念。虽然 `awk` 和 `perl` 都不在本书的范围内，但它们对于 Linux 命令用户来说是非常棒的工具。

# `aspell`—交互式拼写检查器

我们将看到的最后一个工具是 `aspell`，一个交互式拼写检查器。`aspell` 程序是早期程序 `ispell` 的继承者，在大多数情况下可以作为替代品使用。虽然 `aspell` 程序主要被需要拼写检查的其他程序调用，但也可以作为命令行独立工具非常有效地使用。它具有智能检查各种类型文本文件的能力，包括 HTML 文档、C/C++ 程序、电子邮件和其他特殊文本。

要检查包含简单散文的文本文件，可以这样使用 `aspell`：

```bash
aspell check textfile
```

其中 `textfile` 是要检查的文件名。作为一个实际示例，让我们创建一个名为 `foo.txt` 的简单文本文件，其中包含故意的拼写错误：

```bash
@linuxbox~$ cat > foo.txt
The quick brown fox jimped over the lax dog.
```

接下来我们使用 `aspell` 检查该文件：

```bash
@linuxbox~]$ aspell check foo.txt
```

由于 `aspell` 在检查模式下是交互式的，我们将看到这样的屏幕：

```text
The quick brown fox jimped over the lax dog.

+   1) jimped

2) gimped

6) whimped

7) camped

3) comped

4) limped

5) pimped

i) Ignore

r) Replace

a) Add

b) Abort

8) humped

9) impede

O) umped

I) Ignore all

R) Replace all

1) Lower

x) Exit
```

在显示屏的顶部，我们看到了我们的文本，其中一个拼写可疑的单词被高亮。在中间，我们看到了从 0 到 9 的 10 个拼写建议，后面是其他可能的的操作列表。最后，在底部，我们看到一个准备好接受我们选择的提示。

如果我们输入 1，`aspell` 会将错误的单词替换为 `jumped` 并继续处理下一个拼错单词，即 `lazy`。如果我们选择替换为 `lazy`，`aspell` 会替换它并退出。一旦 `aspell` 完成，我们检查文件，发现拼写错误已经得到了纠正：

```text
@linuxbox~$ cat foo.txt
The quick brown fox jumped over the lazy dog.
```

除非通过命令行选项 `--dont-backup` 另有规定，否则 `aspell` 会在文件名后添加 `.bak` 来创建一个包含原始文本的备份文件。

为了展示我们的编辑技巧，我们将故意写一些拼写错误，以便我们可以重用我们的：

```bash
@linuxbox $ sed -i 's/lazy/lazy/;s/jumped/jimped/' foo.txt
```

选项 `-i` 告诉我们“原地”编辑文件，这意味着不再将编辑后的输出发送到标准输出，而是用更改重写文件。我们还看到，可以通过分号分隔多个编辑命令，在同一行中放置多个编辑命令的能力。

接下来，我们将看看 `aspell` 如何处理不同类型的文本文件。使用像 `vim` 这样的文本编辑器（爱冒险的你可能会尝试一下），我们将向文件中添加一些 HTML 标记：

```html
<html>
<head>
<title>Misspelled HTML file</title>
</head>
<body>
<p>The quick brown fox jumped over the lazy dog.</p>
</body>
</html>
```

现在，如果我们尝试对修改后的文件进行拼写检查，我们就会遇到一个问题。如果我们这样做：

```bash
@linuxbox ~ aspell check foo.txt
```

![](img/aa9c1f11ce2d496265d3ab82e4de6f44_295_0.png)

我们将得到这样的：

```html
<html>
<head>
<title>Mispelled HTML file</title>
</head>
<body>
<p>The quick brown fox jimped over the laxy dog.</p>
</body>
</html>
```

```text
+ 1) HTML

2) ht ml

3) ht-ml

i) Ignore

r) Replace

a) Add

b) Abort

4) Hamei

5) Hamil

6) hotel

I) Ignore all

R) Replace all

1) Add Lower

x) Exit
```

`aspell` 会将 HTML 标签的内容视为拼写错误。这个问题可以通过包含 `-H` (HTML) 检查模式选项来解决，如下所示：

```bash
@linuxbox ~$ aspell -H check foo.txt
```

我们的结果是这样的：

```html
<html>
<head>
<title>Mispelled HTML file</title>
</head>
<body>
<p>The quick brown fox jimped over the laxy dog.</p>
</body>
</html>
```

```text
+ 1) Mi spelled

2) Mi-spelled

3) Misspelled

4) Dispelled

5) Spelled

i) Ignore

r) Replace

a) Add

b) Abort

6) Misapplied

7) Miscalled

8) Respelled

9) Misspell

0) Misled

I) Ignore all

R) Replace all

1) Add Lower
```

`aspell` 会将 HTML 标签的内容视为拼写错误。这个问题可以通过包含 `-H` (HTML) 检查模式选项来解决，如下所示：

```bash
@linuxbox ~$ aspell -H check foo.txt
```

我们的结果是这样的：

```html
<html>
<head>
<title>Mispelled HTML file</title>
</head>
<body>
<p>The quick brown fox jimped over the laxy dog.</p>
</body>
</html>
```

```text
+ 1) Mi spelled

2) Mi-spelled

3) Misspelled

4) Dispelled

5) Spelled

i) Ignore

r) Replace

a) Add

b) Abort

6) Misapplied

7) Miscalled

8) Respelled

9) Misspell

0) Misled

I) Ignore all

R) Replace all

1) Add Lower
```

`aspell` 会将 HTML 标签的内容视为拼写错误。这个问题可以通过包含 `-H` (HTML) 检查模式选项来解决，如下所示：

```bash
@linuxbox ~$ aspell -H check foo.txt
```

我们的结果是这样的：

```html
<html>
<head>
<title>Mispelled HTML file</title>
</head>
<body>
<p>The quick brown fox jimped over the laxy dog.</p>
</body>
</html>
```

```text
+ 1) Mi spelled

2) Mi-spelled

3) Misspelled

4) Dispelled

5) Spelled

i) Ignore

r) Replace

a) Add

b) Abort

6) Misapplied

7) Miscalled

8) Respelled

9) Misspell

0) Misled

I) Ignore all

R) Replace all

1) Add Lower
```
