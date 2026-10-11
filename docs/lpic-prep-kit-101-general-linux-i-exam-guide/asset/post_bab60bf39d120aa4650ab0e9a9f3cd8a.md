
gunzip deletes the compressed file after uncompressing it. In addition, you can use the gzip command to uncompress the file by using the -d option.

You can use tar to uncompress a compressed tar archive. Do this by using the z option. So, if you type

```
tar xzvf MyArchive.tar.gz
```

all the files contained in MyArchive.tar.gz will be restored, and the compressed file will still be there because tar does not erase the original file.

## zcat

The zcat utility works like cat, except it enables you to see the contents of a compressed file. It works with files compressed using gzip (.gz extension) or compress (.Z extension). Its syntax is

```
zcat filename
```

After zcat is finished displaying the file's contents, the original file is not changed. It is still on your disk and it is still compressed.

## Summary

Planning and maintaining up-to-date backups is an important part of your job. You should take the time to plan and implement a backup strategy that is appropriate for your organization and that takes into account the cost of the backup strategy versus the cost of data loss.

For the exam, you will need to know how to use tar to create archives and restore files contained in these archives. When creating a tar file, the original files are still left in place. Use the c option to create a new tar file and x to restore the tar file. Also, t can be used to display the contents of the tar file without extracting any of its files. It is important that you be aware of possible problems related to how path names are saved to a tar file.

Another command that can be used to make backups is the cpio command. It can be used to back up or restore files, as well as to copy an entire directory hierarchy. You also will need to know how to use the compression utilities gzip, gunzip, and compress and how to use tar to compress your archives. Remember that gzip and gunzip delete the original file, whereas compress does not. tar has the capability to compress while creating the new tar file.

## QUESTIONS AND ANSWERS

- 1. Your server must be available to your users 24 hours a day, 7 days a week, but you need to add more hard disk space. What can you do?
  - A. To install another hard disk, you will have to take your server offline. However, your users still need to access the server. In this situation, you should consider having a backup server. This would enable you to work on the original server while still providing access to your users.

- 2. You have been given the job of planning the backup strategy for your Web server. What files should you back up and how often should you back them up?
  - A. You should perform a full backup including system files on a regular basis—as often as once a week. On the other days, back up only the information that changes, such as the Web pages.

- 3. You need to back up the employee database and keep the backups for five years. What would be the best way to do this?
  - A. Because this is data that needs to be kept for such a long time, you should select a medium with a shelf life greater than five years. Either CD-ROM or magneto-optical media would be good choices in this instance.

- 4. Your backup plan consists of performing a full backup every Monday and a differential backup nightly on Tuesday through Friday. Your server's hard disk fails on Thursday morning. What do you do to get the server back up as soon as possible?
  - A. First, you would restore the last full backup from Monday. Next, you would need to apply the differential backups in the same order they were made. So, after restoring Monday's full backup, you would restore Tuesday's differential backup, and then Wednesday's. The only potential data loss would be any files that were created or changed after Wednesday's backup but before the server crashed.

- 5. You want to back up your users' home directories. You decide to use the tar utility and archive them to tape. What command should you use?
  - A. You will need to tell tar what files to back up, the name of the tar file, and the device where the tar file is to be created. Therefore, you would type

    ```
    tar cfB /dev/tape 20 /directory
    ```

- 6. You need to restore a file from the backup of the home directories. How can you do this?
  - A. If you know the name of the file you want to restore, you could type
    `tar xf /dev/tape filename`
    However, if you are not sure of the filename, you can have *tar* prompt you with each filename until you find the correct one by typing
    `tar xwf /dev/tape`

- 7. You need to compress your archive to save space on your tape. How would you modify the command you created for question 5?
  - A. You could use *gzip* to compress the *tar* file after you create it. However, a more efficient way would be to *tar* and compress in one action by using *z* and typing
    `tar czfb /dev/tape 20 /directory`

- 8. You have created *tar* files of the employee database and want to store the last six months on a CD-ROM, but there is not enough space. How might you make them fit?
  - A. You should compress these files before copying them to the CD-ROM. You could use the *compress* utility, but *gzip* would be a better choice because it uses a more efficient compression algorithm.

![](img/8c0f494a2e9a2273fb49af52267f311e_291_0.png)

## PRACTICE TEST

- 1. You have been instructed to devise a backup plan that will enable you to limit downtime to an hour while limiting the expense as much as possible. The data on this server changes rarely. Which of the following would be your best choice?
  - a. Clustering
  - b. Standby server
  - c. Backup server
  - d. Back up files to a tape drive

Answer *a* is incorrect; although this would limit your downtime, it is also expensive. Answer *b* is incorrect; although this is less expensive than clustering, this is also an expensive solution. **Answer *c* is correct; because the data seldom changes, this solution would enable you to be back online within the allowed time and cost less than either clustering or a standby server.** Answer *d* is incorrect; even if you have a good backup, if the server is down because of hardware, you probably will not be back up in the allotted period of time.

- 2. You have a server that is using 2GB of disk space and need to devise a backup plan. You want to have the backup finished in as short a period of time without you having to be there to change the tapes, but it takes two tapes to hold a full backup. What would be your best strategy to ensure up-to-date backups?
  - a. Perform a full backup daily when you first get to work.
  - b. Perform a differential backup each evening.
  - c. Perform a full backup weekly and a differential backup on the other days.
  - d. Perform a full backup weekly and have users copy any files they create or modify to a floppy disk.

Answer a is incorrect; although this will give you all the files and you will be there to change the media, it can interfere with your users' work. Answer b is incorrect; although this will get all new and changed files from that day, it would be difficult and time-consuming to perform a restore. **Answer c is correct; this strategy limits the requirement that you be present to change the media every day and reduces the time required for a restore**. Answer d is incorrect; leaving backup to your users will usually result in lost data.

- 3. You use CD-ROMs to back up your system by performing a differential backup on Monday through Thursday and a full backup on Friday. Your supervisor comes to you and tells you that the employee database is corrupt. She wants to restore the version from last Thursday. What can you do?
  - a. Use `grep` to examine each CD-ROM to find the version from last Thursday.
  - b. Check your logbook to determine which CD-ROM has the correct file.
  - c. Restore the employee database from the last full backup before last Thursday and then restore it from each of the differential backups since then.
  - d. Ask the head of the Human Resources Department if she makes a copy of the database on a regular basis.

Answer a is incorrect; although you will eventually find the file you are looking for, it might take you several hours. **Answer b is correct; if you keep your logbook up to date, you will be able to find the correct CD-ROM in no time at all**. Answer c is incorrect; this will get you where you want to be but will take longer than checking the log to find the correct file. Answer d is incorrect; although she might have a copy, it is your responsibility to maintain the backups.
