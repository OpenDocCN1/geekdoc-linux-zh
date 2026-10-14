# Multi-platform Backups Using Amanda

A very robust and powerful multi-vendor UNIX backup platform is the Advanced Maryland Automated Network Disk Archiver (known as Amanda), a project at the University of Maryland. Amanda will also support Windows platforms if you have SAMBA installed in your infrastructure. Information about this software package can be found at http://www.cs.umd.edu/projects/amanda/amanda.html. The latest distribution of the Amanda software can be downloaded from ftp://ftp.amanda.org/pub/amanda.

Once you've downloaded the distribution, you will need to compile and distribute the binaries for each UNIX platform you wish to back up, as well as install the software on the server(s) to which your backup media is attached. Amanda uses a combination of the tar command with gzip compression to perform backups. A central server is configured and remotely manages a list of servers that you define. You will need to create a trust relationship between the Amanda clients and the server for the UID that is responsible for running the backups. In almost every case, you will use the user operator to run the backups, and you will need to create an .rhosts file in /home/operator that contains the following:

```
#
#sample .rhosts file
#
backup.sniglets.com    operator
```

This will allow Amanda to use rsh to initiate the backup process on each remote system. Once the operator user is configured, you are ready to begin configuring and using Amanda. Some of the more frequently used Amanda programs are shown in Table 13.10.

Once you've installed the program, you will need to configure the amanda.conf file to reflect your infrastructure. While each line of

| Table 13.10 Commonly Used Amanda Commands |  |
|---|---|
| Command | Purpose |
| amdump | Performs a backup using Amanda |
| amlabel | Writes valid label to backup media so it can be catalogued by Amanda |
| amrestore | Extracts files from an Amanda tape |
| amcheck | Verifies the correct media is mounted and available |
| amadmin | Administers interface to Amanda |