| Class | IP Address Range | Hosts Per Network | Default Netmask |
|---|---|---:|---|
| A | 001.X.X.X to 126.X.X.X | 16387064 | 255.0.0 |
| B | 128.0.X.X to 191.255.X.X | 64516 | 255.255.0.0 |
| C | 192.0.0.X to 233.255.255.X | 254 | 255.255.255.0 |

medium-sized company will have one or more class B networks, while small companies or individuals will have class C networks.

The netmask determines how you have decided to subnet, or partition, your network. Using the default netmask on a class B network lets all 64 thousand possible systems together. While this may seem ideal, the network delays would be quite large.

For large networks, your network administrators will decide how to partition your network. In practice, small portions of a class A or B network will be grouped together; for example, if you have a class B network and want to merge two networks with the address range 130.207.232 and 130.207.233. This will give you 508 possible hosts on one network.

The binary representation of those networks when translated using the /1’s in the subnet mask and a netmask of 255.254 gives the same value, which shows that the subnets have been concatenated.

```
10000010.11001111.11101000.X
11111111.11111111.11111111.00000000
10000010.11001111.11101000.00000000
```

```
10000010.11001111.11101001.X        (130.207.233)
11111111.11111111.11111111.00000000
10000010.11001111.11101000.00000000
```

If we now use use the 0’s, the operation gives a unique host address with 508 different binary combinations (where X can be any binary value from 1 to 254).

```
10000010.11001111.11101000.X        (130.207.232)
11111111.11111111.11111111.00000000
00000000.00000000.00000000. X
```