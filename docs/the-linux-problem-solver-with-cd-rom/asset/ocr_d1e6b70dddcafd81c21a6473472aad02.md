# Filesharing

The Netatalk filesharing daemon, afpd, allows guest and user logins, as well as automatic access to user home directories. When a user accesses a directory from a Mac, a new afpd runs as that user on the Unix, meaning that the user has read and write privileges identical to those on their Unix account. afpd’s main configuration file is afpd.conf, but an AppleVolumes file allows you to control which directories (volumes) are available over AppleTalk (this setup is similar to the /etc/exports file on NFS servers).

# PROBLEM 43

Symptoms: No afpd options mentioned in this section seem to work. afpd.conf is ignored. Dancing icons appear under MacOS 8.

Problem: You have Netatalk, not the enhanced Netatalk+asun package.

Fix: Use Netatalk+asun (that is, until and if it merges with Netatalk). Obtain Netatalk+asun as mentioned above, or look in support/atalk/samba on this book’s CD-ROM. Among Netatalk+asun’s extra features is a TCP/IP AppleShare server.

You don’t absolutely have to have an afpd.conf file, but the defaults aren’t terribly appealing for two reasons. First, guest access is turned on by default, so any visitor can access any volume other than a user one. The other reason is that you may want to use a server name other than the Linux host name and make it act like multiple servers.

Here’s a relatively simple afpd.conf file:

```
"Private AppleTalk Server" -noguest -nouservol
"Public Software" -nocleartext -defaultvol /etc/AppleVolumes.public
```

The first line sets up a server for users only, and the second sets up a guest-only server with volumes specified in /etc/AppleVolumes.public.