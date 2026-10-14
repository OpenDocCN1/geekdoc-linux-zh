
(again, the f option with the dash argument).

## zip

The zip program is both a compression tool and an archiver. The file format used by the program is familiar to Windows users, as it reads and writes .zip files. In Linux, however, gzip is the predominant compression program with bzip2 being a close second.

In its most basic usage, zip is invoked like this:

zip options zipfile file...

For example, to make a zip archive of our playground, we would do this:

```
[me@linuxbox ~]$ zip -r playground.zip playground
```

Unless we include the -r option for recursion, only the playground directory (but none of its contents) is stored. Although the addition of the extension .zip is automatic, we will include the file extension for clarity.

During the creation of the zip archive, zip will normally display a series of messages like this:

```
adding: playground/dir-020/file-Z (stored 0%)
adding: playground/dir-020/file-Y (stored 0%)
adding: playground/dir-020/file-X (stored 0%)
adding: playground/dir-087/ (stored 0%)
adding: playground/dir-087/file-S (stored 0%)
```

These messages show the status of each file added to the archive. zip will add files to the archive using one of two storage methods: Either it will “store” a file without compression, as shown here, or it will “deflate” the file which performs compression. The numeric value displayed after the storage method indicates the amount of compression achieved. Since our playground only contains empty files, no compression is performed on its contents.

Extracting the contents of a zip file is straightforward when using the unzip program:

```
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ unzip ../playground.zip
```

```
[me@linuxbox ~]$ ls -l /etc/ | zip ls-etc.zip -
adding: - (deflated 80%)
```

In this example we pipe the output of ls into zip. Like tar, zip interprets the trailing dash as “use standard input for the input file.”

The unzip program allows its output to be sent to standard output when the -p (for pipe) option is specified:

```
[me@linuxbox ~]$ unzip -p ls-etc.zip | less
```

We touched on some of the basic things that zip/unzip can do. They both have a lot of options that add to their flexibility, though some are platform specific to other systems. The man pages for both zip and unzip are pretty good and contain useful examples. However, the main use of these programs is for exchanging files with Windows systems, rather than performing compression and archiving on Linux, where tar and gzip are greatly preferred.

## Synchronizing Files And Directories

A common strategy for maintaining a backup copy of a system involves keeping one or more directories synchronized with another directory (or directories) located on either the local system (usually a removable storage device of some kind) or a remote system. We might, for example, have a local copy of a website under development and synchronize it from time to time with the “live” copy on a remote web server.

In the Unix-like world, the preferred tool for this task is rsync. This program can synchronize both local and remote directories by using the rsync remote-update protocol, which allows rsync to quickly detect the differences between two directories and perform the minimum amount of copying required to bring them into sync. This makes rsync very fast and economical to use, compared to other kinds of copy programs.

rsync is invoked like this:

```
rsync options source destination
```

where source and destination are one of the following:

- A local file or directory
- A remote file or directory in the form of [user@]host:path
- A remote rsync server specified with a URI of rsync://[user@]host[:port]/path

Note that either the source or the destination must be a local file. Remote-to-remote copying is not supported.

Let's try rsync out on some local files. First, let's clean out our foo directory:

```
[me@linuxbox ~]$ rm -rf foo/*
```

Next, we'll synchronize the playground directory with a corresponding copy in foo:

```
[me@linuxbox ~]$ rsync -av playground foo
```

We've included both the -a option (for archiving—causes recursion and preservation of file attributes) and the -v option (verbose output) to make a mirror of the playground directory within foo. While the command runs, we will see a list of the files and directories being copied. At the end, we will see a summary message like this:

```
sent 135759 bytes  received 57870 bytes  387258.00 bytes/sec
total size is 3230  speedup is 0.02
```

indicating the amount of copying performed. If we run the command again, we will see a different result:

```
[me@linuxbox ~]$ rsync -av playground foo
building file list ... done
sent 22635 bytes  received 20 bytes  45310.00 bytes/sec
total size is 3230  speedup is 0.14
```

Notice that there was no listing of files. This is because rsync detected that there were no differences between ~/playground and ~/foo/playground, and therefore it didn't need to copy anything. If we modify a file in playground and run rsync again:

```
[me@linuxbox ~]$ touch playground/dir-099/file-Z
[me@linuxbox ~]$ rsync -av playground foo
building file list ... done
playground/dir-099/file-Z
sent 22685 bytes  received 42 bytes  45454.00 bytes/sec
total size is 3230  speedup is 0.14
```
