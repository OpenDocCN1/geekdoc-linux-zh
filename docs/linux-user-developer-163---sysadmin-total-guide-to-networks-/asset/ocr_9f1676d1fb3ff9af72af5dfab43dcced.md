web and mark, work using TCP/IP in order to accept
network connections from the world. We don't worry much
about this for now; more TCP/IP network programming
will be covered in forthcoming tutorials.

The developed server will perform another simple
task: count the total number of successful connections
using a counter. The program writes a message to a log file
e time it receives a signal, which shows the
VALUE COUNTER. The USRT signal will notify the
server.

The full source code of advanced.c, which is based on
logging.c, you can use advanced.c as a
template when you are developing your own server.

```
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <signal.h>
#include <fcntl.h>
#include <string.h>
#include <sys/time.h>
#include <sys/resource.h>
#include <socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
```

```
int counter = 0;

#define DEFINE_LOCK "/tmp/advanced.pid"
#define LOGMODE S_IRUSR_IWUSR_IRGRP_IROTH

#define MAXSIZE 1000
int createUDP(int port)

int sockfd;
struct sockaddr_in in_server;

sockfd = socket(AF_INET, SOCK_DGRAM, 0);
```

```
memset(&server_address, 0, sizeof(server_address));
server_address.sin_family = AF_INET;
server_address.sin_addr.s_addr = htonl(INADDR_ANY);
server_address.sin_port = htons(port);
```

```
bind(sockfd, (struct sockaddr*)&server_address,
     sizeof(server_address));
return sockfd;
```

```
static void signal_handler(int sig) {
    if (sig == SIGHUP) {
        syslog(LOG_INFO, "Total number of
%d:", counter);
        printf("unknown signal!\n");
    }
    return;
```

```
static void signal_handler2(int sig) {
    if (sig == SIGUSR1)
        // Delete lockfile
        // NEEDS TO BE IMPLEMENTED

        syslog(LOG_INFO, "Exiting...");
        exit(0);
    } else
        printf("unknown signal!\n");
        return;
```

# Logging with Go

The Go library, is implemented using
packages that allow you to create servers
sprprisingly easy. The way your
server shows how you can
log information using Go
using the syslog package
provides a simple interface to
tyslog system.

Take a look at the Go server,
which produces output in
the following format:

```
Jan 21 18:51:55 server1
Jan 21 18:51:56 server2 Logging in Go:
```

Unfortunately, you do need
to execute the server without
network workaround
common in
little outlet.

![](bbox=[0.095, 0.675, 0.75, 0.69])

Left: The\command enables
to run your processes
in the background
when paired with

* With