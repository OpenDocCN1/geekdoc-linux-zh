```
```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <limits.h>
#include <time.h>

int main(void)
{
    int fd;                       /* Descriptor for FIFO */
    int len;                     /* Bytes written to FIFO */
    char buf[PIPE_BUF];          /* Ensure atomic writes */
    mode_t mode = 0666;
    time_t tp;                   /* For time call */

    /* Identify myself */
    printf("I am %d\n", getpid());

    Open the FIFO write-only */
    if((fd = open("fifo1", O_WRONLY)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }
    /* Generate some data to write */
    while(1) {
        /* Get the current time */
        time(&tp);
        /* Create the string to write */
        len = sprintf(buf, "wrfifo %d sends %s",
                      getpid(), ctime(&tp));

        /*
        * Use (len + 1) because sprintf does not count
        * the terminating null
        * /
        if((write(fd, buf, len + 1)) < 0) {
            perror("write");
            close(fd);
            exit(EXIT_FAILURE);
        }
    }
}
```
```