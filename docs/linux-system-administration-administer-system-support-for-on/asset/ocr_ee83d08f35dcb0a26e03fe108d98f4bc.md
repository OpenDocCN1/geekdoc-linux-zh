The next screen you have is the actions menu—miscellaneous commands for log, file, and archive management, verifying the backup, and sending a bug report. Figure 10-7 shows Kbackup’s actions menu.

![](bbox=[0.16, 0.18, 0.6, 0.42])

# ## Backing Up with Tar

Among the best backup tools for Linux systems, you’d still find tar high on the list. Though it’s been around for a long time, tar is still reliable and it gets the job done. Many programmers still use it to bundle applications, and IT pros still use it to do backups. It’s easy to use, its syntax is fairly simple, and it’s portable across most UNIX platforms.

The tar command listing shows how versatile it is. The options are shown in Listing 10-1.

**Listing 10-1: Using tar for backup**

```
```text
# tar --help

GNU 'tar' saves many files together into a single tape or disk archive, and
can restore individual files from the archive.

Usage: tar [OPTION]... [FILE]...
```

```

This shows the usage of tar. The tar command’s main options define the archive by creating it, listing the contents, showing the difference between the archive and the actual file system, and extracting the files. You can also add or update files to the archive.

If you are not using a magnetic tape, you can delete files from the archive — but be careful.