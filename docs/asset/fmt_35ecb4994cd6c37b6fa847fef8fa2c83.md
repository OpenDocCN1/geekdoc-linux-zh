
```
$ rm -i ../krsort.dir.new/*
../krsort.dir.new/krsort: ? (y/n) n
../krsort.dir.new/krsort.c: ? (y/n) n
../krsort.dir.new/krsort.dos: ? (y/n) n
../krsort.dir.new/krsort.q: ? (y/n) n
../krsort.dir.new/krsortorig.c: ? (y/n) n
$ ls -l ../krsort.dir.new
total 168
-rwxr-xr-x  1 denise  users  34592 Oct 27 18:44 krsort
-rwxr-xr-x  1 denise  users   3234 Oct 27 18:46 krsort.c
-rwxr-xr-x  1 denise  users  32756 Oct 27 18:46 krsort.dos
-rw-r--r--  1 denise  users   9922 Oct 27 18:46 krsort.q
-rwxr-xr-x  1 denise  users   3085 Oct 27 18:46 krsortorig.c
$
```

![](img/75f39fc91296b889c0653851accdfd46_167_2.png)

显然，这导致没有从 `krsort.dir.new` 中删除任何东西，因为我们在被询问是否要删除文件时回答了 `n`。

现在让我们继续向 `krsort.dir.new` 添加一个以“.”开头的文件。`touch` 命令正是做这个的，创建一个没有内容的文件，如图 3-15 所示：

```
$ touch ../krsort.dir.new/.dotfile
$ ls -al ../krsort.dir.new
total 172
drwxr-xr-x 2 denise users 1024 Oct 27 18:54 .
drwxrwxr-x 4 denise users 1024 Oct 27 18:40 ..
-rw-r--r-- 1 denise users 0 Oct 27 18:56 .dotfile
-rwxr-xr-x 1 denise users 34592 Oct 27 18:44 krsort
-rwxr-xr-x 1 denise users 3234 Oct 27 18:46 krsort.c
-rwxr-xr-x 1 denise users 32756 Oct 27 18:46 krsort.dos
-rw-r--r-- 1 denise users 9922 Oct 27 18:46 krsort.q
-rwxr-xr-x 1 denise users 3085 Oct 27 18:46 krsortorig.c
$
```

![](img/75f39fc91296b889c0653851accdfd46_168_0.png)

![](img/75f39fc91296b889c0653851accdfd46_168_1.png)

如果我们现在尝试使用之前发出的相同 `rm` 命令来删除文件，我们会看到以下结果，如图 3-16 所示：

```
$ rm -i ../krsort.dir.new/*
../krsort.dir.new/krsort: ? (y/n) y
../krsort.dir.new/krsort.c: ? (y/n) y
../krsort.dir.new/krsort.dos: ? (y/n) y
../krsort.dir.new/krsort.q: ? (y/n) y
../krsort.dir.new/krsortorig.c: ? (y/n) y
$ ls -al ../krsort.dir.new
total 4
drwxr-xr-x     2 denise     users        1024 Oct 27 18:57 .
drwxrwxr-x     4 denise     users        1024 Oct 27 18:40 ..
-rw-r--r--     1 denise     users           0 Oct 27 18:56 .dotfile
```

![](img/75f39fc91296b889c0653851accdfd46_169_0.png)

与 `rm` 命令一起使用的通配符 `"*"` 没有删除文件 `.dotfile`。该目录中的文件 `.dotfile` 阻止了 `rmdir` 命令删除 `krsort.dir.new`。在 `rmdir` 命令成功删除 `krsort.dir.new` 之前，必须先删除该文件。

```
$ rmdir -i ../krsort.dir.new
../krsort.dir.new: ? (y/n) y
rmdir: ../krsort.dir.new: Directory not empty
$ rm ../krsort.dir.new/.dotfile
$ rmdir -i ../krsort.dir.new
../krsort.dir.new: ? (y/n) y
$
```

![](img/75f39fc91296b889c0653851accdfd46_170_0.png)

![](img/75f39fc91296b889c0653851accdfd46_170_1.png)

`rmdir` 现在成功删除了 `krsort.dir.new`，因为 `.dotfile` 已消失，如图 3-17 所示：

![](img/75f39fc91296b889c0653851accdfd46_170_2.png)

图 3-17 `rmdir` 删除 `/home/denise/krsort.dir.new`

### 重定向

在讨论文件查看之前，让我们花点时间谈谈重定向，因为我在接下来的章节中会用到一些重定向。我会在 Shell 编程部分详细讲解重定向，但现在我想先给你一个关于重定向的简要介绍，以便我们能更有效地讲解本章中的一些命令。

UNIX 系统的设计使得命令通常从键盘（常被称为`标准输入`）获取输入，并将输出发送到屏幕（常被称为`标准输出`）。命令还会将错误信息发送到屏幕。你并不总是希望输入来自标准输入，或者输出和错误都流向标准输出。系统赋予了你大量的控制权来覆盖这些默认设置。这就是重定向。表 3-4 展示了许多常见的重定向形式。

如表中所示，要将命令的输出从重定向到标准输出到一个文件，请使用 `>`。这在几乎所有情况下都有效。如果你设置了一个名为 `noclobber` 的环境变量，那么重定向到已存在的文件将不起作用（我们将很快讲解环境变量）。`noclobber` 不允许重定向覆盖已存在的文件。如果你试图覆盖一个已存在的文件，例如下面的 `/tmp/processes`，你会收到一条文件已存在的消息：

![](img/75f39fc91296b889c0653851accdfd46_171_0.png)

```
# ps -ef > /tmp/processes
/tmp/processes: File exists
```

然而，你可以使用 `!` 配合重定向来强制覆盖文件。使用 `>!` 会强制覆盖文件，而 `>>!` 则强制将输出追加到已存在文件的末尾。这些用法的示例见表 3-4。

### 表 3-4 常用的重定向形式

| 命令或赋值 | 示例 | 描述 |

| :--- | :--- | :--- |

| `<` | `wc -l < .login` | 标准输入重定向：执行 `wc`（字数统计）并列出 `.login` 中的行数（-l） |

| `>` | `ps -ef > /tmp/processes` | 标准输出重定向：执行 `ps` 并将输出发送到文件 `/tmp/processes` |

| `>>` | `ps -ef >> /tmp/processes` | 追加标准输出：执行 `ps` 并将输出追加到文件 `/tmp/processes` 的末尾 |

| `>`! | `ps -ef >! /tmp/processes` | 追加输出重定向并覆盖 `noclobber`：即使 `/tmp/processes` 存在也进行覆盖写入 |

| `>>`! | `ps -ef >>! /tmp/processes` | 追加标准输出并覆盖 `noclobber`：追加到 `/tmp/processes` 的末尾 |

| `|` (管道) | `ps | wc -l` | 运行 `ps` 并将其结果作为 `wc` 的输入。 |

| `0` - 标准输入 | | |

| `1` - 标准输出 | | |

| `2` - 标准错误 | `cat program 2> errors` | `cat` 文件 `program` 到标准输出，并将错误重定向到文件 `errors`。 |
