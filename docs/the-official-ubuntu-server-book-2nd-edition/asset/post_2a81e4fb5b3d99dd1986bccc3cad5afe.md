
First, BackupPC must be stopped while you do this so that it doesn't write to that directory while you're changing it:

```
$ sudo service backuppc stop
$ sudo mv /var/lib/backuppc /var/lib/backuppc.orig
$ sudo mkdir /var/lib/backuppc
$ sudo chown backuppc:backuppc /var/lib/backuppc
$ sudo mount /dev/sdb1 /var/lib/backuppc
$ sudo rsync -av /var/lib/backuppc.orig/ /var/lib/backuppc/
$ sudo service backuppc start
```

Finally, don't forget to add the new /dev/sdb1 mount point into /etc/fstab so it will mount automatically the next time the system boots.

## Default BackupPC Configuration

Of course, the default Web interface isn't very useful until you add a host. BackupPC's default behavior is defined in /etc/backuppc/config.pl, its core configuration file. If you are unfamiliar with Perl, this file may seem a bit daunting at first as all of the options are configured in Perl data structures. I walk you through adding an Ubuntu host that you will back up with rsync, and as you will see, once you get the core configuration file set, it is relatively simple to add hosts.

The config.pl file defines the default settings for all hosts BackupPC backs up, such as how often to back up, what directories to back up, whether to use smb, rsync, or tar to back up, and even what arguments to pass to those commands. What you want to do is generate a config.pl that works for the majority of your hosts and then create host-specific configuration files when a host needs special options. Any host-specific configuration goes into a .pl file under /etc/backuppc/ named after the host. So if you had a host named web1 and wanted to change some settings just for it, you would copy those specific options from /etc/backuppc/config.pl to /etc/backuppc/web1.pl. Any options you set in web1.pl will override anything in config.pl when web1 is being backed up.

In this example I assume a network mostly made up of other Ubuntu servers and use rsync for the backup. This is all-important because by default BackupPC logs in over SSH as root. On a network of Ubuntu servers this wouldn't work, because root is disabled by default, so we need to change some settings.

There are two different ways to edit the BackupPC configuration. The first (and easier) is through the Web interface; with the second you just open /etc/backuppc/config.pl with a text editor and locate and tweak settings directly.

### Web-Based Configuration

You can actually change all of the options you need directly from the Web interface. From the BackupPC home page click the Edit Config link in the left pane and then click the Xfer link along the top of the right pane. You will then see a configuration screen like the one in Figure 7-2. On the XferMethod drop-down menu change from smb to rsync. Then scroll down until you see the RsyncClientCmd and RsyncClientRestoreCmd options. Change both of them from

```
$sshPath -q -x -l root $host $rsyncPath $argList+
```

to

```
$sshPath -q -x -l backuppc $host sudo $rsyncPath $argList+
```

![](img/304f637afcecc491b152ee8ac5afadee_306_0.png)

Figure 7-2 BackupPC Xfer configuration options

Then scroll back up to the top of the page and click the Save button. Once you are done with all of your changes, click the Admin Options link in the left sidebar and then click Reload so BackupPC can read your new settings.

### Command-Line Configuration

While the Web interface provides an easy way to configure BackupPC, some people prefer doing it all through the command line. If you are one of those people, open the /etc/backuppc/config.pl file in your preferred text editor and then search for the line that matches this one:

```
$Conf{XferMethod} = 'smb';
```

This option defines the default method BackupPC uses to transfer files. SMB might work well for a network of Windows machines, but since we have Ubuntu hosts, we change this to rsync:

```
$Conf{XferMethod} = 'rsync';
```

Next, we need to set BackupPC so that it logs in to each machine as a regular user and then uses sudo to become root. We create a backuppc user on each host along with a secure sudo role so that BackupPC can log in and back up the machine. First locate the following line:

```
$Conf{RsyncClientCmd} = '$sshPath -q -x -l root $host $rsyncPath $argList+';
```

This defines what command BackupPC uses when it backs up with rsync. Change it to

```
$Conf{RsyncClientCmd} = '$sshPath -q -x -l backuppc $host sudo $rsyncPath $argList+';
```
