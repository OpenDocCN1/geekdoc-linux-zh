
## CHAPTER 11 TCP/IP for System Administrators

303 

of the data that has been sent by 192.168.1.12. It's also acknowledging that its available window is now 31,626, which is exactly the original window size (32,120) minus the amount of data that has been received (493 bytes).

A few moments later, in the fourth line, 192.168.1.1 senses that it has successfully transferred the data to the application's buffer and that its window is back to 32,120.

A little confusing? Don't worry too much about it. As a system administrator, you shouldn't have to deal with this level of detail, but it is helpful to know what the numbers mean.

> NOTE You may have noticed an off-by-one error in the math header, 32,120 – 493 is 31,627, not 31,626. This has to do the nuances of sequence numbers, calculations of available space, and other factors. For the full ugliness of how the math works, read RFC 793 (http://ftp.ietf.org/in-notes/rfc793.txt).

5 at the end of the output, you can see the length of the data being sent (5 in this example). Similar to IP's header length, TCP's header length tells us how long the header is, including any TCP options. Whatever value appears in the header length field is multiplied by 4 to get the byte value.

Finally, the last noticeable piece of the TCP header is the urgent pointer (see Figure 11-6). The urgent pointer points to the offset of the following important data. This value is observed when the URG flag is set and tells the receiving TCP stack that important data is present. The TCP stack is supposed to relay this information to the application so that it knows to treat that data with special importance.

In reality, you'll be pressed to see a packet with the URG flag. Most applications have no way of knowing whether data sent to them is urgent or not. As a result, a small chord of paranoia should shake you if you see urgent flags in your network. Make sure it isn't part of a probe from the outside trying to exploit bugs in your TCP stack and cause your servers to crash. (Don't worry about Linux—it knows how to handle the bit correctly.)

## UDP

In comparison to TCP headers, UDP headers are much simpler. Let's start by looking at Figure 11-7.

| 16-bit Source Port Number | 16-bit Destination Port Number | 8 bytes |
| :--- | :--- | :--- |
| 16-bit UDP Length | 16-bit UDP Checksum | |
| Data (if any) | | |

Figure 11-7 The UDP packet header

## Linux Administration: A Beginner's Guide

The first fields in the UDP header are the source and destination port numbers. These are conceptually the same thing as the TCP port numbers. In tcpdump output, they appear in a similar manner. Let's look at a DNS query to resolve www.example.com into an IP address with the example tcpdump -nn -t port 53:

192.168.1.1096 > 192.168.1.83:25851+ A? www.example.com. (31)

In this output, you can see that the port of this UDP packet is 1096 and the destination port is 53. The rest of the line is the DNS request in a human-readable format. The next field in the UDP header is the length of the packet. tcpdump does not display this information.

Finally, the last field is the UDP checksum. This is used by UDP to validate the data has arrived to its destination without corruption. If the checksum is corrupted, tcpdump will tell you.

## A Complete TCP Connection

As we discussed earlier, TCP supports the concept of a connection. Each connection must go through a sequence to be established; after both sides are done sending data, we must go through another sequence to connect the connection. In this section, we review the complete process of a simple HTTP request and view the process seen by tcpdump. Note that all the tcpdump logs in this section were generated with the tcpdump -nn -t port 80 command. Unfortunately, because of the complex nature of TCP, we cannot cover every possible scenario that a TCP connection can take. However, the coverage provided here should be enough to help determine when things are going wrong at the network level rather than at the server level.

## Opening a Connection

TCP undergoes a three-way handshake for every connection it opens. This allows both sides to send each other their state information and give each other a chance to acknowledge the receive of data.

The first packet is sent by the host that wants to open the connection with a server. For this discussion, we will call this the client. The client sends a TCP packet over IP and sets the TCP flag to SYN. The sequence number is the initial sequence number that the client will use for all of the data it will send to the other host (we'll call the server).

The second packet is sent from the server to the client. This packet contains two TCP flags set: SYN and ACK. The purpose of the ACK flag is to tell the client that it has received the first SYN packet. This is double-checked by placing the client's sequence number in the acknowledgment field. The purpose of the SYN flag is to tell the client with which sequence number the server will be sending its responses.

## CHAPTER 11 TCP/IP for System Administrators 305

Finally, the third packet from the client to the server. It has only the ACK bit set in the TCP flags for the purpose of acknowledging to the server that it received its SYN. This ACK packet has the client's sequence number in the sequence number field and the server's sequence number in the acknowledgment field.

Sound a little confusing? Don't worry—it's. Let's try to clarify it with a real example from tcpdump. The first packet is from 192.168.1.1 to 207.126.116.254, and it looks like this (note that both lines are one long line):

```
192.168.1.1.1367 > 207.126.116.254:80: Flags[S], seq 2524389053:2524389053
win 31220 <ms 1460, ack OK, timestamp 26292983 0,wscale 0, length 0
```

192.168.1.1.1367 > 207.126.116.254:80: Flags[S], seq 2524389053:2524389053
win 31220 <ms 1460, ack OK, timestamp 26292983 0,wscale 0, length 0

You can see that the client's sequence number is 1367 and the server's port is 80 (HTTP). The S bit is set and the sequence number is 252438905. After the window is specified as 32,120 bytes, you can see that TCP options are part of the packet. The only option worth noting is the MSS (Maximum Segment Size). This value tells you the maximum size that TCP is for nonsegmented packet. Connections that require small MSS values typically require more packets to transmit the same amount of data. More packets mean more overhead, and that means more CPU cycles are required to process.

Notice that no acknowledgment bit is set and there is no acknowledgment field to this. This is because the client has no sequence number to acknowledge. For the second packet from the server to the client:

```
207.126.116.254.80 > 192.168.1.1.1367: Flags[S.], seq 1998624975:1998624975
ack 32736 <ms 1460, length 0
```

Like the first packet, the second packet has the SYN bit set, meaning that it is OK the client will start its sequence number with (in this case, 1998624975). It's OK that client and server use different sequence numbers. What's important, that the server is acknowledging the client's first packet by turning on the ACK and setting the acknowledgment field to 252438905 (the sequence number that the client used to send the first packet plus).

Now that the server has acknowledged the client's SYN, the client needs to acknowledge receiving the server's SYN. This is done with a third packet that has only the ACK bit set in its TCP flags. packet looks like this:

```
192.168.1.1.1367 > 207.126.116.254.80: Flags[.], ack 1, win 31220
```

You can clearly see that there is only one TCP bit set: ACK (indicated by the dot). The value of the acknowledgment field is shown as a 1. But wait! Shouldn't it be acknowledging 1998624975? Well, don't worry—it's. tcpdump has been kind enough to switch automatically into a mode that prints out the relative sequence and acknowledgment instead of the absolute numbers. This makes the output
