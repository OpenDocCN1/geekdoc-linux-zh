# Chapter 6 • Configuring the X Window System, Localization, and Printing

You can add, delete, or modify printer queues using the CUPS Web control system. To add a printer, follow these steps:

+   1. From the Administration tab, click Add Printer.

> NOTE CUPS is likely to ask for a username and password at this point. Type root as the username and your root password as the password. The need to pass your root password unencrypted is one reason you should be cautious about configuring printers from a remote computer.

+   2. The system displays a page that shows options for printers to add in each of three categories: local printers, discovered network printers, and other network printers. One or more of these categories may be empty. If you're trying to add a local printer and the local printers category is empty, it is either auto-detected or CUPS can't detect any printer interface hardware. Check your cables and drivers, and then restart CUPS and reload its Web page. If you see an option for the printer you want to add, select it and continue.

+   3. If you entered a network printer, the result is a page in which you enter the path to the device. Type the path, such as `lp://printer/brother` to print to the brother queue on the printerserver. Click Continue when you're done.

+   4. CUPS displays a page in which you enter the printer's name, description, and location. You will use the name to specify the printer in both command-line and GUI tools, so a short-one name is best. The description and location fields are descriptive expansions to help users identify the printer. You can also click the Share This Printer check box if you want to share the printer definition with other CUPS-computers on the network.

+   5. You'll see a list of manufacturers. Select one, and click Continue. Alternatively, you can point directly to a PPD file if you have one. If you do this, you'll skip the next step.

+   6. CUPS now displays a complete list of printer models in the class you selected in 5. Select an appropriate model, and click Add Printer. Alternatively, you can provide a PPD file if you have one.

+   7. You should now see a page on which you can set default options, such as the paper size and resolution. The details of what options are available on the printer model you selected. Change any options and click Set Default Options. Your printer is now defined.

If you click the Printers item at the top of the page, you should be returned to the printers list among the printing queues. You can print a test page by clicking the link to the printer and then Selecting Test Page from the button selector that reads Maintenance by default. If all goes well, a test page will emerge from your printer. If it doesn't, go back and review your configuration by selecting Modify Printer from the button selector that reads Administration by default. This action