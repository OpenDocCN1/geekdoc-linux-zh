

## 3 探索系统

现在我们已经知道如何在文件系统中移动，是时候对我们的 Linux 系统进行一次引导式游览了。在开始之前，我们将学习一些在途中会用到的命令：

- ls—列出目录内容。
- file—确定文件类型。
- less—查看文件内容。

### 更有趣的 ls

ls 很可能是使用最频繁的命令，原因也很充分。有了它，我们可以看到目录内容并确定各种重要的文件和目录属性。正如我们所见，我们可以简单地输入 ls 来查看当前工作目录中包含的文件和子目录列表：

```
[me@linuxbox ~]$ ls
Desktop Documents Music Pictures Public Templates Videos
```

除了当前工作目录，我们还可以指定要列出的目录，如下所示：

```
[me@linuxbox ~]$ ls /usr
bin games kerberos libexec sbin src
etc include lib local share tmp
```

甚至可以指定多个目录。在此示例中，我们将同时列出用户的主目录（用 ~ 字符表示）和 /usr 目录：

```
[me@linuxbox ~]$ ls ~ /usr
/home/me:
Desktop Documents Music Pictures Public Templates Videos
/usr:
bin games kerberos libexec sbin src
etc include lib local share tmp
```

我们还可以更改输出格式以显示更多详细信息：

```
[me@linuxbox ~]$ ls -l
total 56
drwxrwxr-x 2 me me 4096 2012-10-26 17:20 Desktop
drwxrwxr-x 2 me me 4096 2012-10-26 17:20 Documents
drwxrwxr-x 2 me me 4096 2012-10-26 17:20 Music
drwxrwxr-x 2 me me 4096 2012-10-26 17:20 Pictures
drwxrwxr-x 2 me me 4096 2012-10-26 17:20 Public
drwxrwxr-x 2 me me 4096 2012-10-26 17:20 Templates
drwxrwxr-x 2 me me 4096 2012-10-26 17:20 Videos
```

通过在命令中添加 -l，我们将输出更改为长格式。

### 选项和参数

这引出了一个关于大多数命令如何工作的重要观点。命令通常后面跟着一个或多个修改其行为的选项，以及一个或多个命令所作用的对象，即参数。因此大多数命令看起来像这样：

```
command -options arguments
```

大多数命令使用由破折号引导的单个字符作为选项，例如 -l。但许多命令，包括 GNU 项目的命令，也支持由两个破折号引导的单词组成的长选项。此外，许多命令允许将多个短选项串联起来。在此示例中，ls 命令被赋予了两个选项，l 选项用于生成长格式输出，t 选项用于按文件的修改时间排序结果：

```
[me@linuxbox ~]$ ls -lt
```

我们将添加长选项 --reverse 来反转排序顺序：

```
[me@linuxbox ~]$ ls -lt --reverse
```

ls 命令有大量可能的选项。最常见的列在表 3-1 中。

### 表 3-1：常见的 ls 选项

| Option | Long Option | Description |
|---|---|---|
| -a | --all | 列出所有文件，即使那些以句点开头、通常不列出（即隐藏）的名称。 |
| -d | --directory | 通常，如果指定了目录，ls 将列出目录的内容，而不是目录本身。使用此选项结合 -l 选项可查看目录本身的详细信息而不是其内容。 |
| -F | --classify | 此选项会在每个列出名称的末尾附加一个指示字符（例如，如果名称是目录，则为正斜杠）。 |
| -h | --human-readable | 在长格式列表中，以人类可读格式显示文件大小而不是字节。 |
| -l |  | 以长格式显示结果。 |
| -r | --reverse | 以相反顺序显示结果。通常，ls 以升序字母顺序显示其结果。 |
| -S |  | 按文件大小排序结果。 |
| -t |  | 按修改时间排序。 |

### 更深入地了解长格式

正如我们之前看到的，-l 选项会使 ls 以长格式显示结果。此格式包含大量有用的信息。以下是 Ubuntu 系统中的 Examples 目录：

```
-rw-r--r-- 1 root root 3576296 2012-04-03 11:05 Experience_ubuntu.ogg
-rw-r--r-- 1 root root 1186219 2012-04-03 11:05 kubuntu-leaflet.png
-rw-r--r-- 1 root root 47584 2012-04-03 11:05 logo-EduBuntu.png
-rw-r--r-- 1 root root 44355 2012-04-03 11:05 logo-Kubuntu.png
-rw-r--r-- 1 root root 34391 2012-04-03 11:05 logo-Ubuntu.png
-rw-r--r-- 1 root root 32059 2012-04-02 11:05 oo-cd-cover.odf
-rw-r--r-- 1 root root 159744 2012-04-02 11:05 oo-derivatives.doc
-rw-r--r-- 1 root root 27837 2012-04-03 11:05 oo-maxwell.odt
-rw-r--r-- 1 root root 98816 2012-04-03 11:05 oo-trig.xls
```

