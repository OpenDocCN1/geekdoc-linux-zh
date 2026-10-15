
`000 500 3330 2697 0 76 0      744      pts/0 00:00:00 ps`

`-u`选项显示了关于进程的各种类型信息，包括你大部分的 CPU 和内存使用情况：

```
# $ ps -u
```

```
USER PID %CPU %MEM VSZ RSS TTY STAT START COMMAND

alex 2697 0.0 0.5 2556 1460 pts/0 S Jul31 00:02 -bash

alex 3330 0.0 0.2 2476 616 pts/0 S Jul31 00:00 -ps
```

`--forest`选项导致`ps`将主页显示为“ASCII 进程树”。它将其他进程的子进程缩进在其父进程下，使得进程层次结构和树更容易查看：

```
# $ ps -ef --forest
```

```
UID PPID C STIME TTY TIME CMD

root 1 0 Jul22 ? 00:00:00 init

root 2 0 Jul22 ? 00:00:00 [kevent]

root 785 1 0 Jul22 ? 00:00:00 /usr/bin/apmd -p 10 -w 5 -W -P

alex 839 1 0 Jul22 ? 00:00:01 /usr/bin/sshd

root 3305 8 0 Aug01 ? 00:00:01 /usr/bin/sshd

alex 3307 8 0 Aug01 ? 00:00:00 /usr/bin/sshd

alex 3308 8 0 Aug01 ? 00:00:00 -bash

alex 3774 3 0 Aug01 ? 00:00:00 -ps -ef --forest

root 1040 1 0 Jul22 ? 00:00:00 login --root

root 3351 1 0 Aug02 ? 00:00:00 -bash

root 3402 3 1102 ?  00:00:00 -bash
```

# `rcp`

向远程计算机或从远程计算机复制一个多个文件
`rcp [options] source-file destination-file`
`rcp [options] source-file-list destination-directory`

`rcp`工具在可以通过网络通信的两台计算机之间复制文件。和`cp`一样，`rcp`有两种模式：第一个将一个文件复制到另一个，第二个将一个或多个文件复制到目录。

# `rcp`不安全

`rcp`工具使用基于主机的信任（这是不安全的）来授权复制文件。请参考第373页的“信任主机”。可用时使用`scp`(`1308`)。

`source-file`、`source-file-list`和`destination-file`是普通文件的路径，而`destination-directory`是目录的路径。不包含冒号(`:`)的路径是本地文件的名称。格式为`name@host:path`的路径指定远程计算机上的文件。路径相对于用户的家目录（除非`path`是绝对路径）。当你省略目标中的`name@`部分时，相对路径相对于执行`rcp`命令的用户家目录。

`source[-list]`是`rcp`将要复制的文件名；`destination-file`是`rcp`为生成的副本指定的名称，或者`destination-directory`是`rcp`存放复制文件的目录名称。当`rcp`将文件复制到`destination-directory`时，文件保持原始文件名。

# 参数

+ `-p`保留每个副本的修改时间和文件访问权限，以与`source-file`。如果不使用`-p`，`rcp`使用远程系统的文件创建掩码（`umask`，第366页）来修改访问权限。

+ `-f`递归 当`source-file-list`中的文件是目录时，此选项将该目录的内容及其任何子目录复制到`destination-directory`中。只有在目标是目录时才能使用此选项。

# 注意事项

你必须在远程计算机上拥有登录账户，才能使用`rcp`向或从远程计算机拷贝文件。`rcp`工具不会提示密码，而是使用几种备选方法来验证你是否有权限在远程系统上读取或写入文件。一种常用的方法要求在远程计算机的`/etc/hosts.equiv`文件中指定你本地计算机的名称。如果你的计算机名称在该文件中，只要你在两台计算机上的登录名相同，且你在远程计算机上的账户具有访问文件所需的必要权限，`rcp`就会允许你拷贝文件。权限也可以按用户进行指定：远程用户的家目录必须包含一个名为`.hosts`的文件，其中列出了远程系统和用户。使用第二种方法时，你的本地和远程用户名可以不匹配，但你的本地用户名必须出现在远程`.hosts`文件中以你本地机器名称开头的行中。有关更多细节，请参阅第1306页关于`rsh`的描述。

如果你在远程路径中使用通配符（如`*`），你必须对通配符字符或路径加引号，这样通配符就会由远程计算机的`shell`解释，而不是由本地`shell`解释。与`cp`一样，如果在执行`rcp`之前目标文件已存在，`rcp`将覆盖该文件。

# 示例

第一个示例将所有以`.c`结尾的文件拷贝到远程计算机上名为`bravo`的目录。由于没有指定存档文件的完整路径，`rcp`假设它是用户家目录到`bravo`的子目录。每个被拷贝的文件保留了其简单文件名。

```
$ rcp *.c bravo:archives
```

下一个示例将`memo`从`/home/jenny`目录拷贝到`bravo`，然后拷贝到本地计算机的工作目录中：

```
$ rcp bravo:/home/jenny/memo .
```

接下来的命令将两个名为`memo.new`和`letter`的文件拷贝到远程计算机`bravo`上 Jenny 的家目录。拷贝文件在`bravo`绝对路径为`/home/jenny/memo.new`和`/home/jenny/letter`：

```
$ rcp memo.new letter bravo:/home/jenny
```

最后一个命令将`bravo`上 Jenny 的`reports`目录中的所有文件拷贝到本地计算机的`oldreports`目录，并保留副本的原始修改日期和文件权限：

```
$ rcp -p 'bravo:reports/*' oldreports
```
