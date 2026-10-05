# TCP/IP and Linux Protocol Implementation

```
37 setimer(ITIMER_REAL, it_interval={0, 0}, it_value={10, 0}, NULL) = 0
38 time(NULL)
39 = 960371553
40 recvfrom(3, "E\u0270\u0261\u0278\u0231\u0273\u0260\u0260\u0263\u342...", 192, 0, {sin_family=
41 AF_INET, sin_port=htons(4288), sin_addr=inet_addr("128.16.5.31")}, [16]) = 84
42 gettimeofday(960371553, 407464, NULL) = 0
43 uname({"linux", node=ovavu.cs.ucl.ac.uk", ...}) = 0
44 socket(PF_INET, SOCK_DGRAM, IPPROTO_UDP, NULL) = 0
45 connect(4, {sin_family=AF_INET, sin_port=53, sin_addr=inet_addr("128.16.5.31")}, [16]) = 0
46 recvfrom(4, "\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231in-\...", 42, 1024, 0, {sin_family=
47 AF_INET, sin_port=htons(53), sin_addr=inet_addr("128.16.5.31")}, [16]) = 215
48 time(NULL)
49 = 960371553
50 poll({fd=4, events=POLLIN, revents=POLLIN}, 5000) = 1
51 recvfrom(4, "\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231\u0231in", 42", 1024, 0, {sin_family=
52 AF_INET, sin_port=htons(53), sin_addr=inet_addr("128.16.5.31")}, [16]) = 215
53 close(4)
54 = 0
55 write(1, "PING bells.cs.ucl.ac.uk (128.16.5.31) from\n"
56 128.16.6.226 : 56(64) bytes of data.
57 64 bytes from bells.cs.ucl.ac.uk (128.16.5.31): icmp_seq=0 ttl=255 time=4.1 ms
58 signal(SIGALRM, SIG_IGN, NULL, 8) = 0
59 write(1, "\n", 1)
60 = 1
61 write(1, "--- bells.cs.ucl.ac.uk ping statistics ---\n"
62 1 packets transmitted, 1 packets received, 0% packet loss round-trip min/avg/max 4.1/4.1/4.1\n"
63 ms
64 ) = 141
65 _exit(0)
66 = ?
```