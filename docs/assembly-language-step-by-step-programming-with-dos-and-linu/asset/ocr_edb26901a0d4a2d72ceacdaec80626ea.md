# CHAPTER 9

# Dividing and Conering

Using Procedures and Macros to Battle Complexity

# ## Programming in Martian

There is a computer language called APL (an acronym for A Programming Language, how clever) that has more than a little Martian in it. APL was the first computer language I learned (on a major IBM mainframe), and when I learned it, I learned a little more than just APL.

APL uses a very compact notation, with dozens of odd little symbols, each of which is capable of some astonishing power as matrix inversion. You can do more in one line of APL than you can in one line of anything else I have learned since. The combination of the strange symbol set and the compact notation makes it very hard to read and remember what a line of code in APL actually does.

So it was in 1977. Having mastered (or so I thought) the whole library of symbols, I set out to write a text formatter program. The program would justify right and left, center headers, and do a few other things of a sort that we take for granted today but which were very exotic in the seventies.

The program grew over a period of a week to about 600 lines of squirmy little APL symbols. I got it to work, and it worked fine—as long as I didn't