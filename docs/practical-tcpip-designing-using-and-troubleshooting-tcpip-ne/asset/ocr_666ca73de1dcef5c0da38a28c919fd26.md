Assuming that octet number 13 is an 8-bit unsigned integer in network byte order, the binary value of this octet is

0 0 0 0 0 0 1 0

and its decimal representation is

```
7 6 5 4 3 2 1 0
0*2 + 0*2 + 0*2 + 0*2 + 0*2 + 0*2 + 1*2 + 0*2 = 2
```

We're almost done, because now we know that if only SYN is set, the value of the 13th octet in the TCP header, when interpreted as a 8-bit unsigned integer in network byte order, must be exactly 2.

This relationship can be expressed as

tcp[13] == 2

We can use this expression as the filter for tcpdump in order to watch packets which have only SYN set:

```
tcpdump -i xl0 tcp[13] == 2
```

The expression says “let the 13th octet of a TCP datagram have the decimal value 2”, which is exactly what we want.

Now, let's assume that we need to capture SYN packets, but we don't care if ACK or any other TCP control bit is set at the same time. Let's see what happens to octet 13 when a TCP datagram with SYN-ACK set arrives:

```
| C | E | U | A | P | R | S | F |
| - | - | - | - | - | - | - | - |
| 1 | 0 | 0 | 1 | 1 | 0 | 0 | 1 |
| - | - | - | - | - | - | - | - |
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
```

Now bits 1 and 4 are set in the 13th octet. The binary value of octet 13 is

0 0 0 1 0 0 1 0

which translates to decimal

```
7 6 5 4 3 2 1 0
0*2 + 0*2 + 0*2 + 1*2 + 0*2 + 0*2 + 1*2 + 0*2 = 18
```

Now we can't just use `tcp[13] == 8' in the tcpdump filter expression, because that would select only those packets that have SYN-ACK set, but not those with only SYN set. Remember that we don't care if ACK or any other control bit is set as long as SYN is set.

In order to achieve our goal, we need to logically AND the binary value of octet 13 with some other value to preserve the SYN bit. We know that we want SYN to be set in any case, so we'll logically AND the value in the 13th octet with the binary value of a SYN: