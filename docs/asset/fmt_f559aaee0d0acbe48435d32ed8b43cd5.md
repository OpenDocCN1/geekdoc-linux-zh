
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

**`awk`** - 在行中搜索指定模式并执行操作。

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

#### find

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
