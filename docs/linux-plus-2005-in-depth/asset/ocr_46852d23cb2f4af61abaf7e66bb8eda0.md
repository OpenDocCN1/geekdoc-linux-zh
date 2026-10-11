You then borrow some bits from the host portion of the subnet mask. Because the number of combinations of binary numbers can be represented in binary powers of two, and valid subnet masks do not contain all 0s or 1s, you can use the equation 2^n - 2 to represent the minimum number of subnets required, where n is the number of binary bits that are borrowed from the host portion of the subnet mask. For our example, this is represented as:

```
2^5 - 2 ≥ 15
2^5 ≥ 17
```

Thus, n = 5 (because 2^5 = 16 is less than 17, but 2^6 = 32 is greater than 17). Following this, our subnet mask borrows five bits from the default Class A subnet mask:

```
255.248.0.0 =       11111111.11111000.00000000.00000000
```

Similarly, because there are 19 zeros in the preceding subnet mask, you can use the 2^n - 2 equation referred to previously to identify the number of hosts per subnet:

```
2^19 - 2        =    number of hosts per subnet
        =    524,286 hosts per subnet
```

You can then work out the IP address ranges for each of the network ranges. Because three bits in the second octet were not borrowed during subnetting, the ranges of IP addresses that can be given to each subnet must be in ranges of 2^3 = 8. Thus, the first five ranges that can be given to different subnets on the 3.0.0.0/8 network that use the subnet mask 255.248.0.0 are as follows:

+   - 3.0.0.1-3.7.255.254
+   - 3.8.0.1-3.15.255.254
+   - 3.16.0.1-3.23.255.254
+   - 3.24.0.1-3.31.255.254
+   - 3.32.0.1-3.39.255.254

From the preceding ranges, a computer with the IP address 3.34.0.6/13 cannot communicate with the computer 3.31.0.99/13 because they are on different subnets. To communicate, there must be a router between them.

![](bbox=[0.13, 0.85, 0.2, 0.93])

# NOTE

When subnetting a Class C network, ensure that you discard the first and last IP address in each range to account for the broadcast and network address for the subnet.