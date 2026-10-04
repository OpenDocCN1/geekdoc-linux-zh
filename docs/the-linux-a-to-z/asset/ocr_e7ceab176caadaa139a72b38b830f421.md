# Tiny Daemon – Case Study

Having looked at the principles involved in setting up a daemon process we will now go back to the example socket server program we looked at in Section 18.2 and see how to make it into a proper daemon process which will continue to run and provide its service even after you log off the machine.

# 23.1 The Daemon Listing

The following program shows the complete listing of the example socket server from Section 18.2, modified to operate as a robust daemon process. You will notice that some changes have been made to the original server code itself, as well as the addition of the setup_daemon() function. All of these will be explained in detail after the listing:

```
```
/****************************************************************
THE SOCKET SERVER DAEMON
****************************************************************/

#include <stdio.h>
#include <string.h>
#include <signal.h>
#include <fcntl.h>
#include <setjmp.h>
#include <sys/param.h>
#include "socklib.h"

/* Server's communication port number */
#define PORT 2121

/* Values for the next_action parameter to fatal() */
#define NA_EXIT 0
```
```