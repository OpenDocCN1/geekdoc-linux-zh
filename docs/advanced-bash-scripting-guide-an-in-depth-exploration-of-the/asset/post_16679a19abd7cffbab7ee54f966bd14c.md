
# Advanced Bash-Scripting Guide

```bash
# --> ################################################################
# --> What is "podcasting"?
# --> It's broadcasting "radio shows" over the Internet.
# --> These shows can be played on iPods and other music file players.
# --> This script makes it possible.
# --> See documentation at the script author's site, above.
# --> ################################################################

# Make script crontab friendly:
cd $0
# --> Change to directory where this script lives.

# datadir is the directory you want podcasts saved to:
datadir=$(date +%Y-%m-%d)
# --> Will create a date-labeled directory, named: YYYY-MM-DD

# Check for and create datadir if necessary:
if test -d $datadir
then
mkdir $datadir

# Delete any temp file:
rm -f temp.log

# Read the bp.conf file and get any url not already
#+ in the podcast.log file:
while read podcast
do do --> Main action follows.
file=$(wget -q $podcast -o - | tr '\' '\\n' | tr '\' '\\' | \
sed -n 's/.*\(.*\*/\\1/p')
for url in $file
do
  echo $url >> temp.log
  if grep -q "$url" $datadir"$url" > /dev/null
  then
    wget -q -P $datadir"$url"
  fi
done < bp.conf

# Move dynamically created log file to permanent log file:
cat podcast.log >> temp.log
sort temp.log | uniq -d podcast.log
rm temp.log

# Create an m3u playlist:
ls $datadir | grep -v m3u > $datadir/podcast.m3u

exit 0

################################################################
For a different scripting approach to Podcasting,
see Phil Talkie's article,
"Internet Radio to Podcast with Shell Tools"
in the September, 2005 issue of LINUX JOURNAL,
http://www.linuxjournal.com/article/8171
```

# Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

Example A-32. Nightly backup to a firewire HD

```bash
#!/bin/bash
# nightly-backup.richardneill.org/source.php#nightly-backup-rsync
# http://www.richardneill.org/
# Copyright (c) 2005 Richard Neill <backup@richardneill.org>
# This is Free Software licensed under the GNU GPL.
# == Included in ABS Guide with script author's kind permission.
# ==> (Thanks!)

# This does a backup from the host computer to a locally connected
# firewire HDD using rsync and ssh.
# (Script work with USB-connected device (see lines 40-43),
# It rotates the backups
# Run via cron every night at 5am.
# This only backs up the home directory.
# If ownership (other than the user's) should be preserved,
# then run the rsync process as root (re-instant the -o).
# We save every day for 7 days, then every week for 4 weeks,
# then every month for 3 months.

# See: http://www.mikerubel.org/computers/rsync_snapshots/
# for more explanation of the theory.
# Save as: $HOME/bin/nightly_backup_firewire-hdd.sh

# Known bugs:
----
# i) Ideally, we want to exclude /tmp and the browser caches.

# ii) If you are sitting at the computer at 5am,
# and files are modified when the rsync is occurring,
# then the BACKUP_JUSTINANCE branch gets triggered.
# To some extent, this is a
# feature, but it also causes a "disk-space leak."
```

```bash
BEGIN CONFIGURATION SECTION ############################################
LOCAL_USER=rjn # User whose home directory should be backed up.
MOUNT_POINT=/backup # Mountpoint of backup drive.
# NO trailing slash! 

# MOUNT_POINT=/media/disk # This must be unique (using a device symlink)
# For USB-connected device.
SOURCE_DIR=/home/$LOCAL_USER # No trailing slash; it DOES matter to rsync.
BACKUP_DEST_DIR=$MOUNT_POINT/backups-hostname+'%s' -${LOCAL_USER}.nightly_backup
DRV_RUN=false # If true, invoke rsync with -n, to do a dry run.
# Comment out or set to false for normal use.

VERBOSE=false # If true, make rsync verbose.
# Comment out or set to false otherwise.
COMPRESS=false # If true, compress.
# Good for internet, but bad on LAN.
# Comment out or set to false otherwise.
```

```bash
E_VARS_NOT_SET=64
E_COMMANDLINE=65
E_MOUNT_FAIL=70
```

Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

E_NOSOURCEDIR=71
E_UNMOUNTED=72
E_BACKUP=73
##### END CONFIGURATION SECTION ###########################

```bash
# Check that all the important variables have been set:
if [ -z "$LOCAL_USER" ] || \
    [ -z "$SOURCE_DIR" ] || \
    [ -z "$MOUNT_POINT" ] || \
    [ -z "$BACKUP_DEST_DIR" ];
then
    echo "one of the variables is not set! Edit the file: $0."
    exit $E_VARS_NOT_SET
fi

if [ "$1" != 0 ]; then # If command-line param(s)
    cat <<ENDOFTEXT
Automatically backup from cron.
Read the source for $BACKUP_DEST_DIR
The backup directory is $BACKUP_DEST_DIR
It will be created if necessary; initialization is no required.
WARNING: Contents of $BACKUP_DEST_DIR are rotated.
Directories named backup_$1 will be eventually deleted.
We keep backups every day for 7 days (1-8),
every week for 4 weeks (9-12),
every month for 3 months (13-15).

You may wish to add this to crontab
# Back up files: $SOURCE_DIR to $BACKUP_DEST_DIR
# every night at 3:15 am
03 * * * /home/$LOCAL_USER/bin/nightly-backup-firewire-hdd.sh

Don't forget to verify that the backups are working,
especially if you don't read cron's mail.
ENDOFTEXT
fi

# Parse the options.
if [ "$DRY_RUN" = "true" ]; then
    DRY_RUN="-n"
    echo "WARNING: THIS IS A DRY RUN!"
    echo "No data will actually be transferred!"
else
    DRY_RUN=""
fi

if [ "$VERBOSE" = "true" ]; then
    VERBOSE="-v"
else
    VERBOSE=""
fi

if [ "$COMPRESS" = "true" ]; then
    COMPRESS="-z"
else
    COMPRESS=""
fi

# Every week (actually 8 days) and every month (0..31).
DAY_OF_MONTH+=%d
if [ "$DAY_OF_MONTH" -eq 01 ]; then # First of month.
    MONTHSTART=true
elif [ "$DAY_OF_MONTH" -eq 08 ]; then # Day 8,
    WEEKSTART=true
elif [ "$DAY_OF_MONTH" -eq 16 ]; then # Day 16,
    WEEKSTART=true
elif [ "$DAY_OF_MONTH" -eq 24 ]; then # Day 24,
    WEEKSTART=true
fi # Day 24 to better handle 31-day months)

if grep "$MOUNT_POINT" >/dev/null; then
    echo "Mount point $MOUNT_POINT is indeed OK."
else
    echo "Attempt to mount $MOUNT_POINT..."
    # If it isn't unmounted, try to mount it.
    sudo mount $MOUNT_POINT 2>/dev/null
fi

if grep "$MOUNT_POINT" >/dev/null; then
    UNMOUNTLATER=TRUE
    echo "OK" # Note: Ensure that this is also unmounted if we exit prematurely with failure.
else
    echo "FAILED"
    echo "Nothing is mounted at $MOUNT_POINT. BACKUP FAILED!"
    exit $E_MOUNT_FAILED
fi

# Check that source dir exists and is readable.
if [ ! -r "$SOURCE_DIR ]; then
    echo "$SOURCE_DIR does not exist, or cannot read. BACKUP FAILED."
    exit $E_NOSOURCEDIR
fi

# Check that the backup structure is as it should be.
# If not, create it.
# Create the subdirectories.
# Note that backup.0 will be created as needed by rsync.
for ((i=1;i<=15;i++)); do
    if [ ! -d $BACKUP_DIR/backup.$i ]; then
        if /bin/mkdir -p $BACKUP_DIR/backup.$i; then # No brackets. Why?
            echo "Warning: $BACKUP_DIR/backup.$i is missing, or was not initialized. (Re-creating it.)
        else
            echo "ERROR: $BACKUP_DIR/backup.$i is missing and could not be created."
            if [ "$MOUNT_LIMIT" == "TRUE" ]; then
                # Before we exit, unmount the mount point if necessary.
                cd
                sudo ummount $MOUNT_POINT &&
                echo "Unmounted $MOUNT_POINT again. Giving up."
            fi
            exit $E_UNMOUNT
        fi
    fi
done

# Set the permission to 700 for security# on an otherwise permissive multi-user system.
if ! /bin/chmod 700 $BACKUP_DEST_DIR ; then
    echo "ERROR: Could not set permissions on $BACKUP_DEST_DIR to 700."
    if [ "$MOUNT_LIMIT" == "TRUE" ]; then
        # Before we exit, unmount the mount point if necessary.
        cd
        sudo umount $MOUNT_POINT
        echo "Unmounted $MOUNT_POINT again. Giving up."
    fi
    exit $E_UNMOUNT
fi

# Create the symlink current -> backup.1 if required.
# A failure here is not critical.
cd $BACKUP_DEST_DIR
if ! /bin/ln -s backup.1 current ; then
    echo "WARNING: could not create symlink current -> backup.1"
fi

# Now, do the rsync.
echo "Doing backup with rsync..."
echo "Source dir: $SOURCE_DIR"
echo "- backup destination: $BACKUP_DEST_DIR\n"
echo -e "backup failed"

/usr/bin/rsync $DRY_RUN $VERSION -a --delete --modify-window=60 \
--link=../backup.1 $BACKUP_DEST_DIR/backup/0/

# Only warn, rather exit if the rsync failed,
# + it may only be a minor problem.
# E.g. if one file is not readable, rsync will fail.
# This shouldn't prevent the rotation.
# Not using, e.g., date +ta since these directories
# - are full of links and don't consume *that* space.

if [ $? != 0 ]; then
  BACKUP_JUSTINCASE=``date +%F_%T`.justincase
```
