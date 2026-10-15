
## LISTING 7.25 Using snoop to Sniff a Connection

```
root@unixhost:~> snoop -o digtest.cap host 192.168.0.5
Using device /dev/hme (promiscuous mode)
2 ^C
root@unixhost:~> ls -l
total 1
-rw-r--r-- 1 root other 248 Jun 24 14:47 digtest.cap
```

In Listing 7.25 snoop was used to capture packets that had the IP address 192.168.0.5 as either source or destination. The captured packets were saved to the file digtest.cap. The line with the number 2 shows the number of captured packets.

The resulting file—especially its permissions—should give you a visual indication why captured files should be stored out of reach from other users. They are world-readable. You could use the command `umask 0077`, but storing the files in a secure location seems to be the best approach.

The command issued on host 192.168.0.5 was `dig examplehost3`, as shown in Listing 7.26.

## LISTING 7.26 dig Command Issued on 192.168.0.5

```
root@unixhost:~> dig examplehost3

;; <<>> DiG 8.3 <<>> examplehost3
;; res options: init recurs defnam dnsrch
;; got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 2
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; QUERY SECTION:
;; examplehost3, type = A, class = IN

;; ANSWER SECTION:
examplehost3. 30M IN A 192.168.0.3

;; Total query time: 224 msec
;; FROM: unixhost to SERVER: default -- 192.168.0.150
;; WHEN: Thu Jun 24 14:47:09 2004
;; MSG SIZE sent: 39 rcvd: 55
```

To inspect the captured packets, you use the command `snoop -i digtest.cap`, as shown in Listing 7.27.

## LISTING 7.27 Displaying the Captured Packets (Default View)

```
root@unixhost:~> snoop -i digtest.cap
1  0.00000 unixhost -> mylocaldns DNS C examplehost3. Internet Addr ?
2  0.22161 mylocaldns -> unixhost DNS R examplehost3. Internet Addr 192.168.0.3
```

The information in Listing 7.27 tells you that a system named unixhost queried a DNS about the IP address of a machine named examplehost3 and the resulting answer. If this is all you need to know, the default view is sufficient. To drill a little deeper, you add the option -V, as shown in Listing 7.28.

## LISTING 7.28 Displaying the Captured Packets a Little More Verbose

```
root@unixhost:~> snoop -V -i digtest.cap
----------------------------------------
1  0.00000 unixhost -> mylocaldns  ETHER Type=0800 (IP), size = 81 bytes
1  0.00000 unixhost -> mylocaldns IP  D= 192.168.0.150 S=192.168.0.5 LEN=67, ID=54825, TOS=0x0, TTL=255
1  0.00000 unixhost -> mylocaldns UDP D=53 S=33107 LEN=47
1  0.00000 unixhost -> mylocaldns DNS C examplehost3. Internet Addr ?

2  0.22161 mylocaldns -> unixhost  ETHER Type=0800 (IP), size = 97 bytes
2  0.22161 mylocaldns -> unixhost  IP  D=192.168.0.5 S=192.168.0.150 LEN=83, ID=0, TOS=0x0, TTL=57
2  0.22161 mylocaldns -> unixhost  UDP D=33107 S=53 LEN=63
2  0.22161 mylocaldns -> unixhost  DNS R examplehost3. Internet Addr 192.168.0.3
```

Now the sequence of the conversation between the hosts becomes visible, but the details are still hidden. To display all captured information, you use the option -v. Listing 7.29 shows the result.

## LISTING 7.29 Displaying All Captured Information

```
# snoop -v -i digtest.cap
ETHER: ----- Ether Header -----
ETHER:
ETHER: Packet 1 arrived at 14:47:9.74
ETHER: Packet size = 81 bytes
ETHER: Destination = 0:30:ab:4:b2:7f,
ETHER: Source = 8:0:20:b3:7:93, Sun
ETHER: Ethertype = 0800 (IP)
ETHER:
IP: ----- IP Header -----
IP:
IP: Version = 4
IP: Header length = 20 bytes
IP: Type of service = 0x00
IP: xxx .... = 0 (precedence)
IP: ...0 .... = normal delay
IP: .... 0... = normal throughput
IP: .... .0.. = normal reliability
IP: .... ..0. = not ECN capable transport
IP: .... ...0 = no ECN congestion experienced
IP: Total length = 67 bytes
IP: Identification = 54825
IP: Flags = 0x4
IP: .1. .... = do not fragment
IP: ..0. .... = last fragment
IP: Fragment offset = 0 bytes
IP: Time to live = 255 seconds/hops
IP: Protocol = 17 (UDP)
IP: Header checksum = 2038
IP: Source address = 192.168.0.5, unixhost
IP: Destination address = 192.168.0.150, mylocaldns
IP: No options
IP:
UDP: ----- UDP Header -----
UDP:
UDP: Source port = 33107
UDP: Destination port = 53 (DNS)
UDP: Length = 47
UDP: Checksum = 6D6E
UDP:
DNS: ----- DNS Header -----
DNS:
DNS: Query ID = 2
DNS: Opcode: Query
DNS: RD (Recursion Desired)
DNS: 1 question(s)
DNS: Domain Name: examplehost3.
```
