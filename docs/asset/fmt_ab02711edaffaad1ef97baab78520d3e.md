
8219 bytes received in 53 secs (196.5 KB/s)

`ftp>`

> 图 12.30 匿名登录下载软件包。

# 基于网络的工具 417

许多下载站点允许使用公共用户名和密码进行匿名 `ftp` 访问。

# 另一种在系统之间复制文件的方法是 `rcp`，它是 remote copy（远程复制）的缩写。`rcp` 功能和用法与第 4 章介绍的 `cp` 命令相似，但它是跨系统的。在本章前面的描述中（例如 `.hosts` 文件），已经描述了 `rcp` 的用法。要使用 `rcp`，你必须对远程系统有密码认证。

## 使用 `rcp` 发送文件

作为一个示例，`rcp` 用于从本地系统发送单个文件到名为 `othercomputer.somedomain.org` 的远程系统。本地系统上的文件是 `~/remote_to_UNIX/chap12/upload/mypic.tif`。你要访问的远程系统账户是 `joely`；位于主目录。图 12.31 展示了实现此操作的 `rcp` 命令。

```
book@mycomputer:~$ rcp Intro_to_UNIX/chap12/upload_files/mypic.tif joely@othercomputer.somedomain.org:
book@mycomputer:~$
```

> 图 12.31 使用 `rcp` 发送单个文件。

在 12.31 中，`rcp` 的第一个参数是你想要发送的文件名，这里使用相对路径指定。最后一个参数是发送文件的目的地。至少，目的地必须包含远程系统名称，当作为 `rcp` 参数使用时后面总是跟着一个冒号（:`）。如果你像图 12.31 所示在冒号后什么都不指定，`rcp` 将发送的文件放在远程系统账户的主目录下。如果你想将文件发送到远程系统的某个子目录，请在远程系统名称和冒号之后指定该子目录名称。同样，如果你发送单个文件并将副本置于不同的文件名，请在冒号后指定替代文件名（如果也指定了替代路径）。

# 418 UNIX/Linux 简介

> 使用 `cop`、`sep` 和 `rex` 时，不需要指定二进制和 ascii 传输模式。

同样注意图 12.31，通过在远程系统名称之前提供用户名和 @ 符号指定了远程系统的替代用户名（`joely`）。如果你希望在远程系统使用与本地系统相同的用户名，请省略远程系统名称之前的用户名和 @ 指定。

如果你希望用 `rep` 发送多个文件，请将额外的文件名作为第二、第三等参数。最后一个参数必须引用这些文件的目的地。图 12.32 显示了如何使用 `rep` 将多个文件发送到远程系统账户中的 `classwork` 子目录。为了方便使用此传输命令，先将工作目录更改为文件所在的子目录。

同样在图 12.32 中，指定了这些发送文件的目标子目录。最后注意，你可以替代使用通配符（如 `*.txt`）指定本地系统的文件。

```
508 book@computer:~$ cd intro_TO_UNIX/chap12/upload_files/
509 book@computer:~/Intro_to_UNIX/chap12/upload_files$ rep homework.txt notes.txt joely@othercomputer.somedomomain.org:classwork
510 book@computer:~/Intro_to_UNIX/chap12/upload_files$ 
```

> 图 12.32 使用 `rep` 向计数远程系统发送多个文件。

> 如果你不在远程系统上指定替代子目录和/或文件名，`rep` 和 `sep` 将文件传输到远程账户的主目录。

## 使用 `rep` 检索文件

要用 `rep` 检索单个文件，只需将第一个参数指定为远程系统加上想要检索的文件名。远程系统名称和文件名之间应用冒号分隔。最后一个参数指定本地系统上检索到的文件的目的地。在这里你可以使用 `.` 表示当前工作目录，或者如果你想将文件放在别处，使用替代目录的名称。例如，图 12.33 展示了如何从示例账户检索单个文件到本地系统目录。

- `/Intro_to_UNIX/chap12/work_files.` 图 12.33 和 12.34 中的示例也演示了在账户中创建必要的 `.rcfile` 文件。

```
521 book@mycomputer:$ rcp liza@workcomputer.workdomain.org:work_report.txt Intro_to_UNIX/chap12/work_files
522 book@mycomputer:$ @
```

**图 12.33** 使用 `rcp` 将单个文件检索到本地系统中的指定目录。

要使用 `rcp` 多个文件，请先指定文件名，每个文件名都以远程系统名和冒号开头。对于最后一个参数，请指定文件在本地系统上的位置，即当前工作目录或另一个目录。例如，图 12.34 显示了如何更改当前工作目录为 `/Intro_to_UNIX/chap12/work_files/`，以及如何从远程系统检索三个文件到此处。

```
527 book@mycomputer:$ cd Intro_to_UNIX/chap12/work_files/
528 book@mycomputer:~/Intro_to_UNIX/chap12/work_files$ rcp liza@workcomputer.workdomain.org:project_files/network-report.ps liza@workcomputer.workdomain.org:project_files/network-present.eps liza@workcomputer.workdomain.org:project_files/re_tar.gz
529 book@mycomputer:~/Intro_to_UNIX/chap12/work_files$ 
```

**图 12.34** 使用 `rcp` 将多个文件检索到当前工作目录。

为了缩短在远程系统指定多个文件名的工作量，请利用第 4 章描述的短语匹配技术。通过这种方式，你可以指定一次远程系统名，但在一组相邻的 `{}` 大括号内指定文件名。图 12.37 显示了如何利用 `scp` 进行短语匹配来实现与图 12.34 相同的效果，尽管相同的技术也可以应用于 `rep`。

# `scp`

出于安全考虑，`scp`（secure copy 的缩写）已成为许多 UNIX/Linux 系统上的首选文件传输应用程序。`scp` 的语法和功能与 `rep` 相似，因此为已经熟悉 `rep` 的用户提供了方便的过渡。这两个应用程序之间有许多相似之处。其之一是你不需要区分 ascii 和二进制传输。另一个相似之处是，你必须在远程系统名后加上冒号。还有一种相似之处是，你可以在系统名前通过 @ 符号指定远程系统上的备用户名。

# 420 UNIX/Linux 简介

`rep` 和 `scp` 之间的区别在于，`scp` 传输加密加密，这保护了它们免受窃听。此外，即使你在远程系统中没有密码认证，仍然可以使用 `scp` 进行传输。然而，如果你有密码认证，可以在不指定密码的情况下传输文件。为了演示 `scp` 用并与目前解释的其他文件传输方式进行比较，文中展示了如何利用 `scp` 为之前描述的 `ftp` 和 `rep` 情况传输文件。

图 12.35 显示了如何使用 `scp` 发送单个文件。与图 12.31 一样，你指定从本地系统账户目录目录文件的相对路径，并将文件放入远程系统账户的家目录。然而，与图 12.31 不同，系统会提示你输入密码。此提示说明了即使在远程账户上没有配置自动密码认证，`scp` 仍然可以工作，而这个特定的远程账户正是如此。

```
$ scp sc$ Intro_to_UNIX/chap12/upload_files/mypic.tif joely@othercomputer.somedomain.org:
Password:mypic.tif 100% 88KB 88.2KB/s 00:00
531 book@mycomputer:"$
```

**图 12.35** 使用 `scp` 在没有自动认证的情况下传输单个文件。

使用 `scp` 传输多个文件（你使用 `rep` 那样），先指定文件名参数，后跟远程系统名。图 12.36 展示了图 12.32 的 `scp` 等效操作。同样，由于你对远程系统账户没有自动密码认证，系统会提示远程系统的密码。

```
531 $ book@mycomputer:"$ cd Intro_to_UNIX/chap12/upload_files/
532 book@mycomputer:"$ Intro_to_UNIX/chap12/upload_files scp homework.txt notes.txt joely@othercomputer.somedomain.org:classwork
Password:
home.txt 100% 35 0.0KB/s 00:00
notes.txt 100% 422 0.4KB/s 00:00
533 book@mycomputer:"/Intro_to_UNIX/chap12/upload_files$ []
```
