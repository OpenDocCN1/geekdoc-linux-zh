The second method still uses a weekly full backup every Sunday. However, the rest of the week, an incremental backup runs that will back up everything that has changed since the last full backup instead of just the previous day. Using this method, the restore effort is greatly simplified because you need only the full backup tape and the last incremental backup tape. As you go through the week, the backups will get longer as the data is updated; and toward the end of the week, if a lot of the data has changed, the backup could be almost as long as a full backup.

Most UNIX backup commands implement the full/incremental backup feature using a set of dump levels, 0–9. A level 0 dump represents a full dump. Levels 1–9 are the incremental dumps that represent filesystem changes against the previous less-than or equal-to dump level.

+   - Level 0 Full dump
+   - Levels 1–9 Incremental dumps

The many backup options are available both through the Web-Based System Manager, which is started by entering the wsm command, and by using SMIT. The top-level backup and restore window for the WebBSM is shown in Figure 25-1.

![](bbox=[0.14, 0.4, 0.85, 0.88])