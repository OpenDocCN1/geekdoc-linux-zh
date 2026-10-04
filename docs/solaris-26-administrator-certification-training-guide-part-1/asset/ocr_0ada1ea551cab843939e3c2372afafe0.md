> NOTE. One printer can be identified as the default printer for the system. If a user does not specify a specific printer when printing, the job will go to the default printer.

Figure 9-5
The Add Local Printer Window.

![](bbox=[0.28, 0.23, 0.68, 0.77])

User Access List—If you wish, enter the names of the systems allowed to print to this printer. If none are entered, all clients are allowed access.

9. After filling in all of the fields, click on the OK button. The window closes and the new printer name appears in the Printer window shown in Figure 9-2.

# Using a Printer Not Listed in the Printer Types Menu

Printer types listed in the Print Manager Window correspond to printers listed in the /usr/share/lib/terminfo directory. If a printer type is not available for the type of printer you are adding, you might need to add an entry in the /usr/share/lib/terminfo database. Each printer is identified in the terminfo database by a short name; for example, an HP LaserJet printer is listed under the /usr/share/lib/terminfo/h directory as hplaserjet. The entries for PostScript printers are in /usr/share/lib/terminfo/P. The name found in the directory is the printer type you specify when setting up a printer.