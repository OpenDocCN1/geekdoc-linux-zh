
# Part III: Ubuntu for System Administrators

FIGURE 33-4

The CUPS server's Web interface

![](img/1a233c34336fbf5a85d6eb785e401709_1139_0.png)

You should be able to go to any of the other hosts on your network and create printer entries there. Adding a printer on an Ubuntu system is discussed in Chapter 20.

## Troubleshooting Remote Printing

This section summarizes a few common sources of diagnostic information and potential problems that you may need to try, depending on the version of CUPS that you are running and whether or not you have typed every URI correctly.

## Checking CUPS Log Files

CUPS servers maintain three log files that provide a variety of information about attempts to access or use them. These log files, stored in the directory `/var/log/cups`, are as follows:

- access_log: Contains log messages for each remote host that attempts to access the CUPS print server.
- error_log: Contains log messages that record any errors encountered or produced by the CUPS print server.
- page_log: Contains log messages for every page printed by the CUPS server. These log messages also summarize information about the host from which the print job was received and so on.

Of these, the access_log and error_log files are the most useful for diagnostic purposes. Examining the end of these files after encountering a print failure shows meaningful messages. The access_log file will identify the IP address of the systems that connected to your print server. Once you've established this, check the error_log file for tips about why your job may not have printed.

## Accessing Portions of CUPS Web Interface

The default configuration on Ubuntu systems tends to change with different releases, reflecting both enhancements and security concerns. It's almost certain that the CUPS print server will be updated at some point while you are using subsequent releases of Ubuntu. If you need to add your remote hosts (or your entire network) to the list of acceptable locations in the CUPS daemon's primary configuration file `/etc/cups/cupsd.conf`, the list of valid locations for print jobs is stored inside `<Location>` entries. If printing suddenly stops, make sure that this stanza contains an entry that either by default or explicitly allows access from all hosts on the local network. For example, the following is a restrictive version of this stanza that denies access from anywhere other than localhost or any hosts on `192.168.6.*` subnet:

```
<Location />
Order Deny,Allow
Deny From All
Allow From localhost
Allow From 192.168.6.*
```

The configuration file provided as part of a standard Ubuntu installation at the time of writing allows access from anywhere (once you've changed CUPS to actually listen on your printer server's external interface, as described earlier). However, changes to the default configuration file are common, and it's depressing to have printing cease to function after an update. Similarly, most administrative functions on modern CUPS servers require that you contact them using a URI that begins with https. You can disable this by commenting out the lines in cupsd.conf that contain the word Encryption or use SSL. When using SSL, you may need to create an exception because this is a self-signed certificate that is not guaranteed by any recognized authority. You will also have to do this on every system that you want to use with the CUPS server's Web-based interface. Your browser will walk you through the steps to create an exception for your printer's certificate.

## Handling Print Jobs

Another common update-related problem may arise if you receive an update that changes how CUPS handles types of incoming print jobs. If you are printing from a remote system, such as a Windows or Mac OS system, system performs print jobs before sending them to the printer. If printing suddenly stops after an update and you see error messages in the error_log file about raw input, make sure that the following entry is in the file `/etc/cups/mine` and is not preceded by a hash mark (#):

```
application/octet-stream
```

After making any changes to any CUPS configuration file, you need to restart the CUPS daemon on your system using the following command:

```bash
sudo /etc/init.d/cups restart
```

## Getting Information About CUPS

As you have probably guessed, CUPS configuration is either extremely rich and powerful or extremely irritating—and usually both. The CUPS configuration file `/etc/cups/cupsd.conf` has so many possible options that makes even the command-line gcc and tar commands jealous. If you try to do anything with CUPS beyond the simple print server described in this chapter, you will get more information. The following are some excellent sources of additional information about CUPS:

- www.cups.org/documentation.php: The online documentation for CUPS that is available from Easy Software, Inc.
- www.linuxprinting.org: Specializing in help with printing on GNU/Linux systems, this site features a very useful database of printers to work with Linux (www.linuxprinting.org/printer_list.cgi) and a good deal of useful information about CUPS, including a great CUPS troubleshooting tutorial. (I left out URL for the latter intentionally because it would line-wrap into the next chapter.)
- CUPS: Common UNIX Printing System by Michael R. Sweet (AMS, 2002; ISBN: 0672321963): Michael Sweet is one of the owners of Easy Software, Inc., and thus, it is a pretty definitive book, not for CUPS, but also for the Internet printing protocol. Unfortunately, the book is a bit old now, but it is still an excellent resource, and my copy is a valuable asset.

## Summary

Centralizing print services on one or a small number of computer systems is a good idea for almost any network. This chapter provided a bit of background about printing on UNIX and Linux systems, and then discussed how to install and configure CUPS, the Common UNIX Printing System. Most modern personal computer systems, including Microsoft Windows or Mac X systems that you may still have lying around, can easily print to a CUPS server that is running on your system.

The next chapter explains how to share directories over a network using NFS, the Network File System, which is the standard distributed filesystem mechanism for all UNIX and Linux systems. Sharing a central repository of project files, documents, and code over a network in a work environment is important from many standpoints, including increasing efficiency, minimizing confusion, and minimizing the size of your backups. Today, it is just as important in many home environments, enabling everyone on your home network to share access to your household's music collection, vacation photos, and any other files that you want your housemates, spouse, or children to be able to see.
