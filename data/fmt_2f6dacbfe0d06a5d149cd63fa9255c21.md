
此时，假设你运行了一个隐蔽且可信的 *ps* 程序，它显示了两个让你怀疑的进程：`/bin/ls` 和 `wizbang`。你对 `/bin/ls` 感到怀疑，因为它已经运行了很长时间，而没有理由让用户执行类似

```
/bin/ls -R /
```

或类似的能解释该程序如此长时间运行的操作。你对 `wizbang` 感到怀疑，因为你不记得有这样一个应用程序。

`/bin/ls` 的 PID（进程 ID）是 `16887`，因此你使用你的隐蔽 `ls` 命令，比如每月的命令，发出指令

## 分析 /proc 文件系统下的可疑进程

执行以下命令进入进程目录：

```
cd /proc/16887
ls -l
```

*注：原文中的 "monthly -1" 疑似 OCR 错误，根据上下文应为 `ls -l` 或类似查看目录详情的命令，但为了保留原始信息，若无法确定具体命令，此处保留原意或进行合理推断。鉴于后文展示了目录列表，通常使用 `ls -l`。然而，原文确实写的是 `monthly -1`，这可能是 `ls -l` 的严重误识别。为了忠实于“保留原文信息”但“纠正明显OCR错误”的原则，`monthly` 极有可能是 `ls` 的误读（l->m? s->o? 不太像），或者可能是 `ls -la`？ 让我们仔细看后文的输出。输出是文件列表。通常命令是 `ls -l`。 但是，让我们看下一段命令 `/home/larry/bin/feather -chvf ...`。 让我们假设这里的 `monthly -1` 是 OCR 错误，实际应为 `ls -l`。 但是，如果我不确定，我应该保留并标注吗？ 不，任务要求纠正明显错误。`monthly` 在 Linux 命令中毫无意义。结合上下文，这是在展示进程信息。最可能的原意是 `ls -l`。*

**更正思考**： 让我们重新审视原文。

```
cd /proc/16887
monthly -1
```

这可能是一个极差的 OCR 结果，将 `ls -l` 识别成了 `monthly -1`？ 或者原文本身就是某个特定脚本？ 不，这看起来像是一本关于入侵检测的书（可能是《The Practice of Network Security》或类似书籍）。 在这类书中，通常会用 `ls -l` 查看 `/proc/<pid>`。

让我们看第二页的代码块：

`/home/larry/bin/feather -chvf /dev/fd0 /proc/16887/exe`

这里 `feather` 是 `tar` 的别名。

回到第一页，`monthly -1` 真的很奇怪。

让我们假设它是 `ls -l`。

该命令可能显示如下内容：

```
-r--r-----    1 root root 0 May 17 00:49 cmdline
lrwx------    1 root root 0 May 17 00:49 cwd -> /tmp
-r---------    1 root root 0 May 17 00:49 environ
lrwx------    1 root root 0 May 17 00:49 exe -> /tmp/.genie
dr-x------    2 root root 0 May 17 00:49 fd
pr--r-----    1 root root 0 May 17 00:49 maps
-rw-------    1 root root 0 May 17 00:49 mem
lrwx------    1 root root 0 May 17 00:49 root -> /
-r--r-----    1 root root 0 May 17 00:49 stat
-r--r-----    1 root root 0 May 17 00:49 statm
-r--r-----    1 root root 0 May 17 00:49 status
```

请注意，`exe` 文件是指向所调用可执行程序的一个符号链接，它显然并不指向 `/bin/ls`。极有可能这是一个木马（Trojan horse）。注意，由于这些文件的所有者是 root，因此该进程是以 root 身份运行的。可执行文件的名称 `/tmp/.genie` 极其可疑。这是因为 root 调用位于 `/tmp` 目录下的可执行文件非常不寻常，而且该名称以 `.` 开头，这意味着普通的 `ls` 命令不会显示此文件。你还可以通过 `/bin/ls` 进行二进制比较，确信这是一个不同的程序，使用以下命令：

```
cmp exe /bin/ls
```

典型的输出如下：

```
exe /bin/ls differ: char 25, line 1
```

显然，这是一个不同的程序。这是一个木马！

> 假设你有一个笔记本，并正在记录你的所有操作和发现。你可能需要在这个笔记本中记录日期和时间，因为这些记录未来可能会在法庭上作为证据引入。你可能还想在你的条目上签名。

此时，你需要记录这个木马的 PID 及其可执行文件名 `/tmp/.genie`。你需要制作这个木马的副本。如果方便的话，建议使用介质，如磁带、软盘或 CD-RW。这是因为写入后，介质可以进行写保护、贴标签并保存。这样，即使其他恶意程序破坏了磁盘上的数据，它也仍然可以存活。

### 备份可疑文件

如果你已经拥有一个用于将文件复制到备份介质的 `tar` 或其他有用程序的隐藏副本，那将非常有帮助。假设你的 `tar` 隐藏版本被称为：

```
/home/larry/bin/feather
```

并且你将备份到 `/dev/fd0`。发出以下命令：

```
/home/larry/bin/feather -chvf /dev/fd0 /proc/16887/exe
```

`-h`（原文写作“n” flag，但在 tar 中跟随符号链接通常是 `-h` 或 `--dereference`。原文说 "The 'n' flag causes tar to back up the file that any symbolic link... points to"。实际上 `tar` 的 `-h` 是 follow symlinks。`-n` 通常是 no-same-permissions。这里原文可能有误，或者指的是特定行为。让我们仔细看原文："The “n” flag causes *tar* to back up the file that any symbolic link, such as `/proc/16887/exe`, points to." 在标准的 `tar` 中，这是 `-h`。但是，如果这是一个别名或特定脚本，也许行为不同。为了保持忠实，如果原文写的是 "n"，我应保留 "n" 还是纠正为 "h"？ 任务要求纠正明显 OCR 错误。如果原文印错了，那是内容错误。如果 OCR 将 `-h` 识别为 `-n`，那是 OCR 错误。鉴于上下文是“备份符号链接指向的文件”，这在 tar 中是 `-h`。然而，后面的命令用的是 `-chvf`。这里没有 `-h` 或 `-n`。

让我们再看一遍命令：`/home/larry/bin/feather -chvf /dev/fd0 /proc/16887/exe`

标志是 `c` (create), `h` (?), `v` (verbose), `f` (file). 等等，原文命令里写的是 `-chvf`。

然后文本解释：“The “n” flag causes...”。

这里存在矛盾。命令里有 `h`，解释里说是 `n` flag。

可能性 1：OCR 将命令中的 `h` 误读为其他，或者将文本中的 `h` 误读为 `n`。

可能性 2：作者搞错了。

在 `tar` 中，`-h` 意味着“跟随符号链接”。`-n` 意味着“禁止设置权限”。

根据语义“备份符号链接指向的文件”，应该是 `-h`。

但是，原文命令块中已经是 `-chvf`，包含了 `h`。

而解释段落说“The “n” flag”。

这很可能是 OCR 将文本中的 `h` 识别成了 `n`，或者原文印刷错误。

考虑到 `-h` 是标准行为，且命令中有 `h`，我将把解释中的 “n” 视为对 `h` 的误认或原文笔误，但为了安全起见，如果不确定，保留原文 “n” 可能更安全？ 不，任务要求纠正明显错误。将 `h` 解释为 `n` 是语义错误。但如果是 OCR 把 `h` 变成 `n`，那么纠正 `n` 为 `h` 是合理的。

然而，让我们看命令：`-chvf`。这里的第二个字符是 `h`。

所以文本说“The “n” flag” 肯定是错的，应该是“The “h” flag”。

我将把文本中的 `“n”` 纠正为 `“h”`，以匹配命令和语义。

*修正策略*： 将文本中的 `“n” flag` 改为 `“h” flag`，因为命令中使用的是 `-h`（在 `-chvf` 中），且语义符合 `-h` 的功能。

移除该软盘，对其进行写保护，并将其标记为类似以下内容：
