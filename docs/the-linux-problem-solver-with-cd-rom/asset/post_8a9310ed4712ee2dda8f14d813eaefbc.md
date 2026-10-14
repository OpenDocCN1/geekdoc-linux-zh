
## Printing

This section details the process of setting up a printer that's already accessible from Unix for a Macintosh to use over the network. To go in the other direction (printing to an AppleTalk printer from Linux), have a look at Section 5.3.

The papd daemon that waits for a print request from a Mac is an odd program; its default behavior assumes certain things about the lpd to which it sends print jobs. This book recommends LPRng as a print daemon. The default configuration files need some changes to allow papd to interact properly with LPRng's lpd.

papd has two configuration files: papd.conf and your system's /etc/printcap file (described in Chapter 5). The papd.conf file has entries such as the following:

```
printername:\n:pr=name_or_command:\n:pd=ppd_filename:\n:op=operator_username:
```

printername is what the printer shows up as on the AppleTalk network; that is, how you see it in the Macintosh Chooser. A PPD file (PostScript Printer Description) specified with ppd_filename helps the Mac's printer driver adapt to the printer. operator_username owns print jobs sent to printername. But the :pr=name_or_command: setting is the one you should pay most attention to when using LPRng's lpd.

Under the defaults (without a :pr=... setting), papd looks through /etc/printcap and tries to find the printer (specified by printername, as in the example above). If papd finds it upon receiving a print job, it looks for the printer's spool directory parameter (specified with :sd=dir:), and attempts to insert the job directly into the spool directory at the correct queue position. If you're running just the old Berkeley lpd, this might actually work. Usually it won't, and you'll wonder where the job went.

Therefore, you should use a command to spool the job instead of relying on papd to do it all for you. You can accomplish this with the :pr=name_or_command: parameter in papd.conf. Here's an example:

```
printername:\n:pr=/usr/bin/lpr -Pprintername:\n..\n..
```

where printername is the printer name in /etc/printcap. Using the :pr=|... parameter means you won't be able to use any additional queuing features from the Mac side (such as canceling a job), but that's better than not being able to print at all.

## Filesharing

The Netatalk filesharing daemon, afpd, allows guest and user logins, as well as automatic access to user home directories. When a user accesses a directory from a Mac, a new afpd runs as that user on the Unix, meaning that the user has read and write privileges identical to those on their Unix account. afpd's main configuration file is afpd.conf, but an AppleVolumes file allows you to control which directories (volumes) are available over AppleTalk (this setup is similar to the /etc/exports file on NFS servers).

### PROBLEM 43

Symptoms: No afpd options mentioned in this section seem to work. afpd.conf is ignored. Dancing icons appear under MacOS 8.

Problem: You have Netatalk, not the enhanced Netatalk+asun package.

Fix: Use Netatalk+asun (that is, until and if it merges with Netatalk). Obtain Netatalk+asun as mentioned above, or look in support/atalk/samba on this book's CD-ROM. Among Netatalk+asun's extra features is a TCP/IP AppleShare server.

You don't absolutely have to have an afpd.conf file, but the defaults aren't terribly appealing for two reasons. First, guest access is turned on by default, so any visitor can access any volume other than a user one. The other reason is that you may want to use a server name other than the Linux host name and make it act like multiple servers.

Here's a relatively simple afpd.conf file:

```
"Private AppleTalk Server" -noguest -nouservol
"Public Software" -nocleartext -defaultvol /etc/AppleVolumes.public
```

The first line sets up a server for users only, and the second sets up a guest-only server with volumes specified in /etc/AppleVolumes.public.

### PROBLEM 44

Symptom: Some users cannot log in (but the systems administrators can).

Problem: The file /etc/shells doesn't contain the users' shells.

Fix: Just as with ftpd, a user must have a shell listed in /etc/shells to gain access to an afpd volume. Either the shell isn't listed there, or you've denied the user access to the machine with an entry in /etc/passwd such as this one:

```
+@normal_users::::::/usr/local/bin/noaccess
```

If you add /usr/local/bin/noaccess to /etc/shells, it may come into conflict with your desire to keep FTP users off of the machine. If that concerns you, you'll just have to turn ftpd off or reconfigure it to your liking.

### PROBLEM 45

Symptom: You can't have more than five Macs accessing the Netatalk server simultaneously.

Problem: You have the compiled-in maximum connection limit set too low.

Fix: Start afpd with -c num, where num is the maximum number of simultaneous connections you want to allow.

### afpd Options

These are the most important afpd options. The full list is in the afpd (8) manual page.

- -C Don't allow clear-text passwords.
- -c num Allow at most num connections at once.
- -d Debug mode (don't run as a daemon; log to standard output).
- -f defvolfile Use defvolfile as the AppleVolumes.default file.
- -G Don't let guests log in (you can also set this on a per-server basis in the afpd.conf file).
- -g username Set username as the guest user (default: nobody).
