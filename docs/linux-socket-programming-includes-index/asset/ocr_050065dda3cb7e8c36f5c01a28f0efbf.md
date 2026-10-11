# Example

```
int i, sd, len, bytes;
char buffer[MSGS][100];
struct iovec io[MSGS];
struct msghdr msg;
struct sockaddr_in addr;

sd = socket(PF_INET, SOCK_DGRAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(8080);
inet_aton(&addr.sin_addr, "127.0.0.1");
bzero(&msg, sizeof(msf));
msg.msg_name = &addr;
msg.msg_namelen = sizeof(addr);
for ( i = 0; i < MSGS; i++ )
{
	io[i].iov_base = buffer[i];
	sprintf(buffer[i], "Buffer #%d: this is a test\n", i);
	io[i].iov_len = strlen(buffer[i]);
}
msg.msg_iov = io;
msg.msg_iovlen = MSGS;
if ( (bytes = sendmsg(sd, &msg, 0)) < 0 )
    perror("sendmsg");
```

# sendfile()

A fast way to transmit a file through a socket. The call reads the data from `in_fd` and writes it out to `out_fd`. The call does not change the file pointer in `in_fd`, but `out_fd`'s file pointer is changed. The call begins reading from `*offset` for count bytes. When done, `*offset` points to the byte after the last byte read. If you need to add header information, refer to the TCP_CORK option in TCP(4) to improve performance.

# Prototype

```
#include <unistd>
int sendfile(int out_fd, int in_fd, off_t *offset,
             size_t count);
```

# Return Value

If successful, the call returns the total number of bytes copied. If error, the call returns −1 and sets errno to the error code.