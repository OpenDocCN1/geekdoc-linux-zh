
## File Sharing

## PART III

If you see a process other than grep, then atalk is running. You can check functionality further by typing

```
cat /proc/net/atalk_iface
```

This command displays information on the devices to which atalkd has attached itself. For instance, on my system, this command reports the following:

```
eth0                 F500:DA  0000-FFFF  0
lo                   0000:00  0000-0000  0
```

This means that atalkd is servicing eth0 by using the address F500:DA (network address 62720, node address 218, expressed in hexadecimal), and is listening on networks 0 through FFFE (65534). The daemon has also attached itself to lo, the loopback interface.

A final test of basic atalkd functionality is to use the aecho command, which is AppleTalk’s equivalent of TCP/IP’s ping—it sends AppleTalk Echo requests to a specified host, waits for the reply, and prints some basic statistics. You can specify either the target computer’s AppleTalk name or its address (network and node, separated by a period, as in 41201.173). Here’s the result of giving the command aecho teela on my network:

```
14 bytes from 41201.173: aep_seq=0, time=0. ms
14 bytes from 41201.173: aep_seq=1, time=0. ms
14 bytes from 41201.173: aep_seq=2, time=0. ms
14 bytes from 41201.173: aep_seq=3, time=0. ms

---41201.173 AEP Statistics---
4 packets sent, 4 packets received, 0% packet loss
round-trip (ms)  min/avg/max = 0/0/0
```

I terminated this test after four packets by pressing Ctrl+C.

> **NOTE**
> 
> You can use either a real Macintosh or another Netatalk-enabled computer as the target of the aecho command. You can’t use aecho on your own computer, though, at this stage of the configuration process.

At this point, I recommend terminating atalkd because in the next sections you’ll learn how to start it, afpd, and papd all with a single command.

## The afpd Daemon

Getting atalkd running is good, but essentially useless by itself. To configure Netatalk to do any real work, you must configure and start afpd, too.

## Configuring afpd

You configure afpd through four files, all located in the /etc/atalk directory:

- config—Sets overall configuration options.
- afpd.conf—Controls options most relevant to authentication and data transfer. Most of these options can be set in the config file.
- AppleVolumes.default—Specifies the directories you want to export.
- AppleVolumes.system—Specifies the Macintosh creator and type codes used for native Linux files.

## Creating a config File

The /etc/atalk/config file is included with the particular RPM distribution on this book's CD-ROM, and is used by the Netatalk startup scripts. Another distribution of Netatalk might not use this file. It contains important configuration parameters for providing AppleTalk services. You set options in this file by giving an option name, equal sign, and value. Important options you can set in this file include the following:

- AFPD_MAX_CLIENTS—This option is the maximum number of client computers the server allows. The default is 5.
- ATALK_NAME—This option is the name of your computer on the AppleTalk network. The default setting attempts to base this name on your Internet machine name, and this usually works. In some cases you might need to specify something else, though.
- AFPD_NOCLR—You set this parameter equal to -c to disable cleartext logins. The version of Netatalk included with this book's CD-ROM doesn't support encrypted logins, so you should leave this line commented out. If you want to enable encrypted logins, you need to obtain the source code to Netatalk and a DES library, and then compile your own custom version of the program.
- AFPD_NOGUEST—You set this parameter equal to -g to disable guest (no password) logins. The default setting permits guest logins.
- AFPD_GUEST—This option specifies the name of the guest user with this parameter. The default is nobody, which gives very restrictive permissions to the guest user.
- PAPD_RUN—This option specifies yes or no to have the startup scripts run papd for printer services.
