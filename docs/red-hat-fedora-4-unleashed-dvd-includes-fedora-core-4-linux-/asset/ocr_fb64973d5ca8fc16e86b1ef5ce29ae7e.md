useful for archiving copies of floppy disks while retaining the capability to restore the data to a floppy intact. For example,

```
# dd if=/dev/fd0 of=floppyimage1.img
```

Swapping the *if=* and *of=* values reverses the process. Although best known for copying images, dd can also be used to convert data, and it is especially useful when restoring older archives or moving data between big endian and little endian systems. Although such esoteric details are beyond the scope of this chapter, remember dd if you need to convert data from obsolete formats.

> CAUTION
> 
> Do not confuse the *if=* and *of=* assignments; if you do, dd will be more than happy to over- write your valid data with garbage. Use the Carpenter’s Rule: “Measure twice—cut once.”

# Using the Amanda Backup Application

Provided with Fedora Core, Amanda is a powerful, network backup application created by the University of Maryland at College Park. Amanda is a robust backup and restore applic-ation best suited to unattended backups with an autoloading tape drive of adequate capacity. It benefits from good user support and documentation.

Amanda’s features include compression and encryption. It is intended for use with high-capacity tape drives, floptical, CD-R, and CD-RW devices.

Amanda uses GNU tar and dump; it is intended for unattended, automated tape backups, and is not well-suited for interactive or ad hoc backups. The support for tape devices in Amanda is robust, and file restoration is relatively simple. Although Amanda does not support older Macintosh clients, it will use Samba to back up Microsoft Windows clients, as well as any Unix client that can use GNU tools (which includes Mac OS X). Because Amanda runs on top of standard GNU tools, file restoration can be made using those tools on a recovery disk even if the Amanda server is not available. File compression can be done on either the client or server, thus lightening the computational load on less powerful machines that need backing up.

> CAUTION
> 
> Amanda does not support dump images larger than a single tape and requires a new tape for each run. If you forget to change a tape, Amanda continues to attempt backups until you insert a new tape, but those backups will not capture the data as you intended them to. Do not use too small a tape or forget to change a tape, or you will not be happy with the results.

There is no GUI interface for Amanda. Configuration is done in the time-honored Unix tradition of editing text configuration files located in /etc/amanda. The default installa- tion in Fedora Core includes a sample cron file because it is expected that you will be