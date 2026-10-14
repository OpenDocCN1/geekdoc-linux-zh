
```
rm: is dangerous recursively on '/'
rm: use --preserve-root to override this failsafe.
```

然而，没有人希望每次运行 `rm` 时都保留 `--preserve-root`，因此你可以将其添加到 `/home` 目录中的 `.bashrc` 文件里：

```
alias rm='rm --preserve-root'
```

这个别名会自动为未来 `bash` 会话中对 `rm` 的所有调用添加 `--preserve-root`。`Ubuntu`（以及 `Debian` 和也许其他发行版）默认已这样做——不是通过在 `bashrc` 中添加别名，而是将 `--preserve-root` 设为该命令的默认值。

## 使用 sort 对文件内容进行排序

假设你有一个文本文件，并且想按字母顺序对其内容进行排序。这很简单。假设你的文本文件每行包含一个字母，大写或小写。运行 `sort` 命令对该文件进行排序时，你会得到以下结果：

```
matthew@seymour:~$ sort testfile.txt
```

a

A

b

这很有用。你也可以按逆序排序

```
matthew@seymour:~$ sort -r testfile.txt
```

该命令输出相同的内容，但这次是从 Z 到 a。

你可以用 `sort` 处理数字文件，但它不会进行数值排序。它会给出如下输出：

```
matthew@seymour:~$ sort numberfile.txt
```

1

14

5

58

6

你可以看到，`sort` 命令对数字执行了一种相当无用的字母式排序。幸运的是，有一个开关可以修复这个问题：

```
matthew@seymour:~$ sort -n numberfile.txt
```

1

5

6

14

58

使用 `sort` 可以做很多很棒的技巧，手册文件中解释了许多参数。对于有多列的情况，例如目录列表，你可以指定 `-k` 开关和想要排序的列的顺序。让我们看一个 `conky` 文件目录的例子，并从以下 `ls` 命令开始：

```
matthew@seymour:/conky$ ls -la
```

```
total 60
drwxr-xr-x 2 matthew 4096 Dec 25 2012
drwxr-xr-x 91 matthew 4096 Jul 28 18:42
drwxr-xr-x 1 matthew 5526 Dec 25 2012 conkyrc_main
drwxr-xr-x 1 matthew 5502 Dec 25 2012 conkyrc_main-
drwxr-xr-x 1 matthew 5387 Apr 16 2008 conkyrc_main (old)
```

```
-rwxr-xr-x 1 matthew matthew 126 Mar 15 2008 conkyrc-weather
-rwxr-xr-x 1 matthew matthew 2549 Oct 23 2009 sample_conky.conf
-rwxr-xr-x 1 matthew matthew 128 Apr 8 2008 start_conky (copy).sh
-rwxr-xr-x 1 matthew matthew 139 Dec 25 2012 start_conky.sh
-rwxr-xr-x 1 matthew matthew 140 Dec 25 2012 start_conky.sh-
-rwxr-xr-x 1 matthew matthew 1503 Sep 30 2007 weather.sh
-rwxr-xr-x 1 matthew matthew 2379 Sep 30 2007 weather.xslt
```

## 使用基本命令

以下是按文件大小排序的列表：

```
matthew@seymour:~$ ls -la | sort -n5
total 60
-rwxr-xr-x 1 matthew matthew 128 Apr 8 2008 start_conky (copy).sh
-rwxr-xr-x 1 matthew matthew 139 Dec 25 2012 start_conky.sh
-rwxr-xr-x 1 matthew matthew 140 Dec 25 2012 start_conky.sh-
-rwxr-xr-x 1 matthew matthew 126 Mar 15 2008 conkyrc_weather
-rwxr-xr-x 1 matthew matthew 1503 Sep 30 2007 weather.sh
-rwxr-xr-x 1 matthew matthew 2379 Sep 30 2007 weather.xslt
-rwxr-xr-x 1 matthew matthew 2549 Oct 23 2009 sample_conky.conf
drwxr-xr-x 2 matthew 4096 Dec 25 2012 .
drwxr-xr-x 9 matthew 4096 Jul 28 18:42 .
-rwxr-xr-x 1 matthew 5387 Apr 16 2008 conkyrc_main (old)
-rwxr-xr-x 1 matthew matthew 5502 Dec 25 2012 conkyrc_main-
-rwxr-xr-x 1 matthew matthew 5526 Dec 25 2012 conkyrc_main
```

## 使用 tail 打印文件的最后几行

如果你想在日志文件被写入时监视它，或者想在用户操作发生时监控用户的操作，在这些情况下，你需要使用 `tail` 命令，它会打印文件的最后几行，并在新行添加时进行更新。以下命令 `tail` 用于打印 `/var/apache2/access.log` 的最后几行，即 Apache 访问日志：

```
matthew@seymour:~$ tail /var/apache2/access.log
```

为了让 `tail` 持续运行并更新文件更改，使用 `-f`（follow）参数：

```
matthew@seymour:~$ tail -f /var/apache2/access.log
```

你可以通过指定 `--pid` 参数将 `tail -f` 的生命周期绑定到某个进程的存在。当这样做时，`tail` 会继续跟踪你打开的文件，直到它发现由 `process ID (PID)` 标识的进程不再运行，此时它会停止跟踪。

如果你在命令行上指定多个文件，`tail` 会跟踪它们所有，并在输入源更改时打印文件头。在模式下，按 Ctrl+C 终止 `tail`。

## 使用 which 打印命令的位置

其目的在于告诉你如果输入该命令，究竟会执行哪个命令。例如，`which mkdir` 返回 `/bin/mkdir`，说明运行命令 `mkdir` 时实际运行的是 `/bin/mkdir`。

## 使用 wget 下载文件

假设你有一些有用的内容需要下载到你的服务器——例如，`http://releases.ubuntu.com`——你希望为在计算机实验室工作的学生提供当前 Ubuntu 版本的 ISO 镜像。这种做法称为镜像，是被普遍接受的。或者，也许你想将最新的 Minecraft 服务器下载到一个文件中，而不先从网站下载到本地机器再上传到服务器。你可以用 `wget` 来完成此操作，`wget` 用于使用 HTTP、HTTPS 和 FTP 下载文件，例如

```
matthew@seymour:$ wget http://releases.ubuntu.com/16.04/ubuntu-16.04-desktop-amd64.iso
```

如果你想将 Web 服务器上的所有内容文件复制到新服务器上？你可以使用 `-m` 或 `--mirror` 标志来实现。此示例会下载你指定的目录下的所有内容（假设你有访问权限），下载到当前目录：

```
matthew@seymour:$ wget http://yourserver.com/website/files
```

> 你可以使用 `wget` 与任何标准 URL 语法，包括指定端口、用户名和密码，但你应该意识到用户名和密码信息会以明文传输；因此，这不被视为安全的数据传输方式。为此，请使用 `scp`，其内容在第 19 章“使用 SSH、Telnet 和 VNC 进行远程访问”中介绍。

## 参考文献

- `gnu.org`——GNU 项目的网站，其中包含大量命令行软件的手册和下载

- `Linux in a Nutshell` 作者 Stephen Figgins、Arnold Robbins、Ellen Siever 和 Robert Love——Linux 命令词典，包含大量 Linux 命令及其说明

- `linuxcommand.org`——一个“命令行一站式商店”，包含大量关于控制台的有用信息

- `The Art of UNIX Programming` 作者 Eric Raymond——专注于 UNIX 背后的哲学，并融入了大量关于命令行的内容

## 第 12 章
