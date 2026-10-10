# Configuring the Appletalk Software

The first thing you need to do to make it all work is to ensure that the appropriate entries in the `/etc/services` file are present. The entries you need are:

+   rtmp 1/ddp # Routing Table Maintenance Protocol
+   nbp 2/ddp # Name Binding Protocol
+   echo 4/ddp # AppleTalk Echo Protocol
+   zip 6/ddp # Zone Information Protocol

The next step is to create the Appletalk configuration files in the `/usr/local/atalk/etc` directory (or wherever you installed the package).

The first file to create is the `/usr/local/atalk/etc/atalkd.conf` file. Initially this file needs only one line that gives the name of the network device that supports the network that your Apple machines are on:

eth0

The Appletalk daemon program will add extra details after it is run.

# Exporting a Linux Filesystems via Appletalk

You can export filesystems from your Linux machine to the network so that Apple machine on the network can share them.

To do this you must configure the `/usr/local/atalk/etc/AppleVolumes.system` file. There is another configuration file called `/usr/local/atalk/etc/AppleVolumes.default` which has exactly the same format and describes which filesystems users connecting with guest privileges will receive.

Full details on how to configure these files and what the various options are can be found in the `afpd` man page.

A simple example might look like:

```
/tmp Scratch
/home/ftp/pub "Public Area"
```

which would export your /tmp filesystem as AppleShare Volume "Scratch" and your FTP public directory as AppleShare Volume "Public Area." The volume names are not mandatory. The daemon will choose some for you, but it won't hurt to specify them anyway.

# Sharing Your Linux Printer Across Appletalk

You can share your Linux printer with your Apple machines quite simply. You need to run the `papd` program, which is the Appletalk Printer Access