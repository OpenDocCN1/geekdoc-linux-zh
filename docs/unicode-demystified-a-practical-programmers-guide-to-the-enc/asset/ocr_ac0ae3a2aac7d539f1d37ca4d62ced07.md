# $ grep portable 2>/dev/null

The preceding command looks for the word portable in the working directory. Any output to standard error (page 552), such as permission or directory errors, is discarded while output to standard output appears on the screen.

/dev/pts The /dev/pts filesystem, a hook into the Linux kernel, helps you visualize the open pseudotystem—it part of the pseudotystem support. Pseudotinals are used by remote login programs, such as ssh, telnet, and xterm. The following sequence of commands demonstrates that the user is logged in on /dev/pts/1. After using who am i to verify the line is logged in on and is to show that that line, the user redirects the output of an echo command to /dev/pts/1; whereupon the output appears on the user's:

```
$ who am i
bravo.tcorp.com!alex pts/1 May 10 13:03
$ ls /dev/pts
0 1 2
$ echo Hi there > /dev/pts/1
Hi there
```

/dev/zero Input you take from this file contains an infinite string of zeros (nulls or numerical, not ASCII, zeros). You can fill a file (as a swap file—page 967) or overwrite a file with zeros with a command such as the following. The od utility shows the contents of the new file:

```
$ dd if=/dev/zero of=zeros bs=1024 count=10
10+0 records out
10+0 records out
$ ls -l zeros
-rw-r--r-- 1 alex 10240 Dec 3 20:26 zeros
$ od -c zeros
0000000 \00 \00 \00 \00 \00 \00 \00 \00 \00 *
0024000
```

When you try to do with /dev/zero what you can do with /dev/null, quickly fill the partition you are working in:

```
$ cp /dev/zero bigzero
cp: writing 'bigzero': No space left on device
$ rm bigzero
```

/etc/aliases Used by the mail system (typically sendmail) to construct aliases for users. Edit this file to suit your local preferences. This file contains a number of good examples showing how you can create aliases for users, creating mailing lists, and direct e-mail to files. After editing this file, run newaliases to rebuild the aliases database. Refer to “aliases: Setting up E-Mail Aliases” on page 1054.