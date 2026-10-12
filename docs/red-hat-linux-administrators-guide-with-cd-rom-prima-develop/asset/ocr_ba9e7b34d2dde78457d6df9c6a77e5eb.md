The at command is very useful for periodic use or when a single request needs to be executed. For more repetitive commands or redundant backups, the cron command is probably preferable.

One of the disadvantages to automated backups is that they leave the machines unattended and, if access to the servers is still fairly unrestricted, anyone with the proper clearance can seize the backup tape when it is completed. Though it seems juvenile or paranoid to suggest that you might not be able to trust your own coworkers, abuses have been known to happen. Someone might not have direct access to certain files on the system but could easily gain them if he or she grabs a backup tape or other backup media. Treat the media the same as you would the servers. Just because they are on tape, CD, or some other media source, that does not mean someone cannot extract the information just as easily or quickly.

Once you have decided how and when to perform backups, set up a schedule specifying when it is best to do the complete backup first and then the incremental backups.

Here is a sample schedule from my own routine that might be used as a template for others:

+   Sunday evening
+   * Full Backup (Level 0)
+   * Automated at 11 P.M.
+   
+   Tuesday morning
+   * Incremental Backup
+   * at job at 6 A.M.
+   
+   Wednesday morning
+   * Incremental Backup (Level 1)
+   * at job at 6 A.M.
+   
+   Thursday morning
+   * Incremental Backup (Level 1)
+   * at job at 6 A.M.