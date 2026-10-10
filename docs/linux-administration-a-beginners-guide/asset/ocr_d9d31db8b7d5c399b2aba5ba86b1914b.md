```
overwrite no guest
rename no guest
log transfers reel in,outbound
password-check rfc282 warn
```

where `/home/ftp/noanonymous` is the text file sent to the client trying to connect as anonymous to inform them that anonymous access is not allowed.

# CONFIGURING A VIRTUAL FTP SERVER

With **wu-ftp** you can set up multiple FTP servers on the same host so long as each server has its own IP address. (This is a limitation of FTP, not the wu-ftp implementation in particular.) This process is quite easy once you have anonymous FTP set up for your primary host. This section assumes that you have already configured an IP alias and fudged the arp table correctly. (This is discussed in the Advanced Networking section later in the book.) This *quick jumpstart* on the process assumes you have one Ethernet card and want to add a single virtual IP address:

+   1. Make sure your new IP address exists in both the local host table (*etc/hosts*) as well as your DNS table. (In this example, we’ll call the host “earth.”)
+   2. Run the *ifconfig* command to configure the *eth0* device with the appropriate address, netmask, and broadcast. For example, to configure with the *192.168.1.42* device on *eth0*, I would use
+   3. Fudge the arp table. You will need your Ethernet card’s hardware address for this. Run the *ifconfig* -a command to get this information. Assuming your Ethernet card’s hardware address is *00:10:48:CB:15:9F*, type

```
ifconfig eth0:0 192.168.1.42 netmask 255.255.255.0 broadcast 192.168.1.255
```

```
arp -s earth 00:10:48:CB:15:9F pub
```

With your virtual IP address established, you now need to create a directory structure similar to that of an anonymous site. This should be placed in the directory that you want to make your virtual FTP site. Then add the virtual command to the end of your *tftp/accesses* file. The command’s format is

```
virtual IP ftype directory
```

where *IP* is the IP address of your virtual FTP server, and *ftype* is the file type that *directory* refers to. The *ftype* value can be either root, banner, or logfile. If the *ftype* is root, *directory* should be the *directory* in which the anonymous FTP files are set up for the virtual site. If *ftype* is either banner or logfile, the *directory* entry should be the corresponding file.