![](bbox=[0.23, 0.08, 0.9, 0.32])

**Figure 13-15** Viewing the cron init script.

# ## Using cron to Manage Scheduled System Jobs

Using cron to run scheduled system jobs is an extremely useful tool for a Linux system administrator. You can configure your systems to perform a wide variety of tasks on a regular schedule automatically, saving you a ton of time and effort.

Remember when I mentioned the problems with running regular backups? Creating a system job in cron that runs a backup on a regular schedule saves me tons of time. If I don’t have time to visit a client site on a particular day, I don’t have to worry. I know that cron will run a backup at the preconfigured time. All I have to do is drop by now and then to verify that everything is still working properly and to perhaps rotate the backup media. I love cron!

To run system jobs, the cron service uses the /etc/crontab file, shown next, to configure what jobs to run.

```
```bash
ws2:/etc#init.d # ls
.
depend.boot
depend.halt
depend.start
depend.stop
ifup-restart init2
ifup-restart init2_setup
ifup-restart2
test
...
cron

boot.idcconfig
boot.leadmodules
boot.local
boot.localnet
boot.md
boot.multipath
boot.proc
boot.netsch
boot.startpreload
boot.swap
boot.systcl
boot.uudev
boot.uudev_retry
cron

irq-balancer
joystick
kbd
kexec
keyscapsd
knockd
lirc
lirc_sensors
misclog
modmd
multiplathd
mySQL
network
network-rmnetns
nfs
nmb
nscd
ntp

rcs.d
rcs.d
rcs.d
rcs.d
reboot
rpcbind
rpcapckd
rpcstat
setwall2
tgla
stalemon
skeleton.compat
smartd
swd
snapt
spand
spandd
```

```bash
ws2:/etc # cat ./crontab
SHELL=/bin/sh
PATH=/usr/bin:/usr/sbin:/usr/bin:/bin:/usr/sbin:/usr/lib/news/bin
MAILTO=root
#
# check scripts in cron.hourly, cron.daily, cron.weekly, and cron.monthly
#
*/15 * * * * root test -x /usr/lib/cron/run-crons && /usr/lib/cron/run-crons
</dev/null 2>&1
ws2:/etc #
```
```

As you can see in this example, the /etc/crontab file contains commands that are used to run scripts found in four different directories:

+   * /etc/cron.hourly   Contains cron scripts that are run every hour.
+   * /etc/cron.daily    Contains cron scripts that are run every day.
+   * /etc/cron.weekly   Contains cron scripts that are run once a week.
+   * /etc/cron.monthly  Contains cron scripts that are run once a month.