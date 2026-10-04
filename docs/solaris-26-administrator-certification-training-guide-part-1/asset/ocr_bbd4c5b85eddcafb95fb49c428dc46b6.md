level 9 dumps. The automated dumps are performed at 4:30 a.m., a time when most systems typically are idle. Automated daily dumps are performed Sunday through Friday mornings. Automated weekly dumps are performed on Saturday mornings. Backups are automated by creating a shell script and using cron to execute the script on a regular basis.

Table 11-7 shows the dump level performed on each day of a typical month. Note that the level 0 dump at the start of the month is performed manually, because the entire system must be idle before you can back up the root file system. One way to ensure that the system is not being used is to take the system into single-user mode. The level 9 and 5 dumps are automated with cron, but also must be conducted when the file systems are not being used.

# Table 11-7 File System Dump Schedule

| | Floating | Monday | Tuesday | Wednesday | Thursday | Friday |
|---|---|---|---|---|---|---|
| 1st of month | 0 | | | | | |
| Week 1 | | 9 | 9 | 9 | 9 | 5 |
| Week 2 | | 9 | 9 | 9 | 9 | 5 |
| Week 3 | | 9 | 9 | 9 | 9 | 5 |
| Week 4 | | 9 | 9 | 9 | 9 | 5 |

The backup schedule in Table 11-7 performs the following:

+   - Each weekday tape accumulates all files changed since the end of the previous week or the initial level 0 for the first week. All files that have changed since the lower-level backup at the end of the previous week are saved each day.
- Each Friday's tape contains all files changed since the last level 0.

This dump schedule requires at least four sets of five tapes, one set for each week and one tape for the level 0 dump. Each set will be rotated each month. The level 0 tapes should not be overwritten and should be saved for at least one year.

Be aware that even with the backup schedule outlined in Table 11-7, data can still be lost. If a hard disk fails at 3 p.m., all modifications since the 4:30 a.m. backup will be lost. Also, files that were deleted mid-week will not appear on the level 5 tapes. Sometimes a user accidentally deletes a file and does not realize it for several weeks. When the user wants to use the file, it is not there. If he asks you to restore it from backup, the only tape it appears on is the level 0, and it could be too far out of date to be useful. If you don't overwrite the daily level 9 tapes so frequently, you can minimize this problem.