# **Table 4.14** Arithmetic and Boolean operators (continued)

| Arithmetic Operators | Description |
| :--- | :--- |
| `!=` | Not equal |
| `+` | Plus |
| `-` | Minus |
| `*` | Multiply |
| `/` | Divide |
| `&` | Bitwise AND |
| `|` | Bitwise inclusive OR |
| `^` | Bitwise exclusive OR |
| **Boolean Operators** |  |
| `and or &&` | Concatenation |
| `or or ||` | Alternation |
| `not or !` | Negation |

To display all packets that originate from a particular Sun system, for example, use this command:

```
tcpdump "ether[6:4]&0xfffffff = 0x08002004"
```

This tells `tcpdump` to examine the sixth byte of the frame (the source frame address) and compare it to the 0x08002004 addresses using the `&` (and) operator. This datalink address represents the address of a local system called `monet`. Recall that Ethernet addresses are six bytes in length and we can use the first four bytes to identify the system desired. As a result, all packets transmitted from `monet` will be displayed. To identify another system, obtain the datalink address of the system, convert it to hexadecimal, and place it on the right side of the preceding command.