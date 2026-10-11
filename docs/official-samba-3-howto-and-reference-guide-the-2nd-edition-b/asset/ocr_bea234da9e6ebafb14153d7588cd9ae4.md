(What You See Is What You Get) is relatively easy, because the on-screen graphic primitives, as well as the on-paper drawn objects, come from one common source. This source, the GDI, often produces a file format called Enhanced MetaFile (EMF). The EMF is processed by the printer driver and converted to the printer-specific file format.

> **NOTE**
> 
> To the GDI foundation in MS Windows, Apple has chosen to put paper and screen output on a common foundation for its (BSD-UNIX-based, did you know?) Mac OS X and Darwin operating systems. Apple's *core graphic engine* uses a *PDF* derivative for all display work.

The example in Figure 21.1 illustrates local Windows printing.

# **Figure 21.1** Windows Printing to a Local Printer.

![](bbox=[0.03, 0.5, 0.97, 0.76])

# **21.4.3** UNIX Printfile Conversion and GUI Basics

In UNIX and Linux, there is no comparable layer built into the OS kernel(s) or the X (screen display) server. Every application is responsible to itself to create its print output. Fortunately, most use PostScript and that at least gives some common ground. Unfortunately, there are many different levels of quality for this PostScript. And worse, there is a huge difference (and no common root!) in the way the same document is displayed on screen and how it is presented on paper. WYSIWYG is more difficult to achieve. This goes back to the time, decades ago, when the predecessors of X.org, designing the UNIX foundations and protocols for graphical user interfaces, refused to take responsibility for "paper output", as some had demanded at the time, and restricted itself to "on-screen only". For some years now, the “Xprint” project has been under development, attempting to build printing support into the X framework, including a PostScript and a PCL driver, but it is not yet...