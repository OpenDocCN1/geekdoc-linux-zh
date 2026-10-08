These steps describe how to configure an Epson Stylus printer because it's a good, inexpensive inkjet printer. The configuration utility can configure many different types of printers, so select the model that's appropriate for you:

+   1. **Log in to your Red Hat Linux print server.**
2. **Click the GNOME Menu button, choose System Settings: Printing, and enter the root password if you're prompted to do so.** Click the **New** button and the Add a New Print Queue window opens.
3. **Click the Forward button and you're prompted to enter a queue name and an optional description.**
   Figure 16-4 shows the Add a New Print Queue window.
   Enter in the **Name** text box the name you want to refer to the printer (the default is *printer*). You can enter any name you want for the queue name. For example, *Epson777* clearly indicates that you're accessing an Epson Stylus 777 printer.
4. **Click the Forward button and the Queue Type dialog box opens.**
   Linux should detect the printer attached to either the USB or parallel port.
   You can configure the printer as a nonlocal device if you have a network printer. For example, if you have a high-end HP LaserJet with a JetDirect interface, select **Networked Jet-Direct** rather than **Locally-Connected**.
   Linux parallel (printer) ports correspond to Windows printer ports. Linux `lp0` is equivalent to `LPT1` and `/dev/lp1` is equivalent to `LPT2`.
5. **Click the local printer device (typically, it should be listed as `/dev/lp0` or `/dev/lp1`) and click the Forward button.**
   The Printer model window pops up.
6. **Click the pull-down menu and select your printer's manufacturer. For example, select *Epson*. The manufacturer's model list appears. Scroll down the model list and select your printer model.**
   Some printers come with more than one driver. Select the driver that best suits your printer. Use trial-and-error if you don't know which driver is best.
7. **Click the Forward button.**
8. **Click the Finish button in the new window and the Question dialog box opens. Click the Yes button and you return to the Printer Configuration window.**
9. **Click the Apply button and the Linux print daemon, `lpd`, restarts and makes the new configuration active.**

![](bbox=[0.13, 0.45, 0.2, 0.53])