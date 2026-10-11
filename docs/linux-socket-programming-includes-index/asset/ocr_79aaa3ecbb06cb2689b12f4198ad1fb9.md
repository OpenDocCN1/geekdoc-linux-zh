# **LISTING 18.3 MyPing Sender Loop**

```
```c
/**** MyPing Sender - Get & toss any pending messages, ***
/*** compose message, send message, and pause. ***
/*** From MyPing.c on Web site. ***

for (;;) {
    int len=sizeof(r_addr);

    /****-Get any message that the kernel may have sent-****/
    if ( recvfrom(sd, &pckt, sizeof(pckt), 0, &r_addr, &len) > 0 )
        printf("***Got message***\n");

    /****-Initialize outgoing packet-****/
    bzero(&pckt, sizeof(pckt));                /* Zero contents */
    pckt.hdr.type = ICMP_ECHO;                 /* Request echo */
    pckt.hdr.un.echo.id = pid;                 /* Set ID */
    for ( i = 0; i < sizeof(pckt.msg) -1; i++ )  /* Fill buffer */
        pckt.msg[i] = i+'0';
    pckt.msg[i] = 0;                            /* Make C-string compatible */
    pckt.hdr.un.echo.sequence = cnt++;          /* Set counter */
    pckt.hdr.checksum =
      checksum(&pckt, sizeof(pckt));           /* Compute checksum */
    if ( sendto(sd, &pckt, sizeof(pckt), 0, addr,  /* SEND! */
              sizeof(*addr)) <= 0 )
        perror("sendto");

    sleep(1);                                   /* Wait for 1 second */
}
```
```

Resetting the message to the same values is not completely necessary but is precautionary. When the destination replies, the sender will get a copy of the message. If you don’t get the message (and any other ICMP messages), the kernel ends up setting aside more and more memory for unwanted messages.

For the algorithm to work correctly, the program has to change some of the socket’s default settings. First, most ping programs set the TTL (time to live) to the highest hop value (255). Also, the sender’s socket must have nonblocking enabled to call recvfrom() without stalling.

The MyPing program is a good starting point for most ICMP-style packet messaging. After you are comfortable with this algorithm, other raw socket programs are similar to datagram programming.