# BACKUP PROGRAMS 225

If no pattern is specified, the list of all backed up files is displayed. Files can be read from the backup by means of the command:

```
(Linux):~# tob -restore /dev/rft0 pattern
```

The files are stored relative to the current directory, unless an additional parameter specifies the corresponding directory. Files are not overwritten, unless the system administrator calls the command in the / directory.

# The tbackup program

The tbackup package was developed to allow simple backing up of large amounts of data on diskettes (!). A number of errors are recognized which would abort the backup with tar or make it unusable. Examples are read or write errors on diskettes or simply a forgotten disk change. It is possible to carry out incremental backups. With as all other packages, it is equally possible to restore individual files. This package uses afio as the archiver.

Here too, a special mention goes to the extensive documentation supplied, which also includes instructions for the creation of emergency diskettes. Installation and configuration (/etc/tbackup/Config) are extensively described in the file /usr/lib/tbackup/README. The creation of an emergency diskette is described in the file /usr/lib/tbackup/rescue/CREATE. In the same directory, you will also find a series of programs which might help with the creation of an emergency diskette.

The tbackup package contains a separate program for practically every function and, in contrast to the other packages, it is not controlled via command options. A backup is started by means of the tbackup command; restoring is done by restore. Further commands call tlist (recreate file list of a backup) and tguess (calculate size of backup).

tbackup has not been developed for backup on magnetic tapes or in background operation. The use of magnetic tapes is possible to a limited extent; delayed backups via cron or at are not implemented.

The tkbackup program, which can also be found at sunsite.unc.edu, is a T/Tk interface for the above tbackup package.

# The KBackup program

The KBackup program by Karsten Balladuer is based on afio and tar. To enhance performance, the multibuf program can be employed. Backup on a tape drive connected to another computer is also supported.

As a user interface, KBackup uses dialog; thus, handling is quite easy.

In my opinion, the most interesting special features are packing or encrypting of