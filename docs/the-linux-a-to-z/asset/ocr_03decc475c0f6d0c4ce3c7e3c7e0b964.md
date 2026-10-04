The functions in the library are sopen(), sclose(), sserver() and sclient(). In essence, a server process will call the sopen() function, which creates a socket and stores the socket descriptor, along with some administrative information, in a structure. The function then returns a pointer to this structure as its return value. You then pass the socket structure pointer, along with the port number that the server will use to offer connections to clients, as parameters to the sserver() call. When a client connects with the server the sserver() call returns with a socket descriptor which can then be used to communicate with the client using, for example, read() and write(). Connections with other clients can be made by further calls to sserver(), using the same socket structure pointer and port number as before. Socket descriptors returned by sserver() should be released with close() when the client communication is over, and the socket pointer returned by sopen() should be released with sclose() when the server shuts down.

At the client end, a call to sopen() will create a socket and return a socket pointer as before. This pointer can then be passed, along with the server's address and port number, into sclient(). When the connection is established, sclient() returns a socket descriptor to communicate with the server. As in the server case, close() and sclose() should be used when the client finishes its task.

# 18.1.1 The sopen() Function

```
/* 1 */
SOCKET *sopen(void)
{
  /* 2 */
  SOCKET *sp;

  /* 3 */
  if ((sp = (SOCKET *)malloc(sizeof(SOCKET)))==0)
    return 0;

  /* 4 */
  if ((sp->sd = socket(AF_INET, SOCK_STREAM, 0))==-1)
  {
    free(sp);
    return 0;
  }

  /* 5 */
  sp->sinlen = sizeof(sp->sin);
  sp->bindflag = S_RESET;
  /* 6 */
  return sp;
}
```