(Chapter 15 covers setting up SAMBA in more detail.) Printing through a Windows machine is as simple as editing your Windows machine so that the printer is shared with other machines on the Network when placing the computer's name in the Printer Entry dialog box as shown in Figure 13.6.

Once again, the name or names of the printer appear in the first field, and the print queue appears just below you. You can choose to limit the size of print jobs so that you do not fill up the available space in the queue or lock up memory on the print server. The two most important features here are the name of the computer to which the printer is attached and the name given to the printer. Adding the IP address of the computer is optional and is needed only for the client. On LANs that share accounts, you can also set up a username and password to send print jobs to any available printer. This helps to curtail large or unauthorized print jobs.

Again, you should fill out the filter correctly to make the right drivers available. After completing these entries, you can return to the Print System Manager.

Depending upon the type of install, you should see a list of available printers. Here much depends upon compatibility. For example, older Okidata printers use the HP Laserjet drivers to run. You may need to know more about the printer than what it stated on the device's case. For the most part, the HP LaserJet drivers apply to most HP LaserJet printers, regardless of the model number. Consult the web page of your printer's manufacturer to find out more about its drivers and connectivity. For the newer printers, such as the HP LaserJet 2100 or 3100 series, the standard HP LaserJet drivers work fine. You may want to test your setup later and verify the accuracy. A couple of other options that the install

![](bbox=[0.19, 0.68, 0.54, 0.92])

FIGURE 13.6
*Editing the fields for a printer connected on a SAMBA, Windows 98, Windows NT* or *Windows 2000 network.*