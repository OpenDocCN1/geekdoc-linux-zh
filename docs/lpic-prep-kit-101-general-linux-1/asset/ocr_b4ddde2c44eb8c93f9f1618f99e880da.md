Outside conditions also can adversely affect your media, such as rodents who like to eat tapes. With time, you can expect that parts of your media will become unusable. You should routinely check your backups to ensure that you can restore these files. This includes verifying that you can restore your entire system.

Depending on what you use for backups, the method you use to restore them will vary. If you use tapes, you will want to use the same utility when restoring that you used to create the backup. If you use read-only media such as CD-ROMS or reusable media such as magneto-optical disks, your indexing process will directly affect how difficult the restoration will be. This is where your logs will save you time.

Next, we will discuss the most common utilities that are used with Linux to create backups. These are also the utilities that will be covered in the exam.

![](bbox=[0.04, 0.445, 0.11, 0.495])

# Key Concept

Backups are perishable. How long they last is dependent on the media used and the way they are stored. Keeping track of where they are stored is also important. To restore files, you must be able to find the correct backup—so keep good logs.

# Backup Utilities

Many utilities and applications are available for you to use to perform your backups. Some of these are quite elaborate and simplify configuring your backup plan. Others are basic to all Linux systems. Choose the one that makes the most sense for your situation.

# tar

The tar (tape archive) utility is used to combine multiple files into one large archive file while retaining the original directory structure. Although originally intended to create archives on a tape, tar files can be saved to any media. tar also has the capability to compress a file at the same time it creates it. Compression is covered in the section “Compressing and Uncompressing Files” later in this chapter.

# Using tar to Create Backups

When creating a tar file, you should use only relative paths. In other words, construct the path to the files you want to archive relative to where you are in the filesystem hierarchy. If your location is /home/hadden and you want to archive all the files in the /home/hadden/test directory, you should enter the path as test/\*.