to choose would be something related to the size of a disk data block.

Repeating the experiments after changing the value of SIZE to 1024 (but making no other changes) increased the file copy rate to a staggering (well I was impressed anyway) 1.3 mega-bytes per second – a speed improvement of over 200 times!

Even taking the speed increase into account, it is sometimes just not convenient to read the data in such large blocks. In this case you can achieve the best of both worlds by doing the data buffering yourself, in user memory space, and taking your small chunks of data from there.

The following code example shows a small amendment to the filecopy() function so that it calls the functions my_read() and my_write() which perform exactly the same as the read() and write() system calls except that they use internal 1024 byte buffers to cut down on the number of times the system calls get used. Using write_close() to close the output file rather than the close() system call is necessary in order to flush any partial write_buf[] contents before closing the file:

```
#include <fcntl.h>
#include <sys/stat.h>

#define NEWFILE (O_WRONLY | O_CREAT | O_TRUNC)
#define MODE600 (S_IRUSR | S_IWUSR)
#define SIZE 1
#define BUF_SIZE 1024

void filecopy(char *infile, char *outfile)
{
    char buf[SIZE];
    int infd, outfd, count;

    if ((infd = open(infile, O_RDONLY))==-1)
        fatal("opening infile");

    if ((outfd = open(outfile, NEWFILE, MODE600))==-1)
        fatal("opening outfile");

    while ((count = my_read(infd, buf, sizeof(buf)))>0)
        if (my_write(outfd, buf, count)!=count)
            fatal("writing data");

    if (count==-1)
        fatal("reading data");

    close(infd);
    write_close(outfd);
}
```