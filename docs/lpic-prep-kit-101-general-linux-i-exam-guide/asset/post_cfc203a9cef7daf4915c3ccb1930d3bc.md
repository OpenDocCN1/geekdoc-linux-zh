
## Permissions for umask

| Value | Permission |
| :--- | :--- |
| 0 | read, write for files; read, write, execute for directory |
| 1 | read, write for files and directories |
| 2 | read for files; read, execute for directories |
| 3 | read for files and directories |
| 4 | write for files; write, execute for directories |
| 5 | write for files and directories |
| 6 | execute for files and directories |
| 7 | no permissions |

Notice that the numbers used for setting permissions and the numbers used for defining a umask do not have the same meaning.

So, if the umask is 002, the permissions on all the new files would be owner, with group having read and write permissions (00) and everyone else having read (2). If you performed an ls -l command to examine the permission block on the newly created file, it would be rw-rw-r--.

For new directories, the permissions would be owner and group read, write, and execute (00), with all others read and execute (2). The permission block on a newly created directory would be rwxrwxr-x.

> **Key Concept**
> You can see that the numbers used for setting permissions using the chmod command and for setting permissions using umask are not the same. A umask of 002 is the same as using chmod 662 for a file or chmod 775 for a directory.

If you want to change your umask value, issue the umask command followed by the permission level you want to define. So, if you want the permissions to be rw-r---- on files and rwxr-x-- on directories, enter the following:

```
umask 027
```

This will temporarily change your mask. After you log off and log on again, the prior setting will return. To make this change permanent, add the previous command to your startup file. Only root can change the system umask value. See Chapter 7 for more information on using your startup files to manage your environment.

## Summary

Permissions are an essential part of managing your system. They enable you to control who gets to access what. The possible permissions are read, write, and execute. For the exam, you need to understand what each permission allows the user to do whether applied to a file or a directory.

The permission block is the first 10 characters that are displayed when issuing the ls -1 command. The first character designates the file type; the next three are the permissions for the owner; the next three after that are the permissions for the group; and the last three are the permissions for user. These permissions are then applied to one of three entities: owner, group, or user. You can change these permissions through the use of the chmod command. Permissions can be changed using either symbols or numbers.

To change the owner of a file or directory, use the chown command. Use either chown or chgrp to change the group associated with a file. The set UID (SUID) and set GID (SGID) are two special permissions that also can be applied. SUID allows an executable to be executed with another user’s permissions instead of those of the user running the executable. The SGID works the same way, except it allows the permissions of another group rather than another user.

Another special permission is the sticky bit. This assists in the management of world-writable directories. It also can be used to improve application execution. In addition, you need to understand what the umask is and how to correctly set it. Default permissions for all newly created files are defined by the system umask value. A user-specific umask also can be defined.

![](img/8c0f494a2e9a2273fb49af52267f311e_239_0.png)

## QUESTIONS AND ANSWERS

- **1. How can a file owner change ownership of files?**
  A. A user cannot change the ownership of her files. Only root can do this. Using `chown` while logged in as root, you will need to change the ownership of the files.

- **2. You have a directory of files containing payroll information that you want to share with other employees in the payroll department. As the system administrator, what would be the best way to do this?**
  A. Use the `chgrp` command and change the group for all the files in the directory to the payroll group. If there are subdirectories, you should use the `-R` option to recursively change the group on all the files. Then, set the permissions for the payroll group appropriately using the `chmod` command.

- **3. You have a new employee, Mary, who replaced Bill. How can you give Bill’s files and directories in the /data/bill1 directory to Mary?**
  A. You will need to change the ownership of the files and directories using the `chown` command with the `-R` option. Then, make sure that Mary is a member of the appropriate groups.

- **4. One of the accounting department’s directories contains information that should be changed only by the head accountant but should be readable by all accounting employees. How do you set the permissions?**
  A. You will want to make the head accountant the owner of the directory and its files. Put all the accounting employees in an accounting group. Set the permissions on the directory for the owner read, write, and execute; the group read and execute; and all others no permissions (`rwxr-x---`). Then, set the permissions on the files for the owner read and write; the group read; and all others no permissions (`rw-r-----`).

- **5. How do you set the permission block on the employee evaluation files so that only the HR director can read or change them?**
  A. Put all the employee evaluation files in a single directory. Make the director of the Human Resources Department the owner of the directory and its files. Then, set the permissions so that the director has read, write, and execute on the directory and read and write on the files. Deny all access to everyone else, including the group.

- **6. All the salespeople save their quotes to a directory called /sales/quotes. Some of them have complained to you that files are being lost. How could you address this problem?**
  A. Set the permissions on the /sales/quotes directory so that the owner and the sales group have read, write, and execute permissions. The permissions on the files for the owner and sales group should be read and write. Deny any access to everyone else. This will keep the files accessible to only the sales group; however, anyone will be able to delete any file. You also should set the sticky bit so that only the owner of a file can delete it.

- **7. You have a user who tells you that every time he creates a new file it has its permissions set as -rw-rw-r--. He wants the new permissions to be -rw-r-----. How can you configure his settings to make this happen?**
  A. The user's umask is 002, which sets the permissions on all newly created files for owner and group to have read and write and all others to read. You will need to change his umask to 022, which will give the owner read and write, and group and others read-only permissions on newly created files. To make this change permanent, this setting will have to be added to the user's startup files.

## PRACTICE TEST

1. The directory /home/bill/letters has a permission block of drwxrw-r-., the owner is Bill, and the group is wp. Mary is a member of the accounting and payroll groups. What would Mary be able to do in this directory?
   - a. Make the /home/bill/letters directory her working directory.
   - b. List the contents of the /home/bill/letters directory.
   - c. Save a file to the /home/bill/letters directory.
   - d. Delete files contained in the /home/bill/letters directory.

   Answer a is incorrect; Mary would need the execute permission to make /home/bill/letters her working directory. **Answer b is correct; the read permission gives Mary permission to list the contents of the /home/bill/letters directory.** Answer c is incorrect; Mary would need the write permission to save a file to this directory. Answer d is incorrect; to delete files in the /home/bill/letters directory, Mary would need the write permission.

2. To give Mary permission to save a file to the /home/bill/letters directory, you would need to
   - a. Make Mary the owner of the directory.
   - b. Make Mary a member of the wp group.
   - c. Change the permissions on the directory to drwxrw-rw..
   - d. Explicitly give Mary read and write permission to the /home/bill/letters directory.

   Answer a is incorrect; although this would allow Mary to save a file to the /home/bill/letters directory, it would take away Bill's permissions as owner. **Answer b is correct; by making Mary a member of the wp group, she would be granted the permissions defined for the group—which are read and write, allowing her to save a file to the directory.** Answer c is incorrect; this would give Mary the needed permissions but would also grant these permissions to everyone else. Answer d is incorrect; you cannot explicitly give permissions to a single individual, only to the owner, the group, or others.

3. Bill has retired and has been replaced by Arthur. How can you transfer Bill's files to Arthur?
   - a. chgrp -R arthur /home/bill
   - b. chmod o+rxw /home/bill
   - c. chown arthur /home/bill
   - d. chown -R arthur /home/bill
