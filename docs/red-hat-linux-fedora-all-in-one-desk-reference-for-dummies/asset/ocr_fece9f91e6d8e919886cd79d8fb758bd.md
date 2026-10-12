After ed opens a file for editing, the current line is the last line of the file. To see the current line number (the current line is the line to which ed applies your command), use the .- command like this:

```
:.=
9
```

This output tells you that the fstab file has nine lines. (Your system's /etc/fstab file may have a different number of lines, in which case ed shows a different number.)

You can use the 1,$p command to see all lines in a file, as the following example shows:

```
:1,$p
LABEL=/                /               ext3    defaults        1 1
LABEL=/boot            /boot           ext3    defaults        1 2
none                   /dev/pts        devpts  gid=5,mode=620  0 0
none                   /proc           proc    defaults        0 0
none                   /dev/shm        tmpfs   defaults        0 0
/dev/hda6              swap            swap    defaults        0 0
/dev/cdrom             /mnt/cdrom      udf,iso9660
/dev/fd0               /mnt/floppy     auto    noauto,owner,kudzu 0 0
:
```

To go to a specific line, type the line number:

```
:6
/dev/hda6              swap            swap    defaults        0 0
:
```

The editor responds by displaying that line.

Suppose you want to delete the line that contains cdrom. To search for a string, type a slash (/) followed by the string that you want to locate:

```
:/cdrom
/dev/cdrom             /mnt/cdrom      udf,iso9660
noauto,owner,kudzu,ro 0 0
:
```

The editor locates the line that contains the string and then displays it. That line becomes the current line.

To delete the current line, use the d command as follows:

```
:d
:
```