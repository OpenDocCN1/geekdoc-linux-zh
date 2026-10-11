# Make the Location Yours

You might see the device location for a PDA as /dev/pilot, renamed or linked as that location by mysterious elves in your computer or by you with this command:

```
ln -s /dev/[Your device location] /dev/pilot
```

The setup assistant shows an error if the device location is not correct. You won't be able to get past the wizard until you answer that Final Leopardy question right.

# The Layout

When you are through the gate and into the actual GNOME Pilot interface (see Figure 7.13), there are more options. The layout of the program is a series of tabs with pop-up dialog boxes for more detailed options.

![](bbox=[0.25, 0.38, 0.64, 0.65])

The Pilots tab lists all your currently configured devices in a table. You can add new PDAs with the Add button. In the Pilot Settings dialog box, you are asked for information about the new PDA. You can type in the User Name and ID to use with the PDA or use the Get from Pilot button. Send the identification information back the other direction with Send to Pilot. Pilot Name is just a name to display in the table. In the Local Basedir field (a shorthand way of saying "base directory"), enter the directory location where you will want to keep the backup files from your PDA. If you are not sure, use the default; it is easily changed later. Sync Action is a choice of actions for when you HotSync the device. You can choose to do a full sync, to only move files to the PDA, to only move files to the computer, or to merge data. The most granular control is to choose Use Conduit Settings. With this choice, you can have different actions for different types of data.

Figure 7.13
The GNOME Pilot interface.