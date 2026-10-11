```
```
int sd;
 sd = socket(PF_INET, SOCK_STREAM, 0);
if ( setsockopt(sd, IPPROTO_TCP, TCP_NOPUSH, &flag,
sizeof(flag)) != 0 )
   PANIC("TCP_NOPUSH not supported");
/****set up addr to destination****/
if ( sendto(sd, buffer, bytes, MSG_FIN, &addr, sizeof(addr))
    < 0 )
   PANIC("sendto");
...
```
```

![](bbox=[0.35, 0.3, 0.74, 0.73])

# **FIGURE 4.1**

*The TCP handshake opens, sends, and closes a dialog in three packets.*

With TCP you have to disable TCP from flushing its buffers too quickly. That is what the *setsockopt()* system call is doing in the example. Also, you can send as many messages as you want, but the last message must have *MSG_FIN* (see above) in the *sendto()* system call.