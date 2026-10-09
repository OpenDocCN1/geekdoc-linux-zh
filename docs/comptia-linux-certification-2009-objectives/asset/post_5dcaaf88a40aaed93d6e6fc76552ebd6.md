
## The restore Command

The *restore* command enables you to restore files or filesystems from backups made using the `dump` command. This command can be used across networks to restore data. Specific data can also be restored using the options of the *restore* command.

The following table describes common *restore* command options.

| Option | Enables You To |
| :--- | :--- |
| `-C` | Compare the backup file with the source file. |
| `-i` | Run the *restore* command in restore mode to restore backups partially. |
| `-r` | Perform a complete recovery of the backed up files. |
| `-f /Location of the backup file` | Specify the location of the backup file. |

### Volume Number

While making backups of large files on removable storage devices, such as tape drives, the total size of the files will be split into smaller volumes and stored in multiple tape drives with each tape drive identified by a specific volume number. When you want to restore the backup made on multiple volumes, specify the volume number starting from the last volume number to the first volume number. The hard disk, because it is a single volume, will always have the volume number 1.

### Restoring Files with the tar Command

The command `tar -xvf` will restore the entire contents of the source file or directory structure. To restore a portion of a tar file, use the path and name of the file you wish to extract. You must use the exact path and name that was used when you created the tar file. You can also make restores interactive by using the command `tar -wxvf [destination] [source].`

### Restoring Files with the cpio Command

The main reason you need to back up data is so that you can retrieve the data if the file gets corrupted or deleted. If you use the `cpio` command to move files to another location, you will need to get the files out of the archive file so that you can use them. The format of the copy-in option is `cpio -icdv < archive_file_name>`.

## How to Back Up and Restore Files

**Procedure Reference: Archive Using the dump Command**

To archive using the `dump` command:

- 1. Log in as root in the CLI.
- 2. Enter `dump -0 -f {target file} {source file}` to make a complete backup.
- 3. Enter `dump -{(Hanoi Sequence)} -f {target file} {source file}` to add updates to the existing backup file.

**Procedure Reference: Back Up Files Using the tar and gzip Commands**

To back up files using the `tar` and `gzip` commands:

- 1. Determine the files you want to back up and put them in a directory.
- 2. Group all the files using the `tar` command.
- 3. Compress the tar file using the `gzip` command.
- 4. Save the file in another location (FTP site, CD, DVD, tape, floppy disk, and so on).

**Procedure Reference: Restore Backups Using the restore Command**

To fully restore the backups:

- 1. Log in as root in the CLI.
- 2. Navigate to the directory where you want to restore backed up files.
- 3. Restore backups.
  - Enter `restore -rf /{location of the backup file}` to restore a backup taken using the `dump` command.

**Procedure Reference: Restore Files from a Backup Using the gzip and tar Commands**

To restore files from a backup using the `tar` and `gzip` commands:

- 1. Copy the files from your backup location (FTP site, CD, DVD, tape, floppy disk, and so on).
- 2. Unzip the files using the `gzip` command.
- 3. Untar the files using the `tar` command.
- 4. If needed, move the individual saved files back to their respective locations.

# ACTIVITY 4-6
Performing Backups

### Before You Begin:

- 1. You have logged in as root in the CLI.
- 2. Enter `mkdir Reports` to create the Reports directory in the root directory.
- 3. Enter `cd Reports` to navigate to the `/root/Reports` directory.
- 4. Enter `vi project` to create the project file to store the project data.
- 5. Save and close the file.
- 6. Enter `clear`.

### Scenario:

Your colleague, Chris, is working on a very important project, and he wants to make a daily backup of his system. He also wants a reminder to be set to create backups whenever he logs in to his system.

All project-related files are in the `/root` directory and they need to be saved as `project_backup` in the `/tmp` directory.

Account information:

- Login name for the root user: root
- Password for the root user: `p@ssw0rd`

### What You Do
How You Do It

- 1. Make a backup of /root files in the /tmp directory.
  - a. Enter `dump -0 -f /tmp/project_backup /root` to make a complete backup.
  - b. Observe that the message "DUMP : DUMP IS DONE" is displayed in the last line indicating that the backup was successful.
  - c. Enter `clear` to clear the terminal screen.
  - d. Enter `bzip2 /tmp/project_backup` to compress the backup file.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_197_0.png)

Compressing the backup file may take a few minutes.

- 2. Set a reminder during system login to perform backups.
  - a. Enter `vi /etc/issue`
  - b. Press **Shift+G** to navigate to the end of the file.
  - c. Press **O** to shift to a new line.
  - d. Type *Welcome to Linux! Remember to Backup Your Project Data*
  - e. Press **Esc**.
  - f. Save and close the file.

- 3. Verify that the reminder is displayed when the user logs in the next time.
  - a. Enter `logout` to verify that the reminder is displayed.
  - b. Observe that the message “Welcome to Linux! Remember to Backup Your Project Data” is displayed.
  - c. Log in as the **root** user.

## ACTIVITY 4-7
Restoring Backup Data

- **Before You Begin:**
  - 1. You are logged in as root in the CLI.
  - 2. Open the /etc/issue file in the text editor and remove the last line that reminds the user to backup project data. Save the file and close the editor.
  - 3. Log out of the CLI. Log in as root in the CLI.
  - 4. Enter `rm -rf /root/Reports`.
  - 5. Enter `clear` to clear the terminal screen.

**Scenario:**

You observe that some of your project files are missing from the Reports directory. Because you make a daily backup of your work, you decide to restore the missing files from the backup. The backup file is available in the /tmp/project_backup.bz2 location.

| **What You Do** | **How You Do It** |
|---|---|
| 1. Identify the missing directory and files. | a. Enter `bunzip2 /tmp/project_backup.bz2` to decompress the file.<br><br>b. Enter `restore -C -f /tmp/project_backup` to view the missing directory and files.<br><br>c. Enter `clear` to clear the terminal screen. |

* Step 1a may take a few minutes.

- 2. Switch to the restore mode.
  - a. Enter `cd /`
  - b. Enter `restore -i -f /tmp/project_backup` to switch to the restore mode.
  - c. At the restore prompt, enter `cd root`

- 3. Extract missing files.
  - a. Enter `add Reports/` to add the directory that needs to be restored.
  - b. Enter `extract` to extract the directory from the backup file.
  - c. Enter `1` to specify the volume number.
  - d. Enter `y` to accept the default owner or mode of the files to be extracted.
  - e. Enter `quit` to quit the restore mode.
  - f. Enter `ls /root/Reports` to check if the Reports directory has been restored.
  - g. Observe that the project file has been restored.
  - h. Enter `clear` to clear the terminal screen.
  - i. Enter `logout`

![](img/477ccb2f05b6ba1b2d563ea74f18c197_200_0.png)

# TOPIC E

# Manage Databases Using MySQL

You worked with files in a Linux filesystem. You may need to store data in a format that will allow you to easily retrieve it when required; a database will serve this purpose. In this topic, you will work with MySQL.

A text file can store volumes of data, but retrieving it will be a problem because you may have to manually locate the information you are looking for. Databases, such as MySQL, allow you to store data in an organized manner, which enables efficient retrieval of specific data. This will save you time and effort.

# Databases

![](img/477ccb2f05b6ba1b2d563ea74f18c197_201_0.png)

**Definition:**

*A database* is an organized collection of information. It is used to facilitate easy storage and retrieval of data. In a database, data may be grouped into a series of records, which can be further organized into smaller segments of data called *fields*. A table is the basic storage unit of a database and it consists of rows and columns. The model of a database decides the way the data is organized in it.

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_201_1.png)

Figure 4-20: A database consisting of two tables.
