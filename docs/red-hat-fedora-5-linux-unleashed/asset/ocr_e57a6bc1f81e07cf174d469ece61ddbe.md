To then initialize Tripwire, use its --init option like so:

```
```bash
# tripwire --init
Please enter your local passphrase:
Parsing policy file: /etc/tripwire/tw.pol
Generating the database...
*** Processing Unix File System ***
.....
Wrote database file: /var/lib/tripwire/shuttle2.twd
The database was successfully generated.
```
```

Note that not all the output is shown here. After Tripwire creates its database (which is a snapshot of your file system), it uses this baseline along with the encrypted configuration and policy settings under the /etc/tripwire directory to monitor the status of your system. You should then start Tripwire in its integrity-checking mode, using a desired option. (See the *tripwire* manual page for details.) For example, you can have Tripwire check your system and then generate a report at the command line, like so:

```
```bash
# tripwire -m c
```
```

No output is shown here, but a report is displayed in this example. The output could be redirected to a file, but a report is saved as /var/lib/tripwire/report/hostname-YYYYMMDD-HHMMSS.twr (in other words, using your host's name, the year, the month, the day, the hour, the minute, and the seconds). This report can be read using the twprint utility, like so:

```
```bash
# twprint --print-report -r \\
/var/lib/tripwire/report/shuttle2-20020919-181049.twr; less
```
```

Other options, such as emailing the report, are supported by Tripwire, which should be run as a scheduled task by your system's scheduling table, /etc/crontab, on off-hours. (It can be resource intensive on less powerful computers.) The Tripwire software package also includes a twadmin utility you can use to fine-tune or change settings or policies or to perform other administrative duties.

# ## Devices

Do not ever advertise that you have set a NIC to promiscuous mode. Promiscuous mode (which can be set on an interface by using ifconfig's promise option) is good for monitoring traffic across the network and can often allow you to monitor the actions of someone who might have broken into your network. The tcpdump command also sets a designated interface to promiscuous mode while the program runs; unfortunately, the ifconfig command does not report this fact while tcpdump is running! Keep in mind that this is one way a cracker will use to monitor your network to gain the ever-so-important root password.