```
# if no argument for directories given
@defaultmanpath = ( '/usr/share/man' );
```

From this, you can imply that the database will end up being saved as /usr/share/man/whatis.db.

5. A smarter way to ascertain the output filename is to simply log in as root (or use su to change to root), then rebuild the database with the -v flag specified.

```
$ makewhatis -v
Open /usr/share/man/whatis.db.tmp
open manpath directory '/usr/share/man'
lots and lots of output as it lists each man page it finds and parses
sort -u > /usr/share/man/whatis.db.tmp
Rename /usr/share/man/whatis.db.tmp to /usr/share/man/whatis.db
2068 entries in /usr/share/man/whatis.db
```

Not only did this answer the question of "where's the database for apropos?" but it also built it!

Contrast the preceding output from Darwin with the following output from Red Hat Linux:

```
# /usr/sbin/makewhatis -v
about to enter /usr/share/man
adding ./uuidegen.1.gz
lots and lots and lots of output omitted
adding ./vacuum.1.gz
about to enter /usr/man
/usr/sbin/makewhatis: cd: /usr/man: No such file or directory
```

Ahhh...very interesting. The command failed on a stock RHL7.2' system. Having to fix bugs and tweak the system just to get things to work in the first place is not an uncommon occurrence in the world of Unix system administration.

So let's fix this bug, shall we?

6. First off, it's rather surprising that there isn't a /usr/man directory, because that's part of standard (System V) Unix. Let's have a peek to ensure that we're reading this properly:

```
$ ls -l /usr
total 152
drwxr-xr-x 2 root root 36664 Nov 21 14:51 bin
drwxr-xr-x 2 root root 4096 Feb 6 1996 dict
drwxr-xr-x 2 root root 4096 Feb 6 1996 etc
drwxr-xr-x 2 root root 4096 Nov 21 14:36 games
drwxr-xr-x 82 root root 8192 Nov 21 14:51 include
drwxr-xr-x 8 root root 4096 Nov 21 14:49 kerberos
```