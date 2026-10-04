```
/* 3 */
return close(sd);
}
```

+   1. The function sclose() closes the socket associated with a given SOCKET pointer. The pointer is passed to the function as a parameter. A value of 0 is returned if the call is successful, otherwise, a -1 is returned on error.
2. The socket descriptor in the sd field of the socket pointer structure is saved in a local variable so that the memory block pointed to by sp can safely be released with free().
3. The saved socket descriptor can now be closed with the close() system call. This system call returns 0 if successful or -1 on error, which is exactly what sclose() should return, so this can all be done in one line.

# 18.1.3 The sserver() Function

```
/* 1 */
sserver(SOCKET *sp, int port, int sync)
SOCKET *sp;
int port, sync;
{
    int flags;
    struct hostent *hostent;
    char localhost[S_NAMLEN+1];

    /* 2 */
    if (sp->bindflag==S_RESET)
    {
        /* 3 */
        if (gethostname(localhost, S_NAMLEN)==-1
        || (hostent = gethostbyname(localhost))==0)
            return -1;

        /* 4 */
        sp->sin.sin_family = (short)hostent->h_addrtype;
        sp->sin.sin_port = htons((unsigned short)port);
        sp->sin.sin_addr.s_addr = *(unsigned long *)hostent->h_addr;

        /* 5 */
        if (bind(sp->sd, (struct sockaddr *)&sp->sin, sp->sinlen)==-1
        || listen(sp->sd, 5)==-1)
            return -1;

        /* 6 */
```