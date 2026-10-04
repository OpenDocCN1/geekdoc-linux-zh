```
#include <fcntl.h>
#include <sys/stat.h>

#define NEWFILE (O_WRONLY | O_CREAT | O_TRUNC)
#define MODE600 (S_IRUSR | S_IWUSR)
#define SIZE 1

void filecopy(char *infile, char *outfile)
{
    char buf[SIZE];
    int infd, outfd, count;

    if ((infd = open(infile, O_RDONLY))==-1)
        fatal("opening infile");

    if ((outfd = open(outfile, NEWFILE, MODE600))==-1)
        fatal("opening outfile");

    while ((count = read(infd, buf, sizeof(buf)))>0)
        if (write(outfd, buf, count)!=count)
            fatal("writing data");

    if (count==-1)
        fatal("reading data");

    close(infd);
    close(outfd);
}
```

The user function fatal() is not listed here but all it needs to do is to output an error message containing its parameter string and then terminate execution of the process.

You already know that the system uses large amounts of memory as a buffer cache for disk file reads and writes and that getting bytes to and from memory is a very fast operation. However, in the case of the filecopy() function, while it works, in that it performs the required copy, it isn't very efficient. There is quite a time overhead for running a system call and this function makes two system calls (one read() and one write()) for every byte copied.

Using the filecopy() function exactly as listed, I ran a few simple timing tests (using the time command) and discovered that on my system I could copy files at about 6.4 kilo-bytes per second. Now it is quite a simple matter to reduce the number of system calls involved in the copy operation – you just increase the value of the SIZE constant. The effect of this is to copy the file in a smaller number of larger-sized chunks. A natural SIZE