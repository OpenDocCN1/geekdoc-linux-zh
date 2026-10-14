> > **Note**
> >
> > You might want to consult the manufacturer as to which printer language your model understands or with which model listed in the printer database your printer is hardware-compatible. The printers must be able to understand the same printer language in terms of hardware, without using additional emulation software.

If you want to use a Ghostscript driver that is not listed, you might find it listed under the manufacturer.

Specific parameters can often be set for each Ghostscript driver. The correlation between a selected value and its options can be seen in the structure of the selection menu itself — in the menu items and their respective subitems.

Not all combinations of driver settings work for every printer model — particularly if a high resolution is selected. Print the YaST2 test page to make sure your settings work. If the test print produces undesired results (e.g., a lot of blank pages with just some characters on them), the print job can be immediately stopped at the printer by taking out all the paper, then clicking the ‘Stop’ button. However, some printers will not print again later if you do that. Therefore, it is better to just click the ‘Stop’ button and wait for the printing to stop.

# Hardware-Dependent Settings

Although all the available options should produce the desired printout, you should still check the settings by printing out a test page.

+   - The page layout can only be specified for ASCII text printouts, not for graphics or documents produced by specific applications.
+   - An ascii queue can be configured for special cases. In ascii queues, the print filter is forced to output ASCII text. This is needed, for instance, when ASCII text files are not recognized as such by the print filter for whatever reason.
+   - Country-specific encoding relates to the display of special characters in ASCII text printouts and simple text output from Netscape HTML pages.