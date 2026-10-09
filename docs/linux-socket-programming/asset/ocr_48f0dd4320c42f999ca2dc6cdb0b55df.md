system call returns to your server with the channels that are ready, and your server retrieves and processes the command.

The temptation to skip multitasking altogether and use these multiplexers may lead to some loss in performance. When using a single task to process information, your program or server has to wait for I/O at various times during the life of the process. If you don't take advantage of this downtime, your servers may lose significant opportunities to do other things. For example, if you have ever compiled the kernel, you may find that it compiles in less time if you force multiple jobs with the -j make option. (If you have the memory, two or three jobs per processor cuts the compilation time noticeably.)

# ## Compromising with a Smart Select

As you create your high-powered, high-demand server, you can use various ways to distribute the load. Two are multitasking and I/O multiplexing. However, if used exclusively, multitasking may lose control of the scheduler and erode precious time to context switching, while I/O multiplexing loses unused CPU bandwidth. An alternative to using either exclusively is a combination of both. Combining the two into a *Smart Select* could help you diminish the disadvantages of each, while giving you their capabilities.

A Smart Select dispatches a few processes. Each process owns a connection channel and a set of open client channels. An I/O multiplexer manages all of the channels. Here is an algorithm for the process:

```
```c
/*****...*******************************...*****/
/*** Smart Select example: each child tries to accept a ***/
/*** connection. If successful, it adds the connection ***/
/*** to the select() list.                ***/
/*** ("smart-select.c" on Web site)              ***/
/*****...*******************************...*****/
int sd, maxfd=0;
fd_set set;
FD_ZERO(&set);
/*** Create socket and fork() processes ***/
/**---In Child---*/
maxfd = sd;
FD_SET(sd, &set);
for (;;) {
        struct timeval timeout={ 2,0 };         /* 2 seconds */
        /**--Wait for some action--*/
if ( select(maxfd+1, &set, 0, 0, &timeout) > 0 )
{
        /**--If new connection, connect and add to list--*/
 if ( FD_ISSET(sd, &set) )
  {  int client = accept(sd, 0, 0);
     if ( maxfd < client )
        maxfd = client;
     FD_SET(client, &set);
  }
        /**--If command/request from client, process--*/
else
        /*** Process client's request ***/
        /*** If client just closed, remove from list ***/
}
}
```
```