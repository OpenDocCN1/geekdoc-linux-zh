```
}

/* Write the buffer contents to the terminal */
write(1, &buf, i);
return 0;
}
```

The last demo program shows how the TIOCINQ IOCTL can be used to query the size of the input queue. It opens the terminal device file specified on the command line, and then enters a loop of fixed duration in which it uses the ioctl() function to query the size of that terminal's input queue. It writes the size of the queue into a file named queue_log in the current working directory.

# Listing ioctl3.c

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <termios.h>
#include <fcntl.h>
#include <sys/ioctl.h>
#include "utils.h"

int main(int argc, char* argv[])
{
    FILE    *fp;
    int     count, i;
    int     fd;

    /* Try to open given terminal device file */
    if ((fd = open(argv[1], O_RDONLY)) == -1)
        die("open", argv[1]);

    /* Open queue log in current working directory */
    if ((fp = fopen("queue_log", "w")) == NULL) {
        printf("Could not open queue_log\n");
        exit(1);
    }

    /* For a fixed amount of time (for simplicity) count queue size */
    for ( i = 0; i < 400; i++ ) {
        if ( ioctl( fd, TIOCINQ, &count ) == -1 )
            die( "ioctl", "TIOCINQ");
        fprintf(fp, "%d chars in queue\n", count);
        /* delay to see changes */
        usleep(100000);
    }

    fclose(fp);
    return 0;
}
```