# Configuring the BRU Backup System for Backups and Restores

You can download a free copy of Enhanced Software Technologies' BRU 2000 PE by browsing to http://www.estinc.com. This is a complete personal edition of a commercial software backup application you can use to back up your system or files using nearly any tape drive, removable hard drive, and even floppies. This section shows you how to configure BRU 2000 PE and highlight selected features of this software, which provides data verification, error detection, data compression, and selective backup and restores.

> The BRU 2000 PE software included with this book's CD-ROM is exactly the same as the commercial version of BRU 2000 but does not support the same features (such as network backups). The personal edition is quite adequate for backup operations on a desktop OpenLinux system.

FIGURE 23.1
The BRU 2000 backup and restore utility features menus and buttons to manage Linux system backups.

![](bbox=[0.28, 0.52, 0.72, 0.78])

Install the BRU software by using the lisa, rpm, glint or kpackage programs (see Hour 22, "Handling Files and Your File System"). The software is installed into the /bru directory in your file system.

You can use the BRU software from the command line or during an X11 session. Using BRU with X is a lot easier, but you can perform backup operations from the command line of a console. BRU has more than 50 command-line options you can use to specify for your backup process. To use BRU at the command line, type `bru [options]`. To start the X interface, type `xbru` in an xterm window. See BRU's man page for details.