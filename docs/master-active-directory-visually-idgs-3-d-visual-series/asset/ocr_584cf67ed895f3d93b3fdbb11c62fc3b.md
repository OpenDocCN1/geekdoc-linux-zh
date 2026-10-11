# BACKING UP THE ACTIVE DIRECTORY

As with any data on your computer, a good backup plan is extremely wise. The Active Directory is no exception, and you should plan a regular backup plan to ensure that you can recover your Active Directory database in case of a system error.

In general, Microsoft recommends that you store your Windows 2000 system files and the Active Directory database and transaction log files on separate disks. If one disk should fail, at least you have not lost all your data at one time. You should also plan to back up the data on a regular basis so that it can be restored if necessary.

To back up the Active Directory database and transaction log files, you use the Backup utility included in Windows 2000. When you use the Backup Wizard to back up your Active Directory, choose to back up “System State Data.”

![](bbox=[0.04, 0.5, 0.48, 0.82])

+   1.  Choose **Start** \> **Programs** \> **Accessories** \> **System Tools** \> **Backup**.

![](bbox=[0.5, 0.5, 0.96, 0.82])

+   2.  Click **Backup Wizard**.