The frequency of the backups in this type of operation can depend in some part on the activity in the database. Here are some guidelines that may help you determine your backup schedule.

| Category | Guideline |
| :--- | :--- |
| Small database | If the database is small, perform a full offline backup every night. This will offer the most protection possible for your data. |
| Large database | If the database is very large but infrequently modified, perform a full offline backup every weekend and incremental backups during the week. |
| Active tablespaces | If certain tablespaces are very active, target them for frequent tablespace backups. |
| Structural changes | Anytime a structural change is made to the database, you should perform a full offline backup. |
| Unrecoverable operations | Anytime unrecoverable operations are performed on the database, a full offline backup should be done. |
| Resetlogs | Anytime that you have to reset the redo logs with the resetlogs command, you should perform a full offline backup. |
| Recover until | Anytime you have recovered with the recovery UNTIL option, you should perform a full offline backup. |
| Archive log files | Every night, back up the archive log files. The frequency depends on the number of archive log files created every day. |

These are a few guidelines that may help you to determine an effective backup strategy for your system.

# ### Scheduling Backups in a 7x24 Shop

The 7x24 shop is much more difficult to plan a backup strategy for, since there is never a time when the system is not in use. Whenever you perform the backups, there will be one or more people that may be inconvenienced by a performance drop. Backups do tend to degrade performance.

The frequency and type of backups will be influenced by the activity of the system. Here are some guidelines that may help you determine your backup schedule.