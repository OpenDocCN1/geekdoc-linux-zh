To extract the file from the floppies, put the first volume in the drive and use the following command:

```
# tar -xvMF /dev/fd0
```

You will be prompted to put in the subsequent floppies, as you were when the archive was written. Unfortunately, the tar command won't allow you to compress a multi-volume backup. If you attempt to do so, you will get the following error:

```
tar: Cannot use multi-volume compressed archives
```

```
tar: Error is not recoverable: exiting now
```

Although tar will write to standard output with the -0 argument, it will not read a file list from standard input, unlike many other archiving utilities. Many consider this to be a major disadvantage. The next two archiving utilities, cpio and afio, have this capability.

# cpio

The cpio utility, named for the cp command and input/output I/O, was designed to have the advantages of both dump and tar, including the ability to backup and restore special files and to provide for the extraction of single files or directories from a cpio archive. Its primary use is to transfer files from one computer to another rather than archiving. However, because cpio reads from standard input and writes to standard output, it is a great candidate for scripted backups. Because the output may be redirected to either a file or a raw device, this command is quite versatile and is frequently used in place of tar. The use of cpio has dropped off somewhat with the advent of afio.

# Archiving to a Local Directory

Since cpio expects the list of files to archive to come from standard input, input and output follow standard redirection cpio uses the o argument to create an archive. Just as tar, the i argument is used to unpack the archive and the t argument is used to list the contents of the archive.

Let's start with a simple example. To archive the files in the current directory into a named archive.cpio, use the following command:

```
# find . | cpio -o > archive.cpio
```

The output will look something like this:

```
cpio: : truncating inode number
```

```
cpio: usr/local/bin: truncating inode number
```

```
cpio: usr/local/bin/gpg-check: truncating inode number
```

```
cpio: usr/local/bin/gpg-encrypt: truncating inode number
```

![](bbox=[0.883, 0.433, 0.953, 0.633])