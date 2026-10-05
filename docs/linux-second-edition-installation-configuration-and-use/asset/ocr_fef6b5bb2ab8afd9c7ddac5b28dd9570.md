# Examples

user tar -cv text/book

stores all files in the current directory and its subdirectories on the default streamer
 displays the stored files on screen.

user tar -cvf /dev/nst0 text/book

as above, but for the streamer connected to /dev/nst0 (in case the default streamer
tar does not correspond to your streamer).

Generally, you should always specify a path when creating archives. This
makes unpacking easier later on (because the files are automatically extracted into
subdirectories, which avoids possible disorder in the current directory).

user tar -czf book.tgz text/book

archives all files of the directory text/book and all subdirectories in the compressed
file book.tgz.

user find -mtime 7 > /tmp/lastweek

user tar -CT /tmp/lastweek

stores on tape all files that have been modified during the past month.

user tar -tzf backup.tgz

displays all files in the archive.

user tiff linux-2.2.0-pre7.tar.bz2

displays all files of a Linux archive compressed with bzip2.

user tar -xzf backup.tgz

extracts the archive into the current directory.

Always look into your archives with tar -t before unpacking them. By doing
so, you will establish whether path information is stored in the archive and where
the files are going to be installed. Thus, you can create a new directory and
this directory before you run tar -x, or you can use the -c option to prevent the
uncontrolled writing of files in your local directory.

user tar -xzf backup.tgz -C /test

extracts the archive into the directory test.

user tar -zf backup.tgz *.tex

as above, in an alternative notation.

user tar -xzf backup.tgz *.tex

only extracts *.tex files from the archive. Please note the quotes for the search
pattern which prevent immediate evaluation by the shell!

```
root# (cd /dir1 ; tar cf - ) | (cd /dir2 ; tar xvf -)
```

copies all files from /dir1 to /dir2. The advantage as opposed to a normal cp
mand is that symbolic links are copied as such (and not the data pointed to by
links). The above command is particularly useful for transferring whole directory
trees from one partition to another.