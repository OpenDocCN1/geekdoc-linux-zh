> NOTE
Using the Custom Device button can be helpful when configuring Red Hat to be a printer attached to your computer's serial port. In this case, the serial port entry may use a device such as /dev/tty0, which corresponds to COM1.

Look through the list manufacturers; then choose a printer model and a driver for your printer. Don't worry if you don't see your model listed; it is possible to use a driver listed under a related printer. For example, nearly all HP printers might be able to use the hpdj or pcl3 drivers.

> NOTE
If you want to learn about a particular print driver, read its manual page. For example, the pcl13 print driver supports printers using PCL 3 imaging has a manual page named gs-pcl13. You can also find manual pages for the bj and dj500 drivers.nYou can also browse to http://www.linuxprinting.org/ to find out drivers to use with your printer or to see a cross-referenced listing of printers supported by each driver. You might also find new and improved drivers for the latest printers on the market.

You might also find multiple drivers listed for your printer; if so, you can experiment which driver performs best. If you select a somewhat-compatible driver, you may not be able to use all the features of your printer, but you will be able to set up printing service. Click Forward when you've made your choice.

The Finish and Create the New Print Queue dialog box shows your printer device and drive type, so you can confirm that the information is correct (see Figure 12.5). If you need to change the options, click Back to previous dialog boxes. To create the new print queue, click Apply.

![](bbox=[0.311, 0.663, 0.703, 0.888])

FIGURE 12.5 Double-check your settings before you commit to creating a new printer entry in /etc/printcap, when the settings are right, click Apply to create the new print queue.