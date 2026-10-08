```
castle% find . -perm u+rwx,g=rx,o=rx
./.dt
./.dt/sessions
./.dt/sessions/current
./.dt/sessions/current.old
./.dt/types
./.dt/types/fp_dynamic
./.dt/tmp
./.dt/sessionslogs
./.dt/icons
./.dt/appmanager
./.dt/help
./.dt/help/winsor-castle-0
./.dt/Trash
./.dt/palettes
./.dt/Printers/sechildl_Print
./.dtprofile
castle% find . -perm -o+w
./.local.chshrc
./.dt/sessions/current/dt.session
./.dt/sessions/current/dt.settings
./.dt/sessions/current/dt.resources
./.dt/sessions/current.old/dt.session
castle$
```

The following example removes all files in your home directory named a.out or *.o
that have not been accessed for a week.

```
castle$ find HOME \-name a.out -name '*.o' \-atime +7 -exec rm {} \\
```

The following example recursively prints all file names in the current directory and
below but skips SCCS directories.

```
castle% find -name SCCS -prune -o -print
```

The following example recursively prints all file names in the current directory and
below, skipping the contents of SCCS directories but pruning the SCCS directories
name.

```
castle$ find . -print -name SCCS -prune
```

The following command is basically equivalent to the -nt extension to test(1).

```
castle$ if [ -n "$(find file1 -prune newer file2)" ]; then printf %s
"file1 is newer than file2"
```

The following command recursively prints all file names whose permission mode
exactly matches, read, write, and execute access for user, read and execute access for
group and other.

```
castle% find . -perm u+rwx,g=rx,o=rx
```

You could also specify the above command in the following way.

```
castle% find -perm a=rwx,g-w,o-w
```