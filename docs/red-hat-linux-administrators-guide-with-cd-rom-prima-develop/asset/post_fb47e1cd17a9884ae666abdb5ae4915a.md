
load is at its lightest. This is recommended in part to avoid conflicts with any programs to which users might need access during the day and because most system resources will be free to accomplish the scheduled task quickly. If a cron job is to delete older files or rotate log files, it is best to accomplish such tasks when no user is actively accessing the system or changing files while cron is manipulating them.

The cron daemon itself takes up a few of the system's resources. However, depending on the type of program it executes, cron can either place a heavy load on the system or run silently without any user noticing its presence. Some routines can be run at any time of the day without causing any problems or slowdowns. If the routines handle simple backup and maintenance tasks that do not affect user files, you can schedule them for most any time without dire consequences. Tasks such as incremental or differential backups are safe to execute in early evening hours, whereas full backups are best left to a late night run. Try to avoid doing any automated tasks at peak hours. Any program that changes or updates system or user files during the day runs the risk of conflicting with user tasks. You can find more information on backups in Chapter 9, “Fixing Mistakes.”

## Managing crontab files

The file that controls the cron daemon is called the crontab, or cron table file. It is a simple binary in the same location as most other binary files in Red Hat Linux, `/usr/bin/`. This executable creates the ASCII text file in which tasks are subsequently saved. These can be unique pathnames to other files, which are executable or files that contain multiple scripts which the system then runs. To execute the crontab command and edit your selection of files to run, you usually type the following:

```
crontab -e
```

The -e flag launches crontab into edit mode. The crontab file will apply only to the files associated with the user who started up the file; these files include not only those that the user owns but those to which he or she has access. The default editor is defined by the system. Red Hat Linux uses vi as its default editor.

If I execute this command as myself or under the username `kerry`, I will create a cron table for my own use. However, root or superuser can create or edit a crontab file for any other user, including root, by simply placing a -u flag followed by the username. If I, as root, still wanted to edit my crontab file, I would type the following command:

```
crontab -u kerry -e
```

This would bring up the crontab file created by the user *kerry*.

Though root can edit anyone else’s file, regular users can only edit their own file. The *fields* and programs executed within the crontab file vary from user to user, but all users still must adhere to the same syntax that govern normal usage on any Linux machine. They can work only with files and directories that they either own directly or for which they share group ownership.

The *file* created by the *crontab* command is a simple *text file* that is kept in the */var/spool/cron* directory. Each respective crontab file is both owned and named after the user who created it.

If the users *kerry* and *root* both create a crontab file, a quick glance in the */var/spool/cron* directory will show that there are now two files, one for each user. However, Red Hat Linux prohibits regular users from viewing the contents of these files. Only *superuser* can view the contents of its own and others’ files.

As the following output shows, *root* can view the contents of the */var/spool/cron* directory. Though the file *kerry* is owned by the group *kerry*, it allows only read and write permissions to the user, which is *root*. The same applies to the contents of the entire directory. Only *root* has read, write, and execute permissions.

```bash
# pwd
/var/spool/cron
# ls -la
total 16k
drwx------    2 root     root    4.0k Sep  2 14:05 .
drwxr-xr-x   19 root     root    4.0k Jun  8 13:49 ..
-rw-------     1 root     kerry   216 Sep  2 14:05 kerry
-rw-------     1 root     root    498 Aug  16 09:17 root
```

Though you can view each file with any text editor, it is recommended that you use the crontab command to edit the file and not do so manually. If you were to use vi and open the file manually, a warning message will state that you should configure the file only by using the crontab -e command. The crontab command creates the simple text file in /var/spool/cron, named after the same user who issued the command. In addition, the temporary file that is produced when you initially create the crontab file is kept in the /tmp directory until you save the crontab file. When you use the command, crontab -e, to open up the text file, you will also notice that at the same time a temporary file named crontab.xxxx is inserted in the /tmp directory. There is little chance any other users will be able to view the file’s contents since the permissions are set at 600 and is owned exclusively by that user executing the file.

**NOTE**

The crontab program operates much like sudo. You can technically open the /etc/sudoers file much like the /var/spool/cron/root file, but you are advised not to do so. Much as the configuration file should only be opened with the visudo command, the crontab file should only be opened with the crontab command.

Usually each user gets one cron file. If allowed, each user on the system can create his or her own crontab file and use it to manage tasks. The corresponding text file carries the owner’s username. If you are migrating users from one Linux machine to another, you should also transfer the respective crontab files because much of the user’s functionality on the new system will be based in its ability to run automated tasks via cron.

The best way to move a crontab file is simply to use ftp to send those files from the /var/spool/cron directory into the same location on a new machine. Be sure to set the permissions for each file to those of the previous owner. If FTP is not set up yet, you can alternatively use the tar command to back up the files into one large file and then manually move it to the new system. For more information on using the tar command and backing up files, see Chapter 9.

In addition to those crontab files used by regular users, there are also crontab files that the system uses. These are predetermined by each Linux release, since each version adds utilities that require automated maintenance. The file that lists what jobs are normally executed by the system on a regular basis is usually /etc/crontab. Here you edit the tasks the system performs and specify when cron will execute those duties. Listing 8.1 shows sample output from a standard Red Hat Linux install.

**Listing 8.1 A Typical `/etc/crontab` File Used by the System for Regular Maintenance**

```
SHELL=/bin/bash
PATH=/sbin/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

The list of environment variables that appears at the beginning of the output is one of the added features that come with the Vixie Cron package. You specify the shell, path, and home directory for each of these tasks, and stipulate who receives via e-mail the results of the crontab run after the task is either successfully or unsuccessfully carried out. Each entry as listed in the /etc/crontab file points to a certain file that contains additional scripts. If you want the system to run a definitive task at a specified time, here is where you can also enter the script or modify an existing one to your liking. Users who prefer to rotate their log files at shorter intervals can find this specific system task in this location as well.

> **CAUTION**
> 
> Bear in mind that any additions to these files will affect the system globally, whereas each user's crontab entries affect only the individual's files. Exercise caution when changing system files. If you break something, certain logs and files may stop working. As a precautionary measure, always make a backup before changing any system file.

**Editing crontab Files**

If you need to remove the cron files of a particular user, simply deleting the user's file from the /var/spool/cron directory is normally sufficient. This is useful if the user is no longer present on the system or if you need to lock his or her account.
