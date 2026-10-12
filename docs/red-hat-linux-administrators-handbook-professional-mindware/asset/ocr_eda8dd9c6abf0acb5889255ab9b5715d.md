+   6.  Test the printer. From the Red Hat Linux Print System Manager screen, select the newly created printer and then click the Tests menu and select a test option to test your printer. If you get output on the printer, your configuration is working. However, if your output is pretty much garbage, go back to the Input Filter configuration dialog box and make changes to get better or appropriate output.

If you successfully test-printed in the last step, you are done with the printer configuration and can use the printer from your Linux applications. For example, to use the printer to print a text file from the command line, use the lpr command as follows:

```
lpr -Pprintername /path/to/file
```

If the printer name is lp and you want to print your /etc/samba/smb.conf file, use the following command:

```
lpr -Plp /etc/samba/smb.conf
```

Use the lpq command to see the print queue, and use the lp rm command to remove print jobs from the queue. Note that when the file being printed is transferred to the Windows print spooler, its status is no longer available to you.

# Sharing a Linux printer with Windows

To share a Linux printer with Windows, modify your /etc/samba/smb.conf file as follows:

+   1. In the [global] configuration section, set the following:

```
printcap name = /etc/printcap
load printers = yes
```

+   2. In your [printers] configuration section, set the following:

```
comments = All Printers
path = /var/spool/lpd
writable = no
printable = yes
browsable = no
guest ok = no
```