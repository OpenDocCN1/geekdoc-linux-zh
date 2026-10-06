# Linux Administration: A Beginner's Guide

After copying the file or downloading the file, you will need to unpack (or untar). When unpacked, a tarball will generally create a new directory for all of its files. The hello tarball (hello-2.10.tar.gz), for example, creates the subdirectory hello-2.10. Most packages follow this standard. If you find a package that not follow it, it is a good idea to create a subdirectory with a reasonable name and place the unpacked source files there. This allows multiple builds to occur at the same time without the risk of two builds conflicting.

First change your working directory to the /usr/local/src directory where the hello tarball downloaded and saved to:

```
[root@server -#] cd /usr/local/src
```

Next use the tar command to unpack and decompress the hello archive:

```
[root@server src]# tar -xzvf hello-2.10.tar.gz
hello-2.10/
hello-2.10/build-aux/
hello-2.10/build-aux/test-driver
hello-2.10/build-aux/texinfo.tex
...<OUTPUT TRUNCATED>...
hello-2.10/NEWS
hello-2.10/README-release
```

> The z parameter in this command invokes gzip to decompress the file before the untar process occurs. The v parameter allows tar to show the name of the file it is unsettling as it goes through the process. This way, you'll know the name of the directory where all the sources are being unpacked.

A new directory, hello-2.10, should have been created for you during the untarring. Change to the new directory and list its contents:

```
[root@server src]# cd hello-2.10  ls
```

> NOTE Do not confuse the Linux gzip program with the Microsoft Windows WinZip program. They are two different programs that use different (but comparable) methods of compression. The Linux gzip program can handle files that are compressed by WinZip, and the WinZip program knows how to deal tarballs.