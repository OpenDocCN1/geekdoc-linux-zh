# 21.17 Printing from CUPS to Windows-Attached Printers

From time to time the question arises, how can you print to a Windows-attached printer from Samba? Normally the local connection from Windows host to printer would be done by USB or parallel cable, but this does not matter to Samba. From here only an SMB connection needs to be opened to the Windows host. Of course, this printer must be shared first. As you have learned by now, CUPS uses backends to talk to printers and other servers.

To talk to Windows shared printers, you need to use the smb (surprise, surprise!) backend. Check if this is in the CUPS backend directory. This usually resides in /usr/lib/cups/backend/. You need to find an smb file there. It should be a symlink to smbpool, and the file must exist and be executable:

```
```
root# ls -l /usr/lib/cups/backend/
total 253
drwxr-xr-x 3 root root 720 Apr 30 19:04 .
drwxr-xr-x 6 root root 125 Dec 19 17:13 ..
-rwxr-xr-x 1 root root 10692 Feb 16 21:29 canon
-rwxr-xr-x 1 root root 10692 Feb 16 21:29 epson
lrwxrwxrwx 1 root root 3 Apr 17 22:50 http -> ipp
-rw-r--r-x 1 root root 17316 Apr 17 22:50 ipp
-rwxr-xr-x 1 root root 15420 Apr 20 17:01 lpd
-rw-r--r-x 1 root root 8656 Apr 20 17:01 parallel
-rwxr-xr-x 1 root root 2162 Mar 31 23:15 pdflatcler
lrwxrwxrwx 1 root root 25 Apr 30 19:04 ptal -> /usr/sbin/ptal-cups
-rwxr-xr-x 1 root root 6284 Apr 20 17:01 scsi
lrwxrwxrwx 1 root root 17 Apr 2 03:11 smb -> /usr/bin/smbpool
-rwxr-xr-x 1 root root 7912 Apr 20 17:01 socket
-rwxr-xr-x 1 root root 9012 Apr 20 17:01 usb
```
```

```
```
root# ls -l `which smbpool`
-rwxr-xr-x 1 root root 563245 Dec 28 14:49 /usr/bin/smbpool
```
```

If this symlink does not exist, create it:

```
```root# ln -s `which smbpool` /usr/lib/cups/backend/smb```
```

smbpool was written by Mike Sweet from the CUPS folks. It is included and ships with Samba. It may also be used with print subsystems other than CUPS, to spool jobs to Windows printer shares. To set up printer winprinter on CUPS, you need to have a driver for it. Essentially this means to convert the print data on the CUPS/Samba host to a format that the printer can digest (the Windows host is unable to convert any files you may send). This also means you should be able to print to the printer if it were hooked directly at your Samba/CUPS host. For troubleshooting purposes, this is what you should do to determine if that part of the process chain is in order. Then proceed to fix the network