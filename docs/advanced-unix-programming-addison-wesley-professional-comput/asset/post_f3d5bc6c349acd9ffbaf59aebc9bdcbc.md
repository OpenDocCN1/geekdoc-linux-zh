
you’re working with, ${ }^{8}$ but some experimentation has shown that, within reason, larger numbers are better than smaller ones, and here’s why: If the number is less than the actual block size, and divides evenly into it, the kernel can very efficiently pack the writes into a buffer and then schedule the buffer to be written when it’s full. If the number is bigger and a multiple of the buffer size, it’s still very efficient for the kernel to fit the data into buffers *and* there are fewer $write$ system calls, which tends to be the overwhelming factor. A similar argument holds for $reads$.

So, by far the easiest thing to do is to use the macro $B U F S I Z$, defined by Standard C, which is what the standard I/O functions (e.g., $f p u t s$) use. It’s not optimized for the actual file systems, being constant, but the experiments showed that that doesn’t matter so much. If space is at a premium, you can even use 512 and you’ll be fine.

## 2.12.2 Functions for User Buffering

It’s convenient to use a set of functions that do reads, writes, seeks, and so on, in whatever units the caller wishes. These subroutines handle the buffering automatically and never stray from the block model. An exceptionally fine example of such a package is the so-called “standard I/O library,” described in most books on C, such as [Har2002].

To show the principles behind a user-buffering package, I’ll present a simplified one here that I call $B U F I O$. It supports reads and writes, but not seeks, in units of a single character. First, the header file bufio.h that users of the package must include (prototypes not shown):

```c
typedef struct {
int fd;
char dir;
size_t total;
size_t next;
unsigned char buf[BUSIZ];
} BUFFIO;
```

Now for the implementation of the package (bufio.c):

```c
BUFIO *Bopen(const char *path, const char *dir)
{
BUFIO *b = NULL;
int flags;

switch (dir[0]) {
case 'r':
flags = O_RDONLY;
break;
case 'w':
flags = O_WRONLY | O_CREAT | O_TRUNC;
break;
default:
errno = EINVAL;
EC_FAIL
}
ec_null( b = calloc(1, sizeof(BUFIO)) )
ec_neg!( b->fd = open(path, flags, PERM_FILE) )
b->dir = dir[0];
return b;

EC_CLEANUP_BGN
free(b);
return NULL;
EC_CLEANUP_END
}

static bool readbuf(BUFIO *b)
{
ec_neg!( b->total = read(b->fd, b->buf, sizeof(b->buf)) )
if (b->total == 0) {
errno = 0;
return false;
}
b->next = 0;
return true ;

EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}

static bool writebuf(BUFIO *b)
{
size_t n, total;

total = 0;
while (total < b->next) {
ec_neg!( n = write(b->fd, &b->buf[total], b->next - total) )
total += n;
}
b->next = 0;
return true;
}

EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}

int Bgetc(BUFIO *b)
{
if (b->next >= b->total)
if (!readbuf(b)) {
if (errno == 0)
return -1;
EC_FAIL
}
return b->buf[b->next++];

EC_CLEANUP_BGN
return -1;
EC_CLEANUP_END
}

bool Bputc(BUFIO *b, int c)
{
b->buf[b->next++] = c;
if (b->next >= sizeof(b->buf))
ec_false( writebuf(b) )
return true;

EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}

bool Bclose(BUFIO *b)
{
if (b != NULL) {
if (b->dir == 'w')
ec_false( writebuf(b) )
ec_neg1( close(b->fd) )
free(b);
}
return true;

EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}
```

## User Buffered I/O

Finally, we recode our file-copy function to use the new package:

```c
#include "bufio.h"

bool copy3(char *from, char *to)
{
BUFIO *stfrom, *stto;
int c;

ec_null( stfrom = Bopen(from, "r") )
ec_null( stto = Bopen(to, "w") )
while ((c = Bgetc(stfrom)) != -1)
ec_false( Bputc(stto, c) )
if (errno != 0)
EC_FAIL
ec_false( Bclose(stfrom) )
ec_false( Bclose(stto) )
return true;

EC_CLEANUP_BGN
(void)Bclose(stfrom);
(void)Bclose(stto);
return false;
EC_CLEANUP_END
}
```

You will notice a strong resemblance between BUFIO and a subset of the standard I/O library. Here’s a version of copy using library functions:

```c
bool copy4(char *from, char *to)
{
FILE *stfrom, *stto;
int c;

ec_null( stfrom = fopen(from, "r") )
ec_null( stto = fopen(to, "w") )
while ((c = fgetc(stfrom)) != EOF)
ec_eof( putc(c, stto) )
ec_false( ferror(stfrom) )
ec_eof( fclose(stfrom) )
ec_eof( fclose(stto) )
return true;

EC_CLEANUP_BGN
(void)fclose(stfrom);
(void)fclose(stto);
return false;
EC_CLEANUP_END
}
```

To see the great benefits of user buffering, Table 2.3 shows the times in seconds for the file copy using **BUFIO**, the standard I/O Library, and the straight-system-call method (shown in *copy2*).

**Table 2.3** Comparison of Buffered and Unbuffered I/O

| Method | User | System | Total |
| :--- | :---: | :---: | :---: |
| **BUFIO** | | | |
| Solaris | 1.00 | 0.51 | 1.51 |
| Linux | 1.00 | 0.28 | 1.28 |
| FreeBSD | 1.00 | 0.45 | 1.45 |
| **Standard I/O** | | | |
| Solaris | 0.57 | 0.24 | 0.81 |
| Linux | 11.32 | 0.15 | 11.48 |
| FreeBSD | 1.02 | 0.20 | 1.22 |
| **BUFSIZ buffer** | | | |
| Solaris | 0.00 | 0.52 | 0.52 |
| Linux | 0.00 | 0.23 | 0.23 |
| FreeBSD | 0.01 | 0.37 | 0.38 |

* All times in seconds and normalized within systems so that user BUFIO time on that system is 1.00.

With user buffering we’ve almost got the best of both worlds: We process the data as we like, even 1 byte at a time, yet we achieve a system time about the same as the **BUFSIZ** buffer method. So user buffering is definitely the right approach. Except for Linux, the standard I/O times are the best; it does what our **BUFIO** functions do, except faster and with more flexibility. The standard I/O user time for Linux (11.32) sticks out. A bit of research showed that while we used the gcc

compiler for all the tests. Linux uses the gcc version of stdio.h, FreeBSD uses one based on BSD, and Solaris uses one based on System V. Looks like the gcc version needs some attention.

The wide acceptance of the standard I/O library is ironic. The ability to do I/O in arbitrary units on regular files has always been one of the really notable features of the UNIX kernel, yet in practice, the feature is usually too inefficient to use.

## 2.13 lseek System Call

The `lseek` system call just sets the file offset for use by the next `read`, `write`, or `lseek`. No actual I/O is performed, and no commands are sent to the disk controller (remember, there's normally a buffer cache in the way anyhow).

```
lseek—set and get file offset

#include <unistd.h>

off_t lseek(
    int fd,          /* file descriptor */
    off_t pos,       /* position */
    int whence       /* interpretation */
);
/* Returns new file offset or -1 on error (sets errno) */
```

The argument `whence` can be one of:

- `SEEK_SET`  
  The file offset is set to the `pos` argument.
- `SEEK_CUR`  
  The file offset is set to its current value plus the `pos` argument, which could be positive, zero, or negative. Zero is a way to find out the current file offset.
- `SEEK_END`  
  The file offset is set to the size of the file plus the `pos` argument, which could be positive, zero, or negative. Zero is a way to set the file offset to the end of the file.

The resulting file offset may have any non-negative value at all, even greater than the size of the file. If greater, the next `write` stretches the file to the necessary length, effectively filling the interval with bytes of zero. A `read` with the file offset set at or past the end generates a zero (end-of-file) return. A `read` of the stretched interval caused by a `write` past the end succeeds, and returns bytes of zero, as you would expect.

When a `write` beyond the end of a file occurs, most UNIX systems don't actually store the intervening blocks of zeros. Thus, it is possible for a disk with, say, 3,000,000 available blocks to contain files whose combined lengths are greater than 3,000,000 blocks. This can create a serious problem if files are backed up file-by-file and then restored; as the files have to be read to transfer them to the backup device, more than 3,000,000 blocks will be written and then read back in! Users who create many files with holes in them usually hear about it from their system administrator, unless the backup program is smart enough to recognize the holes.

Of all the possible ways to use `lseek`, three are the most popular. First, `lseek` may be used to seek to an absolute position in the file:

```
ec_negl( lseek(fd, offset, SEEK_SET) )
```

Second, `lseek` may be used to seek to the end of the file:

```
ec_negl( lseek(fd, 0, SEEK_END) )
```

Third, `lseek` may be used to find out where the file offset currently is:

```
off_t where;
ec_negl( where = lseek(fd, 0, SEEK_CUR) )
```

Other ways of using `lseek` are much less common.

As I said in Section 2.8, most seeks done by the kernel are implicit rather than as a result of explicit calls to `lseek`. When `open` is called, the kernel seeks to the first byte. When `read` or `write` is called, the kernel increments the file offset by the number of bytes read or written. When a file is opened with the `O_APPEND` flag set, a seek to the end of the file precedes each write.

To illustrate the use of `lseek`, here is a function `backward` that prints a file backward, a line at a time. For example, if the file contains:

```
dog
bytes
man
```
