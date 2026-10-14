

虽然我们之前使用 gzip 程序在外部生成压缩归档，但现代版本的 GNU tar 支持使用 z 和 j 选项直接进行 gzip 和 bzip2 压缩。以之前的示例为基础，我们可以这样简化它：

```
[me@linuxbox ~]$ find playground -name 'file-A' | tar czf playground.tgz -T -
```

如果我们想创建 bzip2 压缩的归档，可以这样做：

```
[me@linuxbox ~]$ find playground -name 'file-A' | tar cjf playground.tbz -T -
```

只需将压缩选项从 z 改为 j（并将输出文件的扩展名改为 .tbz 以表示 bzip2 压缩文件），我们就启用了 bzip2 压缩。

tar 命令的另一个有趣用法涉及通过标准输入和标准输出在网络上在系统之间传输文件。假设我们有两台运行 Unix-like 系统的机器，它们都配备了 tar 和 ssh。在这种情况下，我们可以将目录从远程系统（本例中命名为 remote-sys）传输到本地系统：

```
[me@linuxbox ~]$ mkdir remote-stuff
[me@linuxbox ~]$ cd remote-stuff
[me@linuxbox remote-stuff]$ ssh remote-sys 'tar cf - Documents' | tar xf -
me@remote-sys's password:
[me@linuxbox remote-stuff]$ ls
Documents
```

在这里，我们能够将名为 Documents 的目录从远程系统 remote-sys 复制到本地系统上名为 remote-stuff 的目录中的一个目录。我们是如何做到的？首先，我们使用 ssh 在远程系统上启动 tar 程序。你会记得 ssh 允许我们在网络计算机上远程执行程序并在本地系统上“查看”结果——远程系统上产生的标准输出会被发送到本地系统进行查看。我们可以利用这一点，让 tar 创建一个归档（c 模式）并将其发送到标准输出，而不是发送到文件（f 选项带破折号参数），从而通过 ssh 提供的加密隧道将归档传输到本地系统。在本地系统上，我们执行 tar 并让它从标准输入（同样是 f 选项带破折号参数）展开归档。

## zip—打包和压缩文件

zip 程序既是压缩工具也是归档器。该程序使用的文件格式 Windows 用户很熟悉，因为它可以读取和写入 .zip 文件。在 Linux 中，gzip 是主要的压缩程序，bzip2 紧随其后。Linux 用户主要使用 zip 与 Windows 系统交换文件，而不是进行压缩和归档。

在最基本的用法中，zip 的调用方式如下：

```
zip options zipfile file...
```

例如，要制作我们 playground 的 zip 归档，我们会这样做：

```
[me@linuxbox ~]$ zip -r playground.zip playground
```

除非我们包含 -r 选项用于递归，否则只会存储 playground 目录本身（但不包含其内容）。虽然 .zip 扩展名的添加是自动的，但我们为了清晰起见会包含文件扩展名。

在创建 zip 归档期间，zip 通常会显示如下一系列消息：

```
adding: playground/dir-020/file-Z (stored 0%)
adding: playground/dir-020/file-Y (stored 0%)
adding: playground/dir-020/file-X (stored 0%)
adding: playground/dir-087/ (stored 0%)
adding: playground/dir-087/file-5 (stored 0%)
```

这些消息显示添加到归档中的每个文件的状态。zip 会使用两种存储方法之一将文件添加到归档中：要么“存储”文件而不进行压缩，如此处所示，要么“deflate”文件，这会执行压缩。存储方法后显示的数值表示实现的压缩量。由于我们的 playground 只包含空文件，因此其内容不会被压缩。

使用 unzip 程序提取 zip 文件的内容非常简单：

```
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ unzip ../playground.zip
```

关于 zip（与 tar 相反）需要注意的一点是，如果指定了现有归档，它会被更新而不是被替换。这意味着现有归档会被保留，但新文件会被添加，匹配的文件会被替换。

可以通过指定文件让 unzip 从 zip 归档中选择性地列出和提取文件：

```
[me@linuxbox ~]$ unzip -l playground.zip playground/dir-087/file-Z
Archive:  ./playground.zip
Length      Date    Time   Name
--------  ---------- -----  ----
-------- 0 10-05-12 09:25  playground/dir-087/file-Z
--------
        0                 1 file
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ unzip ../playground.zip playground/dir-087/file-Z
Archive:  ../playground.zip
replace playground/dir-087/file-Z? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
extracting: playground/dir-087/file-Z
```

