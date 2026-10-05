# 558 CHAPTER 14 PRINTING WITH CUPS

![](bbox=[0.297, 0.091, 0.843, 0.458])

Figure 14-1 The third Add Printer

After displaying a brief message, the CUPS web interface displays the Printer page (Figure 14-12) showing the new printer. Maintenance↔Print Test to confirm the new setup works. If you want to make this the default printer, click the button labeled Administration and select **Set As Server Default.**

The buttons at the bottom of the Printer page enable you to cancel or move jobs in the print queue. In addition to these tasks, you may be able to reprint jobs. Figure 14-12 shows the Printer page displaying information about how a job is printing.

# TRADITIONAL UNIX PRINTING

Before the advent of GUIs and WYSIWYG (page 1181) word processors, UNIX users would create documents using an editor such as vi and a typesetting markup language such as Tex or nroff, converting the result files to PostScript using an interpreter, and send the PostScript files to the printer using lpr (BSD) or lp (System V). Ubuntu implements both BSD and System V command-line utilities for compatibility. However, these utilities are now wrappers around the equivalent functionality in CUPS rather than core components of the printing system. The corresponding utilities are functionally equivalent; whichever you prefer (Table 14-2).

The *cups-bsd* package holds the BSD utilities; the *cups-client* package holds the System V utilities. From the command line, you can print a text, PostScript, or PDF file using lp:

```
$ lp 1 memo.txt
request id is MainPrinter-25 (1 file(s))
```