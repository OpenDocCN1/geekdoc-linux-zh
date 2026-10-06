# Table 6.1 Collective Terms for Memory

| NAME | DECIMAL | HEX |
|---|---|--|
| Byte | 1 | 01H |
| Word | 2 | 02H |
| Double word | 4 | 04H |
| Quad word | 8 | 08H |
| Ten byte | 10 | OAH |
| Paragraph | 16 | 10H |
| Page | 256 | 100H |
| Segment | 65,536 | 10000H |

10H; the third address 20H, and so on. (Remember that 10H is equal to decimal 16.) Any paragraph boundary may be considered the start of a segment.

This doesn't mean that a segment actually starts every 16 bytes or down throughout that megabyte of memory. A segment is like a shelf in one of those modern adjustable bookcases. On the back face of the bookcase are great many little slots spaced one-half inch apart. A shelf bracket can be inserted into any of the little slots. However, there aren't hundreds of them, but only four or five. Nearly all of the slots are empty and unused. They exist so that a much smaller number of shelves may be adjusted up and down the height of the bookcase as needed.

In a very similar manner, paragraph boundaries are little slots at which a segment may be begun. An assembly language program may make use of only four or five segments, each of those segments may begin at any of the 65,536 paragraph boundaries existing in the megabyte of memory available in the real mode model.

There's that number again: 65,536—our beloved 64K. There are 64 different paragraph boundaries where a segment may begin. Each paragraph boundary has a number. Always, the numbers begin from 0, and go to 64K minus one; in decimal 65,535, or in hex 0FFFFH. Because a segment may begin at any paragraph boundary, the number of the paragraph boundary at which a segment begins is called the segment address of that particular segment. We rarely, in fact, speak of paragraphs or paragraph boundaries at all. When you see the term segment address, keep in mind that each segment address is 16 bytes (one paragraph) farther along in memory than the segment address before it. Figure 6.4.