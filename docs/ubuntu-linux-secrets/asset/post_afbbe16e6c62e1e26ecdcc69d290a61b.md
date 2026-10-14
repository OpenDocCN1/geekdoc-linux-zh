
## Part 3: Managing Your Workstation

The second method is to list the user accounts that are allowed to use the printer. This option means that only the users on the list can print. Obviously, which method you choose depends on whether you have more people you want to allow to print or to restrict from printing.

Be careful when setting this feature. Notice how the two radio buttons are labeled:

- Allow printing for everyone except these users.
- Deny printing for everyone except these users.

If you click the Allow Printing radio button, the user accounts you list will be denied access to the printer—and vice versa for the Deny Printing radio button. That’s just a bit backward, if you ask me!

### Printer Options

The Printer Options group allows you to set some physical properties for the printer. The properties available for you to modify are based on information provided by the individual printer’s PPD file and depend on the physical characteristics of the printer.

These properties are divided into separate categories, depending on the printer’s capabilities. The options available for my test printer are shown in Figure 15-5.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_403_0.png)

**Figure 15-5:** The Printer Options group of the Printer Configuration tool.

The General settings handle properties such as types of paper the printer can handle, print qualities it can produce, and number and types of input trays. You can force the printer server to request a specific paper size for all print jobs or to request which paper tray to take paper from.

The Printout Mode settings control the default print quality used by the printer. Again, these settings depend on the capabilities of the particular printer, but usually there’s a range of dots per inch (dpi) and color settings to choose from.

### Job Options

Finally, the Job Options tab allows you to set the default properties for print jobs sent to the printer. When you request an application to send something to the printer, a standard GNOME Print dialog box appears, as shown in Figure 15-6.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_404_0.png)

**Figure 15-6:** The standard GNOME Print dialog box.

You can select several printing properties for the specific print job, such as whether to print in landscape mode, how many copies of the document to print, the paper size to use, and so on. If you prefer to use any of these settings by default, you can set them in the Job Options tab.

Many more print job options can be specified. The job options are divided into four sections:

- **Common Options:** Sets common printer options, such as number of copies, page orientation, and number of printed sides (for duplex printing).
- **Image Options:** Sets imaging options such as scaling and hue adjustment.
- **Text Options:** Sets features that affect the printed text, such as characters per inch, lines per inch, and margins.
- **Advanced Options:** Allows you to set options available for a specific printer.

The complete list of options appears within the Printer Configuration Properties window, as shown in Figure 15-7.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_405_0.png)

**Figure 15-7:** The Job Options Properties group in the Printer Configuration tool.

If you decide to revert to the default setting for an option, click the Reset button, and the option will return to the default value.

### Scanners

In the digital world it seems like we're always having to convert paper documents into a digital format. Whether it's scanning old pictures to save as digital images or scanning important documents to save in PDF format, a scanner has almost become a necessity for any home workstation.

Ubuntu provides the XSane application to interface with most of the scanners available. This section walks through the things you'll need to know to get the most out of your scanner and Ubuntu.

#### Detecting the Scanner

Before you can start using your scanner you need to ensure that XSane can work with it. Here are the steps to do that:

1. Connect your scanner to your Ubuntu workstation, then turn on the scanner.
2. After starting Ubuntu and logging in to your desktop, start XSane by selecting Applications ➜ Graphics ➜ XSane Image Scanner. The XSane splash screen appears, allowing you to select the scanner, as shown in Figure 15-8.
