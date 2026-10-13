Users typically will sit around the "chill-out" areas and work away on who knows what on their computers. At one point, users started noticing that images on Web pages they were requesting were not what they were expecting. Requests for Google's home page would return Google, but the main image would be different than expected. This same image showed up across multiple pages on multiple sites for multiple users. Of course, being Defcon and the juvenile bent that tends to inhabit attendees, the image was one of a rather horrific nature. Obviously, users expecting Google's iconic logo and receiving a horror show instead led to some truly puzzled users and some amazingly funny reactions (I did mention, "most hostile network on the planet". What were they expecting?)

Various users went about checking DNS settings, checked to see if they were connected to a rogue AP, or went as far as to fire up a packet sniffer to figure out what was happening. Few, if any people (other than the perpetrators) figured out what happened that weekend until the announcement was made later by the perpetrators of this rather hilarious hack. A guy going by the name of Toast took credit and released the tool he coded to do it, called Airpwn.

To understand what is being attacked, you must understand how things operate normally. When you request a Web page, your system connects to the remote server with the basic SYN/ACK handshake:

```
```
Client -> Server "GET /foo.html HTTP/1.0" seqno 123 ack 456
Server -> Client "<HTML...>" seqno 456 ack 145
```
```

The client browser sends a GET request for the page specified, "GET /foo.html HTTP/1.0", along with a sequence (SEQNO) number and an acknowledgment number (ACK) for the previous packet. The server normally returns packets containing the requested hypertext markup language (HTML) page, specifying a higher SEQNO and ACK of the previous packet. The process is repeated for every file on the page (images, Java Script, and so on).

Airpwn works off of a simple premise that works like this: On an open network, an attacker can see your packets go through the air much like an old shared medium (hub-based) wired network. A normal Web server's requests will take a bit of time to make the round trip. Since we are in the same room, we can often reply faster than the remote server.

The attack looks like this: A normal request for a file is made, except that the attacker sees it. He then crafts a response with appropriate SEQNOs and ACKs, forging the source MAC address to appear to be from the access point as if it were the legitimate response, except the response contains the attacker's content. Provided the content is small enough to be sent before the real packets arrive, the attacker can close the connection with a Finish (FIN) packet. The original request will now be out of sequence and be discarded. The browser will accept the attacker's content and render it accordingly to whatever damage to delicate sensibilities that may involve. In the sample configurations, there are several different examples. Figure 2.1 shows simple image replacement where images are replaced with the "AIRPW NED" graphic. Figure 2.2 shows replacement of the HTML.