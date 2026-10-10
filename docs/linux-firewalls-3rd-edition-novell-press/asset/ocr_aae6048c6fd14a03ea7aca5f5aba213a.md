of the binaries, first mount the CD. This is usually accomplished using the `mount` command, although sometimes it's mounted automatically. A common method for mounting the CD-ROM drive in most modern Linux distributions is shown here:

```
`mount -t iso9660 /dev/cdrom /mnt/cdrom`
```

Chkrootkit uses the `-p` option to define the location of the binaries it should use. Therefore, if the CD-ROM is mounted at `/mnt/cdrom`, you'd run Chkrootkit like so:

```
``` 
./chkrootkit -p /mnt/cdrom ```
```

The other method for running Chkrootkit is to physically mount the possibly compromised hard drive into another computer and run Chkrootkit against the contents of that drive. This is accomplished by specifying an alternate “root” directory for Chkrootkit. Assume that the second drive is mounted at `/mnt/drive2`:

```
``` 
./chkrootkit -r /mnt/drive2 ```
```

# ## When Should Chkrootkit Be Run?

Chkrootkit should be run whenever you'd like. There is no recommended schedule for Chkrootkit. I personally run it at irregular intervals for fun, but then again I'm just that type of guy. You should most definitely run Chkrootkit anytime you observe any suspicious activity on the computer or on other computers that may interact or reside on the same network block as the computer in question. Whenever you run Chkrootkit, you should always hop out to the website, http://www.chkrootkit.org/, to check for a new version of the tool. A new signature for a rootkit or additional functionality might have been added since the version you're using.

You can also run Chkrootkit nightly from cron. However, I wouldn't rely on such a report being entirely accurate, but it could provide an early warning of an anomaly that needs your attention. Running Chkrootkit from cron might look like this:

```
`0 4 * * * /path/to/chkrootkit`
```

The cron entry shown will run Chkrootkit every morning at 4:00 a.m. Root (the recipient of cron job output) will receive a report every morning detailing the run of Chkrootkit.

# # Filesystem Integrity

Hand in hand with a rootkit checker such as Chkrootkit goes filesystem integrity software. Filesystem integrity software monitors important files on the computer and generates reports based on changes to those files. The administrator can then watch for unexpected changes to