# Linux Hack

```
# find . -mtime +60
```

Ajay Kumar Tiwari

# How to find files that are modified in the last x number of days?

The following command will list all the files that were modified in the last two days under the current directory.

```
# find . -mtime -2
```

# How to delete all the archive files with extension *.tar.gz and greater than 100MB?

Please be careful while executing the following command as you don’t want to delete the files by mistake. The best practice is to execute the same command with ls -l to make sure you know which files will get deleted when you execute the command with rm.

```
# find / -type f -name *.tar.gz -size +100M -exec ls -l {} \;
```

```
# find / -type f -name *.tar.gz -size +100M -exec rm -f {} \;
```

# How to archive all the files that are not modified in the last x number of days?

The following command finds all the files not modified in the last 60 days under /home/jsmith directory and creates an archive files under /tmp in the format of ddmmyyyy_archive.tar.

```
# find /home/jsmith -type f -mtime +60 | xargs tar -cvf
/tmp/`date '+%d%m%Y'_archive.tar`
```

On a side note, you can perform lot of file related activities (including finding files) using midnight commander GUI, a powerful text based file manager for Unix.