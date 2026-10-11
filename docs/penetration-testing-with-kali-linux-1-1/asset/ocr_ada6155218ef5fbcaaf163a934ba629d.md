Turning on only these bits would give us 00011000, or decimal 24.

```
kali@kali:~$ echo "$(2#00011000)"
24
Listing 132 - Converting the binary bits to decimal in bash
```

We can pass this number to tcppdump with `tcip[13] = 24` as a display filter to indicate that we only want to see packets with the ACK and PSH bits set (“data packets”) as represented by the fourth and fifth bits (24) of the 14th byte of the TCP header. Bear in mind, the tcppdump array index used for counting the bytes starts at zero, so the syntax should be (tcp[13]).

The combination of these two flags will hopefully show us only the HTTP requests and responses data. Here’s the command we’ll use to display packets that have the ACK or PSH flags set:

```
kali@kali:~$ sudo tcppump -A -n 'tcip[13] =~ (24|13)' -r password_cracking_filtered.pcap

05:51:20.802932 IP 208.68.234.99.60509 > 172.16.40.10.81: Flags [P.], seq 185504075:1
E.....@.9.....D..c..
E...@..Q...j...V+....*.......S1.....
....A....GET //admin HTTP/1.1
Host: admin.megacorpone.com:81
User-Agent: Teh Forast Lobster


E.....@.E.........D..c..Q...E...?I.......
..A......HTTP/1.1 401 Authorization Required
Date: Mon, 22 Apr 2013 12:51:20 GMT
Server: Apache/2.2.20 (Ubuntu)
WWW-Authenticate: Basic realm="Password Protected Area"
Vary: Accept-Encoding
Content-Length: 488
Content-Type: text/html; charset=iso-8859-1



88:51:25.044432 IP 172.16.40.10.81 > 208.68.234.99.33313:
E...s...@.E...D...c...@.Q..10...&...u.....
..A......HTTP/1.1 301 Moved Permanently
Date: Mon, 22 Apr 2013 12:51:25 GMT
...
```