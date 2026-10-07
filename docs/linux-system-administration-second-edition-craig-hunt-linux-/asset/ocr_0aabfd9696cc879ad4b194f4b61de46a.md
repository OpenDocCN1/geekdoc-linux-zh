+   3. Click the printer type you want to define and enter a name for the queue for this printer. The remaining instructions assume you opt for a local printer. The network printer definitions are similar, but ask for information on the print server name rather than a local printer port.

+   4. Click Next in the Set the Print Queue Name and Type dialog box. Printconf displays information about the printer ports it has detected. If there is more than one, you must select the port to associate with the printer to be added. (For network printers, additional information specifying the information for that type of printer will be requested instead.) This port detection doesn't always detect all your ports, particularly if you're using an RS-232 serial or USB printer. You can safely ignore these omissions.

+   5. Click Next in the Configure a Local Printer screen. Printconf displays the Select a Print Driver dialog box Shown in Figure 10.4.

![](bbox=[0.18, 0.24, 0.82, 0.6])

Figure 10.4: The Select Print Driver dialog box lets you select the model of the printer you are installing.

+   6. Select the appropriate driver for the printer you are installing. If the driver does not appear, look in the printer's documentation to see if another type is suggested for use. Although Printconf used to require you to enter a lot of information about your printer configuration, it now uses the default values. To change these values, you must edit the printer by selecting Edit from the main screen shown in Figure 10.2.

+   7. After verifying the information for the queue to be created, click Finish, and Create the New Print Queue dialog box. The queue should appear in the main Printconf window (Figure 10.2).

+   8. Select File → Restart LPD in the Printconf window's menu to restart the line printer daemon.

At this point, the printer should be defined. You can click its name in the Printconf window and select the tests under the Test menu item to test the configuration. The Print ASCII Test Page item prints plain ASCII, but there are several other page types that you can test; select the one that best represents what you intend to print from the new printer. These printouts include tips on fixing minor problems, should they appear on the printouts. If the printout doesn't appear from this item, then you've may have selected the wrong printer device file during printer installation or the drivers may not be loading. (The problem could also be more prosaic, as in a failure to turn on the printer.)