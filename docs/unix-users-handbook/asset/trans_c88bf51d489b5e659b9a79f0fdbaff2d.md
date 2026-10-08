
你可以使用 `-F` 选项后跟一个分隔符来指定字段分隔符，在 `passwd.test` 中该分隔符是冒号（`:`）。以下示例指定了字段分隔符，然后评估第一个字段以判断其是否等于 "root"，如果相等，则打印整行：

![](img/75f39fc91296b889c0653851accdfd46_637_0.png)

```
# awk -F: '$1 == "root" {print}' passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
```

以下示例指定了字段分隔符，然后评估第四个字段以判断其是否等于 "0"，这意味着该用户属于与 root 相同的组；如果相等，则打印整行：

```
# awk -F: '$4 == "0" {print}' passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
sync:*:5:0:sync:/sbin/bin/sync
halt:*:7:0:halt:/sbin/sbin/halt
operator:*:11:0:operator:/root:
```

除了 `==` 之外，你还可以使用 `awk` 执行许多其他类型的比较。以下示例展示了对我们熟悉的 `passwd.test` 文件使用几种比较运算符的方法。第一个示例打印所有所在组值小于 14 的用户：

```
# awk -F: '$4 < 14 {print}' passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
bin:*:1:1:bin:/bin:
daemon:*:2:2:daemon:/sbin:
adm:*:3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/sbin/bin/sync
shutdown:*:6:11:shutdown:/sbin:/sbin/shutdown
halt:*:7:0:halt:/sbin/sbin/halt
mail:*:8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
operator:*:11:0:operator:/root:
```

下一个示例打印所有所在组值小于或等于 14 的用户：

![](img/75f39fc91296b889c0653851accdfd46_638_0.png)

```
# awk -F: '$4 <= 14 {print}' passwd.test
root:PgYQCwKH65hyQ:0:0:root:/root:/bin/bash
bin:*:1:1:bin::/bin:
daemon:*:2:2:daemon:/sbin:
adm:*:3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/sbin:/bin/sync
shutdown:*:6:11:shutdown:/sbin:/sbin/shutdown
halt:*:7:0:halt:/sbin:/sbin/halt
mail:*:8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
uucp:*:10:14:uucp:/var/spool/uucp:
operator:*:11:0:operator:/root:
```

现在让我们打印所有所在组值不等于 14 的用户：

```
# awk -F: '$4 != 14 {print}' passwd.test
root:PgYQCwKH65hyQ:0:0:root:/root:/bin/bash
bin:*:1:1:bin::/bin:
daemon:*:2:2:daemon:/sbin:
adm:*:3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/sbin:/bin/sync
shutdown:*:6:11:shutdown:/sbin:/sbin/shutdown
halt:*:7:0:halt:/sbin:/sbin/halt
mail:*:8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
operator:*:11:0:operator:/root:
games:*:12:100:games:/usr/games:
gopher:*:13:30:gopher:/usr/lib/gopher-data:
ftp:*:14:50:FTP User:/home/ftp:
man:*:15:15:Manuals Owner:/
nobody:*:65534:65534:Nobody::/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col:/bin/bash
```

现在让我们打印所有所在组值大于或等于 14 的用户：

```
# awk -F: '$4 >= 14 {print}' passwd.test
uucp:*:10:14:uucp:/var/spool/uucp:
games:*:12:100:games:/usr/games:
gopher:*:13:30:gopher:/usr/lib/gopher-data:
ftp:*:14:50:FTP User:/home/ftp:
man:*:15:15:Manuals Owner:/
nobody:*:65534:65534:Nobody::/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col:/bin/bash
```

最后一个示例显示所有所在组值大于 14 的用户：

```
# awk -F: '$4 > 14 {print}' passwd.test
games:*:12:100:games:/usr/games:
gopher:*:13:30:gopher:/usr/lib/gopher-data:
ftp:*:14:50:FTP User:/home/ftp:
man:*:15:15:Manuals Owner:/
nobody:*:65534:65534:Nobody::/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col:/bin/bash
```

![](img/75f39fc91296b889c0653851accdfd46_639_0.png)

`awk` 的内容远不止本节所涵盖的范围。Shell 编程章节中还有额外的 `awk` 示例。下表总结了本节中介绍的一些 `awk` 比较运算符。

**awk** - 在行中搜索指定模式并执行操作。

比较运算符：

| 运算符 | 描述 |
| :--- | :--- |
| `<` | 小于 |
| `<=` | 小于或等于 |
| `==` | 等于 |
| `~` | 字符串匹配 |
| `!=` | 不等于 |
| `>=` | 大于或等于 |
| `>` | 大于 |

## find

![](img/75f39fc91296b889c0653851accdfd46_639_1.png)

`find` 命令用于通过遍历 UNIX 树结构来定位文件。你可以从系统中的任何位置开始，甚至可以是根级别，并遍历整个层级结构。找到文件后，你还可以执行操作。

`find` 最常见的用途是生成文件列表。你可以生成当前工作目录（由一个点（`.`）指定）中的文件列表，并打印这些文件，如下例所示：

```
# cd /home
# ls -l
total 3
drwxr-xr-x    3 col     users    1024 Nov  8 14:09 col
drwxr-xr-x    6 root    root     1024 Nov  8 14:08 ftp
drwxr-xr-x    6 root    root     1024 Nov  8 14:08 httpd
#
# find . -print
.
./httpd
./httpd/apache
./httpd/apache/doc
./httpd/apache/doc/manual.ps.gz
./httpd/cgi-bin
./httpd/cgi-bin/HelpIndex
./httpd/cgi-bin/HelpScreen
./httpd/html
./httpd/html/dt
./httpd/html/dt/dt.html
./httpd/html/dt/dt.html.idx
./httpd/html/dt/dt.index
./httpd/html/dt/expert.gif
./httpd/html/dt/hint.gif
./httpd/html/dt/index.gif
./httpd/html/dt/info2.gif
./httpd/html/dt/note.gif
./httpd/html/dt/sysadm.gif
./httpd/html/dt/up.gif
./httpd/html/dt/warning.gif
./httpd/icons
./ftp
./ftp/bin
./ftp/bin/gzip
./ftp/bin/ls
./ftp/bin/tar
./ftp/bin/zcat
./ftp/etc
./ftp/etc/group
./ftp/etc/passwd
./ftp/lib
./ftp/pub
./col
./col/.bashrc
./col/.cshrc
./col/.login
./col/.profile
./col/lg
./col/lg/lg_layouts
./col/lg/lg_layouts/User
./col/lg/lg3_prefs
./col/lg/lg3_soundPref
./col/lg/lg3_startup
```

![](img/75f39fc91296b889c0653851accdfd46_640_0.png)

![](img/75f39fc91296b889c0653851accdfd46_640_1.png)

![](img/75f39fc91296b889c0653851accdfd46_640_2.png)

该 `find` 操作是从 /home 目录执行的。请注意，/home 下只有三个主目录，而 `find` 命令遍历了每个主目录的层级结构。请记住，你可能不希望直接在根级别执行此 `find` 操作。那样你将遍历整个层级结构，并获得系统中每个文件的列表。

![](img/75f39fc91296b889c0653851accdfd46_641_0.png)

使用 `find` 时，你可能会发现，当遇到你没有足够权限遍历的文件或目录时，会收到类似以下消息：

```
find: /var/spool/cron: Permission denied
```

`find` 的一般形式如下：

```
find [path] [expression]
```

如果你没有指定 *path*（路径）或 *expression*（表达式），你将执行我们之前执行的操作，即搜索当前目录并打印所有文件的列表。

典型的 find 命令会指定搜索特定文件的路径。在这种情况下，*expression*（表达式）是你想要搜索的文件 *name*（名称），如下例所示：

```
# find /home -name ftp
/home/ftp
```

在这个例子中，我们在 *path*（路径）/home 中搜索名为 **ftp** 的 *name*（名称）。

你可能希望执行 **find** 操作以仅生成文件列表，而不包括目录。以下 **find** 操作与我们之前执行的操作类似，但这次仅生成文件列表：

```
# find /home -type f
/home/httpd/apache/doc/manual.ps.gz
/home/httpd/cgi-bin/HelpIndex
/home/httpd/cgi-bin/HelpScreen
/home/httpd/html/dt/dt.html
/home/httpd/html/dt/dt.html.idx
/home/httpd/html/dt/dt.index
/home/httpd/html/dt/expert.gif
/home/httpd/html/dt/hint.gif
/home/httpd/html/dt/index.gif
/home/httpd/html/dt/info2.gif
/home/httpd/html/dt/note.gif
/home/httpd/html/dt/sysadm.gif
/home/httpd/html/dt/up.gif
/home/httpd/html/dt/warning.gif
/home/ftp/bin/gzip
/home/ftp/bin/ls
/home/ftp/bin/tar
/home/ftp/etc/group
/home/ftp/etc/passwd
/home/col/.bashrc
/home/col/.cshrc
/home/col/.login
/home/col/.profile
/home/col/lg/lg_layouts/User
/home/col/lg/lg3_prefs
/home/col/lg/lg3_soundPref
/home/col/lg/lg3_startup
```

执行 **find** 操作时，一个有用的测试是查找空文件。以下示例搜索系统中所有空文件和目录：

```
# find / -empty
/lost+found
/var/adm/LST/analyse
/var/spool/lpd
/var/spool/news
/var/spool/uucp
/var/spool/mqueue
/var/spool/atjobs/.SEQ
/var/spool/atspool
/var/spool/cron
/var/spool/fax/outgoing/locks
/var/spool/fax/incoming
/var/spool/voice/incoming
/var/spool/voice/messages
/var/spool/rwho
/var/spool/uucppublic
/var/lib/LST/log
/var/lib/LST/analyse
/var/lib/LST/disks
/var/lib/LST/catalog
/var/lib/LST/conflicts
/var/lib/LST/saved
/var/lib/LST/replaced
/var/lib/LST/deleted
/var/lib/games
/var/local
/var/lock/subsys/inet
/var/lock/subsys/ipx
/var/lock/subsys/syslog
/var/lock/subsys/amd
/var/lock/subsys/cron
/var/lock/subsys/atd
/var/lock/subsys/mta
/var/lock/subsys/rstatd
/var/lock/subsys/httpd
/var/log/httpd/apache/access_log
/var/log/xferlog
/var/log/uucp
/var/log/secure
/var/log/spooler
/var/named
/var/nis
/var/preserve
/var/run/xlaunch
/var/tmp
/var/catman/TeX/cat1
/var/catman/TeX/cat2
/var/catman/TeX/cat3
```

![](img/75f39fc91296b889c0653851accdfd46_642_0.png)

