can program the servlet to compare the connection with the message it receives. It's not difficult, but you have to plan your program a little more.

The last limitation of this algorithm is its support of long-term (deep transaction) connections. This algorithm remains stable, if you have a client and server doing single transactions or short interactions. However, deep transaction connections usually require multiple states. This complicates your server tremendously. Also, because the connection is active longer, the possibility of getting your load out of balance increases.

# # Redistributing the Load

You can solve the load distribution limitation if you switch to threads instead of using processes. As described above, the server cannot easily distribute the number of connections per task. (You can do this with IPC, but it's more trouble than it's worth.) Threading lets you share everything between tasks, including the file descriptor table.

In a similar vein, your server may have several threads running, making it difficult to assign connections. You have a descriptor array and can use the poll() system call. (You can use the select() call, but the algorithm is not as straightforward.) Each thread owns one portion of the array. This works only if the parent accepts all connections. When your server sees a connection request, the parent accepts it and places it in the array of descriptors.

Depending on the implementation of poll(), your threads may have to time out frequently so that they can pick up any changes to the descriptor array. A few implementations simply cycle through testing each descriptor; others (more likely used in Linux) actually register the descriptors into a system call. The system call waits and reports on descriptor activity. Therefore, if the parent adds a new descriptor, the thread must call poll() again to begin processing it.

```
/*****************************************/
/*** Fair load distribution example: parent accepts ***/
/*** and assigns connections to various threads. ***/
/*** ("fair-load.c" on Web site)   ***/
/*****************************************/
int fd_count=0;
struct pollfd fds[MAXFDs]; /* cleared with bzero() */
/*---parent---*/
int sd = socket(PF_INET, SOCK_STREAM, 0);
/***Bind() and listen() socket***/
for (;;) {
    int i;
    /*--- Find an available slot before accepting conn. ---*/
    for ( i = 0; i < fd_count; i++ )
        if ( fds[i].events == 0 )
            break;
    if ( i == fd_count  &&  fd_count < MAXFDs )
        fd_count++;
    /*---If you have an available slot, accept connection---*/
    if ( i < fd_count )
    {
        fds[i].fd = accept(sd, 0, 0);
        fds[i].events = POLLIN | POLLHUP;
    }
    else                    /* otherwise, yield for a little while */
                        /* or, some yielding delay */
        sleep(1);
}
/*---child---*/
```