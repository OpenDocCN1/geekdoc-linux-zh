When given a filename as its argument, the script will try to restore that file or directory (if there’s only one match), or it will show a list of candidates for restoration and allow the user to specify which version of the deleted file or directory to restore.

# The Results

Without any arguments specified, the script shows what’s in the deleted files archive as Listing 2-8 shows.

```
$ unrm
Contents of your deleted files archive (sorted by date):
detritus          this is a test
detritus           garbage
```

> Listing 2-8: Running the unrm shell script with no arguments lists the current files available to restore

When a filename is specified, the script displays more information about the file if there are multiple files with that name, as shown in Listing 2-9.

```
$ unrm detritus
More than one file or directory match in the archive:
1) detritus (size = 7688Kb, deleted = 11/29 at 10:00:12)
2) detritus (size = 4Kb, deleted = 11/29 at 09:59:51)
Which version of detritus should I restore ('0' to quit)? [1] : 0
unrm: Restore canceled by user.
```

> Listing 2-9: Running the unrm shell script with a single argument attempts to restore the file

# Hacking the Script

If you use this script, be aware that without any controls or limits, the files and directories in the deleted files archive will grow without bound. To avoid this, invoke find from within a cron job to prune the deleted files archive, using the -mtime flag to identify those files that have been sitting untouched for weeks. A 14-day archive is probably quite sufficient for most users and will keep the archival script from consuming too much disk space.

While we’re at it, there are some improvements that could make this script more user friendly. Think about adding starting flags like -1 to restore latest and -0 to delete 0 additional copies of the file. Which flags would you add, and how would they streamline processing?

# #17 Logging File Removals

Instead of archiving deleted files, you may just want to keep track of what deletions are happening on your system. In Listing 2-10, file deletions with the rm command will be logged in a separate file without notifying the user.