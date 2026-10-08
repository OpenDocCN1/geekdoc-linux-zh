![](bbox=[0.19, 0.06, 0.89, 0.48])

+   3. When the command prompt loads, run the following command to create a backup of your entire Windows 8 install:

`wbadmin start backup -allCritical -backupTarget:d:`

Replace d: with the drive letter where you want your backup to be stored. It can be the drive letter of any drive in your PC or connected via USB, but cannot be the drive that you are backing up.

You can also replace d: with a UNC network path. For example:
`wbadmin start backup -allCritical -backupTarget:\servername\sharename`. 4. If the command was entered properly, you receive a confirmation screen asking you if you want to start the backup operation, as shown in Figure 4-4. Type Y and your backup will begin.

When finished, store your backup data in a safe place.