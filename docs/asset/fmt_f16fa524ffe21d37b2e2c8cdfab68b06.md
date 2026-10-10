
```
root@kemal:~/zeyno# cat >> test
Debian Whezy
root@kemal:~/zeyno# cat -A test
Kali Linux 2.0 (Kali Sana)
^IDebian^IWhezy$
root@kemal:~/zeyno# _
```

为了将文本文件中的小写字母转换为大写字母，或者反之，我们可以将 `cat` 和 `tr` 命令结合使用。例如，要将 `test` 文件中的小写字母转换为大写，我们可以使用 `cat test | tr 'a-z' 'A-Z'`。

```
root@kemal:~/zeyno# cat test
Kali Linux 2.0 (Kali Sana)
Debian Whezy
root@kemal:~/zeyno# cat test | tr 'a-z' 'A-Z'
KALI LINUX 2.0 (KALI SANA)
DEBIAN WHEEZY
root@kemal:~/zeyno# _
```

## 68 | Linux 命令大师

在这里，我想简要谈一下我们将再次用到的内容，关于 `|` 符号和管道 `pipe`。如上面的示例所示，通过管道传输，一个输出命令的输出将作为另一个命令的输入。当我们检查示例时，读取 `test` 文件的内容作为输入传递给 `tr` 命令，而 `tr` 命令根据文件内容及其使用的参数进行转换。管道过程通过 `|` 实现。是的，让我们回到示例。

我们讨论过可以使用 `cat` 命令在终端读取文本文件的内容。现在，例如，使用 `cat /etc/passwd` 命令查看 `passwd` 文件内容：

```
root@kemal:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
demon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/usr/sbin/nologin
sys:x:3:3:dev:/usr/sbin/nologin
sync:x:4:6534:sync:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
```

（此处）

文件内容按原样显示。如果我们想带行号查看内容，必须使用 `cat -n /etc/passwd` 命令。

```
root@kemal:~$ cat -n /etc/passwd
1 root:x:0:0:root:/root:/bin/bash
2 demon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
3 bin:x:2:2:bin:/usr/sbin/nologin
4 sysys:x:3:3:dev:/usr/sbin/nologin
5 sync:x:4:6534:sync:/bin/sync
6 games:x:5:60:games:/usr/games:/usr/sbin/nologin
7 lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
8 mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
9 news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
10 uuc:x:10:10:uuc:/bin:/usr/sbin/nologin
11 proxy:x:12:13:proxy:/bin:/usr/sbin/nologin
12 www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
13 backup:x:34:34:backup:/var/backup:/usr/sbin/nologin
14 list:x:38:38:Mailing List:/var/list:/usr/sbin/nologin
15 irc:x:39:39:irc:/var/run/irc:/usr/sbin/nologin
```

### Echo

通常情况下，使用此命令可以将任何所需的语句作为输出发送到终端屏幕。此外，它还可以用于创建文件并在其中写入任何字符串。现在让我们也使用 `echo` 命令创建一个新文件并写入内容。

```
root@kemal:~/zeyo# echo "master of linux" > linuxcmd
root@kemal:~/zeyo# ls
linuxcmd test-1 test-2
root@kemal:~/zeyo# cat linuxcmd
master of linux
```

正如你通过 `echo "master of linux" > linuxcmd` 文件看到的，我们创建了之前不存在 `linuxcmd`。之前可以通过这种方式写入空文件。但如果文件不是空的，我们可以像之前那样使用 `>>` 运算符。

```
root@kemal:~/zeyno# echo "master of linux"
linuxcmd
root
root@kemal:zeyno# cat test-2
Ali
Veli
Ayşe
Fatma
root@kemal:~/zeyno# echo "master of linux" >> test-2
master of linux
```

## 70 | Linux 命令大师

```
root@kemal:~/zeyo# echo "linux commands"
linux commands
root@kemal:~/zeyo# echo *
linuxcmd test-1 test-2
```

-rw-- 1 root 30 Jan 56 list

1 root:x:0:0:root:/root:/bin/bash

2 demon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin

3 bin:x:2:2:bin:/usr/sbin/nologin

4 sysys:x:3:3:dev:/usr/sbin/nologin

5 sync:x:4:6534:sync:/bin/sync

6 games:x:5:60:games:/usr/games:/usr/sbin/nologin

7 lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin

8 mail:x:8:8:mail:/var/mail:/usr/sbin/nologin

9 news:x:9:9:news:/var/spool/news:/usr/sbin/nologin

10 uuc:x:10:10:uuc:/bin:/usr/sbin/nologin

11 proxy:x:12:13:proxy:/bin:/usr/sbin/nologin

12 www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin

13 backup:x:34:34:backup:/var/backup:/usr/sbin/nologin

14 list:x:38:38:Mailing List:/var/list:/usr/sbin/nologin

15 irc:x:39:39:irc:/var/run/irc:/usr/sbin/nologin

### Less (查看)

再次，为了读取文件内容，你可以使用的另一个命令是 `less` 命令。使用此命令作为 `more` 命令，我们显示了长文件的输出，以便于阅读。使用向上和向下方向键可以翻页。使用空格键跳到下一页，使用 `b` 键回到上一页。退出使用的 `q` 键与我们之前提到的相同。

### Head-Tail (头与尾)

在查看文件内容的前的前十行时使用 `head` 命令，查看最后十行时使用 `tail` 命令。这些参数的用法如果你想查看特定数量的行，必须用 `-n` 参数指定。例如，要查看前五行可以使用 `head -n 5`，查看后五行可以使用 `tail -n 5` 命令。
