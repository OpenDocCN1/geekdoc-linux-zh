```
# file *
debug:        ASCII text
history:       ASCII text
```

![](bbox=[0.03, 0.17, 0.12, 0.28])

# ## Data File (UNIX example)

(Described by the **file** command as *data*.)

![](bbox=[0.03, 0.28, 0.12, 0.39])

```
# ls -l Static.dat
-rw-r--r--    1    201        users     235874 Aug 26  1999 Static.dat
# file Static.dat
Static.dat:     data
#
```

# ## Source Code File (UNIX example)

(Described by the **file** command as *c program text*.)

```
# ls -l krsort.c
-rwxrwxrw    1    201        users     3234 Nov 16  1999 krsort.c
# file krsort.c
krsort.c:      c program text
#
```

# ## Source Code File (Linux example)

(Described by the **file** command as *C program text*.)

```
# ls -l *.c
-rw-r-r--    1 root        root     4521 Jul 12  1999 intl-bindtextdom.c
-rw-r-r--    1 root        root     6234 Jul 12  1999 intl-cat-compact.c
-rw-r-r--    1 root        root     14128 Jul 12  1999 intl-dgettext.c
-rw-r-r--    1 root        root     1750 Jul 12  1999 intl-dgettext.c
-rw-r-r--    1 root        root     12759 Jul 12  1999 intl-finddomain.c
-rw-r-r--    1 root        root     1907 Jul 12  1999 intl-gettext.c
-rw-r-r--    1 root        root     1646 Jul 12  1999 intl-intl-compact.c
-rw-r-r--    1 root        root     5361 Jul 12  1999 intl-loadmsgcat.c
-rw-r-r--    1 root        root     7271 Jul 12  1999 intl-localealias.c
-rw-r-r--    1 root        root     2914 Jul 12  1999 intl-textdomain.c
# file *.c
intl-bindtextdom.c:  C program text
intl-cat-compact.c:  C program text
intl-dgettext.c:     C program text
intl-finddomain.c:   C program text
intl-gettext.c:      C program text
intl-intl-compact.c: C program text
intl-loadmsgcat.c:   C program text
intl-localealias.c:  C program text
intl-textdomain.c:   C program text
#
```