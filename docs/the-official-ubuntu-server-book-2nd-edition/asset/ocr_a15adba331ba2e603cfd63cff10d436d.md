There are two different ways to edit the BackupPC configuration. The first (and easier) is through the Web interface; with the second you just open /etc/backuppc/config.pl with a text editor and locate and tweak settings directly.

# Web-Based Configuration

You can actually change all of the options you need directly from the Web interface. From the BackupPC home page click the Edit Config link in the left pane and then click the Xfer link along the top of the right pane. You will then see a configuration screen like the one in Figure 7-2. On the XferMethod drop-down menu change from smb to rsync. Then scroll down until you see the RsyncClientCmd and RsyncClientRestoreCmd options. Change both of them from

```
$sshPath -q -x -l root $host $rsyncPath $argList+
```

to

```
$sshPath -q -x -l backuppc $host sudo $rsyncPath $argList+
```

![](bbox=[0.22, 0.68, 0.89, 0.895])

Figure 7-2 BackupPC Xfer configuration options