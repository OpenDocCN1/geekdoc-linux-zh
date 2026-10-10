
5. You type `mkdir one/two/three` and receive an *error message* that reads, `No such file or directory.` What can you do to overcome this problem? (Select all that apply.)

- A. Add the `--parents` parameter to the `mkdir` command.
- B. Issue three separate `mkdir` commands: `mkdir one`, then `mkdir one/two`, and then `mkdir one/two/three`.
- C. Type `touch /bin/mkdir` to be sure the `mkdir` program file exists.
- D. Type `rmdir one` to clear away the interfering base of the desired new directory tree.

6. Which of the following commands are commonly used to create archive files? (Select all that apply.)

- A. `restore`
- B. `tar`
- C. `tape`
- D. `cpio`

7. You’ve received a tarball called `data79.tar` from a colleague, but you want to check the names of the files it contains before extracting them. Which of the following commands would you use to do this?

- A. `tar uvf data79.tar`
- B. `tar cvf data79.tar`
- C. `tar xvf data79.tar`
- D. `tar tvf data79.tar`

8. You want to create a link from your home directory on your hard disk to a directory on a CD-ROM drive. Which of the following types of links might you use?

- A. Only a symbolic link.
- B. Only a hard link.
- C. Either a symbolic or a hard link.
- D. None of the above; such links aren’t possible under Linux.

9. What command would you type (as root) to change the ownership of `somefile.txt` from ralph to tony?

- A. `chown ralph:tony somefile.txt`
- B. `chmod somefile.txt tony`
- C. `chown somefile.txt tony`
- D. `chown tony somefile.txt`

10. Typing `ls -ld wonderjaye` reveals a symbolic file mode of `drwxr-xr-x.` Which of the following are true? (Select all that apply.)

- A. `wonderjaye` is a symbolic link.
- B. `wonderjaye` is an executable program.
- C. `wonderjaye` is a directory.
- D. `wonderjaye` may be read by all users of the system.

11. When should programs be configured SUID root?

- A. At all times; this permission is required for executable programs.
- B. Whenever a program should be able to access a device file.
- C. Only when they require root privileges to do their job.
- D. Never; this permission is a severe security risk.

12. Which of the following commands would you type to enable world read across access to the file myfile.txt? (Assume that you're the owner of myfile.txt.)

- A. chmod 741 myfile.txt
- B. chmod 0640 myfile.txt
- C. chmod u+r myfile.txt
- D. chmod o+r myfile.txt

13. Which of the following umask values will result in files with rw-r----- permissions?

- A. 640
- B. 210
- C. 022
- D. 027

14. You see the usrquota and grpquota options in the /etc/fstab entry for a filesystem. What is the consequence of these entries?

- A. Quota support will be available if it's compiled into the kernel; it will be automatically activated when you mount the filesystem.
- B. Quota support will be available if it's compiled into your kernel, but you must activate it with the quotaon command.
- C. Quota support will be disabled on the filesystem in question unless you activate it with the quotaon command.
- D. Nothing; these options are malformed and so will have no effect.

15. Which of the following commands can be used to summarize the quota information about all filesystems?

- A. repquota
- B. repquota -a
- C. quotacheck
- D. quotacheck -a

16. You've installed a commercial spreadsheet program called WonderCalc on a workstation. In which of the following directories are you most likely to find the program executable file?

- A. /usr/sbin
- B. /etc/X11
- C. /bin
- D. /opt/wcalc/bin

17. Which of the following file-location commands is likely to take the *most* time to find a file that may be located anywhere on the computer (assuming the operation succeeds)?

- A. The **find** command.
- B. The **locate** command.
- C. The **whereis** command.
- D. They're all equal in speed.

18. What can the **type** command do that **whereis** can't do?

- A. Identify the command as being for **x86** or **x86-64** CPUs
- B. Locate commands based on their intended purpose, not just by name
- C. Identify a command as an alias, internal command, or external command
- D. Assist in typing a command by finishing typing it for you

19. You want to track down all the files in **/home** that are owned by **karen**. Which of the following commands will do the job?

- A. **find** **/home** -uid **karen**
- B. **find** **/home** -user **karen**
- C. **locate** **/home** -username **karen**
- D. **locate** **/home** **karen**

20. What can you conclude from the following interaction?

```
$ which man
/usr/bin/man
```

- A. The only file called man on the system is in /usr/bin.
- B. The /usr/bin/man program was installed by system package tools.
- C. The /usr/bin/man program will be run by any user who types man.
- D. The first instance of the man program, in path search order, is in /usr/bin.

## Answers to Review Questions

- 1. B. The mount command takes a device filename first and a mount point second, so option B is correct. There is no need for special mount point preparation, as option A implies, other than the existence of the mount point directory. Contrary to option C, /dev/cdrom is often a valid device file for CD-ROMs (or more precisely, a symbolic link to a valid device file). Furthermore, the error message mentions /media/cdrom, not /dev/cdrom. Defective CD-ROMs and drives can certainly cause problems, as option D implies, but this error message refers to block devices, suggesting the problem is one of Linux configuration, not media viability.

- 2. A, D. A mount directory must be specified between the device entry (/dev/hda8) and the filesystem type code (nfs). The nfs filesystem type code may only be used with an NFS export specification of the form *server:/export* as the device specification. Fields in /etc/fstab are separated by spaces or tabs, not commas (but commas are used between individual options if several options are specified in the options column). The default option may be used with any filesystem type.

- 3. A. The -l parameter produces a long listing, including file sizes. The -a parameter produces a listing of all files in a directory, including the dot files. Combining the two produces the desired information (along with information about other files). The -p, -R, and -d options don't have the specified effects.

- 4. D. When moving from one partition or disk to another, we must necessarily read and copy the file and then delete the original if that copy was successful. If both filesystems support ownership and permissions, they'll be preserved; you don't need an explicit --preserve option to do this, and this preservation does not rely on having exactly the same filesystem types. Although mv doesn't physically rewrite data when moving within a single low-level filesystem, this approach can't work when you're copying to a separate low-level filesystem (such as from a hard disk to a pen drive); if the data isn't written to the new location, it won't be accessible should the disk be inserted in another computer.

- 5. A, B. If you try to create a directory inside a directory that doesn't exist, mkdir responds with a No such file or directory error. The --parents parameter tells mkdir to automatically create all necessary parent directories in such situations. You can also manually do this by creating each necessary directory separately; (it's possible that mkdir one wouldn't be necessary in this example if the directory one already existed. No harm will come from trying to create a directory that already exists, although mkdir will return a File exists error.)

- 6. B, D. The tar and cpio programs are common Linux archive-creation utilities. The restore command restores (but does not back up) data; its backup counterpart command is dump, but dump is no longer a recommended backup tool on Linux. There is no standard tape command in Linux.

- 7. D. With the tar utility, the --list (t) command is used to read the archive and display its contents. The --verbose (v) option creates a verbose file listing, and --file (f) specifies the filename—data79.tar in this case. Option D uses all of these features. Options A, B, and C all substitute other commands for --list, which is required by the question.
