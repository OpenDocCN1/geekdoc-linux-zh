with associative arrays. This script, called array-2, when given the name of a directory, prints a listing of the files in the directory along with the names of the file's owner and group owner. At the end of the listing, the script prints a tally of the number of files belonging to each owner and group. Here we see the results (condensed for brevity) when the script is given the directory /usr/bin:

```
[me@linuxbox ~]$ array-2 /usr/bin
/usr/bin/2to3-2.6          root    root
/usr/bin/2to3             root    root
/usr/bin/a2p              root    root
/usr/bin/abrowser         root    root
/usr/bin/aconnect         root    root
/usr/bin/acpi_fake key    root    root
/usr/bin/acpi_listen      root    root
/usr/bin/add-apt-repository root root
-- snip --
/usr/bin/zipgrep          root    root
/usr/bin/zipinfo          root    root
/usr/bin/zipnote          root    root
/usr/bin/zip              root    root
/usr/bin/zipsplit         root    root
/usr/bin/zsdecode         root    root
/usr/bin/zsoelim          root    root

File owners:
daemon  :   1 file(s)
root    : 1394 file(s)

File group owners:
crontab :   1 file(s)
daemon  :   1 file(s)
lpadmin :   1 file(s)
mail    :   4 file(s)
mlocate :   1 file(s)
root    : 1380 file(s)
shadow  :   2 file(s)
ssh     :   1 file(s)
tty     :   2 file(s)
utmp    :   2 file(s)
```

Here is a listing (with line numbers) of the script:

```
1   #!/bin/bash
2
3   # array-2: Use arrays to tally file owners
```