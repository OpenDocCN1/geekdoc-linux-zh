
# man man
Reformatting Page. Please wait... Done

User Commands                                      `man(1)`

## NAME
`man` - find and display reference manual pages

## SYNOPSIS
`man [-] [-adFlrt] [-M path] [-T macro-package]`
    `[-s section] name ...`

`man [-M path] -k keyword ...`

`man [-M path] -f file ...`

## DESCRIPTION
The `man` command displays information from the reference manuals. It displays complete manual pages that you select by name, or one-line summaries selected either by keyword (`-k`), or by the name of an associated file (`-f`). If no manual page is located, `man` prints an error message.

### Source Format
Reference Manual pages are marked up with either `nroff(1)` or `sgml(5)` (Standard Generalized Markup Language) tags. The `man` command recognizes the type of markup and processes the file accordingly. The various source files are kept in separate directories depending on the type of markup.

### Location of Manual Pages
The online Reference Manual page directories are conventionally located in `/usr/share/man`. The `nroff` sources are located in the `/usr/share/man/man*` directories. The SGML sources are located in the `/usr/share/man/sman*` directories. Each directory corresponds to a section of the manual. Since

.
.
.

`*passwd*` 主题展示了 `man` 命令的不同命令行参数，因为 `passwd(1)` 是一个命令，而 `passwd(4)` 是一个系统文件。以下示例列出了所有名为 `passwd` 的手册页：

```text
# man -l passwd
passwd (1)       -M /usr/share/man
passwd (4)       -M /usr/share/man
#
```

请注意，两个手册页都被列出。此外，还会显示相应的 `-M` 命令行参数，以指明手册页的位置。手册页的默认路径名为 `/usr/share/man`。

以下示例显示了 `passwd(1)` 手册页：

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

请注意，`man -s 1 passwd` 会提供相同的结果。在未指定章节的情况下，手册页会按章节进行搜索，并打印第一个找到的条目。要显示 `passwd(4)` 手册页，必须指定章节，如下例所示：

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
