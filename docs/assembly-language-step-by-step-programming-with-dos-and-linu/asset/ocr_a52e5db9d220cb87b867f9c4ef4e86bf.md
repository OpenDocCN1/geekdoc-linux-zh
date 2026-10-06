MyByte could have any of three possible addresses:

+   - 000H : 002DH
- 001H : 001DH
- 002H : 000DH

![](bbox=[0.199, 0.155, 0.72, 0.621])

**Figure 6.5** Segments and offsets.

thumb, however, I recommend using all four hex digits in both components of the address *except* when all four digits are zeros. In other words, you can abbreviate 0000:0061 to 0:0061 or 0B00:0000 to 0B00:

The universe is perverse, however, and clever eyes will perceive that **MyByte** has two other perfectly legal addresses: 0002D and 000200D. How so? Keep in mind that a segment may start every 16 bytes throughout the full megabyte of real memory. A segment, once begun, embraces all bytes from its origin to 65,535 bytes further up in memory. There's nothing wrong with segments overlapping, and in Figure 6.3 we have three overlapping segments. **MyByte** is 2DH bytes into the first segment, which begins at segment address 0000H. **MyByte** is 1DH bytes into the second segment, which begins at segment address