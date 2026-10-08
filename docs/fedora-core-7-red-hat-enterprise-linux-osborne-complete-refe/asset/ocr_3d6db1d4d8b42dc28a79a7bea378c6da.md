# Anonyomous FTP Server Directories

As previously noted, the FTP home directory is named **ftp** and is placed in the *var* directory. When users log in anonymously, they are placed in this directory. An important part of protecting your system is preventing remote users from using any commands or programs not in the restricted directories. For example, you would not let a user use your **ls** command to list filenames, because **ls** is located in your *bin* directory. At the same time, you want to let the FTP user list filenames using an **ls** command. Never FTP daemons like vsftpd and ProFTPD solve this problem by creating secure access to needed system commands and files, while restricting remote users to only the FTP site's directories. In any event, make sure that the FTP home directory is owned by the root user, not by the FTP user. Use the **ls -d** command to check on the ownership of the FTP directory.

```
```bash
# ls -d /var/ftp
```
```

To change a directory's ownership, you use the **chown** command, as shown in this example:

```
```bash
# chown root.root /var/ftp
```
```

Another, more traditional, solution is to create copies of certain system directories and files needed by remote users and to place them in the *ftp* directory where users can access them. A **bin** directory is placed in the *ftp* directory and remote users are restricted to it, instead of the system's **bin** directory. Whenever they use the **ls** command, remote users are using the one in *ftp/bin*, not the one you use in */bin*. If, for some reason, you set up the anonymous FTP directories yourself, you must use the **chmod** command to change the access permissions for the directories so that remote users cannot access the rest of your system. Create an *ftp* directory and use the **chmod** command with the permission 555 to turn off write access: **chmod 555 ftp**. Next, make a new **bin** directory in the *ftp* directory, and then make a copy of the **ls** command and place it in *ftp/bin*. Do this for any commands you want to make available to FTP users. Then create an *ftp/etc* directory to hold a copy of your **passwd** and **group** files. Again, the idea is to prevent any access to the original files in the *etc* directory by FTP users. The *ftp/etc/passwd* file should be edited to remove any entries for regular users on your system. All other users should have their passwords set to **x** to block access. For the **group** file, remove all user groups and set all passwords to **x**. Create an *ftp/lib* directory, and then make copies of the libraries you need to run the commands you placed in the **bin** directory.

# Anonyomous FTP Files

A directory named **pub**, located in the FTP home directory, usually holds the files you are making available for downloading by remote FTP users. When FTP users log in, they are placed in the FTP home directory (*/var/ftp*), and they can then change to the **pub** directory to start accessing those files (*/var/ftp/pub*). Within the **pub** directory, you can add as many files and directories as you want. You can even designate some directories as upload directories, enabling FTP users to transfer files to your system.

In each subdirectory set up under the **pub** directory to hold FTP files, you should create a **README** file and an **INDEX** file as a courtesy to FTP users. The **README** file contains a brief description of the kind of files held in this directory. The **INDEX** file contains a listing of the files and a description of what each one holds.