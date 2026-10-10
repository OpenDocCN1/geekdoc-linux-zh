# Table 8-3 Isolating NDPS printer problems (continued)

| Condition | Possible Problem | Action |
| --- | --- | --- |
| Printer offline | The printer is out of paper or turned off. | Make sure the print device is on, and check for any error messages on the print device panel. |
|  | The printer cable is defective or disconnected. | Check the printer cable to make sure it's securely attached to the print device and interface. If the printer still shows offline status, test and replace the printer cable. |
| Printer status is grayed out | Print Manager is not loaded. | Load the Print Manager on the server console. |
|  | The wrong Print Manager is loaded. | If you have multiple Print Managers in your tree, verify that the correct Print Manager for the printer is loaded. If necessary, unload the incorrect Print Manager and load the correct one. |
|  | The new printer agent encountered an error when first loading. | If a print device or interface is not attached to the network, the printer is turned off, or the remote printer software has not yet been loaded on a Windows 95/98 computer, you'll see an error message when creating the printer agent and the status will be grayed out in the Printer Control dialog box. Close the Printer Control dialog box, and then reopen it to view the printer status. |
| Jobs print but remain in the job list | User or operator hold is on. | Click the Configuration button in the Printer Control dialog box, and then modify the Job Hold settings of any job configurations listed in the Printer Configurations dialog box. |
| Jobs removed from the job list but not printed | Incorrect driver language | Verify that the correct printer driver is configured for the printer agent. Incorrect drivers can cause the printer to disregard print jobs. |
|  | Cable problem | Faulty printer cables or broken wires can prevent data from reaching the print device. Test and replace the printer cable. |
| Jobs not displayed in the job list | Computer printer configuration problem | Check the printer configuration on the computer to make sure it's using the correct driver and is printing to the correct printer agent or print queue. |
|  | Users do not have rights to print to the printer. | Verify that the printer agent is in the same container as the users who are printing. Verify that users who are not in the same container as the printer agent have been added to the access control list. |