The next command configures an HP Laser-compatible printer with a JetDirect interface that is connected directly to the LAN at 192.168.1.103 and names this printer HPLJ. Specifying a socket in the protocol part of the URI instructs CUPS to use the JetDirect protocol, a proprietary protocol developed by HP for printers connected directly to a network.

```
$ lpadmin -p HPLJ -E v socket://192.168.1.103 -P /usr/share/ppd/custom/laserjet.ppd.gz
```

The lpadstat utility with the -d option displays the name of the default printer:

```
$ lpadstat -d
system default destination: MainPrinter
```

CUPS automatically makes the first printer you define the default printer. The following command makes HPLJ the default printer:

```
$ lpadmin -d HPLJ
```

The following command removes the configuration for the ColorPtr:

```
$ lpadmin -x ColorPtr
```

# PRINTING QUOTAS

CUPS provides rudimentary printing quotas. You can define page count and file size. File size quotas are almost meaningless because a small PostScript file can take a long time to interpret and require a lot more ink to print than a large one. Page quotas are more useful, although their implementation is flawed. To determine the number of pages in a document, CUPS examines the PostScript input. If a job is submitted in the printer's native language, such as PCL, CUPS bypasses this mechanism. Also, if page is used to create a PostScript file with multiple pages printed on each sheet, CUPS counts each page in the original document, rather than each sheet of it prints on.

Use job-quota-period and either job-page-limit or job-k-limit to establish a quota for each user on a given printer. The job-quota-period specifies the number of seconds that the quota remains. The following command establishes a quota of 20 pages per day for the printer named HPLJ:

```
$ lpadmin -p HPLJ -o job-quota-period=86400 -o job-page-limit=20
```

The k-limit works similarly but defines a file size limit in kilobytes. The limit is the total number of kilobytes each user can print during the quota period. Once a user has exceeded her quota, she will not be allowed to print until the next quota.

# MANAGING PRINT QUEUES

When a printer is operating normally, it accepts jobs into its print queue and processes those in the order they are received. You can give the command cupsreject followed by the name of a printer to cause a printer to not accept jobs into its print queue; give the command cupsaccept to enable it. You can also use system-config-printer to