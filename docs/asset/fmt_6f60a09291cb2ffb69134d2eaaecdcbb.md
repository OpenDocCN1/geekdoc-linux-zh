
```bash
root@kemal:~/zeyno# cat LISTA
Ahmet
Mehmet
Ali
Veli
Zeyno
root@kemal:~/zeyno# cat LISTA | tr a-z A-Z
AHMET
MEHMET
ALI
VELI
ZEYNO
root@kemal:~/zeyno# _
```

我们讨论过重定向操作符（`>` 和 `>>`）。除此之外，我们还有 `<` 运算符。这些运算符与其他不同，它们将文件作为输入。因此是读取文件的内容，启用与之相关的活动。现在，让我们结合 `tr` 命令和 `>` 以及 `<` 运算符使用。例如，使用命令 `tr a-z A-Z < LISTA > NEW_LISTA`。

```bash
root@kemal:~/zeyno# tr a-z A-Z < LISTA > NEW_LISTA
root@kemal:~/zeyno# cat NEW_LISTA
AHMET
MEHMET
ALI
VELI
ZEYNO
root@kemal:~/zeyno# _
```

通过我们的命令，我们以 `LIST` 文件作为输入，将文本中的小写字母转换为大写并写入 `NEW_LISTA` 文件。如果使用带有 `d` 的 `tr` 命令，指定的字符将被忽略。例如，当我们使用 `cat LISTA | tr -d A,e` 命令时，`LISTA` 文件中的 `A` 和 `e` 字符将被忽略。

```bash
root@kemal:~/zeyno# cat LISTA
Ahmet
Mehmet
Ali
Veli
Zeyno
root@kemal:~/zeyno# cat LISTA | tr -d A,e
hmt
Mhmt
li
Vli
Zyno
root@kemal:~/zeyno# _
```

### Cmp

我们可以用于比较文件的命令之一是 `cmp` 命令。例如，我使用 `cmp hacker test` 来比较名为 `hacker` 和 `test` 的两个文件。结果中，它将显示文件的差异、首次出现差异的行以及字节数。

```bash
root@kemal:~/zeyno# cmp hacker test
hacker test farkli: bayt 1, satır 1
root@kemal:~/zeyno# _
```

使用此命令有几个参数，但你可以通过 `man cmp` 来进行实验。例如，当你使用 `-l` 参数时，每个差异的字节数以及不同的字节值将发送到标准输出（屏幕/终端）。

### Diff

同样，这是一个用于比较文件的命令。如果是两个文件之间的比较，应使用 `diff`；如果是三个文件之间的比较，则应使用 `diff3` 命令。例如，要查看 `hacker` 和 `test` 文件之间的差异，使用 `diff hacker test`。

```bash
root@kemal:~/zeyno# diff hacker test
1,3c1,2
< Linux users
< Network
< Computer
...
> Kali Linux 2.0 (Kali Sana)
> Debian Whezy
root@kemal:~/zeyno# _
```

现在，使用 `diff3 hacker test` 命令比较两个文件并查看 `hacker`、`test` 和 `linux` 之间的差异。

```bash
root@kemal:~/zeyno# diff3 hacker test linux
===
1:1,3c
Linux users
Network
2:1,2c
Kali Linux 2.0 (Kali Sana)
Debian Whezy
3:1,2c
forever linux
root@kemal:~/zeyno# _
```

如果你在 `diff` 命令中使用 `-y`，输出将并排投影在屏幕上。不仅是文件，`diff` 命令也可以比较目录。例如，通过 `diff -r zeyno /home`，比较 `zeyno` 和 `home` 目录（`-r`）并列出差异。

```
root@kemal:-# diff -r zeyno /home
zeyno:hacker
zeyno:LISTA
zeyno:LISTB
zeyno:LISTC
zeyno:linux
home:MATERYAL
home:test-1
home:test-2
root@kemal:-#
```

### Find

有时，你只记得名称的一部分，但不记得文件和目录在哪个目录下。为了找到这些文件并执行与其相关的各种操作，我们使用 `find` 命令。使用模式的方法是 `find [file_path] [search_phrase]`。所以，在第一个目录搜索中输入我们要做的操作，然后用 `-name` 定义搜索表达式。例如，要列出 `/etc` 下的文件，，可以使用 `find /etc -name *.conf`。

```
root@kemal:~# find /etc -name *.conf
/etc/ldap/ldap.conf
/etc/avahi/avahi-daemon.conf
/etc/cracklib/cracklib.conf
/etc/xdg/user-dirs.conf
/etc/redsocks.conf
/etc/udev/udev.conf
/etc/nikto.conf
/etc/john/john-mail.conf
/etc/john/john.conf
/etc/pam.conf
/etc/systemd/journald.conf
/etc/systemd/bootstrap.conf
```

另一个例子是 `find /etc -name *apache*`，我们再次在 `/etc` 目录下搜索包含 `apache` 单词的文件。

```bash
root@kemal:~# find /etc -name *apache*
/etc/default/apache2
/etc/rc5.d/K01apache
/etc/init.d/apache2
/etc/cron.daily/apache2
/etc/rc0.d/K01apache
/etc/rc3.d/K01apache
/etc/logrotate.d/apache2
/etc/rc6.d/K01apache
/etc/rc4.d/K01apache
/etc/bash_completion.d/apache2
/etc/rc1.d/K01apache
/etc/apache2
/etc/apache2/apache2.conf
/etc/rc2.d/K01apache
```

在进行搜索时可以使用一些参数来方便我们的工作，并帮助我们获得想要的结果：

- `perm 755`（访问权限为 755 的文件/目录）

- `-type f`（文件）

- `-type d`（目录）

- `-size +100k`（大于 100 Kbytes的文件）

- `-ctime 3`（恰好 3 天前修改的文件/目录）

- `-ctime +7`（7 天前修改的文件/目录）

- `-ctime -7`（7 天内修改的文件/目录）

让我们做几个例子：

例如，我们想列出在工作目录下 `find /root -type f -name '*.txt'` 命令的文件以及 `txt` 扩展名。工作目录是在尝试输入 `/root` 时已经存在的目录，可以使用 `.`（点）来使用此命令。因为点标记了我们正在工作的地方。

```
root@kemal:-# find /root -type f -name '*.txt'
root/Masaüstü/Aproce/LINKLER.txt
root/Masaüstü/Aproce/serverda loglar nererede.txt
root/important.txt
root/.config/libreoffice/4/user/uno_packages/cache/log.txt
root/.config/libreoffice/4/user/extensions/shared/log.txt
root/account.txt
root/deneme.txt
root/users.txt
root/test.txt
root/conf.txt
root/.cache/tracker/last-crawl.txt
root/.cache/tracker/db-version.txt
root/.cache/tracker/db-locale.txt
root/.cache/tracker/first-index.txt
root/.cache/tracker/miner-applications-locale.txt
root/mozilla/firefox/x4wo2r.default/SiteSecurityService.State
root/mozilla/firefox/x4wo2r.default/revocations.txt
```

### Exe

为了对文件执行各种操作，请在 `find` 命令中配合 `exec`。
