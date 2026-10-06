# CHAPTER 13

# Coding for Linux

# Applying What You've Learned to a True Protected Mode Operating System

I can see the "fan" mail now: "How can you claim your book is about Linux assembly language when you don't present any Linux code until the very last chapter?” (I get notes like this every time the book I wrote isn't exactly the book that a reader has hoped to find.) The answer here, of course, is that this book isn't about Linux assembly language. It's about assembly language for Intel's x86 family of processors. Most people still start fooling around with x86 assembly under DOS, so that's where I started. Many who started with assembly under DOS would like to move on to something more powerful and pertinent to real computing today, and more and more people see that destination as Linux.

So, where I began this book against a DOS backdrop, I'm finishing against a Linux backdrop. The book, however, is about neither DOS nor Linux. Nearly everything that I've taught so far applies to Linux as truly as DOS: addressing modes, machine instructions, and one- and two-level data tables, to name just a few. In truth, some things apply: real mode segmented model and DOS calls, primarily. The rest is as good under Linux as it is under DOS.

That being the case, you now have most of what you need to write assembly language programs for x86 processors under Linux. This chap-

451