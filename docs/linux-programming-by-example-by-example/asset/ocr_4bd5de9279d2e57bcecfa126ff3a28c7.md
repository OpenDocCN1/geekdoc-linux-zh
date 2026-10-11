```
```
close (infd);
close (outfd);
exit (EXIT_SUCCESS);
}
```
```

The input file, devices.txt, is included on this book's Web site in this chapter's source code directory. Instead of hard coding an output filename, the program uses the mkstemp call to open a uniquely named file in the current directory. After setting the file pointer 100 bytes into the file, the program then reads 10 bytes, writes them out to the output file, then seeks forward 90 more bytes. The name of the output file will vary from run to run. A test run produced the following output:

![](bbox=[0.05, 0.26, 0.2, 0.32])

# **Output**

```
```
$ ./seek
output file is ttmpjtQXQN
$ cat ttmpjtQXQN
sed: Augusnumbers an included om
ftp://fteX versionunix Files/linux-stanly.        Alloc in the puributed wi
```
```

# **Truncating Files**

Obviously, to lengthen a file, you just write more data to it or lseek over the end. How, then, do you truncate a file? Use the truncate or ftruncate calls, of course. Declared in <unistd.h>, their prototypes are as follows:

```
```
int truncate (const char *pathname, off_t length);
int ftruncate (int fd, off_t length);
```
```

Both calls shorten their file, pathname or fd, to length length, returning 0 on success. Recall that many of the file I/O system calls have two forms, one that takes a standard null-terminated string (truncate) and another, prefixed with f_, that accepts a file descriptor instead of a pathname (ftruncate). If an error occurs, they return -1 and set errno. If you use ftruncate, the file must be opened for writing.

Why would you want to shorten a file using one of these calls? One typical reason is to delete unneeded data from the end of a file while preserving the rest of the file. Truncating a file to the desired length is much easier than creating a new file, reading the data you want from the old file, writing it out to the new file, and deleting the old file. The single truncate or ftruncate call replaces at least four calls, an open, a read, a write, and an unlink.