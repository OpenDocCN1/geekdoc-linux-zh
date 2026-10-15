# Printer selection

Individual software packages may have their own defaults regarding paper size. For example, GNU **enscript** is maintained in Finland by Markku Rossi and defaults to A4 paper. If you’re American and your distribution hasn’t compiled in a different default, one option is to grab the source code for **enscript** and reconfigure it. Typically, however, it’s easier to set the paper type on the command line or in a GUI configuration file. If your documents come out with the ends or sides cut off, paper size conflicts are a likely explanation.

You may also be able to adjust the default paper size for many printing tasks with the **paperconfig** command, the PAPERSIZE environment variable, or the contents of the **/etc/papersize** file. (Note: **paperconfig != paperconf**.)

Admittedly, not all output is on paper. If you take a color picture to the bakery department of a large supermarket, they can probably make you a cake that has a copy of that picture on top of it. These pictures are printed by specialized bitmap printers that use edible inks. Large, rectangular cakes are known as sheet cakes, and they come in standard sizes, too. Unfortunately, we’ll have to limit our discussion of sheet sizes to paper. You can’t talk about everything…

# 26.11 PRINTER PRACTICALITIES

Printers can bring troubles and frustrations. Here are some general guidelines to help limit those. When all else fails, just be glad you’re not still using a dot-matrix printer connected via an RS-232 serial port. (Unless, of course, you are.)

# Printer selection

If you’re using CUPS, before you buy a printer or accept a “free” printer that someone else is throwing away, go to the Foomatic database at linuxprinting.org (funded and run by the Linux Foundation) and check to see how well the printer is supported. The database classifies printers into four categories ranging from Paperweight to Perfectly; you want Perfectly.

Everyone likes printers with embedded PostScript interpreters. Configuration of these printers is invariably easy.

Non-PostScript printers tend to be less well supported. To print to these, you need software that converts print jobs into the printer’s preferred PDL or data format. Chances are, this software is available either from your Linux/UNIX vendor or from one of the other locations mentioned in this chapter. Still, CUPS handles most of these printers pretty well, too.

If you’re not using CUPS and you have a PostScript printer, you’re probably still in good shape. If you have a non-PostScript printer, try using Ghostscript to turn PostScript and PDF documents into something your printer can accept.