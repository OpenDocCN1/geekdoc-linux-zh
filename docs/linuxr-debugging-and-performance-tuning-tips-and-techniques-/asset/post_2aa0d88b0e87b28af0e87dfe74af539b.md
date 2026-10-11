
## 5.4.4.2 The V7 cat Revisited

In Section 4.4.4, “Example: Unix `cat`,” page 99, we promised to return to the V7 `cat` program to review its use of the `stat()` system call. The first group of lines that used it were these:

```c
31 fstat(fileno(stdout), &statb);
32 statb.st_mode &= S_IFMT;
33 if (statb.st_mode!=S_IFCHR && statb.st_mode!=S_IFBLK) {
34     dev = statb.st_dev;
35     ino = statb.st_ino;
36 }
```

This code should now make sense. Line 31 calls `fstat()` on the standard output to fill in the `statb` structure. Line 32 throws away all the information in `statb.st_mode` except the file type, by ANDing the mode with the `S_IFMT` mask. Line 33 checks that the file being used for standard output is *not* a device file. In that case, the program saves the device and inode numbers in `dev` and `ino`. These values are then checked for each input file in lines 50–56:

```c
50 fstat(fileno(fi), &statb);
51 if (statb.st_dev==dev && statb.st_ino==ino) {
52     fprintf(stderr, "cat: input %s is output\n", fflg ? "-" : *argv);
53     fflg ? "-" : *argv);
54     fclose(fi);
55     continue;
56 }
```

If an input file’s `st_dev` and `st_ino` values match those of the output file, then `cat` complains and continues to the next file named on the command line.

The check is done unconditionally, even though `dev` and `ino` are set only if the output is not a device file. This works out OK, because of how those variables are declared:

```c
17 int dev, ino = -1;
```

Since `ino` is initialized to −1, no valid inode number will ever be equal to it.¹ That `dev` is not so initialized is sloppy, but not a problem, since the test on line 51 requires that both the device and inode be equal. (A good compiler will complain that `dev` is used without being initialized: `gcc -Wall` does.)

Note also that neither call to `fstat()` is checked for errors. This too is sloppy, although less so; it is unlikely that `fstat()` will fail on a valid file descriptor.

The test for input file equals output file is done only for nondevice files. This makes it possible to use `cat` to copy input from device files to themselves, such as with terminals:

```bash
$ tty
/dev/pts/3
$ cat /dev/pts/3 > /dev/pts/3
This is a line of text
this is a line of text
```

Print current terminal device name
Copy keyboard input to screen
Type in a line
cat repeats it

## 5.4.5 Working with Symbolic Links

In general, symbolic links act like hard links; file operations such as `open()` and `stat()` apply to the pointed-to file instead of to the symbolic link itself. However, there are times when it really is necessary to work with the symbolic link instead of with the file the link points to.

For this reason, the `lstat()` system call exists. It behaves exactly like `stat()`, but if the file being checked happens to be a symbolic link, then the information returned applies to the symbolic link, and not to the pointed-to file. Specifically:

- `S_ISLNK(stbuf.st_mode)` will be true.
- `stbuf.st_size` is the number of bytes used by the name of the pointed-to file.

We already saw that the `symlink()` system call creates a symbolic link. But given an existing symbolic link, how can we retrieve the name of the file it points to? (`ls` obviously can, so we ought to be able to also.)

Opening the link with `open()` in order to read it with `read()` won't work; `open()` follows the link to the pointed-to file. Symbolic links thus necessitate an additional system call, named `readlink()`:

```c
POSIX

#include <unistd.h>
int readlink(const char *path, char *buf, size_t bufsiz);
```

*readlink*() places the contents of the symbolic link named by *path* into the buffer pointed to by *buf*. No more than *bufsiz* characters are copied. The return value is the number of characters placed in *buf* or –1 if an error occurred. *readlink*() does *not* supply the trailing zero byte.

Note that if the buffer passed in to *readlink*() is too small, you will lose information; the full name of the pointed-to file won't be available. To properly use *readlink*(), your code should do the following:

1. Use *lstat*() to verify that you have a symbolic link.
2. Make sure that your buffer to hold the link contents is at least `*buf.st_size*` + `1` bytes big; the `+` `1` is for the trailing zero byte to turn the buffer into a usable C string.
3. Call *readlink*(). It doesn't hurt to verify that the returned value is the same as `buf.st_size`.
4. Assign `'\0'` to the byte after the contents of the link, to make it into a C string.

Code to do all that would look something like this:

```c
/* Error checking omitted for brevity */
int count;
char linkfile[PATH_MAX],  realfile[PATH_MAX];  /* PATH_MAX is in <limits.h> */
struct stat sbuf;

... fill in linkfile with path to symbolic link of interest ... 
lstat(linkfile, & sbuf);                      /* Get stat information */
if ( ! S_ISLNK(sbuf.st_mode))                  /* Check that it's a symlink */
        /* not a symbolic link, handle it */
if (sbuf.st_size + 1 > PATH_MAX)               /* Check buffer size */
        /* handle buffer size problems */

count = readlink(linkfile, realfile, PATH_MAX);  /* Read the link */
if (count != sbuf.st_size)
        /* something weird going on, handle it */

realfile[count] = '\0';                        /* Make it into a C string */
```

This example uses fixed-size buffers for simplicity of presentation. Real code would use *malloc*() to allocate a buffer of the correct size since the fixed-size arrays might be too small. The file *lib/xreadlink.c* in the GNU Coreutils does just this. It reads the contents of a symbolic link into storage allocated by `malloc()`. We show here just the function; most of the file is boilerplate definitions. Line numbers are relative to the start of the file:

```c
55  /* Call readlink to get the symbolic link value of FILENAME.
56      Return a pointer to that NUL-terminated string in malloc'd storage.
57      If readlink fails, return NULL (caller may use errno to diagnose).
58      If realloc fails, or if the link value is longer than SSIZE_MAX + 1) ,
59      give a diagnostic and exit.  */
60
61 char *
62 xreadlink (char const *filename)
63 {
64   /* The initial buffer size for the link value.  A power of 2
65      detects arithmetic overflow earlier, but is not required.  */
66   size_t buf_size = 128;
67
68   while (1)
69     {
70       char *buffer = xmalloc (buf_size);
71       ssize_t link_length = readlink (filename, buffer, buf_size);
72
73       if (link_length < 0)
74         {
75           int saved_errno = errno;
76           free (buffer);
77           errno = saved_errno;
78           return NULL;
79         }
80
81       if ((ssize_t) link_length < buf_size)
82         {
83           buffer[link_length] = 0;
84           return buffer;
85         }
86
87       free (buffer);
88       buf_size *= 2;
89       if (SSIZE_MAX < buf_size || (SSIZE_MAX / 2 < SSIZE_MAX && buf_size == 0))
90         xalloc_die ();
91     }
92 }
```

The function body consists of an infinite loop (lines 68–91), broken at line 84 which returns the allocated buffer. The loop starts by allocating an initial buffer (line 70) and reading the link (line 71). Lines 73–79 handle the error case, saving and restoring `errno` so that it can be used correctly by the calling code.

Lines 81–85 handle the “success” case, in which the link’s contents’ length is smaller than the buffer size. In this case, the terminating zero is supplied (line 83) and then the

---
1 The technical term is a warm fuzzy.
