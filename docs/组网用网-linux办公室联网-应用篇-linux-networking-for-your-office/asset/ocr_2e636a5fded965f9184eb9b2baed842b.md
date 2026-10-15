# Advantages of Using Ghostscript

When you configure a printer to use a queue that incorporates a Ghostscript filter, you use a PostScript driver on the client systems. In general, you use a PostScript driver that comes with the client OS. You probably need to select a specific model of printer when you install a driver in your client OS, but of course you don’t see the model you’re using on a list, because as far as the OS is concerned, that model is not a PostScript printer.

# Tip

> I’ve found that drivers for Apple LaserWriter printers tend to work well with Ghostscript when using monochrome printers. When using color printers, drivers for the QMS magicolor printer usually work well. You might want to research the capabilities of the printer whose driver you’re using relative to your actual printer. Pay particular attention to resolution. If you use a client-OS driver for a printer with a substantially lower resolution than your printer (or its Ghostscript driver) can produce, you might find that you don’t get the maximum benefit of the printer’s resolution in all situations.

The strong points of using a client-OS PostScript driver and Ghostscript on Linux include the following:

+   - Reduced network traffic—When you’re printing text, especially to low-end inkjet printers, PostScript tends to produce smaller files, and hence less network traffic. This advantage isn’t universal, though; for printing graphics to certain printers, there might be little difference or even more traffic when using PostScript drivers.

+   - Uniform output across printers—Especially if you use the same PostScript driver for multiple printers, your formatting doesn’t change when you change printers. Sometimes changing a printer driver in a client OS also changes your document’s fonts, word spacing, and so on. Of course, your documents might still look different when printed on different printers—you don’t magically get 600dpi or color printing from a 300dpi laser printer, for instance, and even different color printers can render colors differently.

+   - Simplified client-driver maintenance—If your network contains several printers, using Ghostscript to turn them all into PostScript printers from the client’s point of view can simplify client-side driver maintenance. Rather than deal with drivers for several different printers, you can install and maintain only one driver, connected to several client-OS queues. Even if you select PostScript drivers for several different models of PostScript printers, the client OS might install but a single driver, along with configuration files for each specific model.