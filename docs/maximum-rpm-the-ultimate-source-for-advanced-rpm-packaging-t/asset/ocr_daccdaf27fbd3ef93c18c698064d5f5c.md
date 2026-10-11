```
# rpm2cpio logrotate-1.0-1.i386.rpm > blah.cpio
# file blah.cpio
blah.cpio: ASCII cpio archive (SVR4 with CRC)
```

Here we've directed rpm2cpio to convert the logrotate package file. We've also redirected rpm2cpio's output to a file called blah.cpio. Next, using the `file` command, we find that the resulting file is indeed a bona fide cpio archive file. The following command is entirely equivalent to the previous one and shows rpm2cpio's capability to read the package file from its standard input:

```
# cat logrotate-1.0-1.i386.rpm | rpm2cpio > blah.cpio
```

# 8.2.2. A More Real-World Example: Listing the Files in a Package File

While there's nothing wrong with using rpm2cpio to create a cpio archive file, it takes a few more steps and uses a bit more disk space than is strictly necessary. A somewhat cleaner approach would be to pipe rpm2cpio's output directly into cpio:

```
# rpm2cpio logrotate-1.0-1.i386.rpm | cpio -t
usr/man/man8/logrotate.8
usr/sbin/logrotate
14 blocks
```

In this example, we used the -t option to direct cpio to produce a table of contents of the archive created by rpm2cpio. This can make it much easier to get the right filename and path when you want to extract a file.

# 8.2.3. Extracting One or More Files from a Package File

Continuing the previous example, let's extract the man page from the logrotate package. In the table of contents, we see that the full path is usr/man/man8/logrotate.8. All we need to do is to use the filename and path as shown here:

```
# rpm2cpio logrotate-1.0-1.i386.rpm |cpio -ivd usr/man/man8/logrotate.8
usr/man/man8/logrotate.8
14 blocks
```

In this case, the cpio options -i, -v, and -d direct cpio to do the following:

+   1. Extract one or more files from an archive.
+   2. Display the names of any files processed, along with the size of the archive file, in 512-byte blocks. (Note that the size displayed by cpio is the size of the cpio archive and not the package file.)
+   3. Create any directories that precede the filename specified in the cpio command.