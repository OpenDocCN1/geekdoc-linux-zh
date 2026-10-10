NOTE Remember there are many ways to perform the same task using Linux.

There are other commands that handle compressed files (bzip for bzip2 compressed files, xzcat for xz compressed files and zcat for gzip compressed files) and each one is used to view the contents of a compressed file based on the compression algorithm used.

Verify that the newly created file ftu.txt is the only one in the directory, then create a gzip compressed version of the file:

```
$ ls ftu* ftu.txt $ gzip ftu.txt $ ls ftu* ftu.txt.gz
```

Next, use the zcat command to view the contents of the gzipped compressed file:

```
$ zcat ftu.txt.gz bzip2 cat cut head less md5sum nl od paste sed sha256sum sha512sum sort split tail tr uniq wc xzcat zcat
```

Note that gzip will compress ftu.txt into ftu.txt.gz and it will remove the original file. By default, no output from the gzip command will be displayed. However, if you do want gzip to tell