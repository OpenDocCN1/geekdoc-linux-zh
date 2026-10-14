
# Figure 10-8: Printing a file to PDF in most GNOME applications

## Canceling a Print Job

It happens to all of us. You wanted to print just 1 page of a 57-page document, but you accidentally started printing the whole thing. What can you do to save your ink and 56 sheets of paper? Fortunately, the solution is simple.

Once you’ve clicked the Print button and the print job is sent to your printer, a small printer icon will appear somewhere at the right end of the top GNOME panel (usually to the left of the other items there), as you can see in Figure 10-9.

![](img/f7cef0df22f9dba5a41777808c98eece_239_0.png)

# Figure 10-9: A printer icon appears in the GNOME panel while printing.

Just click that icon once, and a window showing your current and queued print jobs will appear (as shown in Figure 10-10). Your errant print job will be listed in that window, so right-click the name of the job to select it, and then, in the pop-up menu, select Cancel. You’ll be asked whether you really want to cancel the job; click Yes.

After you do this, the print job listed in the queue window will disappear, and your printer will stop printing. You can then close the print queue window. This is a very easy process that you may well find is more effective than what you’ve experienced in other operating systems.

![](img/f7cef0df22f9dba5a41777808c98eece_240_0.png)

Figure 10-10: Canceling a print job via the print queue window

In some cases, things will be even easier, particularly if you installed your printer driver yourself by means of the installer that came packaged with the driver. In many such cases, the driver will provide its own progress window that will appear whenever you print a document. If so, you can simply click the Cancel button (or equivalent) in that window to cancel the printing job.

> NOTE In some cases, you may have to clear your printer after canceling a print job. You can do this by turning your printer off, waiting a few seconds, and then turning it on again.

## Checking Ink Levels and Other Printer Maintenance Tasks

Printer ink (and toner) has a knack of vanishing at a rate of knots, so it’s natural to want to check up on how your cartridges are doing. You might also run into problems with the printer, such as streaks on printouts or jagged lines that should really be straight, so it might be necessary to clean or align the print heads too. Unfortunately, there’s no one simple method of doing this since every make of printer handles it differently. I’ll just mention a few ways you can access these options for the most common brands:

- HPLIP This works only for Hewlett-Packard printers. Open the Ubuntu Software Center, and install HPLIP Toolbox. Select System ▸ Preferences ▸ HPLIP Toolbox to run it, and use the Supplies tab to check ink levels and the Actions tab to align and clean your cartridges.
- Inkblot This works for a number of Epson, Canon, and HP printers—check http://libinklevel.sourceforge.net/#supported/ to see whether your printer is supported. Open the Ubuntu Software Center, install Inkblot, and then select Applications ▸ System Tools ▸ Inkblot to check your ink levels.
- escputil This works for some Epson printers and is worth a try if Inkblot doesn’t support your model. Open the Ubuntu Software Center, and install escputil. Then, open a Terminal by selecting Applications ▸ Accessories ▸ Terminal. Type escputil -i (don’t forget the space) and hit ENTER to display the ink levels. To clean the print head, type escputil -c.

If you have no luck with these utilities or if your printer’s make isn’t listed, you might still be able to access ink levels and maintenance functions using the manufacturer’s own Linux driver, if one exists. Also, some newer printers allow you to check ink levels and align and clean cartridges using controls on the printer. When in doubt, check your printer’s manual.

## Scanners

Scanners are extremely useful and about as cheap a peripheral device as you can get. They allow you to take images or pages of text and input them, in digital form, into your computer—in much the same way as you would duplicate a document on a copy machine.

Even though scanners have been around for a relatively long time, support for them in Linux is still a bit spotty. Fortunately, this is changing for the better with every new Linux release. The backend—the hidden part of your system that handles scanner recognition and support in Linux—is called Sane. If you are wondering whether Linux will be able to recognize your scanner or if you are trying to figure out what type of scanner to buy, you can visit the Sane website at http://www.sane-project.org/sane-mfgs.html/.

There will be able to see whether your scanner is supported or get tips about what scanner to buy. The page is pretty long, so you might want to use the Find function in your web browser (select Edit ▸ Find in Firefox) to search for your scanner model. As I have mentioned, you can also try the Ubuntu forums (http://www.ubuntuforums.org/) and ask for Ubuntu-specific recommendations there.

## Scanning, No Questions Asked, with Simple Scan

Simple Scan is a new addition to Ubuntu’s line-up of default applications, and it certainly lives up to its name—it doesn’t take many clicks to get a document from scanner bed to computer screen. To run Simple Scan, make sure that your scanner is connected and switched on, and then select Applications ▸ Graphics ▸ Simple Scan. If you get a warning saying that no scanners were detected, skip to “Unrecognized Scanners” on page 207.

Assuming that your scanner has been recognized, you’ll be presented with the screen in Figure 10-11.

It’s pretty easy from here—select the type of document you’re scanning (Text or Photo) from the drop-down menu next to the Scan button (the menu’s icon is a small down-arrow), and then click Scan. Your scanner will roar into action, and, after a short wait, you’ll be presented with a preview of the picture or document you placed on the scanner. You can crop and rotate the image by using the options in the Page menu or by right-clicking the preview. When you’re happy with your scan, select Document ▸ Save to finish up.
