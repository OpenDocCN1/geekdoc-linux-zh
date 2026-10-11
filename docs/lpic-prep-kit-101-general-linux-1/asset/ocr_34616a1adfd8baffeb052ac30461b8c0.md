+   □ Type of backup made
+   □ What filesystem was backed up
+   □ Where the backup media is stored

This log will assist you when you need to restore a file. Where you keep the log is up to you. You can keep the log with the media itself or next to the server. To further improve your ability to recover from a disaster, consider keeping a copy of your log in both locations.

# ### Restoring Files from Backup

Even though you have a backup plan implemented, you still are not done. The backups you make are worthless unless you can retrieve that information. Don’t wait until you have a system crash or a user comes to you needing a file restored to find out whether your restore works.

If you perform a full backup every day, restoring your system will consist of restoring the last backup you made. If you are using the backup plan shown in Figure 11.1, your restoration plan will be more complex than if you did a full backup every day.

If you have a file called MyFile, it will be backed up every Friday. As shown in Figure 11.2, the file MyFile was changed on Monday and Wednesday, so it also was backed up on those days.

![](bbox=[0.3, 0.6, 0.8, 0.67])

# **Figure 11.2**

> When doing differential backups, only files that were changed are backed up. When using differential backups to restore, you must restore the backups in the order that they were made.

If your system crashes on Thursday, to restore it you would first need to restore the full backup from the previous Friday. Then, you would need to apply each differential backup that had been made since then in the order they were made. So, you would need to restore Monday’s tape, then Tuesday’s tape, and finally Wednesday’s tape. This would ensure that the latest version of all files would be restored.

A lot of things can go awry with your backups without you knowing about it. For example, your media might go bad. When you reuse your media, it suffers wear and tear.