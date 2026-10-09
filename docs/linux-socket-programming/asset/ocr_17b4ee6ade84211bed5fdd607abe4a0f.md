+   * ``fork()`` The return value indicates whether you're in the child or in the parent. And, you might want to separate the child from the parent's execution path. Also, you can check for any errors. If the return value is negative, you have not created the child, and you may have more systemic problems.
* ``pthread_create()`` Like the ``fork()`` call, you might want to verify that the call succeeded in creating the new child.
* ``setsockopt() / getsockopt()`` The sockets have many options you can work with to tune the behavior. Generally, you may want to know if the call was successful so that you can proceed on that assumption.

All these calls share one common fate if they fail—your program may terminate or behave unpredictably. This is a good rule of thumb: If the call seriously impairs the reliability of your program, always check the return value. If any problem is evident, report it to the console. This alerts the user early of any problems.

The following are less important calls, a few that you could get away with ignoring the return value:

+   * ``socket()`` The only time you fail this call is if you request a socket you can't have (permission or lack of kernel support), if you have a bad parameter, or you have a full descriptor table. In call cases, the ``bind(), connect(),`` or I/O call acts as backup to catch the fault with a "not a socket" error.
* ``listen()`` You are unlikely to get an error from this call if ``bind()`` previously succeeded. It does have a limit to the depth of the listening queue. If you use 15–20 entries, your program can work well even with a large connection rate.
* ``close()`` or ``shutdown()`` If the file descriptor is bad, the file is gone anyway. In either case (success or failure), the file is gone, and your program can move on. (You may want to check the location in your program that calls this if you suddenly start running out of file descriptors.)

API calls that are not as critical often have other important calls that can pick up the slack following right behind them. Also, if they fail, they may not cause any catastrophic failures. This is not a license to ignore the return values of these calls; in all circumstances, checking verifies success and thus increases your program's reliability.

You can use other measures to capture errors that occur while you may not be in a system or library call. These errors happen because of the dynamics of the network and the possibility that the server or client could go silent. The networking subsystem keeps track of some of these errors in the TCP protocols, because TCP constantly ensures that the channel is clear for bi-directional communications.

If your program does not send a message for a while, you need to check on the connection manually. If you do not, the error eventually appears as an I/O fault. To access this information, you can use the ``getsockopt()`` system call with ``SO_ERROR`` option:

```
```
int error;
socklen_t size=sizeof(error);
if ( getsockopt(sockfd, SOL_SOCKET, SO_ERROR, &error, &size) == 0 )
    if ( error != 0 )
        fprintf(stderr, "socket error: %s(%d)\n", strerror(error), error);
```
```