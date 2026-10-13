The following example shows how you can use the **man** command to display the **man(1)** man page. Note that man pages longer than one screen use the **more(1)** command to display one screen of the man page at a time:

```
# man man
Reformatting Page. Please wait... Done
```

# User Commands　　　　　　　　　　　　　　　　　　　　　　　　　man(1)

# NAME

man - find and display reference manual pages

# SYNOPSIS

```
man [- · ] [ -adFlrt ] [ -M path ] [ -T macro-package ]
    [ -s section ] name ...

man [ -M path ]  -k keyword ...

man [ -M path ]  -f file ...
```

# DESCRIPTION

The man command displays information from the reference manuals. It displays complete manual pages that you select by name, or one-line summaries selected either by keyword (-k), or by the name of an associated file (-f). If no manual page is located, man prints an error message.

# Source Format

Reference Manual pages are marked up with either nroff(1) or sgml(5) (Standard Generalized Markup Language) tags. The man command recognizes the type of markup and processes the file accordingly. The various source files are kept in separate directories depending on the type of markup.

# Location of Manual Pages

The online Reference Manual page directories are conventionally located in /usr/share/man. The nroff sources are located in the /usr/share/man/man* directories. The SGML sources are located in the /usr/share/man/sman* directories. Each directory corresponds to a section of the manual. Since

```
.
.
.
```

The *passwd* topic shows the different **man** command-line arguments because **passwd(1)** is a command and **passwd(4)** is a system file. The following example lists all man pages named *passwd*:

```
# man -l passwd
passwd (1)       -M /usr/share/man
passwd (4)       -M /usr/share/man
#
```

Note that both man pages are listed. In addition, an appropriate **-M** command-line argument is displayed to show the location of the man pages. The default pathname for man pages is /usr/share/man.