
```bash
$ ls -a /home/denise | grep netscape
.netscape-bookmarks.html
.netscape-cache
.netscape-history
.netscape-newsgroups-news.sprry.com
.netscape-newsgroups-newsserv.hp.com
.netscape-preferences
$ ls -a /home/denise | grep -c netscape
6
$ ls -a /home/denise | grep NETSCAPE
$ ls -a /home/denise | grep -i NETSCAPE
.netscape-bookmarks.html
.netscape-cache
.netscape-history
.netscape-newsgroups-news.sprry.com
.netscape-newsgroups-newsserv.hp.com
.netscape-preferences
$ ls -a /home/denise | grep -F "netscape
> ,c"
.cshrc
.cshrc.orig
.netscape-bookmarks.html
.netscape-cache
.netscape-history
.netscape-newsgroups-news.sprry.com
.netscape-newsgroups-newsserv.hp.com
.netscape-preferences
.newsrc-news.sprry.com
.newsrc-newsserv.hp.com
$
```

### 图 10-8 `grep` 命令

首先，我们搜索模式 `netscape`。这产生了一个文件列表，所有文件都以 .netscape 开头。

接下来，我们使用 `-c` 选项来创建 `netscape` 被找到的次数计数。结果是 6。

你认为 `grep` 区分大小写吗？下一个例子展示了搜索模式 `NETSCAPE`，并且不存在匹配的模式。

使用 `-i` 选项会使 `grep` 忽略大写和小写，只搜索该模式，并且再次找到所有原始匹配项。

此外，还可以搜索多个模式。使用 `-F` 选项，`netscape` 和 .c 都会被搜索，并找到更长的匹配列表。请注意，要搜索的两个模式用双引号括起来，并由换行符分隔。

现在让我们来看看使用 `grep` 的几个更高级的搜索。我们将使用 `passwd.test` 文件作为搜索的基础，因为其中的每一行都包含大量信息。首先，以下是 Linux 系统上 `passwd.test` 文件的内容：

```bash
# cat passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
bin::*:1:1:bin:/bin:
daemon::*:2:2:daemon:/sbin:
adm::*:3:4:adm:/var/adm:
lp::*:4:7:lp:/var/spool/lpd:
sync::*:5:0:sync:/sbin/bin/sync
shutdown::*:6:11:shutdown:/sbin:/sbin/shutdown
halt::*:7:0:halt:/sbin/sbin/halt
mail::*:8:12:mail:/var/spool/mail:
news::*:9:13:news:/var/spool/news:
uucp::*:10:14:uucp:/var/spool/uucp:
operator::*:11:0:operator:/root:
games::*:12:100:games:/usr/games:
gopher::*:13:30:gopher:/usr/lib/gopher-data:
ftp::*:14:50:FTP User:/home/ftp:
man::*:15:15:Manualls Owner:/
nobody::*:65534:65534:Nobody:/ /bin/false
col:WhozYfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col:/bin/bash
```

![](img/75f39fc91296b889c0653851accdfd46_622_0.png)

![](img/75f39fc91296b889c0653851accdfd46_622_1.png)

![](img/75f39fc91296b889c0653851accdfd46_623_0.png)

我们可以像在之前的 `grep` 示例中一样在密码文件中搜索字符串。下面的示例在 `passwd.test` 文件中搜索 `news`。

```bash
# grep news passwd.test
news:::9:13:news:/var/spool/news:
```

现在让我们检查一下 `passwd.test` 文件中是否有一个名为 `bin` 的用户。为了让名为 `bin` 的用户在 `passwd.test` 文件中有一个条目，用户名（在这种情况下是 `bin`）必须是该行中的第一个条目。以下是搜索该用户的结果：

```bash
# grep bin passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
bin::*:1:1:bin:/bin:
daemon::*:2:2:daemon:/sbin:
sync::*:5:0:sync:/sbin:/bin/sync
shutdown::*:6:11:shutdown:/sbin:/sbin/shutdown
halt::*:7:0:halt:/sbin:/sbin/halt
nobody::*:65534:65534:Nobody::/:/bin/false
col:Wh0yzfAV2gm2Y:100:100:Caldera OpenLinux User:/home/col:/bin/bash
```

![](img/75f39fc91296b889c0653851accdfd46_623_1.png)

`passwd.test` 中确实生成了许多包含字符串 `bin` 的行；然而，我们必须浏览这些行才能找到用户 `bin`，即 `bin` 作为第一个出现的字符串的那一行。这超出了我们发起搜索时的需求。我们想看到一个出现在行开头的用户名 `bin`。我们可以进一步限定我们的搜索，在这种情况下，将搜索限制为行开头的字符串，通过使用与 `vi` 非常相似的模式匹配。你可以参考本书中的 `vi` 章节或 `vi` 快速参考卡来查看一些模式匹配选项。在这种情况下，我们只想在行开头搜索 `bin`，因此我们将使用脱字符（`^`）来限定我们的搜索。

要将搜索限制在行的开头，如下例所示：

```
# grep ^bin passwd.test
bin:*:1:1:bin:/bin:
```

![](img/75f39fc91296b889c0653851accdfd46_624_0.png)

此搜索产生的结果正是我们感兴趣的信息，即一个以 `bin` 开头的行。当使用特殊字符（如此例中的脱字符 `^`）时，你应该用单引号（`'`）将这些特殊字符括起来。特殊字符可能会被 shell 解释，从而导致我们要发送给 `grep` 的参数出现问题。将搜索模式用单引号括起来可以确保搜索模式（在此例中为 `^bin`）直接传递给 `grep`。用单引号括起来的搜索模式如下所示：

```
# grep '^bin' passwd.test
bin:*:1:1:bin:/bin:
```

由于我们在找到该行后还需要在 `passwd.test` 文件中搜索这一行，因此我们不妨使用 `-n` 选项同时打印出行号和该行本身，如下例所示：

```
# grep -n '^bin' passwd.test
2:bin:*:1:1:bin:/bin:
```

以下是 `grep` 命令的摘要：

## `grep` - 搜索文本并显示结果。

![](img/75f39fc91296b889c0653851accdfd46_625_0.png)

### 选项

- `-c` 返回匹配的数量，而不显示文本。
- `-h` 显示文本，但不引用文件名。
- `-i` 搜索时忽略大小写。
- `-l` 返回包含匹配项的文件名，而不显示文本。
- `-n` 返回文件中搜索到的文本的行号以及文件本身。
- `-v` 返回不包含搜索文本的行。
- `-E` 搜索多个表达式（等同于 `egrep`）。
- `-F` 搜索多个表达式（等同于 `fgrep`）。

## `sed`

![](img/75f39fc91296b889c0653851accdfd46_625_1.png)

![](img/75f39fc91296b889c0653851accdfd46_625_2.png)
