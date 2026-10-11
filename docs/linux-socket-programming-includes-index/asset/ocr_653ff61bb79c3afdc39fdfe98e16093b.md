Because the user may want to test the round-trip time, the program often has two processes running—one for sending and the other for receiving. The sender process typically waits one second between each transmission, and the receiver keeps track of the messages and their times.

# ### The MyPing Receiver

The receiver is simple. After creating the raw socket, it repeatedly calls `recvfrom()`, as shown in Listing 18.2.

# #### LISTING 18.2\* MyPing Receiver Loop

```
```c
/*\n *\n * MyPing Receiver – Get pending message and display it.\n * From MyPing.c on Web site.\n *\n */
for (;;) {
    int bytes, len=sizeof(addr);

    bzero(buf, sizeof(buf));          /* Clear buffer & Get msg */
    bytes = recvfrom(sd, buf, sizeof(buf), 0, &addr, &len);
    if ( bytes > 0 )                  /* If no error, */
        display(buf, bytes);         /* check ID & display */
    else
        perror("recvfrom");
}
```
```

The `display()` call converts the buf to a packet_struct and checks for the ID. If the ID matches, the packet really does belong to the process.

The ID is needed because of how the kernel delivers messages to raw sockets. As noted earlier, the kernel has no way to determine the correct destination of a raw packet without ports, so it delivers all raw packets to all raw sockets of a particular protocol.

The protocol is a key for the kernel. If your program registers a raw socket with an ICMP protocol, the program gets all ICMP messages (even those meant for other processes). How do you tell the difference? ICMP includes an ID field into which most programs place their PID (process ID). The responding host echoes back everything that it receives, including the ID. If the ID does not match the PID, the receiver drops it.

# ### The MyPing Sender

The sender has a little more work to do. Along with preparing and shipping the message, it has to accept any spurious messages the kernel chooses to place in its queue (see Listing 18.3).