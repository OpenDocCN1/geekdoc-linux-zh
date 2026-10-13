
Part of the system outside the share is followed. This is combined with the follow symlinks option (default is Yes), which permits or denies the use of symlinks to files. The wide symlinks option, when set to No, prevents users from following a symlink if it changes directory to outside the share. But setting the follow symlinks option to Yes enables a user to read a file anywhere on the system. The difference is subtle and often confusing, especially because the two are implemented separately. Note that setting follow symlinks to no slows down filename lookups.

The other parameters that are of interest are the four exec options. These options execute programs as the user logs in or out, whether as the user or as root. Consideration needs to be given regarding the security risk or necessity of running a program either as the user or as root. For example, the mount (and umount) command might need to be run as root unless you have an entry in the /etc/fstab file for that mount, permitting the user to perform the action.

## HOMES SHARE

The Homes share is a special share. When it is implemented, each user accessing the Samba box has his username compared to /etc/passwd for his home directory. That user’s Linux home directory is made available as a share, but other users’ home directories do not appear. This can provide users with a directory that is “safe” from the prying eyes of other Samba users. It might be prudent to give users a subdirectory to use to avoid naming convention problems between Linux and Microsoft clients. This is one share that does not default to /tmp; rather, it automatically defaults to the user’s home directory.

## SHARING PRINTERS ACROSS THE NETWORK

Printing within Linux tends to be one of the most difficult things for novice users to set up—and it is extremely difficult to understand. This text assumes that you can set up and print files from your Linux host. If printing from Linux cannot be accomplished, Samba does not help because it adds yet another layer of complexity. However, when you can print from Linux, printing from Samba is simpler.

To begin, printers can be connected in one of three ways for use on the network.

- They can be connected directly to a port on the Linux host, in which case they use the Linux print daemon and print spool.
- They can be connected directly to a Microsoft host, and that host can share the printer on the network, in which case the Microsoft host is spooling jobs for the printer.
- The third way of connecting has two variations. The printer is connected to the network through a print spooler. This can be an HP JetDirect card, an IBM print spooler, or another print spooler. The key is that the printer itself is identified as a host with its own IP address (and possibly a DNS entry). This third way is considered to work as one of the two preceding options: Either a Microsoft host has this printer set up as part of its print spooler, or the Linux host acts as the print spooler. So you are back to treating printers as though they are spooled by Linux or by a Microsoft host.

From a UNIX (Linux) perspective, the server that acts as the print server owns printers. This print server is in charge of formatting documents for the specific printer. The print server receives the document to print as either ASCII text or generic PostScript, formats it for the specific printer using its filter, and prints the document. Alternatively, it can receive a document that is formatted by the client for the printer and, by use of the `-b` binary switch, the server can pass the document untouched to the printer.

Enter Microsoft print spoolers. Despite the widespread use of the server to format the document for the specific printer to which it was spooling, Microsoft required clients to always know to which printer they were printing, and to have the spooler act like a UNIX print spooler that was always invoked with the `-b` switch. Although this reduced the load on the print spooler, it added complexity by forcing clients to know specifically about every printer on the network to which they might be printing. In an effort to reduce administrative burdens, Microsoft print spoolers that are shared on the network can communicate to other Microsoft hosts (but not to UNIX hosts) what kind of printer driver is needed when the client connects for the first time. In version 2.0.x, Samba also permits this kind of communication (see the section “Printing Options”).

To print using Samba shares on a Linux box, you can choose one of two avenues. You can set up each client that is to connect to a printer on a Samba share to print natively to the printer (using a specific Microsoft driver for the printer), or you can set up all clients to use a generic Passthrough PostScript driver and allow them to print to any Samba client and any printer identically, regardless of the printer type.

## The Printers Share

The Printers share is a special share that is similar to the Homes share. This share needs to be created on the Printers page and can only be removed on the Printers page. After it is created, the Printers share only appears on the Printers page.

The Printers share is created by default with path = `/tmp` and print ok = Yes. If the global default for load printers has not been changed from Yes to No, after the Printers share is created, all printers in `/etc/printcap` show up in the list of print shares. They can be identified by the \* in front of the share name. If you delete the Printers share or turn off the Global load printers option, these printer shares no longer appear. The printer shares that are identified with \* cannot be deleted from Samba—they can just be made not to appear.

If changes are made to the Printers page, the changes are global for all the printers that are marked with an asterisk. If you choose one of the printcap printers (ones with an asterisk) and make a configuration change that applies to that printer only, a new section under Printers is created with the name of that printer (without the asterisk) in the `smb.conf` file. That printer now also appears in the Printers list in swat without the asterisk. You’ll notice that in the View page this printer now has its own entry. If that share is subsequently deleted, it reverts to showing up with an asterisk and has the Printers defaults. If the Printers share is deleted, this print share without the asterisk remains. In other words, when it is created as a share by itself, it behaves as if it were created from the swat Printers page. Otherwise, it has an asterisk and is only an appendage to the special Printers share.

**Tip**  
When setting up printers, the most common printing problem is that the spool directory does not have the proper permissions. These directories are world writable with the sticky bit set—that is, chmod 1777 spool.

Going through the functional areas that are available under printing, you’ll see a few differences from the Shares functional areas. Again, some of these options are only available from the swat Advanced View page.

### BASE OPTIONS

These options are no different from the Base Options in Shares: a comment field for identification and a path for the spool directory.

### SECURITY OPTIONS

Only four options are available, but they are important. The first, guest account, is only of interest if Guest OK is set to Yes. The default guest account is nobody, and this account can be so restricted that printing isn’t possible. You might want to change this to the account FTP or to another account set up for the purpose of printing.

**Tip**  
Make sure that your guest account has enough privileges to print before looking elsewhere.

### LOGGING OPTIONS

Read the entry under Shares called Logging Options. You’ll find this in swat in the Shares section, Advanced View, between the Security Options and Tuning Options.

### TUNING OPTIONS

The only option here, `min print space`, defaults to 0, meaning that a user can always print. But this might become a problem on a system with low disk space and large print jobs.

### PRINTING OPTIONS

This section is specific to printers. The first option, `print ok`, must be Yes for all print shares. Many of the other options are for commands. These depend on your system. Linux uses LPRng, so the commands for LPRng need to be used, although the defaults in swat work.

The last two options are probably of interest to those with extensive Microsoft hosts on their network. The printer driver must be the name that the Microsoft hosts are expecting. If you don’t know, don’t fill it in—let one of the Microsoft machines provide you with a list, and you can copy the printer driver from that list. It must be an exact match, including case. The next option, printer driver location, must be a share that you set up called PRINTER$, where the printer drivers (copied from a Microsoft host or from the Microsoft CD-ROM) are located.
