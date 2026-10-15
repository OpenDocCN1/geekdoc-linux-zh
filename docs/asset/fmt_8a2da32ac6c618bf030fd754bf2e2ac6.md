
在 UNIX 系统上，大部分编辑工作都是使用 `vi` 完成的。由于 `vi` 作为 UNIX 编辑器的突出地位，我在本书中专门为其开辟了一章。很多时候，当我们需要编辑文件时，并没有调用 `vi` 的“奢侈”条件。你可能正在编写 shell 程序或在进程之间通过管道传递信息，需要以非交互方式编辑。`sed` 在这里可以派上用场。它的名字源于*流编辑器*（stream editor），它是用于过滤文本文件的工具。

你可以使用 `sed` 指定要编辑的文件名，或者让它从标准输入获取数据。`sed` 一次读取一行，并对每一行执行你指定的编辑操作。你也可以为 `sed` 指定特定的行号进行编辑。

`sed` 使用许多与 `ed` 相同的命令。你可以在 `vi` 章节中查看其中的一些 `ed` 命令，我也在本 `sed` 章节末尾提供了这些命令的摘要。让我们看几个使用 `sed` 可以执行的操作的简单示例。

使用 `passwd.test` 文件，让我们先查看完整文件，然后使用 `p` 命令仅查看第 16、17 和 18 行。

```
# cat passwd.test
root:PGyQCKVH6ShY0:0:0:root:/root:/bin/bash
bin:4:1:bin:/bin:
daemon:4:2:2:daemon:/sbin:
adm:4:3:4:adm:/var/adm:
lp:4:4:7:lp:/var/spool/lpd:
sync:5:0:sync:/sbin:/bin/sync
shutdown:4:6:11:shutdown:/sbin:/sbin/shutdown
halt:4:7:0:halt:/sbin:/sbin/halt
mail:4:8:12:mail:/var/spool/mail:
news:4:9:13:news:/var/spool/news:
uucp:4:10:14:uucp:/var/spool/uucp:
operator:4:11:0:operator:/root:
games:4:12:100:games:/usr/games:
gopher:4:13:30:gopher:/usr/lib/gopher-data:
ftp:4:14:50:FTP User:/home/ftp:
man:4:15:15:Manualls Owner:/:/
nobody:4:65534:65534:Nobody:/:/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col/bin/bash
#
# sed 16,18p passwd.test
root:PGyQCKVH6ShY0:0:0:root:/root:/bin/bash
bin:4:1:1:bin:/bin:
daemon:4:2:2:daemon:/sbin:
adm:4:3:4:adm:/var/adm:
lp:4:4:7:lp:/var/spool/lpd:
sync:5:0:sync:/sbin:/bin/sync
shutdown:4:6:11:shutdown:/sbin:/sbin/shutdown
halt:4:7:0:halt:/sbin:/sbin/halt
mail:4:8:12:mail:/var/spool/mail:
news:4:9:13:news:/var/spool/news:
uucp:4:10:14:uucp:/var/spool/uucp:
operator:4:11:0:operator:/root:
games:4:12:100:games:/usr/games:
gopher:4:13:30:gopher:/usr/lib/gopher-data:
ftp:4:14:50:FTP User:/home/ftp:
man:4:15:15:Manualls Owner:/:/
nobody:4:65534:65534:Nobody:/:/bin/false
nobody:4:65534:65534:Nobody:/:/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col/bin/bash
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col/bin/bash
#
# sed -n 16,18p passwd.test
man:4:15:15:Manualls Owner:/:/
nobody:4:65534:65534:Nobody:/:/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col/bin/bash
```

![](img/75f39fc91296b889c0653851accdfd46_626_0.png)

![](img/75f39fc91296b889c0653851accdfd46_626_1.png)

第一次尝试仅打印第 16、17 和 18 行时，结果打印了文件中的所有行，并且第 16、17 和 18 行被打印了两次。原因是 `sed` 读取每一行输入并对每一行进行操作。为了指定要操作的行，我们使用了 `-n` 开关来抑制所有行输出到标准输出。然后我们指定要打印的行，这些行确实会被发送到标准输出。

既然我们已经知道如何查看文件第 16、17 和 18 行，让我们再次查看 `passwd.test` 并使用 `d` 命令删除这三行：

![](img/75f39fc91296b889c0653851accdfd46_627_0.png)

```
# cat passwd.test
root::PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
bin:::1:1:bin:/bin:
daemon:::2:2:daemon:/sbin:
adm:::3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/sbin/bin/sync
shutdown:7:6:11:shutdown:/sbin:/sbin/shutdown
halt:::7:0:halt:/sbin:/sbin/halt
mail:::8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
uucp:::10:14:uucp:/var/spool/uucp:
operator:*:11:0:operator:/root:
games:::12:100:games:/usr/games:
gopher:::13:30:gopher:/usr/lib/gopher-data:
ftp::*:14:50:FTP User:/home/ftp:
man:::15:15:ManuLs  Owner:/:
nobody:::65534:65534:Nobody::/bin/false
col:Why0yzfAV2gqM2Y:100:100:Caldera OpenLinux User:/home/col:/bin/bash
#
# sed 16,18d passwd.test
root::PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
bin:::1:1:bin:/bin:
daemon:::2:2:daemon:/sbin:
adm:::3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/sbin/bin/sync
shutdown:7:6:11:shutdown:/sbin:/sbin/shutdown
halt:::7:0:halt:/sbin:/sbin/halt
mail:::8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
uucp:::10:14:uucp:/var/spool/uucp:
operator:*:11:0:operator:/root:
games:::12:100:games:/usr/games:
gopher:::13:30:gopher:/usr/lib/gopher-data:
ftp:*:14:50:FTP User:/home/ftp:
```

![](img/75f39fc91296b889c0653851accdfd46_627_1.png)

![](img/75f39fc91296b889c0653851accdfd46_627_2.png)

正如我们之前 `grep` 示例中那样，我们将特殊字符用单引号括起来，以确保它们不受干扰，并原封不动、未经 shell 解释地直接传递给 `sed`。在此示例中，我们指定要删除的行范围，从 16 到 18，以及用于删除的 `d`。我们可以指定仅删除一行（例如第 16 行），而不指定整个范围。由于我们没有在 `sed` 命令行中重定向输出，结果会被发送到标准输出。原始文件保持完整不变。
