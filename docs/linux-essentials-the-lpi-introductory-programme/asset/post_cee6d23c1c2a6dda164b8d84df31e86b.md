
62%", for example, means that, inside the archive, the file is only 38% of its original size). `zip` automatically chooses the more sensible approach, unless you disable compression completely using the `-0` option.

If you invoke `zip` with an existing ZIP archive as its first parameter and do not specify anything else, the files to be archived are *added* to the archive on top of its existing content (existing files with the same names are overwritten). In this case `zip` behaves differently from `tar` and `cpio` (just so you know). If you want a "clean" archive, you must remove the file first.

Besides stupidly adding of files, `zip` supports several other modes of operation: The `-u` option "updates" the archive by adding files to the archive only if the file mentioned on the command line is newer than a pre-existing file of the same name in the archive (named files that are not in the archive yet are added in any case). The `-f` option "refreshes" the archive---files inside the archive are overwritten with newer versions from the command line, but only if they actually exist in the archive already (no completely new files are added to the archive). The `-d` option considers the file names on the command line as the names of files within the archive and deletes those.

Newer versions of `zip` also support the `-F5` ("filesystem sync") mode: This mode "synchronises" an archive with the file system by doing essentially what `-u` does, but also deleting files from the archive that have not been named on the command line (or, in case of `-r`, are part of a directory being searched). The advantage of this method compared to a full reconstruction of the archive is that any preexisting unchanged files in the archive do not need to be compressed again.

`zip` supports all sorts of options, and you can use `zip -h` to look at a list (or `-h2` to look at a more verbose list). The man page, `zip(1)`, is also very informative.

You can unpack a ZIP archive again using `unzip` (this can also be a ZIP archive from a Windows machine). It is best to take a peek inside the archive first, using the `-v` option, to see what is in there---this may save you some hassle with subdirectories (or their absence).

```
$ unzip -v test
Archive:  test.zip
Length  Method   Size  Cmpr  Date   Time  CRC-32  Name
--------  ----------  ------  ----  ---------- -----  ---------  ----------------
     0   Stored         0   0% 2012-02-29 09:29  00000000  ziptest/
   16163 Defl:N     6191  62% 2012-02-29 09:46  0d9df6ad  ziptest/testfile
   18092 Defl:N     6811  62% 2012-02-29 09:01  4e46f1a1  ziptest/file2
   35147 Defl:N    12119  66% 2012-02-29 09:01  6777f57c  ziptest/file1
--------          ----------  -----  ---------  ----------------
   69402         25121   64%                    4 files
```

Calling `unzip` with the name of the archive as its single parameter suffices to unpack the archive:

```
$ mv ziptest ziptest.orig
$ unzip test
Archive:  test.zip
 creating: ziptest/
 inflating: ziptest/testfile
 inflating: ziptest/file2
 inflating: ziptest/file1
```

Use the `-d` option to unpack the archive in a different directory than the current one. This directory is created first if necessary:

```
$ unzip -d dir test
Archive:  test.zip
creating: dir/ziptest/
inflating: dir/ziptest/testfile
inflating: dir/ziptest/file2
inflating: dir/ziptest/file1
```

If you name particular files on the command line, then only these files will be unpacked:

```
$ rm -rf ziptest
$ unzip test ziptest/file1
Archive:  test.zip
inflating: ziptest/file1
```

(In this case, the ziptest directory will also be created.)

Alternatively, you can use the -x option to selectively exclude certain files from being unpacked:

```
$ rm -rf ziptest
$ unzip test -x ziptest/file1
Archive:  test.zip
creating: ziptest/
inflating: ziptest/testfile
inflating: ziptest/file2
```

You can also use shell search patterns to unpack certain files (or prevent them from being unpacked):

```
$ rm -rf ziptest
$ unzip test "ziptest/f*"
Archive:  test.zip
inflating: ziptest/file2
inflating: ziptest/file1
$ rm -rf ziptest
$ unzip test -x "*/*"
Archive:  test.zip
creating: ziptest/
inflating: ziptest/file2
inflating: ziptest/file1
```

(Note the quotes, which are used to hide the search patterns from the actual shell so unzip gets to see them.) Unlike in the shell, the search patterns refer to the *complete* file names (including any “/”).

As is to be expected, unzip also supports various other options. Look at the program’s help information using “unzip -h” or “unzip -hh”, or read unzip(1).

## Exercises

- 11.10 [!2] Create some files inside your home directory and store them in a zip archive. Look at the content of the archive using “unzip -v”. Unpack the archive inside the /tmp directory.
- 11.11 [!1] What happens if a file that you are about to unpack using unzip already exists in the file system?
- 11.12 [2] A ZIP archive *files.zip* contains two subdirectories *a* and *b*, which in turn contain a mixture of files with various suffixes (e.g., *.c*, *.txt*, and *.dat*). Give an unzip command to extract the complete content of *a* except for the *.txt* files (in one step).

## Commands in this Chapter

- bunzip2: File decompression program for .bz2 files [bzip2(1), p. 152]
- bzip2: File compression program [bzip2(1), p. 147]
- gzip: File compression utility [gzip(1), p. 147]
- split: Splits a file into pieces up to a given maximum size [split(1), p. 147]
- tar: File archive manager [tar(1), p. 146]
- unzip: Decompression software for (Windows-style) ZIP archives [unzip(1), p. 153]
- zip: Archival and compression software like PKZIP [zip(1), p. 152]

## Summary

- “Archival” collects many files into one large file. “Compression” reversibly determines a more compact representation for a file.
- tar is the most common archival program on Linux.
- gzip is a program for compressing and decompressing arbitrary files. It can be used together with tar.
- bzip2 is another compression program. It can achieve higher compression ratios than gzip, but also needs more time and memory.
- The *zip* and *unzip* programs are available to process ZIP archives as used (for example) by the PKZIP program on Windows.

## Bibliography

- **RFC1951** P. Deutsch. “DEFLATE Compressed Data Format Specification version 1.3”, May 1996. http://www.ietf.org/rfc/rfc1951.txt

![](img/44bdd771e9c9b1353d2401c2892b2459_156_0.png)

# 12

## Introduction to System Administration

### Contents

- 12.1 System Administration Basics . . . . . . . . . . . . . . . . . . . . 158
- 12.2 System Configuration . . . . . . . . . . . . . . . . . . . . . . . . . . 159
- 12.3 Processes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 160
- 12.4 Package Management . . . . . . . . . . . . . . . . . . . . . . . . . . 165

### Goals

- Having insight into the role of a system administrator
- Understanding the basics of the operating system kernel and processes
- Knowing about package management concepts

### Prerequisites

- Basic use of the shell (Chapter 4)
- Knowledge of Linux file system structure (Chapter 10)

# 12.1 System Administration Basics

What does a system administrator do? Configure computers, install software (and occasionally remove it), connect peripherals and make them usable, make back-ups (and occasionally restore them), add and remove user accounts, help users with problems, … it is an impressive list of tasks. In the old days of home computers, the user of a computer was also the administrator, and this idea has been kept going for a long time in systems like Windows (even once Windows had acquired the notion of different users, it was common to have to use the “Administrator” account, simply because various important programs assumed the corresponding privileges were available). Unix—the system that inspired Linux—was set up from its very beginnings to support several users, and hence the separation between an “administrator” with special privileges and “normal” users is rooted far more deeply in the system than with operating systems from the home computer tradition.

![](img/44bdd771e9c9b1353d2401c2892b2459_157_0.png)

The LPI's *Linux Essentials* exam does not emphasise system administration, but you should have at least a general overview—perhaps not to *be* the system administrator, but to achieve a better understanding of what your system administrator does for you, or at some point *become* a system administrator. Knowledge important for system administrators is part of the LPI's LPIC certification track, particularly LPIC-2 and LPIC-3.

In this chapter we shall mention several topics that have less to do with the immediate use of a Linux computer, but include, for example, how to get a picture of what is running on the computer (cue “Why is my computer so slow??”), and how software is managed on the computer. We’re really after the big picture here, not details.

On a Linux system, the system administrator has access to a special user account, *root*. This account is exempt from the access checks (Chapter 14) which are otherwise performed, and can therefore access all files on the system. This is necessary, for example, to install new software—“normal” users may read and execute program files from system directories but, in order to prevent manipulations to the detriment of other users, not write them. The administrator must also be able to read *any* user's files in order to create backup copies (and to write them back if a backup needs to be restored).

![](img/44bdd771e9c9b1353d2401c2892b2459_157_1.png)

It is obvious that the ability to write all files on the system includes the opportunity to damage the system seriously. If you are logged in as *root*, Linux does not prevent you from using a command like

```
rm -rf /
```

to destroy the whole file system (and there are lots of more subtle ways to do damage). Hence you should avail yourself of *root* privileges only if you actually need them. Surfing the web or reading mail while logged in as *root* is RIGHT OUT.

![](img/44bdd771e9c9b1353d2401c2892b2459_157_2.png)

If you can read all files on the system as *root*, you might succumb to the temptation of, say, regularly inspecting your boss's (or spouse's) e-mail. DON’T DO IT. It may be destructive (at least in the case of your spouse) and /or illegal (at least in the case of your boss) and it can get you into all sorts of trouble that are liable to spoil your fun with Linux and system administration, to say nothing of domestic or workplace peace. There is nothing wrong with taking an isolated brief peek, in consultation with the people involved, into a mailbox file in order to diagnose or repair a problem—but do not let it become a habit.

![](img/44bdd771e9c9b1353d2401c2892b2459_157_3.png)

When in doubt, think of Peter Parker, a. k. a. Spider-Man: “With great power comes great responsibility.”
