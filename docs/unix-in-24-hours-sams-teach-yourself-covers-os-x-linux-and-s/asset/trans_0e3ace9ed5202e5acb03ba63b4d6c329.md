

difference.

不出所料，目录除了两个默认条目外是空的。(目录本身) 和 .. (父目录，即你的主目录)。

**4.** 仔细查看目录的权限。请记住，默认目录权限是你的 `umask` 设置的结果。正如你在上一小时所学到的，改变 `umask` 设置会改变默认目录权限。然后，当你创建一个新目录时，新的权限就会生效：

[点击此处查看代码图片](#)

```
❯ umask
07
❯ umask 0
❯ mkdir NEWDIR2
❯ ls -ld NEWDIR2
drwxrwxrwx  2 taylor        24 Nov  5 10:53 NEWDIR2
❯ umask 222
❯ mkdir NEWDIR3
❯ ls -ld NEWDIR3
dr-xr-xr-x  2 taylor        24 Nov  5 10:54 NEWDIR3
```

**5.** 如果你尝试使用一个已经被使用的名称创建目录会发生什么？

❯ `mkdir NEWDIR`
`mkdir: NEWDIR: File exists`

**6.** 要在当前位置之外创建目录，请在新目录名前加上位置：

[点击此处查看代码图片](#)

```
❯ mkdir /tmp/testme
❯ ls -l /tmp
-rwx--  1 zhongqi     22724 Nov  4 21:33 /tmp/a.out
-rw----  1 xujia       95594 Nov  4 23:10 /tmp/active.10122
-rw-r--r-- 1 beast         572 Nov  5 05:59 /tmp/anon1
-rw-rw-rw- 1 root            0 Nov  5 10:30 /tmp/bar.report
-rw---  1 qsc             0 Nov  5 00:18 /tmp/lh013813
-rwx---  1 steen       24953 Nov  5 10:40 /tmp/mbox.steen
-rw---  1 techman      3711 Nov  5 10:45 /tmp/mbox.techman
-rw-r--r-- 1 root        99756 Nov  5 10:58 /tmp/quotas
-rw---  1 zhongqi    163579 Nov  4 20:16 /tmp/sp500.1
drwxrwxrwx 2 taylor        24 Nov  5 10:56 testme
-drwxr-- 1 aru           90 Nov 5 02:55 /tmp/trouble21972
```

大多数 Unix 变体对 `mkdir` 没有参数，因此使用起来非常简单。某些变体，如 Oracle Solaris，提供一个或多个标志，最常见的是 `-m` mode 用于显式指定权限而不是留给 `umask` 设置，以及 `-p` 用于让 `mkdir` 在其操作过程中创建所需的任何中间目录。请记住两点：如果你要创建新目录，必须对当前目录具有写权限，并且应确保目录名称与已存在的目录名称不同（或为避免混淆，名称不要相似）。

# Task 6.2: 使用 cp 复制文件到新位置

在任何系统中，最基本的操作之一就是移动文件，这相当于现代办公室计算机中的纸张整理。在计算机上，移动文件只是一个使用一两个命令的简单问题：你可以将文件移动到不同位置，或者你可以复制文件并将副本移动到不同位置。

Windows 和 Mac OS X GUI 对区分移动和复制有一种有趣的策略。如果你将文件拖到同一设备上的另一个位置（例如硬盘），默认情况下计算机将文件移动到该位置。如果你将文件拖到不同设备上的位置（例如从 USB 棒到硬盘），计算机会自动复制文件，将新命名的副本放置在新设备上，同时保留旧副本。

Unix 缺乏这种细微差别（或，取决于你的观点，行为不一致）。相反，Unix 让你选择要执行哪两种操作中的一种。这两个命令通常是简洁的 Unix 助记符：mv 用于移动文件，cp 用于复制文件。mv 命令还具有双重用途，可让你重命名文件。

# Note

将 cp 发音为“sea-pee”。然而，当你谈论复制文件时，说“copy”。同样，将 mv 发音为“em-vee”，但当你谈论移动文件时，说“move”。

我发现自己使用 cp 比 mv 更频繁，因为它提供了一种稍微更安全的文件组织方式：如果我困惑并重命名文件以至于覆盖了另一个文件（你很快就会明白我的意思），我仍然拥有所有文件的原始副本。

- 1. 对于 cp 命令，先指定要复制的文件名，然后指定新文件名。两个名称都可以是相对文件名（即，没有前导斜杠或其他目录指示）或绝对文件名。先从复制你的 .login 文件开始，并将新副本命名为 login.copy，或者，如果你没有 .login，则改用你的 .profile 文件执行相同操作：

点击此处查看代码图片

```
% cp .login login.copy
% ls -ld .login login.copy
-rw--- 1 taylor 1858 Oct 12 21:20 .login
-rw--- 1 taylor 1858 Nov 5 12:08 login.copy
```

你可以看到新文件在大小和权限上是相同的，但它具有更近的创建日期，这当然是有道理的。

- 2. 如果你尝试复制一个目录会发生什么？

点击此处查看代码图片

```
% cp olddir newdir
cp: olddir: Is a directory (not copied).
```

通常，Unix 不允许你使用 cp 命令复制目录。

