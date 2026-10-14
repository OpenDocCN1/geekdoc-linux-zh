

要获得更详细的列表，我们可以添加 v（verbose）选项：

```bash
[me@linuxbox ~]$ tar tvf playground.tar
```

现在，让我们在新位置提取 playground。我们将通过创建一个名为 foo 的新目录、切换到该目录并解压 tar 归档来实现：

```bash
[me@linuxbox ~]$ mkdir foo
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ tar xf ../playground.tar
[me@linuxbox foo]$ ls
playground
```

如果我们检查 ~/foo/playground 的内容，就会发现归档已成功安装，创建了原始文件的精确复制品。然而有一个需要注意的地方：除非你以超级用户身份运行，否则从归档中提取的文件和目录会归执行恢复操作的用户所有，而不是原始所有者。

tar 的另一个有趣行为是它处理归档中路径名的方式。路径名的默认形式是相对的，而不是绝对的。tar 在创建归档时只是简单地删除路径名前导的斜杠。为了演示这一点，我们将重新创建我们的归档，这次指定一个绝对路径名：

```bash
[me@linuxbox foo]$ cd
[me@linuxbox ~]$ tar cf playground2.tar ~/playground
```

请记住，~/playground 在我们按下回车键时会展开为 /home/me/playground，因此我们将为演示获得一个绝对路径名。接下来，我们将像之前一样解压归档并观察会发生什么：

```bash
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ tar xf ../playground2.tar
[me@linuxbox foo]$ ls
home  playground
[me@linuxbox foo]$ ls home
me
[me@linuxbox foo]$ ls home/me
playground
```

在这里我们可以看到，当我们解压第二个归档时，它相对于我们当前的工作目录 ~/foo 重新创建了目录 home/me/playground，而不是相对于根目录，就像使用绝对路径名时那样。这看起来可能是一种奇怪的工作方式，但实际上这样更有用，因为它允许我们将归档提取到任何位置，而不是被迫提取到其原始位置。重复该练习并加上 verbose 选项（v）将更清晰地显示正在发生的事情。

让我们考虑一个假设的、但实用的 tar 使用示例。想象一下，我们想将 home 目录及其内容从一台系统复制到另一台系统，并且我们有一个大容量的 USB 硬盘可用于传输。在我们的现代 Linux 系统上，该驱动器会被“自动”挂载到 /media 目录。让我们再假设当我们连接它时，磁盘的卷名为 BigDisk。要创建 tar 归档，我们可以这样做：

```bash
[me@linuxbox ~]$ sudo tar cf /media/BigDisk/home.tar /home
```

tar 文件写入后，我们卸载驱动器并将其连接到第二台计算机。同样，它被挂载在 /media/BigDisk。要解压归档，我们这样做：

```bash
[me@linuxbox2 ~]$ cd /
[me@linuxbox2 /]$ sudo tar xf /media/BigDisk/home.tar
```

这里重要的是要看到，我们必须先切换目录到 /，以便解压相对于根目录进行，因为归档中的所有路径名都是相对的。

在解压归档时，可以限制从归档中解压的内容。例如，如果我们只想从归档中解压单个文件，可以这样做：

```bash
tar xf archive.tar pathname
```

通过在命令末尾添加路径名，tar 只会恢复指定的文件。可以指定多个路径名。请注意，路径名必须是存储在归档中的完整、精确的相对路径名。在指定路径名时，通常不支持通配符；然而，GNU 版本的 tar（这是 Linux 发行版中最常找到的版本）使用 --wildcards 选项支持它们。下面是使用我们之前的 playground.tar 文件的一个示例：

现代版本的 GNU tar 直接支持 gzip 和 bzip2 压缩，分别使用 z 和 j 选项。以我们之前的示例为基础，我们可以这样简化它：

```bash
[me@linuxbox ~]$ find playground -name 'file-A' | tar czf playground.tgz -T -
```

如果我们想创建 bzip2 压缩的归档而不是 gzip，可以这样做：

```bash
[me@linuxbox ~]$ find playground -name 'file-A' | tar cjf playground.tbz -T -
```

只需将压缩选项从 z 改为 j（并将输出文件的扩展名改为 .tbz 以表示 bzip2 压缩文件），我们就启用了 bzip2 压缩。

tar 命令与标准输入和输出的另一个有趣用法涉及通过网络在系统之间传输文件。想象一下，我们有两台运行 Unix-like 系统的机器，它们都配备了 tar 和 ssh。在这种情况下，我们可以将目录从远程系统（本例中命名为 remote-sys）传输到本地系统：

```bash
[me@linuxbox ~]$ mkdir remote-stuff
[me@linuxbox ~]$ cd remote-stuff
[me@linuxbox remote-stuff]$ ssh remote-sys 'tar cf - Documents' | tar xf -
me@remote-sys’s password:
[me@linuxbox remote-stuff]$ ls
Documents
```

在这里，我们能够将名为 Documents 的目录从远程系统 remote-sys 复制到本地系统上名为 remote-stuff 的目录中的目录。我们是如何做到这一点的？首先，我们使用 ssh 在远程系统上启动 tar 程序。你会记得 ssh 允许我们在网络计算机上远程执行程序并在本地系统上“查看”结果——远程系统上产生的标准输出会被发送到本地系统进行查看。我们可以利用这一点，让 tar 创建一个归档（c 模式）并将其发送到标准输出，而不是文件（f 选项的连字符参数），从而通过 ssh 提供的加密隧道将归档传输到本地系统。在本地系统上，我们执行 tar 并让它从标准输入扩展归档（x 模式）。

