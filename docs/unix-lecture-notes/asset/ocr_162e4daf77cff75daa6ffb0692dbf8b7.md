there are no processes writing to the FIFO, so if no clients attempt to write to the server, or if all clients that were writing close their ends of the FIFO and exit, the server would receive a 0 from the read(). If we designed the loop so that it was re-entered when read() returned 0, this would not be a problem. However, it is a cleaner design to let the server open the FIFO for writing, so that there is always at least one process holding the FIFO open for writing, and so that the return value of read() will be either positive or negative, unless there is some unanticipated error condition.

Therefore, the server begins by creating the FIFO and opening it for both reading and writing, even though it will only read from it. Since the server never writes to this pipe, it does not matter whether or not writes are non-blocking, but POSIX does not specify how a system is supposed to handle opening a file in blocking mode for both reading and writing, so it is safer to open it with the O_NONBLOCK flag set, since POSIX does not specify how a system is supposed to handle opening a file in blocking mode for both reading and writing, we avoid possibly undefined behavior.

The server is run as a background process and is the process that must be started first, so that it can create the FIFO. If the server is not running and a client is started up, it will exit, because the FIFO does not exist.

The common header file is listed first, in Listing 8.9, followed by the server code.

# Listing 8.9: fifo1.h

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>
#include <limits.h>
#include <errno.h>
#include <sys/stat.h>

#define PUBLIC "/tmp/FIFODEMO1_PIPE"
```

# Listing 8.10: rcvfifo1.c

```
#include <signal.h>
#include "fifo1.h"

int     dummyfifo;      /* file descriptor to write-end of PUBLIC */
int     publicfifo;     /* file descriptor to read-end of PUBLIC */

/** on_signal()
 *  This closes both ends of the FIFO and then removes it, after
 *  which it exits the program.
 */
void on_signal( int sig )
{
    close(publicfifo);
    close(dummyfifo);
    unlink(PUBLIC);
    exit(0);
}
```