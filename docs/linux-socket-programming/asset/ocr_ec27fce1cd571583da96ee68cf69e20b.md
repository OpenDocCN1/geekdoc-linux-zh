For the algorithm to work correctly, the program has to change some of the socket's default settings. First, most ping programs set the *TTL* (time to live) to the highest hop value (255). Also, the sender's socket must have nonblocking enabled to call *recvfrom*() without stalling.

The MyPing program is a good starting point for most ICMP-style packet messaging. After you are comfortable with this algorithm, other raw socket programs are similar to datagram programming.

# ## How Does Traceroute Work?

Another type of ICMP-style raw socket program is traceroute. You probably have used trace route for figuring out the path of a host-visitor or a spam message. The program builds on top of the MyPing program because it uses ICMP messages.

The basic algorithm is to send a ping message to the destination with an insufficient TTL. The intercepting router expires the packet and spits back an error. Repeat with a larger TTL until the message arrives at the destination. The result is actually pretty clever: The router between the source and the destination discovers that the TTL has expired, so it sends back an error (ICMP message) to the source. The router places its address in the error message. Only a raw ICMP socket works here because you may not get the error messages from the routers.

The loop is similar to the MyPing's sender process. The program needs a little extra logic to interpret the replies:

```
```C
TTL = 0;
do
{
  int len=sizof(r_addr);
  struct iphdr *ip;

  TTL++;
  if ( setsockopt(sd, SOL_IP, IP_TTL, &TTL,
                  sizeof(TTL)) != 0) 
    perror("Set TTL option");
  /****Initialize the message (see MyPing's sender)****/

  if ( sendto(sd, &pkt, sizeof(pkt), 0, addr, 
              sizeof(*addr)) <= 0) 
    perror("sendto");
  if ( recvfrom(sd, buf, sizeof(buf), 0,
                &r_addr, &len) > 0 ) 
  {
    struct hostent *hname;
    ip = (void*)buf;
    printf("Host #%d: %s \n", cnt-l, /* Print router IP */
           inet_ntoa(ip->saddr));
    hname = gethostbyaddr(
          (void*)&r_addr, sizeof(r_addr),
          r_addr.sin_family);   /* Try getting name */
    if ( hname != NULL )
      printf("(%s)\n", hname->h_name);
    else 
      perror("Name");
  } 
  else 
    perror("recvfrom");
}
/*----Repeat until the destination is the same as the reply---*/
while ( r_addr.sin_addr.s_addr != addr->sin_addr.s_addr );
```
```