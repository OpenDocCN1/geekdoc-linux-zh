command-line.

```
#!/bin/bash
if [ -d "$@" ]; then
echo "Files found: $(find "$@" -type f | wc -l)"
echo "Folders found: $(find "$@" -type d | wc -l)"
else
echo "[ERROR] Please retry with another folder:"
exit 1
fi
```

If the directory you specify is not available you will be asked to try again with a different one. The same message will appear if you do not have permission to access the specified directory.

# ## How to Clean Log Files

In the next demonstration, you can see how shell scripts can be used easily in real life. We are going to delete every log file stored in the directory called /var/log. If you want to clean up different logs, simply change the variable holding the directory:

```
#!/bin/bash
LOG_DIR=/var/log
cd $LOG_DIR

cat /dev/null > messages
cat /dev/null > wtmp
echo "Logs cleaned up."
```

Important – this shell script must be run as root.

# ### Using Bash to Back Up Your Script

Shell scripts provide a strong, effective way of backing up directories and files. In the next example, you can see how to back up every file and directory that was modified in the preceding 24 hours. The Linux find command is used for this.

```
#!/bin/bash

BACKUPFILE=backup-$(date +%m-%d-%Y)
archive=${1:-$BACKUPFILE}

find . -mtime -1 -type f -print0 | xargs -0 tar rvf "$archive.tar"
echo "Directory $PWD backed up in archive file \"$archive.tar.gz\"."
exit 0
```