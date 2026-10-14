# 6.2 File System Hierarchy

The file system hierarchy in Tru64 UNIX version 5 has been modified slightly from the version 4 layout.

The version 5 file system layout is illustrated in Figure 6-4. The root (/), /usr, and /var directories have a new directory, named /cluster, added to each directory. Underneath each cluster directory is the members directory. The members directory is where the member-specific directories will be located. As you can see by the figure, each members directory currently contains two files:

+   - member
+   - member0

The member0 file is the standalone system's member-specific directory, while the member file is a member-neutral identity link, a CDSL, to allow you to get to that member's member-specific directory quickly.

```
# for i in /usr /var
> do
> cd $i(/)/cluster/members
> print "$i(${PWD})"
> ls -ld *
> done

[/cluster/members]
lrwxr-xr-x 1 root system 6 Jan 26 08:46 member -> (memb)
drwxr-xr-x 9 root system 8192 Feb 6 18:41 member0

[/usr/cluster/members]
lrwxr-xr-x 1 root system 6 Jan 26 08:47 member -> (memb)
drwxr-xr-x 7 root system 8192 Jan 26 08:47 member0

[/var/cluster/members]
lrwxr-xr-x 1 root system 6 Jan 26 08:51 member -> (memb)
drwxr-xr-x 22 root system 8192 Feb 6 17:02 member0
```

The other CDSL in the diagram is a hidden file in the root (/) directory called ".local..".

```
# ls -l /.local.. | awk '{ print $9,$10,$11 }'
/.local.. -> cluster/members/(memb)
```

This example illustrates a quick way to show a file name and its link. Since this command will come in handy throughout this chapter (and the rest of the book), let's create a function to use this command so you can save on typing. To make this change even more permanent, you can place it in your ".profile" file. Note: this particular function works in the Korn shell.