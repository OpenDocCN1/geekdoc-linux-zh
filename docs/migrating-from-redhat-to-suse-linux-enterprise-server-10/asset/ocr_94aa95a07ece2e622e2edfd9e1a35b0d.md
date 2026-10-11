When you view the files in a directory such as /etc/init.d/rc3.d/, you see two kinds of files—those that start with a “K” and those that start with an “S”:

```
gal0:~ # ls /etc/init.d/rc3.d/
K10cron K1network S07auditd
K10smbfs K2haldaemon S07portmap
K1nscd K21acpid S07splash_early
K1postfix K21dbus S08 nfs
K12alsasound K21fbset S08nfsboot
K12boot.apparmor K21irq_balancer S10alsasound
K12 cups K21random S10boot.apparmor
K12microcode K21resmgr S10cups
K12powersaved S01acpid S10kbd
K12splash S01dbus S10microcode
K12shd S01fbset S10powersaved
K14 nfs S01irq_balancer S10splash
K14nfsboot S01random S10sshd
K15auditd S01resmgr S11ncsd
K15portmap S02haldaemon S11postfix
K15splash_early S05network S12cron
K6novell-zmd S06novell-zmd S12smbfs
K16s1pd S06s1pd
K16syslog S06syslog
```

The first letter is always followed by 2 digits and the name of a service. Whether a service is started in a specific runlevel depends on whether there are **S**\*\*\*service and **K**\*\*\*service files in the /etc/init.d/rc\*.d/ directory.