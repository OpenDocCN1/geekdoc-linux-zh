
# Using Third-Party Drivers

Recently, more Linux printer drivers are becoming available. If you don't find your printer on that second page of the printer setup wizard, just try searching the Web for the make and model of your printer plus the word linux. In the past, for example, I had a laser printer that did not appear at http://www.openprinting.org/printers/, so I searched for the printer, samsung+SCX410+, which led me to http://www.driverstock.com/, a site that provides free drivers for most operating systems, including Linux. On that site, I found not only the driver for my printer but also the driver for its built-in scanner.

You might also want to check the website of the manufacturer of your printer, because many provide Linux drivers for a number of their printers. Brother, Lexmark, Hewlett-Packard, Canon, and Samsung, to name a few. There is also a German company (http://www.turbprint.info/; site in English) that provides Linux drivers, albeit for a fee, for machines that are really hard to deal with and for high-quality graphics solutions.

If you happen to find and download a driver for your printer that does not come with its own installer, follow the directions for trying Windows drivers. Finally, don't forget to check the Ubuntu forums (http://www.ubuntuforums.org/) and try to see whether anyone has any experience getting the printer to work on his system.

# Trial and Error

Finally, there is always the old trial-and-error approach, which works on occasion. When setting up your printer via the wizard window, try choosing one of the other models and/or drivers available from your printer's manufacturers.

After you are done with the wizard, double-click the printer you added in the Printing window, click the Settings tab, and then click the Print Test Page button to see what happens. If nothing happens, click the Change button on the far right end of the Make and Model row on the Settings screen; select a different printer and/or driver; and then, click on the Print Test Page button again. Repeat that process until something works. With any luck, something will ... might ... well, just give it a try if you're desperate.

# Printing Details

Now that your printer is set up, you will no doubt want to start printing! This is an easy task, and it isn't very different from how it works in the Windows and Mac worlds, so you shouldn't need much explanation to proceed. In fact, printing in Ubuntu has become easier than ever, because all the settings you would normally want to toy with are all on their own tabs within the Print window that appears when you select Print in an application's File menu. I would even dare that figuring out printing options in Ubuntu is now easier than it is in Windows or OS X.

You should be aware that the function of the tabs can vary depending on the application you happen to be printing from. For instance, the tabs you'll see when printing from the GIMP will be slightly different from those you will see when printing from Firefox. The General and Page Setup tabs will almost be be there. All that I said, I'll give you an idea of the settings that are available within some of the Print window's tabs:

- **General**: Printer selection, pages to print, number of copies, order of printing, collating
- **Page Setup**: Pages per sheet, scaling, paper type, paper source, output tray
- **Options**: Print frames, shrink to fit page, print background, headers and footers
- **Image Settings**: Size, resolution, at time
- **Job**: Print timing (now, later, at), cover page

# Printing in LibreOffice

Occasionally, you will come across an application that has a slightly different way of handling printing. Fortunately, the differences may actually make printing in LibreOffice more easier for newbies from the Windows-like world to follow along with. As you can see in Figure 10-6, the main window for LibreOffice applications allows you to select the printer you want to use, the range of pages, and how many copies you want to print. You can access other options by clicking the Properties and/or Options.

![](img/d35fa962e6f9664d66dc83916f426418_224_0.png)

Figure 10-6: Print settings in LibreOffice

# Printing to PDF

One of the nice features of Linux is that you can save most documents and web pages as PDF files. In some cases, such as in LibreOffice, you do this by exporting the document to PDF. In most other applications, however, you do it via the Print window, in which case you are said to be "printing to PDF." Whether you are saving as PDF, exporting to PDF, or printing to PDF, you are essentially doing the same thing: creating a PDF file of your document.

This is very helpful, because it allows you to create documents that cannot be altered by others and can be easily read regardless of the word processor or operating system the reader is using. Best of all, this feature, which you would have to pay a pretty penny for in the Windows world, costs you nothing because it is built into your system.

In most applications, you can print to PDF by going to the File menu of the application in question and selecting Print. When the Print window (Figure 10-7) appears, select Print to File in the list of printers and make sure PDF is the output format. Choose a name for the PDF file and then click the Print button to save.

![](img/d35fa962e6f9664d66dc83916f426418_225_0.png)

Figure 10-7: Printing to PDF in GNOME

# Canceling a Print Job

It happens to all of us. What can you do if you accidentally started the whole thing? Frankly, the solution is simple.

Click the printer icon on the top panel and select Printers from the menu. A window showing your current jobs will appear (as shown in Figure 10-8). Right-click the name of the job to select it and then, in the pop-up menu, select *Cancel*. You'll be asked whether you want to cancel the job; click **Yes**.

![](img/d35fa962e6f9664d66dc83916f426418_226_0.png)

Figure 10-8: Canceling a print job via the Print Queue

After you do, the print job listed in the queue will disappear, and your printer will stop printing. You can then close the window. In some cases, things will be even easier, particularly if you installed your printer driver by means of the installer that came with the driver. In such cases, the driver might provide its own progress window that will appear whenever you print a document. If so, you can simply click the Cancel button (or equivalent) in that window to cancel the job.

> NOTE In some cases, you may have to clear your printer after canceling a print job. You can do this by turning your printer off, waiting a few seconds, and then turning it on.

# Checking Ink Levels and Other Printer Tasks

Printer ink or toner has a knack for vanishing like freshly baked cookies, so it's natural to check on how your cartridges are. You might also run into problems with the printer, such as streaks on printouts or jagged lines that should really be straight, so it may be necessary to clean or align the print heads. Unfortunately, there's no one simple method of doing this since every make of printer handles it differently. I'll just mention a few ways you can access these options for the most common brands:

- **HPLIP**: This works for Hewlett-Packard Software Center and install HPLIP Toolbox. Search for HPLIP Toolbox in the Dash to run it; use the Supplies tab to check ink levels and the Actions tab to align and clean your cartridges.
- **Mtink**: This works for a number of Epson, Canon, and HP printers—check http://xtools.automatix.de/english/overview.html#PRINTERS to see whether your printer is supported. Open the Ubuntu Software Center, install Mtink, and then open it from the Dash to check your ink levels.
