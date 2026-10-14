
Using the -l option causes unzip to merely list the contents of the archive without extracting the file. If no file(s) are specified, unzip will list all files in the archive. The -v option can be added to increase the verbosity of the listing. Note that when the archive extraction conflicts with an existing file, the user is prompted before the file is replaced.

Like tar, zip can make use of standard input and output, though its implementation is somewhat less useful. It is possible to pipe a list of file-names to zip via the -@ option:

```
[me@linuxbox foo]$ cd
[me@linuxbox ~]$ find playground -name "file-A" | zip -@ file-A.zip
```

Here we use find to generate a list of files matching the test -name "file-A" and then pipe the list into zip, which creates the archive file-A.zip containing the selected files.

zip also supports writing its output to standard output, but its use is limited because very few programs can make use of the output. Unfortunately, the unzip program does not accept standard input. This prevents zip and unzip from being used together to perform network file copying like tar. zip can, however, accept standard input, so it can be used to compress the output of other programs:

```
[me@linuxbox ~]$ ls -l /etc/ | zip ls-etc.zip -
adding: - (deflated 80%)
```

In this example, we pipe the output of ls into zip. Like tar, zip interprets the trailing dash as "use standard input for the input file."

The unzip program allows its output to be sent to standard output when the -p (for pipe) option is specified:

```
[me@linuxbox ~]$ unzip -p ls-etc.zip | less
```

We touched on some of the basic things that zip and unzip can do. They both have a lot of options that add to their flexibility, though some are platform specific to other systems. The man pages for both zip and unzip are pretty good and contain useful examples.

## Synchronizing Files and Directories

A common strategy for maintaining a backup copy of a system involves keeping one or more directories synchronized with another directory (or directories) located on either the local system (usually a removable storage device of some kind) or a remote system. We might, for example, have a local copy of a website under development and synchronize it from time to time with the "live" copy on a remote web server.

### rsync—Remote File and Directory Synchronization

In the Unix-like world, the preferred tool for this task is rsync. This program can synchronize both local and remote directories by using the rsync remote-update protocol, which allows rsync to quickly detect the differences between two directories and perform the minimum amount of copying required to bring them into sync. This makes rsync very fast and economical to use, compared to other kinds of copy programs.

rsync is invoked like this:

```
rsync options source destination
```

where source and destination are each one of the following:

- A local file or directory
- A remote file or directory in the form of user@host:/path
- A remote rsync server specified with a URI of rsync://user@host[:port]/path

Note that either the source or the destination must be a local file. Remote-to-remote copying is not supported.

Let’s try rsync out on some local files. First, let’s clean out our foo directory:

```
[me@linuxbox ~]$ rm -rf foo/*
```

Next, we’ll synchronize the playground directory with a corresponding copy in foo:

```
[me@linuxbox ~]$ rsync -av playground foo
```

We’ve included both the -a option (for archiving—causes recursion and preservation of file attributes) and the -v option (verbose output) to make a mirror of the playground directory within foo. While the command runs, we will see a list of the files and directories being copied. At the end, we will see a summary message like this, indicating the amount of copying performed:

```
sent 135759 bytes  received 57870 bytes  387258.00 bytes/sec
total size is 3230  speedup is 0.02
```

If we run the command again, we will see a different result:

```
[me@linuxbox ~]$ rsync -av playground foo
building file list ... done
sent 22635 bytes  received 20 bytes  45310.00 bytes/sec
total size is 3230  speedup is 0.14
```

Notice that there was no listing of files. This is because rsync detected that there were no differences between ~/playground and ~/foo/playground, and therefore it didn’t need to copy anything. If we modify a file in playground and run rsync again, we see that rsync detected the change and copied only the updated file.
