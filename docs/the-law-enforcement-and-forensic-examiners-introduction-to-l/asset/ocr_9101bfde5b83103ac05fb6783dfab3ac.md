```
barry@forensic1:~/able_3$ cat able_3.00* | grep -abi cybernetic
429415089:Cybernetic proudly presents...
429422127:Email: cybernetic@nym.alias.net
429422159:Finger: cybernetic@nym.alias.net
163278854*: updated by Cybernetic for linux rootkit
2934551933:231040 Cybernetic.net
```

We use the cat command to stream our splits for grep for our search. This is no different reconstructing the file (creating a single image with cat >), but instead we just pass the output of cat straight to grep. The results are slightly different from our able2 search, but we are going to concentrate on the same match we used for our able2 ext2 exercise. That would be the keyword hit at 1632788547.

Remember our steps from here. We need to calculate the offset in sectors (divide by 512), then the offset in the volume we found the keyword in, and then subtract the volume offset from the keyword offset to find the offset to the string in the volume. Make sure we calculate using the correct block size for the file system. We are working with data blocks. The fsstat command will give you the proper size for this file system.

We end up with the numbers below. Review the previous exercise if you have any questions on the steps above:

```
barry@forensic1:~/able_3$ echo $((1632788547/512))
3189040
```

| Slot | Start | End | Length | Description |
|---|---|---|---|---||
| 000: Meta | 000000000 | 000000000 | 000000001 | Safety Table |
| 001: | 000000000 | 000002047 | 000002048 | Unallocated |
| 002: Meta | 000000001 | 000000001 | 000000001 | GPT Header |
| 003: Meta | 000000002 | 000000033 | 000000032 | Partition Table |
| 004: | 000002048 | 000104447 | 000102400 | Linux filesystem |
| 005: | 000104448 | 000309247 | 000204800 | Linux filesystem |
| 006: | 0000309248 | 000571391 | 000262144 | Unallocated |
| 007: 002 | 0000571392 | 000388574 | 000781783 | Linux filesystem |
| 008: | 0000388575 | 000388607 | 0000000033 | Unallocated |

```
barry@forensic1:~/able_3$ fsstat -o 571932 able_3.000 | less
FILE SYSTEM INFORMATION
------------------------------------
```