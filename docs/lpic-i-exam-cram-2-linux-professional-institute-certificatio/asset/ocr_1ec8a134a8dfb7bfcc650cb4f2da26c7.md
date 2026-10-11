This command uncompresses a copy of the etc/sysconfig directory and its contents in the current directory, in a tree that begins with the etc directory. The use of a hyphen (-) as the file specifier in the tar command means that tar is accepting the standard output of the zcat command and sending that output directly to the tar command as a set of files to be uncompressed.

![](bbox=[0.12, 0.22, 0.25, 0.3])

> This is useful for only one or two exam questions if you find yourself on an older system or a Solaris box that offers only precompression tar.

# ## Using gzip and bzip2 for Compression

The gzip and bzip2 compression utilities are more up-to-date and useful than compress and zcat, and they are similar in their functions and operations. The main difference is that bzip2 offers slightly better compression than gzip, but gzip is much more widely used.

![](bbox=[0.12, 0.46, 0.25, 0.55])

> These commands replace the original file with a new file that has an additional extension, so don't delete the .gz or .bz2 files with you create. They are the original files in a compressed wrapper!

To compress all the files in the current directory with gzip or bzip2, use this command:

```
```
gzip *
```
```

This replaces all the regular files (not the directories or their contents) in the current directory with the original filenames plus a .gz extension. So, if you had two files named file1 and file2 in the directory, they would be replaced with

```
```
file1.gz
file2.gz
```
```

To uncompress these files, just do the exact opposite of the compression:

```
```
gunzip *
```
```

This restores the original files.

Using bzip2 produces the same sort of results. You can issue the following command in the same directory:

```
```
bzip2 *
```
```