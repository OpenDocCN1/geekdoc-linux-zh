# QUESTIONS AND ANSWERS

1. Your server must be available to your users 24 hours a day, 7 days a week, but you need to add more hard disk space. What can you do?

A. To install another hard disk, you will have to take your server offline. However, your users still need to access the server. In this situation, you should consider having a backup server. This would enable you to work on the original server while still providing access to your users.

2. You have been given the job of planning the backup strategy for your Web server. What files should you back up and how often should you back them up?

A. You should perform a full backup including system files on a regular basis— as often as once a week. On the other days, back up only the information that changes, such as the Web pages.

3. You need to back up the employee database and keep the backups for five years. What would be the best way to do this?

A. Because this is data that needs to be kept for such a long time, you should select a medium with a shelf life greater than five years. Either CD-ROM or magneto-optical media would be good choices in this instance.

4. Your backup plan consists of performing a full backup every Monday and a dif-ferential backup nightly on Tuesday through Friday. Your server's hard disk fails on Thursday morning. What do you do to get the server back up as soon as possible?

A. First, you would restore the last full backup from Monday. Next, you would need to apply the differential backups in the same order they were made. So, after restoring Monday's full backup, you would restore Tuesday's differential backup, and then Wednesday's. The only potential data loss would be any files that were created or changed after Wednesday's backup but before the server crashed.

5. You want to back up your users' home directories. You decide to use the tar utility and archive them to tape. What command should you use?

A. You will need to tell tar what files to back up, the name of the tar file, and the device where the tar file is to be created. Therefore, you would type

```
```
tar cfb /dev/tape 20 /directory
```
```