
```
darkstar:~$ ls -l /bin | more

        total 1611
        -rwxr-xr-x   1 root    bin            1248 Sep 17 04:25 arch*
        -rwxr-xr-x   1 root    bin          295940 Sep  5 01:45 bash*
        -rwxr-xr-x   1 root    bin           4840 Nov 24  1993 cat*
        -rwxr-xr-x   1 root    bin           9220 Jul 20 12:06 chgrp*
        -rwxr-xr-x   1 root    bin          13316 Jul 20 12:06 chmod*
        -rwxr-xr-x   1 root    bin          13316 Jul 20 12:06 chown*
        lrwxrwxrwx   1 root    root              17 Dec  7 13:37 compress ->
        /usr/bin/compress
        -rwxr-xr-x   1 root    bin           21508 Jul 20 12:06 cp*
        -rwxr-xr-x   1 root    bin          41988 May  1  1994 cpio*
        lrwxrwxrwx   1 root    root               4 Dec  7 13:40 csh -> tcsh
        -rwxr-xr-x   1 root    bin           5192 Nov 24  1993 cut
        -rwxr-xr-x   1 root    bin          19872 Mar 23  1994 date
        -rwxr-xr-x   1 root    bin          17412 Jul 20 12:06 dd
        -rwxr-xr-x   1 root    bin          13316 Jul 20 12:06 df
        -rwxr-xr-x   1 root    bin          66564 Jun  9  1994 dialog*
        -rwxr-xr-x   1 root    bin           1752 Sep 17 04:25 dmesg
        lrwxrwxrwx   1 root    root               8 Dec  7 13:37 dnsdomainname -> hostname
        -rwxr-xr-x   1 root    bin          13316 Jul 20 12:06 du
        -rwxr-xr-x   1 root    bin           3312 Mar 23  1994 echo
        -rwxr-xr-x   1 root    bin          36684 May  4  1994 ed
        -rwxr-xr-x   1 root    bin            326 Mar 23  1994 false
        --More--
```

屏幕底部的 `--More--` 告诉你还有更多内容。要转到下一屏文本，请按下空格键。每次按下空格键，`more` 都会显示另一屏文本。当最后一屏文本显示完毕后，`more` 会返回 Linux 提示符。

> **提示**
>
> `more` 命令还可以做很多其他事情。例如，要一次向前移动一屏，请按下 `b` 键表示“back”（后退）。（并非所有版本的 `more` 都支持 `b` 选项。）另一个有用的命令是 `q` 键，表示“quit”（退出）。这让你可以立即离开，而无需遍历所有剩余的文本屏幕。`Ctrl+C` 也能做到同样的事情。
>
> 在 `more` 中，按下 `h` 键获取“help”（帮助）。这会列出 `more` 内部可用的命令。

### 注意

Linux 有时包含命令 `less` 而不是 `more`。你会注意到的一个区别是，与 `more` 不同，`less` 要求你输入 `q` 才能返回命令行，即使你处于待显示文本的末尾也是如此。这可能会显得繁琐，但它防止你因多次按空格键而意外退出程序。

名称 `less` 是对 `more` 的戏仿。最初，`less` 被设计为拥有许多 `more` 缺乏的功能。然而，大多数 Linux 系统包含的 `more` 版本已经具备了这些功能中的大部分。

稍后将讨论的 Linux `man` 程序使用 `less` 来显示文本。大多数其他 UNIX 系统默认使用 `more`。不要混淆。只需记住按 `q` 键从 `less` 中退出！

你可以在 Linux 中做的另一件事是将输出发送到文件而不是屏幕。你之所以想要这样做有很多不同的原因。也许你想保存命令输出在某个时刻的“快照”，或者你想保存命令的输出以便进一步检查。你也可能想保存运行时间很长的命令的输出，等等。

要将输出发送到文件，请使用 `>` 符号（位于键盘上的句号上方）。例如，你可以输入 `ls -l /bin > output`，将 `ls -l /bin` 命令的输出放入名为 `output` 的文件中。同样，`>` 周围的空格是可选的，也不是严格必需的，但它们确实使命令更易于阅读。

如果你现在输入 `ls` 或 `ls -l` 命令，你会发现你已经在自己的目录中创建了一个名为 `output` 的新文件。

要查看文件内容，你可以再次使用 `more` 命令。只需指定你要查看的文件名即可。在这种情况下，输入 `more output`。

# 警告

小心！当你使用 `>` 时，你指定的输出文件（如果该文件存在）的先前内容会被完全覆盖。例如，如果我们目录中已经有一个名为 `output` 的文件，其旧内容将被 `ls -l /bin` 的输出完全替换。Linux 不会警告你即将这样做！

> 如果你不在通常的目录中，或者你是以 root 身份登录的，请特别小心。例如，你可能不小心覆盖了一个 Linux 程序。在使用 `>` 之前检查输出文件是否已存在是个好主意。在我们的示例中，我们可以事先输入 `ls -l output`。如果没有显示信息，则该文件不存在。

你可以使用 `>>` 指定将输出添加到文件末尾，而不是替换文件内容。输入 `who >> output` 将 `who` 命令的输出添加到文件 `output` 中已有的文本末尾。

你可以使用 `more` 或 `less` 翻页到文件末尾，或使用 Linux 命令 `tail` 来检查结果，该命令显示指定文件的最后几行。在这种情况下，输入 `tail output` 以查看文件 `output` 的最后几行。试试使用 `tail`！

## 用于描述 Linux 命令的符号约定

有一套被接受的符号约定，用于以简洁且一致的方式描述任何给定 Linux 命令的正确语法。这规定了你必须使用哪些选项或参数，你可以或不可以使用哪些选项或参数，等等。有时这套约定用于给出命令语法的完整且详尽的列表，显示每个可能的命令和参数。有时它用于使特定示例更通用，并使命令的基本用法更清晰。你将在手册、man 页面和其他信息来源中遇到这些符号表示。

如果你记住以下五条基本规则，原则上你将能够理解任何 Linux 或 UNIX 命令的语法。

### Linux 符号表示的六条基本规则

1. 任何独立存在且不在 `[ ]`、`< >` 或 `{ }` 内部的文本，必须按照显示的样子准确输入。
2. 方括号 `[]` 内的任何文本都是可选的。你可以输入它，也可以不输入它。例如，语法 `ls [-1]` 意味着你必须输入 `ls`（根据第一条规则），而添加 `-1` 是可选的但不必要。不要输入方括号本身！在我们的示例中，输入 `ls` 或 `ls -1`。不要输入 `ls [-1]`。

## Linux 中的在线帮助

Linux 提供了在线帮助设施。如果你忘记了某个命令的确切用法，不确定某个选项的含义，或者在寻找合适的命令，答案可能直接来自 Linux 本身。我们将尝试使用的两种帮助设施是 `bash` shell 的 `help` 命令和 `man` 命令，后者几乎在所有 UNIX 系统（包括 Linux）上都可用。

### Linux man 手册页

"man pages"（man 手册页）中的 "man" 代表 "manual"（手册）。（一如既往，UNIX 的创造者将一个冗长但描述性强的词缩短为一个简短而晦涩的词！）输入 `man <command>` 可以让你查看关于特定命令的手册页。

尝试输入 `man passwd`，查看 Linux 手册对 `passwd` 命令的描述。

man 手册页的一般布局如下：
