
general. You set the umask by subtracting each number of the umask from 7 to arrive at permissions. If you were to start with the permission 777, setting the umask to 202 would leave the file at 575 (or rwxrwx-x, which is strange). By default, the umask is usually 022.

## THE SUID BIT

The SUID bit, which sets the user ID to zero, enables a program to be run as root, without giving the user root access. Certain programs, such as `passwd`, already have the SUID bit set.

Listing 5-4 shows the files in the `/usr/bin` directory that use the SUID bit.

### Listing 5-4: Viewing /usr/bin directory files that use the SUID bit

```bash
# ls -l /usr/bin | grep /usr/bin
-rws--x--x   1 root     bin      21872 Apr   9 18:35 at
-rws--x--x   1 root     root     33972 Mar 18 14:52 chage
-rws--x--x   1 root     root     28480 Mar 18 14:52 chfn
-rws--x--x   1 root     root     26588 Mar 18 14:52 chsh
-rws--x--x   1 root     bin      13376 Apr   9 18:35 crontab
-rws--x--x   1 root     bin      2608 Feb 23 15:56 dumpgrep
-rws--x--x   1 root     root     17712 Mar 18 14:52 expiry
-rwsp--x--   1 root     floppy   20000 Apr 18 00:33 fdmount
-rws--x--x   1 root     root     32752 Mar 18 14:52 gpasswd
-rws--x--x   1 root     bin     130956 Apr  3 22:16 minicom
-rws--x--x   1 root     root     19340 Mar 18 14:52 newgrp
-rws--x--x   1 root     root     34828 Mar 18 14:52 passwd
-rwsp--sr--x  1 root     mail     55884 Apr 30 11:41 popmail
-rwsr--xr-x   1 root     bin      17760 Apr 29 22:00 rcp
-rws--x--x   1 root     bin       4648 Feb 23 15:56 restorefont
-rws--x--x   1 root     bin      4336 Feb 23 15:56 restorerpalette
-rws--x--x   1 root     bin      4016 Feb 23 15:56 restorerxtmode
-rwsr--xr-x   1 root     bin      13688 Apr 29 22:00 rlogin
-rws--x--x   1 root     bin      26936 Mar 26 1997 sudo.bin
-rws--x--x   1 root     bin      463936 Mar 23 00:03 su/pdiper15.00404
```

![](img/8ad518fddafc7f5e73715a2604b61d50_149_0.png)

> If you are developing applications, consider carefully whether your program must use critical files that require root access.

To run executables with the SUID bit set, you must use a file with SUID access (such as the `/etc/passwd` file in the `passwd` command). Always be mindful, however, that such access can be a security risk.

![](img/8ad518fddafc7f5e73715a2604b61d50_150_0.png)

Be careful of how you run SUID programs; they can give hackers entry to your system.

To change permissions or ownership of a file, use the commands `chown`, `chgrp`, and `chmod`. You can also get rid of the SUID bit with the `chmod` command. For example, if you have a program that no longer needs SUID, you can remove it with the command:

```bash
# chmod u-s filename
```

To add SUID, type the following:

```bash
# chmod u+s filename
```

## THE SGID BIT

The SGID bit sets the default for the file's group identification number (GID) to the same GID as its directory instead of the user who is creating the file. For example, if a user, named ace, who is in the spade group, creates a file with the SGID set and the directory is for the group diamondd, the file would then belong to the group diamondd.

To set the GUID bit, type the following:

```bash
# chmod g+s filename
```

To remove the GUID bit, enter:

```bash
# chmod g-s filename
```

Often, root needs to create a file in a user's directory that root itself doesn't need but the user does. When you're happy with the file's contents, change the ownership:

```bash
# chown user:group filename
```

Also change the permissions after finalizing file content:

```bash
# chmod 700 filename
```

![](img/8ad518fddafc7f5e73715a2604b61d50_150_1.png)

Keeping the file permissions simple (such as 700 for a user file) means users need not worry that someone may inadvertently change or delete their files. Giving users full permissions (rwx) makes working easier for them.

## Using the ls command

The ls command is very powerful. With ls, you can get a lot of information about a file. You can find out inode information, links, dot files, directory entries, control characters, and sort to name a few. If you want, you can even have a directory listing in color.

Even if you're familiar with ls as a user, you may find it a wonderful tool for administrative use as well. This command is useful if you're looking for files with control characters. (It can happen accidentally or on purpose, depending on what type of havoc someone is trying to cause.) To list a file with control characters, use the -N or -q option. The -N option displays the control characters, and the -q option replaces the control characters with question marks.

```bash
# ls -N
```

If you're looking for dot files (or hidden files), you may want to use the -A option. The -a option will not hide any . and .. entries (the current and parent directories), but the -A option will. It makes it easier to find the dot files this way.

```bash
# ls -A ~bob
. less
. lessrc
stuff
```

The -a option gives you this:

```bash
# ls -a ~bob
.
..
. less
. lessrc
stuff
```

> The A option can help you find any extra dot files that might cause security problems or could be Trojan horses. A hacker might type in triple dots ( ... ) to get around normal directory listings, or put named dot files ( such as .myfile) in a directory. Also, keep special track of dot files ( such as .netrc ) that store unencrypted passwords!

You can also ignore backup files (files with the ~ at the end) with the -B option. Emacs regularly creates these files. You can define which files to ignore with the --ignore=PATTERN option.

For a convenient example, let's use the following directory listing to see the current files in the directory.

```bash
$ ls
dump
ext2fs
info.txt
info2.txt
ls.txt
mknod
moreinfo
morestuff
```

If you wanted to ignore the file info.txt you would include it with the -ignore option.

```bash
$ ls --ignore=info.txt
dump
ext2fs
info2.txt
ls.txt
mknod
moreinfo
morestuff
```

You can get more information from a directory listing by using the long listing options. The most common one is -l, which can tell you a great deal about a file - including permissions, user, group, file size, modification date and time, and file-name. The l option also provides information on symbolic links, directories, and other special files.

```bash
$ ls -l
-rw-r--r--    1 stripes    users      15908  Aug 10 17:39  dump
-rw-f-r--    1 stripes    users      17944  Aug 10 17:55  ext2fs
-rw-xr-xr-x    1 stripes    users       1452  Aug 11 14:12  info.txt
-rw-f-r--    1 stripes    users       1557  Aug 11 14:15  info2.txt
-rw-f-r--    1 stripes    users       4464  Aug 11 21:42  ls.txt
-rw-f-r--    1 stripes    users       2524  Aug 10 17:25  mknod
drwxr-xr-x    2 stripes    users       1024  Aug 6 17:06  moreinfo
drwxr-xr-x    2 stripes    users       1024  Aug 6 17:07  morestuff
```

You can also get a long listing without the group information by using the -0 option. If you want to have trailing characters to define file type in your listing, use the -F option. From the following listing, you can see executable files identified by asterisks (*); the names of directories appear with forward slashes (/).

```bash
$ ls -F
dump
ext2fs
info.txt*
info2.txt
ls.txt
mknod
moreinfo/
morestuff/
```

You can get more detailed information from the `ls` command. This includes directory long listings. You can also get the file size in kilobytes or blocks. Table 5-1 shows the options that give you various types of file information.

### TABLE 5-1 FILE INFORMATION OPTIONS

| Option | What It Does |
| :--- | :--- |
| -d | Shows directory entries instead of files |
| -i | Prints index number of each file |
| -k | Displays file size in kilobytes |
| -L | Lists entries pointed to by symbolic links |
| -G | Indicates not to show group information |
| -n | Displays numeric UID and GID of a file |
| -R | Recursively lists all subdirectories (use with \| more) |
| -S | Displays file size in blocks |
| --time=WORD | Shows time as WORD instead of modification time: atime, access, use, ctime, or status |

## Monitoring with tail -f

Another basic command with administrative uses is `tail`. For example, if you’re watching a communications device try to connect, you can use `tail -f /var/adm/messages` to monitor its progress, printing new information as it’s happening. It’s like watching the evening news. It’s also a good way to monitor who is getting root access. Listing 5-5 shows an example of the end of `/var/adm/messages`.
