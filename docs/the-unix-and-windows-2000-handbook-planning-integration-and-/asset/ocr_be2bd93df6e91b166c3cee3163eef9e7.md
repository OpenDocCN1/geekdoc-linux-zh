| Table 13.4 | Simple Backup Schedule |  |
|---|---|---|
| Sunday | Monday | Tuesday | Wednesday | Thursday | Friday | Saturday |
| Level 0 | Level 1 | Level 2 | Level 3 | Level 4 | Level 5 | Level 6 |

As you can see, this schedule employs an increasing level for each day of the week. This scheme will provide a high level of data integrity, while utilizing the least amount of archive resources. On each day except Sunday, only the previous day's changes will be archived. For some backup processes, this is called differential backup, as you are only archiving the difference between the current data and yesterday's data. While this is a resource-efficient backup process, the restoration process may be inefficient. Should an entire filesystem become corrupted after the level 6 dump, but before the next level 0, you would need to restore files from each tape, starting with the last level 0, then level 1, and so on. If restoring data quickly is a requirement of your infrastructure, this may not be the most efficient model to follow. Table 13.5 shows a different backup schedule that provides a mechanism for quicker backups, but requires more archiving resources.

In this schedule, level 0 backups are performed over the weekend, providing a backup window from 8pm Friday night until 6am Monday morning. This is useful if you have a great deal of data to back up and a 10- or 12-hour window is insufficient to archive all the data. Also, this schedule is built to only require two tapes to restore any file or filesystem. In the event of a failure, the latest weekend backup tape, along with the most current level 1 tape, will allow the administrator to reproduce the most up-to-date version of the data.

The downsides of this schedule are threefold. First, with backups running over the weekend, any data that changes won't be archived until the Monday day evening backup. If your environment is 24 × 7, this may not provide the level of data integrity your users require. Second, if a great deal of data changes over the week, the Wednesday and Thursday backups will become large and may not fit into the designated backup windows. Finally, you will notice that our backup strategy creates a 24-hour window where data can be lost. With every backup strategy, there will always be a window of risk of losing data, and your job as an administrator is to limit this risk to be as small a window as possible.

| Table 13.5 | Backup Schedule with Large Weekend Backup Window |  |
|---|---|---|
| Sunday | Monday | Tuesday | Wednesday | Thursday | Friday | Saturday |
| None | Level 1 | Level 1 | Level 1 | Level 1 | Level 0 | None |