# Advanced Bash-Scripting Guide

```
echo "WARNING: the rsync process did not entirely succeed.
echo "Something might be wrong."
echo "Saving an extra copy to $BACKUP_JUSTINCASE"
echo "WARNING: if this occurs regularly, a LOT of space will be consumed,"
echo "even though these are just hard-linked!"
fi
```

```
# Save a readme in the backup directory.
# Save another one in the recent subdirect.
echo "Backup of $SOURCE_DIR on '$hostname' was last run on \"
"date" > $BACKUP_DEST_DIR/README.txt
echo "This backup of $SOURCE_DIR on '$hostname' was created on \"
"date" > $BACKUP_DEST_DIR/backup.0/README.txt
```

```
# If we are not in a dry run, rotate the backups.
[ "$DRY_RUN" != "" ]
# Check if the backup disk is.
# Warn if 90% or 98%, we'll probably fail, so give up.
# (Note: we can count to more than one line).
We test this, rather than before
# so that rsync may possible, have a chance.
DISK_FULL_PERCENT=$(/bin/df $BACKUP_DEST_DIR | tr -d "%" | awk '{print $1}' | grep -e [0-9]+)
echo "Disk space created on backup partition \"
MOUNT_POINT=$DISK_FULL_PERCENT%
if [ $DISK_FULL_PERCENT -ge 90 ]; then
echo "WARNING: Disk space is greater than 90% full."
nfi
```

```
if [ $DISK_FULL_PERCENT -ge 98 ]; then
echo "Error: Disk is full! Giving up."
if [ "$MOUNT_LATER" == "TRUE" ]; then
# Before we exit, unmount the mount point if necessary.
cd; sudo unmount $MOUNT_POINT &&
echo "Unmounted $MOUNT_POINT again. Giving up."
nfi
exit $S_UNMOUNTED
```

```
# Create an extra backup, give up.
if [ -n "$BACKUP_JUSTINCASE" ]; then
if ! /bin/cp -al $BACKUP_DEST_DIR/backup.0 \\
$BACKUP_DEST_DIR/$BACKUP_JUSTINCASE
then
echo "ERROR: Failed to create extra copy \"
$BACKUP_DEST_DIR/$BACKUP_JUSTINCASE"
if [ "$MOUNT_LATER" == "TRUE" ]; then
# Before we exit, unmount the mount point if necessary.
cd; sudo unmount $MOUNT_POINT &&
echo "Unmounted $MOUNT_POINT again. Giving up."
fi
exit $S_UNMOUNTED
```

```
# At start of month, rotate the oldest 8.
if [ "$MONTHSTART" == "true" ]; then
echo -e "\nstart of month. \"
Removing oldest backup: $BACKUP_DEST_DIR/backup.15" $&
```

Appendix A. Contributed Scripts

685