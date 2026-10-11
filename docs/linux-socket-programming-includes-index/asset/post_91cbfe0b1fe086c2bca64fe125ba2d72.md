
- **TCP_NODELAY** TCP uses the Nagle Algorithm, which forbids sending any message that is smaller than the MSS until the receiver acknowledges (ACK) all outstanding messages. If you enable this option, you turn off the Nagle Algorithm, making it possible to send several short messages before getting the ACKs. (Boolean, disabled by default.)
- **TCP_STDURG** This option specifies where in the stream to find the 00B data byte. By default it is the byte following the 00B flag. Since all implementations recognize this default, you may never need to use this option. Linux replaced this option with the `sctl1()` system call. (Integer, 1 by default.)

## Recovering the Socket Descriptor

You may write many servers as you learn how to do network programming. You may run into a problem where the `bind()` fails because of an address in use error. This is the most common error programmers get (even experienced ones) and one of the most common questions asked on the Usenet. The problem comes from the way the kernel allocates the ports.

Most kernels wait for a few seconds before reallocating a port (some specifications claim up to a minute). This policy is important for security. The delay makes sure that floating packets are dead before permitting a new connection.

You can get around this problem if you use the `SO_REUSEADDR` option. In fact, some say that you should enable this option on all your servers. As stated in the previous section, this option lets you reconnect quickly even though the kernel may still have it allocated. To enable the option, you can use the following excerpt:

```c
/***** REUSING A PORT EXAMPLE (FOR SERVERS THAT DIE AND     ****/
/**** NEED TO RESTART) .                                             *****/
/***** REUSING A PORT EXAMPLE (FOR SERVERS THAT DIE AND     ****/
int value = 1; /* TRUE */
int sd = socket(PF_INET, SOCK_STREAM, 0);
if (setsockopt(sd, SOL_SOCKET, SO_REUSEADDR, &value, sizeof(value)) != 0)
    perror("setsockopt() failed");
/***** bind(), listen(), and accept()      ****/
```

Another procedure you could follow is to retry the `bind()` system call if it returns the `EAGAIN` error. One caveat for using this option is that no other programs could be using your port. The `SO_REUSEADDR` option lets your programs share ports. That may cause problems. You don't want two HTTP servers running at the same time, both using port 80. Also, trying to start a server that's already started is a common sysadmin goof.

Some programmers leave this feature disabled and retry a few times to detect if the program is already running. If you want to use this option (which actually is a good idea), be sure to use a different locking mechanism, like the PID in `/var`.

## Sending Before Received: Message Interleave

One aspect of server responsiveness is its quick recovery. Another aspect is how quickly the client can get the request out to the server. You can also use `TCP_NODELAY` to assist your server’s performance by getting out the client’s query as quickly as possible.

As previously mentioned, TCP uses the Nagle Algorithm to limit the number of small messages on a WAN. It forbids sending any message that is smaller than the MSS until the receiver acknowledges (ACK) all outstanding messages. Of course, if the sender buffer has more than MSS bytes of data, it sends it as quickly as possible. What this means to you is that if you have several short requests, you may wait longer for their replies. This is because they are not sent as soon as you `write()` them, but they are serialized into send-ACK-send interactions.

The only loss possible when using this approach is loss of network throughput, but you can control that. Remember that if the number of bytes in the header begins to outweigh the data itself, the throughput suffers. If you can limit the messages so that they are not too small (try building them manually first into a buffer), then you can send them in a burst. The result is getting the throughput of instant transmission while minimizing the throughput drain.

## Noting File I/O Problems

As you look at the options for building the messages, you may be tempted to use the standard file I/O system calls or the higher-level `FILE*` library calls. Up to this point, this text tells you that this interchangeability is great.

Using the standard calls is very useful for quick prototypes and fast development. They are familiar and have several features that can make your programming very easy. In fact, as you do rapid prototyping, use those calls that most closely match the ones in the Sockets API. Try to limit those, like `printf()`, which may be harder to convert.

The problem with using the file I/O calls stems from the way the libraries and system manage them. When you make one of the file I/O calls with a socket descriptor or you use `fopen()`, the system may copy your data a few times from the file buffers to the socket buffers. This dings your client’s or server’s stellar performance. Even the low-level file I/O, `read()` and `write()`, looks at your descriptor, determines that it needs socket I/O, and makes the appropriate call.

Eventually, you might want to use the Sockets API exclusively. This can also help readability and maintainability of your code; it makes it very easy to see that your program is working on a file versus a socket.

## Using Demand-Based I/O to Recover CPU Time

Your servers, clients, and peers all share two common features: your algorithms and the I/O subsystem. You can control your programs by good design and profiling. The I/O subsystem is not as flexible. (One of the most appealing aspects of Linux is that you can get into it and change it.) The I/O system calls in the Sockets API offer you a lot of control over how you send and receive your data. Mixed with the control from `fcntl()`, this provides some very powerful tools.

In most cases, the kernel simply buffers the messages you send. This means you can focus on getting information and processing it. Chapter 8, “Choosing when to Wait for I/O,” explains how to use asynchronous I/O (or demand-based I/O) for letting the kernel do some of the work for you.

Asynchronous I/O (not the real-time definition) works with your program by placing the burden of notification on the I/O subsystem. During the life of your program, you may do several reads and writes.

## Speeding Up a send()

When you send a message, the kernel copies the message into its buffers and starts the process of constructing the packets. Upon completion, the kernel returns to your program with a status. The only reason for the delay is to generate the results of the `send()`. If you have any problems with your message, the kernel can reply with an error message.

However, most errors after you have connected come from transmission, not from the `send()` command. Unless you have something such as an illegal memory reference (which the call detects quickly), you may not get an error until after the `send()` finishes. You can get these errors from the `SO_ERROR` socket option before the library’s `errno` gets it.

You can speed up the `send()` operation with the `MSG_DONTWAIT` system call option. With this option, the call copies your data and immediately returns. From that point you can proceed with other operations. However, it is your responsibility to check the error codes carefully.

The only time that a write operation blocks is when the transmit buffers are full. This does not happen very often when you have a lot of unused memory. If it does, you can use asynchronous I/O with signals to let you know when the buffers are available.

## Offloading the recv()

Unlike the `send()` system call, most `recv()` system calls I/O block, because your program usually runs faster than the arriving data. If the receive buffers have data, the read operation copies the information and returns. Even if one byte is ready in the buffers, the read operation returns
