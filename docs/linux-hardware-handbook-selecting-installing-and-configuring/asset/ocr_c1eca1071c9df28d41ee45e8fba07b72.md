multiple fonts or graphics, something more is required. Printer manufacturers have therefore developed printer languages, which are ways of encoding data such that the printer can produce good-looking results. The simplest printer languages are very crude; they consist of little more than special codes that precede characters in order to alter the appearance of those characters. Others are sophisticated computer programming languages. Printer languages that fall into this latter class are often referred to as *page description languages* (PDLs). 

Some printers support only one language, but others support two or more languages. Multilanguage printers are particularly common among mid-range and high-end laser printers, which frequently support both PostScript and PCL (Printer Command Language, described later in the chapter). Most of these devices can automatically detect what printer language is being used, but some earlier models require hints in the form of special escape codes.

# PostScript

Adobe’s (http://www.adobe.com) PostScript was the first sophisticated PDL. This is particularly true for Linux use, because most programs that print in Linux output either ASCII or PostScript. Therefore, PostScript printers require no drivers or special treatment; the Linux printing system can take program output and dump it directly to the printer port.

When a program prints PostScript to a non-PostScript printer, the *Ghostscript* program intervenes. Ghostscript converts PostScript into a format that can be understood by non-PostScript printers. Doing so chews up CPU time and RAM, however, so printing to a non-PostScript printer is generally slower than printing to a PostScript printer with similar specifications.

![](bbox=[0.15, 0.68, 0.3, 0.73])

> Ghostscript converts PostScript data into a bitmap, which is then sent to the printer. Therefore, features such as a large selection of built-in fonts are generally useless under Linux, unless the printer supports PostScript.

Because PostScript is such a complete language, it requires more in the way of onboard printer capability than do most other printer languages. This fact raises the cost of PostScript printers. So does the fact that Adobe charges fairly high licensing fees for PostScript. The high cost of genuine PostScript has created a market for an assortment of PostScript clones. Since the late 1990s, major companies such as Hewlett-Packard and Lexmark have begun to abandon genuine Adobe PostScript in favor of clones. In years past, PostScript clones often did a poor job of handling PostScript files, but most recent implementations are quite good. Nonetheless, if you regularly create unusual or demanding PostScript output, you should carefully investigate