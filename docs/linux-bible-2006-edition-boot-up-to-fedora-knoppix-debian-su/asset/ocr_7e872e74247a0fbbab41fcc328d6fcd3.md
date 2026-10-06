# 700 Part V ♦ Running Servers

Printing should be working at this point. (If you want to share this printer with other computers on your network, refer to the “Configuring Print Servers” section of this chapter).

Adding a printer in the K Desktop Environment (KDE) is very similar to the GNOME process. Select System Menu -> Print Add Printer; the New Printer Wizard opens. See http://docs.kde.org/development/kdebase/kdeprint/ for more details on using the New Printer Wizard (and printing in general).

# Editing a Local Printer in Red Hat

After you have created a printer, you can edit the printer definitions to change how the printer behaves. From the Printer Configuration window, do the following:

+   1. Select your printer, and click Edit. The Edit a Print Queue page appears. The following steps describe how to change options besides those you added originally.
2. Click the Queue Options tab. From this, you can:
   * Add banner pages at the beginning and/or end of a job — This is good practice for a printer shared by many people. The banner page helps you sort gets which ID of print job, the title of the file, the user who requested the print job, and any billing information associated with it.
   * Change the image area by setting all four sides — The default is 36 points (one inch) on all margins. You can adjust any of the four margins.
   * Add or remove filter options. These options define attributes of the selected printer. Click the Add button to see queue options you can add. Options are stored in the /etc/cups/options file for each printer. The options you might want to include dpi (print text documents 10, 12, or 17 characters per inch) or lpi (print text documents 6 or 8 lines per inch). For descriptions of other options check out the CUPS Internet Protocol (/usr/share/doc/cups-*/ipp.html).
3. Click Driver Options sets defaults for options related to the printer driver. You can override many of these options when you print a document. Here are a few of the options you might want to set:
   * Media Source — For multiplay printers, you can select which to use by default.
   * Page Size — The default is U.S. letter size, but you can also ask the printer to print legal size, envelopes, or ISO A4 and A3 standard pages.