# ### Special Comments for Network Printers

If you’re trying to configure FreeBSD to use a network printer, you won’t be able to perform a raw printer test. You should verify that your network is functioning, though, as described in Chapter 14. If possible, you should also verify that you can print from the print server computer itself and from another network print client computer. If this is the first network print client you set up and you encounter problems, you may have to debug both the client and the server systems. The upcoming section, “Controlling Remote Printer Access,” covers configuring a system as a print server.

# ### Creating a Spool Directory

FreeBSD needs to be able to store print jobs somewhere, so the first step in building a print queue is to create an appropriate directory for this purpose. This directory is often called a spool directory, and it’s traditionally located in /var/spool/lpd. The spool directory is normally owned by the user daemon and the group daemon, and has permissions that allow only daemon to read from or write to it. (The daemon user and group is used by some FreeBSD servers. FreeBSD gives this user and group access to certain directories and files so the servers can run with non-root privileges.)

You can achieve these effects with commands like this:

```
# mkdir /var/spool/lpd/hp4000
# chown daemon:daemon /var/spool/lpd/hp4000
# chmod 770 /var/spool/lpd/hp4000
```

These commands create a spool directory called hp4000. It’s usually best to create spool directories that are easy to associate with the name you intend to use for the print queue. Using the same name works well in most cases, so this spool directory will be used by a queue called hp4000.

# ### The /etc/printcap File Format

The trickiest aspect of FreeBSD printer configuration is setting up Ghostscript and a smart driver, as described in the upcoming section, “Setting Up Ghostscript.” The second-trickiest aspect is configuring the /etc/printcap file. This file’s name is short for printer capabilities, and it tells the lpd program how to process files for a given printer—what filters to use, whether to print separator pages between print jobs, which port or network server to use, and so on. Some programs also refer to this file to obtain a list of available printers.

> The BSD LPD and LPng systems both use /etc/printcap with basically the same format. CUPS doesn’t use printcap, but because some programs rely on its contents, systems that use CUPS often implement a stripped-down printcap file for their benefit.