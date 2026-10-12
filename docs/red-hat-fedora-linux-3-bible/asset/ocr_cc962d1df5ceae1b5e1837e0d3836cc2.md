# ## Editing a local printer

After you have created a printer queue, you can edit the printer queue definitions to change how the printer behaves. From the Printer configuration window, do the following:

+   1. **Edit** — With your printer selected, click **Edit**. The Edit a Print Queue page appears. The following steps describe how to change options besides those you added originally.
+   2. **Queue options** — Click the **Queue options** tab. From this tab, you can:
+      - Add banner pages at the beginning and/or end of a job. This is good practice for a printer that is shared by many people. The banner page helps you sort who gets which print job. The standard banner page shows the ID of the print job, the title of the file, the user that requested the print job, and any billing information associated with it.
+      - Change the imageable area by setting all four side margins. The default is 36 points (one inch) on all four margins. You can adjust any of the four margins.
+      - Add or remove filter options. These options define attributes of printing to the selected printer. Click the **Add button** to see queue options you can add. Options are stored in the /etc/cups/ippoptions file for each printer. Options that you might want to change include cpi (print text documents 10, 12, or 17 characters per inch) or lpi (print text documents 6 or 8 lines per inch). For descriptions of other options, look at the CUPS Internet Printing Protocol page ( /usr/share/doc/cups-* /ipp.html ).
+   3. **Driver options** — Click **Driver options** to set defaults for options related to the printer driver. Many of these options can be overridden when someone prints a document. Here are a few of the options you might want to set:
+      - **Media Source** — For multiray printers, you can select which tray to use by default.
+      - **Page Size** The default is U.S. letter size, but you can also ask the printer to print legal size, envelopes, or ISO A4 standard pages.
+      - **Resolution** — Select the default printing resolution (such as 300, 600, or 1,200 dots per inch). Higher resolutions result in better quality, but take longer to print.
+      - **Printing Mode** — Choose to print in grayscale or color.

Click **OK** when you are satisfied with the changes you made to the local printer.

# ## Configuring remote printers

To use a printer that is available on your network, you must identify that printer to your Fedora Linux system. Supported remote printer connections include Networked CUPS (IPP) printers, Networked UNIX (LPD) printers, Networked Windows (SMB) printers, NetWare printers and JetDirect printers. (Of course, both CUPS and UNIX print servers can be run from Linux systems, as well as other UNIX systems.)

In each case, you need a network connection from your Fedora Linux system that enables you to reach the servers to which those printers are connected. To use a remote printer, of course,