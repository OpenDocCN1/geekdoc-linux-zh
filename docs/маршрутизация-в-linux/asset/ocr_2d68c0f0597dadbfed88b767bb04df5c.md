from the left, since it feels more natural for some. The first byte, 01001101, breaks down to the following, which is shown in two different ways:

0x2^7 + 1x2^6 + 0x2^5 + 0x2^4 + 1x2^3 + 1x2^2 + 0x2^1 + 1x2^0 = 77
0x128 + 1x64 + 0x32 + 0x16 + 1x8 + 1x4 + 0x2 + 1x1 = 77

The second byte, 00011101, breaks down into:
0x128 + 0x64 + 0x32 + 1x16 + 1x8 + 1x4 + 0x2 + 1x1 = 29

The third byte, 10111001:
1x128 + 0x64 + 1x32 + 1x16 + 1x8 + 0x4 + 0x2 + 1x1 = 185

And, finally, the fourth byte, 10110110:
1x128 + 0x64 + 1x32 + 1x16 + 0x8 + 1x4 + 1x2 + 0x1 = 182

So the decimal version of this IP address is 77.29.185.182. Now that we've got the address itself, we want to know things like which are the network bits and which are the host bits. To do that, we have to look at the standard IP address class table, as shown in Table 4.1.

# Table 4.1 IP Address Class Ranges, Without Special Addresses Removed and with Network Portions in Bold and Host Portions in Non-Bold

| Class | Start | End |
| --- | --- | --- |
|  | BINARY | DECIMAL | BINARY | DECIMAL |
| A | 00000001.00000000.00000000.00000000 | 1.0.0.0 | 01111111.00000000.00000000.00000000 | 127.0.0.0 |
| B | 10000000.00000000.00000000.00000000 | 128.0.0.0 | 10111111.11111111.00000000.00000000 | 191.255.0.0 |
| C | 11000000.00000000.00000000.00000000 | 192.0.0.0 | 11011111.11111111.11111111.00000000 | 223.255.255.0 |
| D | 11100000.00000000.00000000.00000000 | 224.0.0.0 | 11101111.11111111.11111111.11111111 | 239.255.255.255 |

This isn't the whole story, though. Not all of these addresses are actually available. Let's weed out the network addresses first. For example, the entire network 127.0.0.0 is only used to loop back to the same machine you're working in. You can't use it to reach another machine. No one is assigned this network number. The very first network 0.0.0.0 isn't even listed. It's used to point to the default route.

We also can't use the very first and last address in each class. All addresses where all of the variable bits are either 0s or 1s are reserved for special use. This means that the following addresses also are unavailable:

+   - Class A. These have already been mentioned, but they are included here for easy reference. 0.0.0.0 and 127.0.0.0 are unavailable.
+   - Class B. 128.0.0.0 and 191.255.0.0 are unavailable.
+   - Class C. 192.0.0.0 and 223.255.255.0 are unavailable.