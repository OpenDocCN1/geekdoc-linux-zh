# ## Sending Before Received: Message Interleave

One aspect of server responsiveness is its quick recovery. Another aspect is how quickly the client can get the request out to the server. You can also use `TCP_NODELAY` to assist your server’s performance by getting out the client’s query as quickly as possible.

As previously mentioned, TCP uses the Nagle Algorithm to limit the number of small messages on a WAN. It forbids sending any message that is smaller than the MSS until the receiver acknowledges (ACK) all outstanding messages. Of course, if the sender buffer has more than MSS bytes of data, it sends it as quickly as possible. What this means to you is that if you have several short requests, you may wait longer for their replies. This is because they are not sent as soon as you write() them, but they are serialized into send-ACK-send interactions.

The only loss possible when using this approach is loss of network throughput, but you can control that. Remember that if the number of bytes in the header begins to outweigh the data itself, the throughput suffers. If you can limit the messages so that they are not too small (try building them manually first into a buffer), then you can send them in a burst. The result is getting the throughput of instant transmission while minimizing the throughput drain.

# ## Noting File I/O Problems

As you look at the options for building the messages, you may be tempted to use the standard file I/O system calls or the higher-level `FILE*` library calls. Up to this point, this text tells you that this interchangeability is great.

Using the standard calls is very useful for quick prototypes and fast development. They are familiar and have several features that can make your programming very easy. In fact, as you do rapid prototyping, use those calls that most closely match the ones in the Sockets API. Try to limit those, like `printf()`, which may be harder to convert.

The problem with using the file I/O calls stems from the way the libraries and system manage them. When you make one of the file I/O calls with a socket descriptor or you use `fopen()`, the system may copy your data a few times from the file buffers to the socket buffers. This dings your client’s or server’s stellar performance. Even the low-level file I/O, `read()` and `write()`, looks at your descriptor, determines that it needs socket I/O, and makes the appropriate call.

Eventually, you might want to use the Sockets API exclusively. This can also help readability and maintainability of your code; it makes it very easy to see that your program is working on a file versus a socket.