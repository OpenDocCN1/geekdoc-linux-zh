+   3. Put the Cd into the directory.
+   4. Extract the file using tar: tar xvf afile.tar.

If the maker of the tar file was conscientious enough to place all the files into a directory, you are set. Sometimes the tar file will contain a file called install.sh or some other installation script. Follow instructions as per any readme files (view them with a page such as less).

# UNIX Compressed Archives: Gzip and Compress

Many times tar files will be distributed in compressed format; the typical extensions for compressed files are .gz (gnu zip, or gzip), .Z for the compress program, and .zip for Windows zip compressed archives. If the file has a name like file.tar.gz, that file is a gnu zip compressed tar file. To extract it, you’ll have to specify the z option to tar:

```
[alberto@digital /tmp]$ tar -xzvf file.tar.gz
nsmail/
nsmail/Drafts
nsmail/.Drafts.summary
nsmail/Trash
nsmail/.Trash.summary
nsmail/Sent
nsmail/.Sent.summary
nsmail/Unsent Messages
nsmail/.Unsent Messages.summary
nsmail/Inbox
nsmail/.Inbox.summary
```

Another way of accomplishing the same task is to use pipes using the gzcat program (similar to cat). This program reads information in the compressed archive, decompresses it, and copies it out to the STDOUT. Here’s an example of how to use gzcat and tar together:

```
gzcat file.tar.gz | tar -xf -
```

In this example, gzcat pipes the resulting output, a tar file, to the tar program. The tar program looks for data in its STDIN stream because the dash (–) is provided to the f option as an argument.

Another way is to decompress the gzip file and then use tar normally. This is more inefficient, and if you are short on disk space, it could cause you to run out of space:

```
gunzip file.tar.gz; tar -xf file.tar
```

The gunzip, gzcat, and the z option to tar can handle files with the .gz or Z extension. If you find a really old archive, you might find it with a .z extension; this is also a gzip compressed file.

If the file is not compressed with tar, it just sports a .gz extension. You can