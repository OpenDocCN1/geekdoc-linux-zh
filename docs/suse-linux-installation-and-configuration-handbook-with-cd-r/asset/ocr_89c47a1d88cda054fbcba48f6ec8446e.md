# Allowing Other UNIX/Linux Machines to Use Your Printer

Thanks to the networked architecture of the printing system on Linux, this is a fairly simple process. Any machine can print to your printer if it has the correct permissions to do so.

To configure your system to allow others to print to it over the network, you will need to manually edit your system files. The good news is that you need to edit only one file, /etc/hosts.lpd. This file contains a list of hosts that are allowed to print to your printer.

The format of this file is simple; just add an entry for every host you want to allow to print on your printer. For example, if you want accounting.company.com to print to your printer, just add this line to /etc/hosts.lpd:

```
accounting.company.com
```

That's it, simple isn't it? Do the same for all the machines that you want to print to your printer.

# Allowing Other Microsoft Windows Machines to Use Your Printer

If you want to enable Microsoft Windows machines to print to your printer, you will need to configure this in Samba. For detailed information about setting up your Samba server, please refer to Chapter 15.

To enable others to print to your printer via Samba, you need to define a [printers] section in your /etc/smb.conf file. The [printers] section in Samba is a special section that defines a shared printer to be exported to other Microsoft Windows machines in the network. A typical [printers] section looks like this:

```
[printers]
comment = All Printers
browseable = no
printable = yes
guest ok = no
read only = yes
create mode = 0700
directory = /tmp
```

This section defines a shared printer on your machine. But, it will require a username and password to enable print jobs to be sent to it. This is because of the guest ok = no option. To enable anyone to use the printer without the need for a username and password, use guest ok = yes. Your printer share will now be visible to all other Windows machines on the network.