| Saturday | Level 4 (incremental dump) |

Note that after the full backup on Sunday, a level 9 incremental dump is done the next day, and a successively lower dump level is done each day after that. This results in all the files that have changed since Sunday being backed up on every single incremental backup. Each incremental backup is thus larger than the previous one; the backup contains all of the files from the previous incremental backup plus any files that have changed since then. This may seem wasteful of storage space on the backup tape, but it will save a lot of time and effort should there be a need to restore the file system.

For example, imagine that your hard drive crashed on Friday. After replacing the hard drive, you can restore the entire file system in two steps: restore the full backup from the prior Sunday, and then the most recent incremental backup from Thursday. You can do this because Thursday's backup contains all of the files from Monday, Tuesday, and Wednesday's tape as well as the files that changed after that. If the dump levels had progressed in positive order (level 1 for Monday, level 2 for Tuesday, and so on), all of the incremental backups would have to be restored in order to restore the file system to its most current state.

# ### Automating Backups with cron

You can automate most of your backups with shell scripts and the cron daemon. Use the su command to become root, and then cd to the /usr/local/bin directory. Use any text editor to create a shell script called backups.sh that looks similar to the following:

```
```
#!/bin/sh
#
# backups.sh - A simple backup script, by Thad Phetteplace
#
# This script takes one parameter, the dump level.
# If the dump level is not provided, it is
# automatically set to zero. For level zero (full)
# dumps, rewind and eject the tape when done.
#
if [ $1 ]; then
    level=$1
else
    #
    # No dump level was provided, so set it
    # to zero
    #
    level="0"
fi

/sbin/dump $level uuf /dev/nrft0 /
/sbin/dump $level uuf /dev/nrft0 /home
```
```