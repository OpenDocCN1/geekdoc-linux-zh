![](bbox=[0.13, 0.05, 0.47, 0.15])

Figure 6.3 IP address example.

# Binary

When decimal numbers are entered into the computer, the system converts these into binary format, 0s and 1s, which basically correlate to electrical charges—charged versus uncharged. IP addresses, for example, are subnetted and calculated with binary notation. An example of an IP address with 24 bits in the mask is shown in Figure 6.3.

The first octet (206) indicates a Class C (Internet-assigned) IP address range with the format *network.network.network.host*, with a standard mask binary indicating 255.255.255.0. This means that we have 8 bits in the last octet for hosts.

The 8 bits that make up the last, or fourth, octet are understood by infrastructure equipment such as routers and software in the following manner:

| Bit: | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| Value: | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 = 255 (254 usable hosts) |

In this example of a full Class C, we only have 254 usable IP addresses for hosts; 0 and 255 cannot be used as host addresses since the network number is 0 and the broadcast address is 255.

Note that when a bit is used, we indicate it with a 1:

| 3 Bits: | 1 | 1 | 1 |
|---|---|---|---|
| Value: | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

When a bit is not used, we indicate this with a 0:

| 3 Bits: | 0 | 0 | 0 | 0 | 0 |
|---|---|---|---|---|---|
| Value: | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

As a result:

| 3 Bits: | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
|---|---|---|---|---|---|---|---|---|
| Value: | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

We add the decimal value of the used bits: 128 + 64 + 32 = 224. This means that the binary value 11100000 equates to the decimal value 224.

| DECIMAL | BINARY |
|---|---|
| 224 | 11100000 |