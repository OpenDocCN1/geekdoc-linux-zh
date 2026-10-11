
## 2.1 命令输入和输出

此外，您可以将重定向和管道组合使用；但是，输入重定向必须出现在管道的开头，而输出重定向必须出现在管道的末尾。以下输出展示了一个示例，该示例将前一个示例中使用的 prologue 文件中所有小写字母 A 替换为大写字母 A，然后对文件进行排序，为每一行编号，并将输出保存到名为 newprologue 的文件中，而不是将输出发送到终端屏幕。

```
[root@server1 root]# tr a A <prologue | sort | nl >newprologue
[root@server1 root]# cat newprologue
   1 And the continuance of their parents' rage.
   2 A pair of star-cross'd lovers take their life.
   3 Do with their death bury their parents' strife.
   4 From ancient grudge break to new mutiny.
   5 From forth the fatal loins of these two foes
   6 In fair Verona, where we lay our scene,
   7 Is now the two hours' traffic of our stage;
   8 The fearful passage of their death-mark'd love,
   9 The which if you with patient ears attend,
  10 Two households, both alike in dignity,
  11 What here shall miss, our toil shall strive to mend.
  12 Where civil blood makes civil hands unclean.
  13 Which, but their children's end, nought could remove,
  14 Whole misadventured piteous overthrows
[root@server1 root]# _
```

许多 Linux 命令可用于提供大量有用的文本信息。因此，Linux 管理员经常使用 `sed` 和 `awk` 过滤命令与管道配合，以操作从这些命令获取的文本信息。

`sed` 命令通常用于搜索特定的字符串，并使用语法 `s/search/replace/` 将该文本字符串替换为另一个文本字符串。例如，以下输出演示了如何使用 `sed` 在之前使用的 prologue 文件中搜索字符串 "the" 并将其替换为字符串 "THE"：

```
[root@server1 root]# cat prologue | sed s/the/THE/
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take their life;
Whole misadventured piteous overthrows
Do with THEIR death bury their parents' strife.
The fearful passage of THEIR death-mark'd love,
And THE continuance of their parents' rage,
Which, but THEIR children's end, nought could remove,
Is now THE two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```

从上面的输出可以看出，`sed` 仅搜索并替换了每一行中字符串 "the" 的第一次出现。若要使 `sed` 全局替换每一行中字符串 "the" 的所有出现，只需在搜索和替换表达式后添加 `g`：

```
[root@server1 root]# cat prologue | sed s/the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth THE fatal loins of THESE two foes
A pair of star-cross'd lovers take THEIR life;
Whole misadventured piteous overthrows
Do with THEIR death bury THEIR parents' strife.
The fearful passage of THEIR death-mark'd love,
And THE continuance of THEIR parents' rage,
Which, but THEIR children's end, nought could remove,
Is now THE two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```

您可以通过在搜索和替换表达式前添加前缀，告知 `sed` 要搜索的具体行。例如，若要强制 `sed` 在包含字符串 "love" 的行上全局将字符串 "the" 替换为 "THE"，可以使用以下命令：

```
[root@server1 root]# cat prologue | sed /love/s/the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take THEIR life;
Whole misadventured piteous overthrows
Do with their death bury THEIR parents' strife.

The fearful passage of THEIR death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, nought could remove,
Is now the two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```

您还可以强制 `sed` 仅对特定行执行搜索和替换。若仅在第 5 到第 8 行上全局将字符串 "the" 替换为 "THE"，可以使用以下命令：

```
[root@server1 root]# cat prologue | sed 5,8s/the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth THEe fatal loins of THESE two foes
A pair of star-cross'd lovers take THEIR life;
Whole misadventured piteous overthrows
Do with THEIR death bury THEIR parents' strife.
The fearful passage of their death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, naught could remove,
Is now the two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```

您还可以使用 `sed` 删除不需要的文本行。若要删除所有包含单词 "the" 的行，可以使用以下命令：

```
[root@server1 root]# cat prologue | sed /the/d
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
Whole misadventured piteous overthrows
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```

与 `sed` 类似，`awk` 命令搜索文本模式并对找到的文本执行某些操作。然而，`awk` 命令将每一行文本视为数据库中的一个记录，将每一行中的每个单词视为数据库中的一个字段。例如，行 "Hello, how are you?" 有四个字段："Hello,"、"how"、"are" 和 "you"。这些字段可以在 `awk` 命令中使用 $1、$2、$3 和 $4 来引用。例如，要仅在包含单词 "the" 的 prologue 文件行上显示第一个和第四个单词，可以使用以下命令：

```
[root@server1 root]# cat prologue | awk '/the/ {print $1, $4}'
From fatal
A star-cross'd
Do death
The of
And of
Which, children's
Is two
[root@server1 root]# _
```

默认情况下，`awk` 命令使用空格或制表符字符作为每行中每个字段的分隔符。然而，Linux 系统上的大多数配置文件使用冒号（`:`）字符作为分隔符。若要更改 `awk` 使用的分隔符，您可以为命令指定 `-F` 选项。例如，以下示例列出了冒号分隔文件 `/etc/passwd` 的最后 10 行，并仅查看该文件最后 10 行中包含单词 "bob" 的行的第 6 和第 7 个字段：

```
[root@server1 root]# tail /etc/passwd
ldap:x:55:55:LDAP User:/var/lib/ldap:/bin/false
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
fax:x:78:78:mgetty fax spool user:/var/spool/fax:/sbin/nologin
nut:x:57:57:Network UPS Tools:/var/lib/ups:/bin/false
privoxy:x:73:73::/etc/privoxy:/sbin/nologin
tomcat:x:53:53:Tomcat server::/var/lib/tomcat:/sbin/nologin
cyrus:x:76:12:Cyrus IMAP Server::/var/lib/imap:/bin/bash
exim:x:93:93::/var/spool/exim:/sbin/nologin
bob:x:500:500::/home/bob:/bin/bash
[root@server1 root]# tail /etc/passwd | awk -F ':' '/bob/{ print $6, $7}'
/home/bob /bin/bash
[root@server1 root]# _
```

> **注意**
> `awk` 和 `sed` 都允许您在搜索模式中指定正则表达式。

## 2.2 Shell 变量

BASH shell 在任何时候内存中都有几个变量。回想一下，变量只不过是包含可能被访问的信息的保留内存部分。Shell 中的大多数变量被称为环境变量，因为它们通常由系统设置，并包含系统和程序经常访问的信息。用户还可以创建自己的自定义变量。这些变量称为用户定义变量。除了这两种类型的变量外，还有特殊的变量可用于执行命令以及创建新文件和目录时。

