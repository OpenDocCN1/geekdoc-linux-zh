# The SMART standard provides a mechanism for running disk self-tests and for monitoring aspects of disk performance.

the log is empty. Typically, one should worry only if disk errors start to appear in large numbers. An occasional transient error that does not recur usually is benign. The smartmontools Web page has a number of examples of smartctl -a output showing some illustrative error log entries. They are timestamped with the disk’s power-on lifetime in hours when the error occurred, and the individual ATA commands leading up to the error are timestamped with the time in milliseconds after the disk was powered on. This shows whether the errors are recent or old.

The final part of the smartctl output (Listing 5) is a report of the self-tests run on the disk. These show two types of self-tests, short and long. (ATA-6/7 disks also may have conveyance and selective self-tests.) These can be run with the commands smartctl -t short /dev/hda and smartctl -t long /dev/hda and do not corrupt data on the disk. Typically, short tests take only a minute or two to complete, and long tests take about an hour. These self-tests do not interfere with the normal functioning of the disk, so the commands may be used for mounted disks on a running system. On our computing cluster nodes, a long self-test is run with a cron job early every Sunday morning. The entries in Listing 5 all are self-tests that completed without errors; the LifeTime column shows the power-on age of the disk when the self-test was run. If a self-test finds an error, the Logical Block Address (LBA) shows where the error occurred on the disk. The Remaining column shows the percentage of the self-test remaining when the error was found. If you suspect that something is wrong with a disk, I strongly recommend running a long self-test to look for problems.

The smartctl -t offline command can be used to carry out off-line tests. These off-line tests do not make entries in the self-test log. They date back to the SFF-8035i standard, and

```
Listing 4. Output of smartctl -l error /dev/hda

SMART Error Log Version: 1
No Errors Logged
```

Listing 5. Output of smartctl -l selftest /dev/hda

SMART Self-test log, version number 1
Num Test_Description Status Remaining LifeTime(hours) LBA_of_first_error
# 1 Extended off-line Completed 00% 3525 -
# 2 Extended off-line Completed 00% 3357 -
# 3 Short off-line Completed 00% 3059 -

update values of the Attributes that are not updated automatically under normal disk operation (see the UPDATED column in Listing 3). Some disks support automatic off-line testing, enabled by smartctl -o on, which automatically runs an off-line test every few hours.

The SMART standard provides a mechanism for running disk self-tests and for monitoring aspects of disk performance. Its main shortcoming is that it doesn’t provide a direct mechanism for informing the OS or user if problems are found. In fact, because disk SMART status frequently is not monitored, many disk problems go undetected until they lead to catastrophic failure. Of course, you can monitor disks on a regular basis using the smartctl utility, as I’ve described, but this is a nuisance.

The remaining part of the smartmontools package is the smartd daemon that does regular monitoring for you. It monitors the disk’s SMART data for signs of problems. It can be configured to send e-mail to users or system administrators or to run arbitrary scripts if problems are detected. By default, when smartd is started, it registers the system’s disks. It then checks their status every 30 minutes for failing Attributes, failing health status or increased numbers of ATA errors or failed self-tests and logs this information with SYSLOG in /var/log/messages by default.

You can control and fine-tune the behavior of smartd using the configuration file /etc/smartd.conf. This file is read when smartd starts up, before it forks into the background. Each line contains Directives pertaining to a different disk. The configuration file on our computing cluster nodes look like this:

```
# /etc/smartd.conf config file
/dev/hda -s on -o on -a -I 194 -m sense@phys.uwm.edu
/dev/hdc -s on -o on -a -I 194 -m sense@phys.uwm.edu
```

The first column indicates the device to be monitored. The -o on Directive enables the automatic off-line testing, and the -s on Directive enables automatic Attribute autosave. The -m Directive is followed by an e-mail address to which warning messages are sent, and the -a Directive instructs smartd to monitor all SMART features of the disk. In this configuration, smartd logs changes in all normalized attribute values. The -I 194 Directive means ignore changes in Attribute #194, because disk temperatures change often, and it’s annoying to have such changes logged on a regular basis.

Normally smartd is started by the normal UNIX init mechanism. For example, on Red Hat distributions, /etc/rc.d/init.d/smartd start and /etc/rc.d/init.d/smartd stop can be used to start and stop the daemon.

Further information about the smartd and its config file can be found in the man page (man smartd), and summaries can be found with the commands smartd -D and smartd -h. For example, the -M test Directive sends a test e-mail warning message to confirm that warning e-mail messages are delivered correctly. Other Directives provide additional flexibility, such as monitoring changes in raw Attribute values.

What should you do if a disk shows signs of problems? What if a disk self-test fails or the disk’s SMART health status fails? Start by getting your data off the disk and on to another system as soon