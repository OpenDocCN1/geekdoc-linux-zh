Let’s assume this leaves us with/dev/hda1,/dev/hda3,/dev/hda5, and/dev/hda6. To back up these to/dev/nst0, compressing them along the way, we would issue the following series of commands:

```
[root@scribe /root]# mt -f /dev/nst0 rewind
[root@scribe /root]# dump -0uz -f /dev/nst0 /dev/hda1
[root@scribe /root]# dump -0uz -f /dev/nst0 /dev/hda3
[root@scribe /root]# dump -0uz -f /dev/nst0 /dev/hda5
[root@scribe /root]# dump -0uz -f /dev/nst0 /dev/hda6
[root@scribe /root]# mt -f /dev/nst0 rewind
[root@scribe /root]# mt /dev/nst0 eject
```

The first **mt** command is to make sure the tape is completely rewound and ready to accept data. Then come all the **dump** commands, which are run on the partitions using zlib compression. We finally rewind the tape and eject it.

![](bbox=[0.12, 0.41, 0.25, 0.44])

It’s considered dangerous to dump file systems that are being actively used. The only way to be 100 percent sure that a file system is not in use is by unmounting it first. Unfortunately, very few people can afford the luxury of unmounting a system for the time necessary to do a backup. The next best thing is to go through the unappealing task of verifying backups on a regular basis. Verification is best done by testing to see if the **restore** program (discussed in the next section, “Using restore”) can completely read the tape and extract files from it. It’s tedious, and it isn’t fun. But many a systems administrator has lost a job over bad backups—don’t be one of them!

# Using restore

The **restore** program reads the dump files created by **dump** and extracts individual files and directories from them. Although **restore** is a command-line tool, it does offer a more intuitive interactive mode that lets you go through your directory structure from the tape.

Table 21-3 shows many of the command-line options for the **restore** utility.

| restore Option | Description |
| :--- | :--- |
| -I | Enables interactive mode for **restore**. The utility will read the directory contents of the tape and then give you a shell-like interface in which you can move directories around and tag files you want to recover. When you’ve tagged all the files you want, **restore** will go through the dump and restore those files. This mode is handy for recovering individual files, especially if you aren’t sure which directory they’re in. |

**Table 21-3** Common Options for the restore Command