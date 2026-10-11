
Chapter 3 described the process as a three-way handshake. This handshake establishes the communication level for streaming your data between programs. Since UDP does not support streams, the connect() system call only simplifies the message passing.

The connect() system call on a UDP connection merely records the destination of any messages you send. You can use read() and write() like a TCP connection, but you do not have the reliability and ordering guarantees. The algorithm presented in Listing 4.1 is very similar to that of TCP programming.

## LISTING 4.1 A Simple Connected Datagram

```c
/**** Sample datagram example with connection ****/
/**** Excerpt from connected_peer.c ****/

int sd;
struct sockaddr_in addr;
sd = socket( PF_INET, SOCK_DGRAM, 0);  /* datagram socket */
bzero( &addr, sizeof( addr ) );
addr. sin_family = AF_INET;
addr. sin_port = htons( DEST_PORT );
inet_aton( DEST_IPADDR, &addr. sin_addr );
if ( connect( sd, &addr, sizeof( addr) ) == 0 )  /* connect! */
    perror("connect");

/**** Note: this is not a streamed send--- */
send( sd, buffer, msg_len);  /* send like TCP */
```

Normally, when using UDP, you use the sendto() or recvfrom() system call (described later in this chapter). The send() system call assumes that the program has already registered the destination with a connect().

The peer (or server) that waits for the connection may use the same connection interface, or it could use sendto() and recvfrom(). However, for the program to connect to the peer, it is necessary for the peer to publish its port number with the bind() system call. For a complete description of the bind() system call, please refer to the "Sending a Direct Message" section, later in this chapter.

The example code fragment in Listing 4.1 refers to DEST_PORT. This number is an agreed-upon port interface between the two programs. The listening peer sets up the port by calling bind() to request DEST_PORT. When your message arrives, the destination may issue a connect() system call itself.

Unlike TCP's connect() system call, your program can reconnect as many times as you wish to other peers or servers without closing the socket. With TCP, you cannot connect to other peers or servers unless you close and then reopen the socket. One of the most important features UDP offers is the capability to send messages to different destinations without closing the socket. Using the connect() system call with UDP protocol still affords you this flexibility. Again, if you use UDP in any form, you elect the unreliability that goes with it. You could lose packets, or the packets may arrive out of order. The connect() system call for UDP only records the destination and does not increase the reliability of the channel between your programs.

## Reliably Delivered Messages (RDM)

The Reliably Delivered Messages (RDM) protocol [RFC908,RFC1151] provides the guaranteed delivery that TCP offers but also lets you have the message-based (non-streamed) speed of UDP. RDM may still get the messages out of order, but it provides a good compromise between UDP and TCP. Unfortunately, even though this protocol has been on the books for a number of years, Linux (and other UNIX operating systems) does not yet support it.

## Example: Connecting to the HTTP Daemon

The most common protocol users connect with is HTTP. It describes a very simple interface that includes a query. The server, in turn, interprets the query and replies with a message that the client can understand. That message may be any document inside a simple email header format.

The simplicity of the interface demonstrates for you many of the transactions on the network. Most client-server interactions are single-transaction based. All of the overhead of TCP interfacing and reliability checking can be wasteful on a single transaction. Still, that is the accepted standard.

## Simplified HTTP Protocol

To send a request to an HTTP server, you only need to know a single command. This is an oversimplified representation of the HTTP protocol. Chapter 6, “A Server Primer;” covers the protocol in greater depth:

```
GET <query> HTTP/1.0<cr><cr>
```

The query typically looks like a directory path, but it can take parameters and variables. When you enter the URL, http://www.kernel.org/mirrors/ in your browser, your browser opens a socket to www.kernel.org and sends the following message:

```
GET /mirrors/ HTTP/1.0<cr><cr>
```

It may also send a lot of other information about what kind of data it can receive. This helps data translation. The last two `<cr><p>`s are newlines that indicate the end of the message. The client can send any number of parameters and settings, but it must end the message with two newlines.

The connection is streamed, so you don't know if you have hit the end of the message. This could lead to waiting indefinitely for something that never arrives. The two newlines tell the server that the client is done talking.

## Getting an HTTP Page

Composing the query is the easiest part of the connection. The query also gives you a lot of flexibility in adding what you need. The only requirement is to make sure that the server can understand your message. Listing 4.2 presents one way of getting a Web page. This program opens a connection specified on the command line and sends an HTTP request. The program prints the results on stdout.

### LISTING 4.2 Getting a Web Page from an HTTP Server

```c
/****...
 * Excerpt from the http-client.c (on Web site) file. **/
int sd;
struct servent *servv;
if ( (servv = getservbyname("http", "tcp")) == NULL )
    PANIC("HTTP servent");
if ( ( sd = socket(AF_INET, SOCK_STREAM, 0) ) < 0 )
    PANIC("Socket");

/*---Initialize server address/port struct----*/
bzero(&dest, sizeof(dest));
dest.sin_family = AF_INET;
dest.sin_port = servv->s_port;        /* HTTP Server */
if ( inet_addr(Strings[1], &dest.sin_addr.s_addr) == 0 )
    PANIC(Strings[1]);

/*---Connect to server----*/
if ( ( connect(sd, &dest, sizeof(dest)) != 0 )
    PANIC("Connect");

/*---Compose the query and send it-----*/
sprintf(buffer, "GET %s HTTP/1.0\n\n", Strings[2]);
send(sd, buffer, strlen(buffer), 0);

/*---While there's data, read and print it---*/
do
{ bytes_read = recv(sd, buffer, sizeof(buffer)-1, 0); buffer[bytes] = 0; if ( bytes_read > 0 ) printf("%s", buffer); } while ( bytes_read > 0 );
```

The program in Listing 4.2 opens the connection, sends the command-line request, and displays everything it gets until the server closes the connection. Later versions of the HTTP protocol (1.1 and the proposed HTTP-NG) include the capability to leave the channel open, taking advantage of the TCP connection. Again, this feature emphasizes the need to tell the receiver when the sender is done talking. You can read much more about the new versions of HTTP in the RFCs found at www.w3c.org.

## What Are Connectionless Sockets?

Not every communication requires having a full bi-directional channel open between peers. If the telephone is an example of a streaming connection, the postal system best represents a message-based (or connectionless) system. Like the postal system, UDP composes messages, assigns a destination, and ships it off without any tracking of the message as it travels to the destination. (Just to reiterate: A datagram’s unreliability means that it offers no guarantee of delivery. That does not mean it does not work.)

## Setting the Socket’s Address

The full installation of a Linux distribution usually includes tools that allow you to send and receive notes from other workstations on the network. The tools require only a machine address and maybe a username. You could implement this kind of tool on your own using a UDP socket. To do this, you need to see if the current user is the recipient of the message.

These messenger-style tools use the two pieces of data (hostname and username) to identify the recipient uniquely. The tool has no streamed data, so your implementation could use a connectionless interface.

The connectionless interface does not make the connect() system call, but you can’t call send() or recv() without a connection. Instead, the operating system offers two lower-level system calls that include the destination address: recvfrom() and sendto(). These calls act similarly to recv() and send(), but you provide the destination as part of the call:

```c
#include <sys/socket.h> #include <resolv.h>
```
