You may want to go through the main program storage directories (/usr/local/ bin, /usr/local/sbin, and /usr/X11R6/bin) and check the status of every program. You can use pkg_info to determine what package owns a file, thus:

```
```
$ pkg_info -W /usr/X11R6/bin/xwave
/usr/X11R6/bin/xwave was installed by package xwave-2.2
$ pkg_info xwave-2.2
Information for xwave-2.2:

Comment:
Audio player/recorder/editor for the X Window System
```
```

**Note** *Some program files, particularly in the /bin, /sbin, /usr/bin, and /usr/sbin directories, don’t appear in the FreeBSD package database. Such programs were installed as part of the base FreeBSD system or by compiling a program from source code without the benefit of the FreeBSD ports system. You’ll have to evaluate these programs in other ways.*

The second `pkg_info` command in the preceding example returns additional information you can use to evaluate whether or not you really need the program installed on the computer. If you don’t, remove the program by using `pkg_delete`, as described further in Chapter 11:

```
```
# pkg_delete xwave-2.2
```
```

Although going through these directories shouldn’t be necessary very frequently, doing so isn’t a bad idea once you’ve become familiar with FreeBSD, in order to help identify and clean out unnecessary programs.

# Keeping a Tab on Users’ Files

Users sometimes consume excessive amounts of disk space. You can check on individual users’ disk space usage with the `du` command, which displays the disk space consumed by every subdirectory of the one you specify. To learn how much disk space is used in a particular directory and all its subdirectories, add the `-s` option. For instance, to learn how much disk space `sskinner` is using, type the command

```
```
# du -s /home/sskinner
61034      /home/sskinner
```
```