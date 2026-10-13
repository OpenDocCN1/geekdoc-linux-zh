
以下示例演示了如何使用 **man** 命令显示 **man(1)** 手册页。请注意，超过一屏的手册页会使用 **more(1)** 命令一次显示一屏内容：

```text
# man man
Reformatting Page. Please wait... Done

User Commands                                      man(1)

NAME
        man - find and display reference manual pages

SYNOPSIS
        man [-] [-adFlrt] [-M path] [-T macro-package]
            [-s section] name ...

        man [-M path] -k keyword ...

        man [-M path] -f file ...

DESCRIPTION
        The man command displays information from the reference manuals. It displays complete manual pages that you select by name, or one-line summaries selected either by keyword (-k), or by the name of an associated file (-f). If no manual page is located, man prints an error message.

Source Format
        Reference Manual pages are marked up with either nroff(1) or sgml(5) (Standard Generalized Markup Language) tags. The man command recognizes the type of markup and processes the file accordingly. The various source files are kept in separate directories depending on the type of markup.

Location of Manual Pages
        The online Reference Manual page directories are conventionally located in /usr/share/man. The nroff sources are located in the /usr/share/man/man* directories. The SGML sources are located in the /usr/share/man/sman* directories. Each directory corresponds to a section of the manual. Since

.
.
.
```

*passwd* 主题展示了 **man** 命令的不同命令行参数，因为 **passwd(1)** 是一个命令，而 **passwd(4)** 是一个系统文件。以下示例列出了所有名为 *passwd* 的手册页：

```text
# man -l passwd
passwd (1)       -M /usr/share/man
passwd (4)       -M /usr/share/man
#
```

请注意，两个手册页都被列出。此外，还会显示相应的 **-M** 命令行参数，以指明手册页的位置。手册页的默认路径名为 /usr/share/man。

以下示例显示了 **passwd(1)** 手册页：

```text
# man passwd
Reformatting Page. Please wait... Done

User Commands                                      passwd(1)

NAME
        passwd - change login password and password attributes

SYNOPSIS
        passwd [ -r files ] [ -r ldap ] [ -r nis ] [ -r nisplus ]
                [ name ]

        passwd [ -r files ] [ -egh ] [ name ]

        passwd [ -r files ] -s [ -a ]

        passwd [ -r files ] -s [ name ]

        passwd [ -r files ] [ -d | -l ] [ -f ] [ -n min ]
                [ -w warn ] [ -x max ] name

        passwd -r ldap [ -egh ] [ name ]

        passwd -r nis [ -egh ] [ name ]

        passwd -r nisplus [ -egh ] [ -D domainname ] [ name ]

        passwd -r nisplus -s [ -a ]

        passwd -r nisplus [ -D domainname ] -s [ name ]

        passwd -r nisplus [ -l ] [ -f ] [ -n min ] [ -w warn ]
                [ -x max ] [ -D domainname ] name

DESCRIPTION
        The passwd command changes the password or lists password
.
.
.
```

请注意，**man -s 1 passwd** 会提供相同的结果。在未指定章节的情况下，手册页会按章节进行搜索，并打印第一个找到的条目。要显示 **passwd(4)** 手册页，必须指定章节，如下例所示：

```text
# man -s 4 passwd
Reformatting Page. Please wait... Done

File Formats                                      passwd(4)

NAME
        passwd - password file

SYNOPSIS
        /etc/passwd

DESCRIPTION
        /etc/passwd is a local source of information about users'
        accounts. The password file can be used with
        other password sources, including the NIS maps
        passwd.byname and passwd.byuid and the NIS+ table passwd.
        Programs that use the getpwnam(3C) routines to access this information.

        Each passwd entry is a single line of the form:

            username:password:uid:
            gid:gcos-field:home-dir:
            login-shell

        where

        username
            is the user's login name. It is recommended that this
            field conform to the check performed by pwck(1M).

        password
            is an empty field. The encrypted password for the user
            is in the corresponding entry in the /etc/shadow file.
            pwconv(1M) relies on a special value of 'x' in the
            password field of /etc/passwd. If this value of 'x'
.
.
.
```

![](img/b957f979417d9f16274c2eb52c8f2c9f_60_0.png)

由于难以记住所有 Solaris 8 命令（尤其是所有命令行参数），man 命令提供了一种快速获取详细信息的方法。请记住，多个手册页可能具有相同的名称，因此了解哪个部分可能包含所需信息，并理解使用 **-s** 命令行参数来指定相应部分非常重要。如果您记不住 man 命令行参数，可以使用 man 命令来显示它们，即运行 man man。

以下示例使用 **-a** 命令行参数显示所有 passwd 手册页：

```text
# man -a passwd
Reformatting Page. Please wait... Done

::::::::::::::
/usr/share/man/cat1/passwd.1
::::::::::::::

User Commands                                      passwd(1)

NAME

       passwd - change login password and password attributes

SYNOPSIS
       passwd [ -r files | -r ldap | -r nis | -r nisplus ]
          [ name ]

       passwd [ -r files ] [ -egh ] [ name ]

       passwd [ -r files ] -s [ -a ]

       passwd [ -r files ] -s [ name ]

       passwd [ -r files ] [ -d | -l ] [ -f ] [ -n min ]
          [ -w warn ] [ -x max ] name

       passwd -r ldap [ -egh ] [ name ]

       passwd -r nis [ -egh ] [ name ]

       passwd -r nisplus [ -egh ] [ -D domainname ] [ name ]

       passwd -r nisplus -s [ -a ]

       passwd -r nisplus [ -D domainname ] -s [ name ]

       passwd -r nisplus [ -l ] [ -f ] [ -n min ] [ -w warn ]
          [ -x max ] [ -D domainname ] name
.
.
.
::::::::::::
/usr/share/man/cat4/passwd.4
::::::::::::

File Formats                                      passwd(4)

NAME
       passwd - password file

SYNOPSIS
       /etc/passwd

DESCRIPTION
       /etc/passwd is a local source of information about users'
       accounts. The password file can be used with
       other password sources, including the NIS maps
       passwd.byname and passwd.byuid and the NIS+ table passwd.
       Programs that use the getpwnam(3C) routines to access this information.

       Each passwd entry is a single line of the form:

           username:password:uid:
           gid:gcos-field:home-dir:
           login-shell

       where

       username
           is the user's login name. It is recommended that this
           field conform to the checks performed by pwck(1M).

       password
           is an empty field. The encrypted password for the user
           is in the corresponding entry in the /etc/shadow file.
           pwconv(1M) relies on a special value of 'x' in the
.
.
.
```

请注意，前面的示例（显示手册页）都以 *正在重新分页。请稍候...完成。* 这一短语开头。手册页以 nroff(1) 源文件或 sgml(5) 源文件形式存储。**sgml** 格式的手册页在由 **nroff** 命令格式化之前，会先经过 SGML 预处理器处理。

任何对手册页的搜索基本上都是暴力搜索——也就是说，系统会逐一搜索包含手册页的每个目录，直到找到指定的手册页。为了加快显示和搜索速度，您可以生成并存储手册页的预格式化版本。系统会尽可能使用预格式化版本。在预格式化过程中，还会生成手册页关键字索引。该索引称为 *windex* 数据库。**catman(1M)** 命令负责格式化手册页并生成 windex 数据库。请注意，根据系统 CPU 的速度和当前负载，**catman** 命令可能需要相当长的时间来格式化所有手册页。

此外，拥有 windex 数据库后，您可以在手册页中搜索关键字和文件。以下示例演示了使用 **-f** 命令行参数搜索手册页中与 /etc/passwd 文件相关的内容，以及使用 **-k** 命令行参数搜索关键字 *passwd*：

```text
# man -f /etc/passwd
passwd          passwd (1)          - change login password and
                                      password attributes
passwd          passwd (4)          - password file

# man -k passwd
dpasswd         dpasswd (4)         - dial-up password file
getpw           getpw (3C)          - get passwd entry from UID
kpasswd         kpasswd (1)         - change a user's Kerberos
                                      password
nispasswd       nispasswd (1)       - change NIS+ password information
nispasswd       rpc.nispasswd (1M) - NIS+ password update daemon
passwd          passwd (1)          - change login password and
                                      password attributes
passwd          passwd (4)          - password file
pwconv          pwconv (1M)         - installs and updates
                                      /etc/shadow file information
                                      from /etc/passwd
rpc.nispasswd   rpc.nispasswd (1M) - NIS+ password update daemon
rpc.ypasswdd    rpc.ypasswdd (1M)  - server for modifying NIS
                                      password file
yppasswd        yppasswd (1)      - change your network password
                                      in the NIS database
yppasswdd       rpc.yppasswdd (1M) - server for modifying
                                      NIS password file
#
```

您可以使用 **-d** 命令行参数查看 **man** 命令在尝试定位指定的手册页时的搜索过程。以下示例搜索 windex 数据库。所有可用的章节在 /usr/share/man/man.cf 文件中以章节标识符列表的形式标识，该列表被定义为 **MANSECTS** 变量的内容。每个章节标识符都会被附加
