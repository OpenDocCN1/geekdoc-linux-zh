# # Performing Backups with BRU-2000

OpenLinux users who purchase the commercial version of COL 2.2 will find that the CD-ROM includes a copy of Enhanced Software Technologies' BRU PE include on the CD-ROM. In fact, if you did the recommended install from either Lisa or Lizard, then it is already installed. BRU-PE is a personal edition of the more robust BRU-2000 commercial edition. Though only a personal edition, it is still a fairly advanced backup and restore utility. In fact, it supports

+   - Command line or graphical interface for KDE
+   - Error detection during backup
+   - Data integrity verification
+   - Backup and restore of live file systems
+   - On-line help
+   - Automatic recognition of compressed files
+   - Background mode for scheduled backups

The BRU software is actually two programs, the standard BRU for performing backups from the console and the GUI program xbru for use under KDE. BRU-PE uses several files and directories on your Linux system. Much of the graphical interface support is found under `/opt/xbru`, and the configuration file `/etc/brutab` is used to configure various backup devices.

As mentioned earlier, if you did the recommended install with either Lisa or Lizard, BRU-PE is already installed. If not, you will have to install it manually. To do so, mount your COL 2.2 CD. Then, as `root` go to the `/OpenLinux/install/RPMS` directory on the CD and issue the following command:

```
``` 
rpm -ivh BRU+.rpm 
```
```

To do full or incremental backups of your system, you must be logged in as user `root`. To use the graphical interface version, you can start the program in many ways. You can initiate it by choosing the K menu, Utilities, BRU-PE backup utility, or you can press Alt+F2 and then type `xbru` in the command-line box that appears. At this point the dialog box seen in Figure 23.1 should appear.