The exams don't focus much on compress or its sister utility, *uncompress*. It's enough to know the information in this small section so you can identify a *compress* archive and know what to do with it.

*compress*, *uncompress*, and *zcat* are utilities that date back to when the *tar* command didn't offer the *gzip* and *bzip2* compression options.

Creating an archive in precompression *tar* days was a two-step process: You archived the files in a *.tar* file and then ran *compress*, *gzip*, or *bzip2* on the file. Using any of the three replaced the original file with one that added an extension to the original filename that indicated it was compressed.

For example, the first step in the process is to use the following command to create a *.tar* file:

```
tar -cf archive.tar /tarfoo
```

This creates a file named *archive.tar* in the current directory. The next step is to run the *compress* command on the file:

```
compress archive.tar
```

This produces a file named *archive.tar.z* in the current directory, replacing the *archive.tar* file.

Using *uncompress*, you can then uncompress the *archive.tar.z* archive with the following command:

```
uncompress archive.tar.z
```

Or, you can use the *gunzip* command to uncompress the file, meaning you can then recompress it with *gzip* or do whatever you want with it:

```
gunzip archive.tar.z
```

Either way, uncompressing the *archive.tar.z* file removes the compression and the *.z* extension, leaving only the original *.tar* file.

Another utility used in conjunction with the *compress* and *uncompress* commands is the *zcat* utility. You should never use *zcat* on a *.z* compressed file because it shows the contents of the file as if you had used *cat* on the original file and makes a lot of horrible beeping noises when the control codes in the binary file are shown onscreen.

For example, you can take a compressed file such as a copy of the /etc/sysconfig directory contained in a file named *sysconfig.tar.gz* and uncompress it with the *tar* command and the *zcat* command:

```
zcat sysconfig.tar.gz | tar xvf -
```