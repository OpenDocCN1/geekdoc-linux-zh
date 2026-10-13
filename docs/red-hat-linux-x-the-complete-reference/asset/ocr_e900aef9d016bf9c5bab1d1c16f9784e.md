```
[homes]
comment = Home Directories
browseable = no
writeable = yes
valid users = %S
create mode = yes
directory mode = 775
```

# Printer Section

The Printers section specifies the default controls for accessing printers. These are used for printers for which no specific sections exist. In this case, Samba uses printers defined in the server's printcap file.

In this context, setting browseable to no simply hides the Printers section from the client, not the printers. The path entry specifies the location of the spool directory Samba will use for printer files. To enable printing at all, the Printable entry must be set to yes. To allow guest users to print, set the guest ok entry to Yes. The writeable entry set to no prevents any kind of write access, other than the printer's management of spool files. On SWAT, select the PRINTER page and the Printers entry in the drop-down menu, and then select Choose Printers. A standard implementation of the Printers section is shown here:

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = yes
writeable = no
printable = yes
```

If you can't print, be sure to check the Default Print entry. This specifies the command the server actually uses to print documents.

# Shares

Sections for specific shared resources, such as directories on your system, are usually placed after the Homes and Printers sections. For a section defining a shared directory, enter a label for the system. Then, on separate lines, enter options for its pathname and the different permissions you want to set. In the path = option, specify the full pathname for the directory. The comment = option holds the label to be given the share. You can make a directory writable, public, or read-only. You can control access to the directory with the Valid Users entry. With this entry, you can list those users permitted access. For those options not set, the defaults entered in the Global, Homes, and Printers segments are used.

On SWAT, you use the SHARES page to create and edit shared directories. Select the one you want to edit from the drop-down menu and click Choose Share. The Basic View shows the commonly used entries. For entries such as Valid Users, you need to select the Advanced View. Be sure to click Commit Changes before you move on to another Share or Printer section (see Figure 37-5).