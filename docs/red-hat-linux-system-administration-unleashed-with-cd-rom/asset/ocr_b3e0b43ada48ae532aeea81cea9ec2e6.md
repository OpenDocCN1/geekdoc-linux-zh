# Caution

Linux and Windows use a different end-of-line sequence in text files. When editing a file through Samba, the text file protocol is determined by the OS of the client. This means that if the same file is edited by clients of both operating systems, corruption can result.

The final entry sets the default file permissions for any files created in the shared directory.

# The [printers] Section

There are two ways in which Samba can make printers available to the network. One method is to create a specific share section for each printer in printcap that you want to share. The other method is to use the [printers] special section in order to share all of the printers defined in the /etc/printcap file.

# Note

This section mentions /etc/printcap, printcap, and printcap printers several times. /etc/printcap is a file defining all the Linux system's printers. A printcap printer is a printer defined by name in /etc/printcap.

It is possible to create /etc/printcap entries with a text editor, but on your Red Hat Linux system, the preferred method is to use printtool. The printtool creates both local and remote printers through an easy-to-use graphical interface.

The following is a sample [printers] special section. It shares all of the printers defined in the printcap file and permits anyone to print except the guest account.

```
[printers]
comment = All Printers
browseable = no
create mode = 0700
path = /var/spool/samba
printable = yes
public = no
writable = no
```

The [printers] section defines how printing services are uncontrolled if no specific entries are found in the smb.conf file. As with the [homes] section, if no specific entry is found for