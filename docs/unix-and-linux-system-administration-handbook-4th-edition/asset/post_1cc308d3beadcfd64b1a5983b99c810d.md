
You can diff a couple of related PPDs (try pxlmono.ppd and pxlcolor.ppd) to see exactly how two printers differ.

If you need a PPD file and your printer vendor doesn’t supply one—say, because the printer doesn’t have a PostScript interpreter and the vendor doesn’t care about anything but Windows—go to linuxprinting.org and hunt through the Foomatic database for more information. Your printer may also be supported by the Gutenberg print project (gutenprint.sourceforge.net). If you have a choice of PPDs from these sources and your users want every last drop of quality, the ones marked “foomatic+gutenprint” are often quite good. However, you’ll still have to experiment with the printer configuration to find out what options give the best output.

If a PPD file is nowhere to be found:

- You should have consulted linuxprinting.org before you acquired the printer. Even if you got the printer out of a dumpster, “free” doesn’t always mean “inexpensive.”
- There may well be a PPD file that will let you print something, even if it doesn’t take advantage of all your printer’s features. For example, we’ve had good luck using generic HP drivers on non-HP printers.

Though CUPS depends on PPDs, older printing systems make no use of them. For the BSD or System V printing systems, you can either massage your PostScript or you can live with what you get by default.

## 26.10 PAPER SIZES

Users want output on physical sheets of paper. Paper comes in sizes and shapes. To make your users happy, you should know the basic facts about paper sizes.

In the United States and Canada, the most common paper size is called letter and is 8.5 × 11 inches. Some Linux distributions (e.g., Knoppix and SUSE) are produced in Europe, where they don’t even know what inches are, or in England, where they do know but don’t use them to measure paper. In these places, and in Japan, the common paper type is called A4, and printers all come with A4 trays. Ergo, some distributions’ printing utilities produce A4 page images by default.

There are also an ISO B series and C series that preserve the √2 aspect ratio but have different base areas. B0 paper is one meter tall, and C0 paper has an area of two square meters. Engineers will see immediately that the sides of Bn paper are the geometric means of An − 1 and An sides, while Cn paper sides are the geometric means of An and Bn.

What does all this mean? Bn has the same look as An but is bigger, and Cn is intermediate between the two. A report on A4 paper fits beautifully in a C4 Manila folder. Folding an A4 letter down the middle to make it A5 lets it slide into a C5 envelope. Fold it again and it slides just as nicely into a C6 envelope.

To confuse things slightly, Japan has its own B series that’s similar but different. Although it has the same aspect ratio as the ISO papers, the size of Japanese B4 paper is the arithmetic mean of A3 and A4, which (engineers will also see immediately) makes it slightly larger than ISO B4 paper. There is no Japanese C series.

Just as the ISO system makes it easy to copy two pages of a B5 textbook onto a single B4 handout, it makes all types of n-up printing (printing several reduced-sized page images on the same page) trivial. European copiers often have buttons that reduce or expand by a factor of √2.

If you have a CUPS system with the paperconf command, you can use it to print the dimensions of various named papers in inches, centimeters, or printer’s points (72nd of an inch). For the Americans, Table 26.7 lists some typical uses for common sizes to give a sense of their scale.

### Table 26.7 Common uses for ISO paper sizes

| Sizes | Common uses |
|-------|-------------|
| A0, A1 | Posters |
| A3, B4 | Newspapers |
| A4 | Generic "pieces of paper" |
| A5 | Note pads (roughly 5 × 8 inches) |
| B5, B6 | Books, postcards, German toilet paper |
| A7 | "3 × 5" index cards |
| B7 | Passports (even U.S. passports are B7) |
| A8 | Business cards |
| B8 | Playing cards |

Unfortunately, A4 paper is slightly thinner and longer (8.3 × 11.7 inches) than American letter paper. Printing an A4 document on letter paper typically cuts off vital slivers such as headers, footers, and page numbers. Conversely, if you’re in Europe or Japan and try to print American pages on A4 paper, you may have the sides of your documents chopped off, though the problem is less severe.
