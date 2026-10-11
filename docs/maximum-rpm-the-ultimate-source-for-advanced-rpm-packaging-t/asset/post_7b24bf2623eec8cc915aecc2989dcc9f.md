
# 8. Miscellanea

As with any other large, complex subject, there are always some leftovers—things that just don't seem to fit in any one category. RPM is no exception. This chapter covers those aspects of RPM that can only be called “miscellanea.”

## 8.1. Other RPM Options

The options described in the following sections normally are not used on a day-to-day basis. However, some of them can be quite important when the need arises. One such option is `--rebuilddb`.

### 8.1.1. `--rebuilddb`: Rebuild RPM Database

We all hope the day never comes, and for many of us, it never does. But still, there is a chance that one day, while you're busy using RPM to install or upgrade a package, you'll see this message:

```
free list corrupt (42) - contact rpm-list@redhat.com
```

When this happens, you'll find there's very little that you can do, RPM-wise. However, before you fire off an e-mail to the RPM mailing list, you might try the `--rebuilddb` option. The format of the command is simple:

```
rpm --rebuilddb
```

The command produces no output. After a few minutes, it completes with nary a peep. Here's an example of `--rebuilddb` being used on an RPM database that wasn't corrupt. First, let's look at the files that comprise the database:

```
# cd /var/lib/rpm
# ls
total 3534
-rw-r--r--    1 root     root      1351680 Oct 17 10:35 fileindex.rpm
-rw-r--r--    1 root     root       16384 Oct 17 10:35 groupindex.rpm
-rw-r--r--    1 root     root       16384 Oct 17 10:35 nameindex.rpm
-rw-r--r--    1 root     root      2342536 Oct 17 10:35 packages.rpm
-rw-r--r--    1 root     root       16384 Oct 17 10:35 providesindex.rpm
-rw-r--r--    1 root     root       16384 Oct 17 10:35 requiredby.rpm
#
```

Then, issue the command:

```
# rpm --rebuilddb
#
```

After a few minutes, the command completes, and we take a look at the files again:

```
# ls
total 3531
-rw-r--r--    1 root     root      1351680 Oct 17 20:50 fileindex.rpm
-rw-r--r--    1 root     root       16384 Oct 17 20:50 groupindex.rpm
-rw-r--r--    1 root     root       16384 Oct 17 20:50 nameindex.rpm
-rw-r--r--    1 root     root      2339080 Oct 17 20:50 packages.rpm
-rw-r--r--    1 root     root       16384 Oct 17 20:50 providesindex.rpm
-rw-r--r--    1 root     root       16384 Oct 17 20:50 requiredby.rpm
#
```

You'll notice that packages.rpm decreased in size. This is due to a side-effect of the --rebuilddb option. While it is going through the database, it is getting rid of unused portions of the database. Our example was performed on a newly installed system where only one or two packages have been upgraded, so the reduction in size was small. For a system that has been through a complete upgrade, the difference would be more dramatic.

Does this mean that you should rebuild the database every once in a while? Not necessarily. Since RPM eventually will make use of the holes, there's no major advantage to regular rebuilds. However, when an RPM-based system has undergone a major upgrade, it certainly wouldn't hurt to spend a few minutes using --rebuilddb to clean things up.

### 8.1.2. `--initdb`: Create a New RPM Database

If you are already using RPM, the --initdb option is one you'll probably never have to use. The --initdb option is used to create a new RPM database. That's why you'll probably not need it if you're already using RPM. You already have an RPM database.

It might seem that the --initdb option would be dangerous. After all, won't it trash your current database if you mistakenly use it? Fortunately, the answer is no. If there is an RPM database in place already, it's still perfectly safe to use the option, even though it won't accomplish much. As an example, here's a listing of the files that make up the RPM database on a Red Hat Linux system:

```
# ls /var/lib/rpm
total 3559
-rw-r--r--    1 root     root       16384 Jan  8 22:10 conflictsindex.rpm
-rw-r--r--    1 root     root      1351680 Jan  8 22:10 fileindex.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 groupindex.rpm
-rw-f--r--    1 root     root       16384 Jan  8 22:10 nameindex.rpm
-rw-r--r--    1 root     root      2349640 Jan  8 22:10 packages.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 providesindex.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 requiredby.rpm
#
```

Next, let's use the --initdb option, just to see what it does to this database:

```
# rpm --initdb
# ls /var/lib/rpm
total 3559
-rw-r--r--    1 root     root       16384 Jan  8 22:10 conflictsindex.rpm
-rw-r--r--    1 root     root      1351680 Jan  8 22:10 fileindex.rpm
-rw-f--r--    1 root     root       16384 Jan  8 22:10 groupindex.rpm
-rw-f--r--    1 root     root       16384 Jan  8 22:10 nameindex.rpm
-rw-f--r--    1 root     root      2349640 Jan  8 22:10 packages.rpm
-rw-f--r--    1 root     root       16384 Jan  8 22:10 providesindex.rpm
-rw-f--r--    1 root     root       16384 Jan  8 22:10 requiredby.rpm
#
```

Since an RPM database existed already, the `--initdb` option did no harm to it—there was no change to the database files.

The only other option that can be used with `--initdb` is `--dbpath`. This permits the easy creation of a new RPM database in the directory specified with the `--dbpath` option.

### 8.1.3. `--quiet`: Produce As Little Output As Possible

Adding the `--quiet` option to any RPM command directs RPM to produce as little output as possible. For example, RPM's build command (the subject of Part II, “RPM and Developers: How to Distribute Your Software More Easily with RPM”) normally produces reams of output; by adding the `--quiet` option, this is all you'll see:

```
# rpm -ba --quiet bother-3.5.spec
Package: bother
1 block
3 blocks
#
```

The `--quiet` option can silence even the mighty `-vv` option:

```bash
# rpm -Uvv --quiet eject-1.2-2.i386.rpm
```

### 8.1.4. `--help`: Display a Help Message

RPM includes a concise built-in help message for those times when you need a reminder about a particular command. Normally, you'll want to use the `--help` option by itself, although you might want to pipe the output through a pager such as `less`, since the output is more than one screen long:

```
# rpm --help|less
```

```
RPM version 2.3
Copyright (C) 1995 - Red Hat Software
This may be freely redistributed under the terms of the GNU Public License
usage:
--help			- print this message
--version	- print the version of rpm being used
all modes support the following arguments:
-rcfile <file>	- use <file> instead of /etc/rpmrc and $HOME/.rpmrc
-vv		- be a little more verbose
-qv		- be incredibly verbose (for debugging)
-q			- query mode
--root <dir>	- use <dir> as the top level directory
--dbpath <dir>	- use <dir> as the directory for the database
--queryformat <s>	- use s as the header format (implies -i)
install, upgrade and query (with -p) allow ftp URL's to be used in place of
file names as well as the following options:

--ftp-proxy <host>	- hostname or IP of ftp proxy
--ftpport <port>	- port number of ftp server (or proxy)
```

This is just the first screen of RPM's help command. To see the rest, give the command a try. Practically everything there is to know about RPM is present in the `--help` output. It's a bit too concise to learn RPM from, but it's enough to refresh your memory when the syntax of a particular option escapes you.

### 8.1.5. `--version`: Display the Current RPM Version

If you're not sure what version of RPM is presently installed on your system, the easiest way to find out is to ask RPM itself using the `--version` option:

```
# rpm --version
RPM version 2.3
#
```

## 8.2. Using rpm2cpio

From time to time, you might find it necessary to extract one or more files from a package file. One way to do this would be the following:

1.  Install the package.
2.  Make a copy of the file(s) you need.
3.  Erase the package.

An easier way would be to use `rpm2cpio`.

### 8.2.1. `rpm2cpio`: What Does It Do?

As the name implies, `rpm2cpio` takes an RPM package file and converts it to a cpio archive. Because it's written to be used primarily as a filter, there's not much to be specified. `rpm2cpio` takes only one argument, and even that's optional!

The optional argument is the name of the package file to be converted. If there is no filename specified on the command line, `rpm2cpio` will simply read from standard input and convert that to a cpio archive. Let's give it a try:

```
# rpm2cpio logrotate-1.0-1.i386.rpm
0707020001a86a000081a400000000000000000000000001313118b000000c20000000000
0000300000000000000000190000673ueurs/man/man8/logrotate.8." logrotate
_Log file rotator
.TH rpm 8 "28 November 1995" "Red Hat Software" "Red Hat Linux"
.SH NAME
```

Note that this is only the first few lines of output.

What on earth is all that stuff? Remember that `rpm2cpio` is written as a filter. It writes the cpio archive contained in the package file to standard output, which, if you've not redirected it some-how, is your screen. Here's a more reasonable example:
