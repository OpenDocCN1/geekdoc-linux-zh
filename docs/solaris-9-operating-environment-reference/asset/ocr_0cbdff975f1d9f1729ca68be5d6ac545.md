# vi, view, vedit 1521

# Files

+   - index File where source for index is created.
 /usr/lib/vgrindefs
- Language descriptions.
 /usr/lib/vfontedpr
- Preprocessor.
 /usr/share/lib/vmac/tmac.vgrind
- Macro package.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUMdoc |

# See Also

csh(1), ctags(1), eqn(1), tbl(1), troff(1), attributes(5), vgrindefs(5)

# vi, view, vedit - Screen-Oriented Visual Display Editor on ex

# Synopsis

```
/usr/bin/vi [- -s] [-l] [-L] [-R] [-r [filename]] [-S] [-t tag] [-v]
[-V] [-wn] [-C] [+command] [-c command] filename...
/usr/bin/view [- -s] [-l] [-L] [-r [filename]] [-S] [-t tag] [-v]
[-V] [-wn] [-C] [+command] [-c command] filename...
/usr/bin/vedit [- -s] [-l] [-L] [-r [filename]] [-S] [-t tag]
[-V] [-X] [-wn] [-C] [+command] [-c command] filename...
/usr/vi [- -s] [-l] [-L] [-r [filename]] [-S] [-t tag]
[-v] [-X] [-wn] [-C] [+command] [-c command] filename...
/usr64/bin/view [- -s] [-l] [-L] [-R] [-S] [-t tag]
[-v] [-X] [-wn] [-C] [+command] [-c command] filename...
/usr64/bin/vedit [- -s] [-l] [-L] [-r [filename]] [-S]
[-t tag] [-v] [-wn] [-C] [+command] [-c command]
filename..
```

# Description

vi(visual) is a display-oriented text editor based on the underlying ex line. You can use the command mode ex from within vi, and you can use the command mode vi from within vi. The visual commands are described on this manual page. Refer to the ex(1) manual for information about all ex line editor commands and how to