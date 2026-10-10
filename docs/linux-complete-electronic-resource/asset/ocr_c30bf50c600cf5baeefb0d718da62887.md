is based upon what utilities are available to satisfy your needs, as well as personal taste.

Many people consider groff’s formatting language to be a bit obscure and find \TeX more readable. However, groff produces ASCII output that can be viewed on a terminal more easily, while \TeX is intended primarily for output to a printing device. Various add-on programs are required to produce ASCII output from \TeX formatted documents or convert \TeX input to groff format.

Another program is texinfo, an extension to \TeX that is used for software documentation developed by the Free Software Foundation. Texinfo can produce printed output or an online-browseable hypertext Info document from a single source file. Info files are the main format of documentation used in GNU software like emacs.

Text processors are used widely in the computing community for producing papers, theses, magazine articles, and books. (This chapter was written in LaTeX.) The ability to process source language as a text file opens the door to many extensions of the text processor itself. Because a source document is not stored in an obscure format that only one word processor can read, programmers can write parsers and translators for the formatting language and thus extend the system.

What does a formatting language look like? In general, a formatted source file consists mostly of the text itself, with control codes to produce effects like font and margin changes, and list formatting.

Consider the following text:

> Mr. Torvalds:
> 
> We are very upset with your current plans to implement post-hypnotic suggestions in the Linux terminal driver code. We feel this way for three reasons:

+   1.  Planting subliminal messages in the terminal driver is not only immoral; it is a waste of time;
+   2.  It has been proven that post-hypnotic suggestions are ineffective when used upon unsuspecting Unix hackers;
+   3.  We have already implemented high-voltage electric shocks, as a security measure, in the code for login.

We hope you will reconsider.

# Introduction to Linux 11

![](bbox=[0.93, 0.09, 0.99, 0.24])