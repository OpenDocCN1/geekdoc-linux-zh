
In the following example, root changes the ownership of the hello.txt file from geeko to the user tux by using chown:

```text
da10:/tmp # ls -la hello.txt
-rw-r--r-- 1 geeko users 0 2006-04-06 12:43 hello.txt
da10:/tmp # chown tux:users hello.txt
da10:/tmp # ls -la hello.txt
-rw-r--r-- 1 tux users 0 2006-04-06 12:43 hello.txt
da10:/tmp #
```

In the following example, chown is used to limit access to the list.txt file to members of the group advanced:

```text
da10:/tmp # ls -la list.txt
-rw-r--r-- 1 geeko users 0 2006-04-06 12:43 list.txt
da10:/tmp # chown :advanced list.txt
da10:/tmp # ls -la list.txt
-rw-r--r-- 1 geeko advanced 0 2006-04-06 12:43 list.txt
da10:/tmp #
```

Of course, root and the file owner continue to have rights to access the file. Although the group has changed, the owner permissions remain the same.

![](img/9129877170834ca9d5fdac5319bf5f12_308_0.png)

## Exercise 9-2: Manage File Permissions and Ownership

In this exercise, you create directories with different permissions.
First, create a /files/ directory with two subdirectories (private/ and public/).
Change the permissions for the private/ directory so that only root has read, write, and execute permissions, and the permissions for public/ so that everyone has rights to that directory.
Then, switch to user geeko. Try to create a geeko file inside each of these directories.
Change the permissions for the /files/public/geeko file, so that the users group has write permissions and others do not have any permissions.

## Detailed Steps to Complete This Exercise

Part I: Create a Private and a Public Directory
Part II: Try to Create a File as a Normal User in Both Directories

## Part I: Create a Private and a Public Directory

To create a private and a public directory, do the following:

- 1. Open a terminal window.
- 2. Switch to root (su -) with a password of n0v3ll.
- 3. Create the /files/ directory by entering

```text
mkdir /files
```

- 4. Change to the `/files/` directory by entering
  ```
  cd /files
  ```
- 5. To create the private and public subdirectories under `/files/`, enter
  ```
  mkdir private public
  ```
- 6. Change the permissions on the `private/` directory so that only root has read, write, and execute permissions by entering
  ```
  chmod 700 private
  ```
- 7. Change permissions on the `public/` directory so that everyone has rights to the directory by entering
  ```
  chmod 777 public
  ```
- 8. Verify the changes by entering
  ```
  ls -l
  ```

## Part II: Try to Create a File as a Normal User in Both Directories

To try to create a file as a normal user in both directories, do the following:

- 1. Switch to virtual terminal 3 by pressing Ctrl+Alt+F+3.
- 2. Log in as geeko with a novell password.
- 3. Switch to the `/files/` directory by entering
  ```
  cd /files
  ```
- 4. Try to create a file named geeko in the `private/` directory by entering
  ```
  touch private/geeko
  ```
  Notice that permission is denied.
- 5. Try to create a file named geeko in the `public/` directory by entering
  ```
  touch public/geeko
  ```
- 6. Verify that the file is created by entering
  ```
  ls public
  ```
- 7. Change to the `public/` directory by entering
  ```
  cd public
  ```
- 8. List the permissions of the geeko file by entering
  ```
  ls -l geeko
  ```
  Notice that the group users and others have only read permission for the file.
- 9. Change permissions so that the group users has write permissions and others does not have any permissions by entering
  ```
  chmod g+w,o-r geeko
  ```
- 10. Verify the change by entering
  
      ls -l
  
- 11. Log out as geeko by entering `exit` (or by pressing Ctrl+d); then return to the GNOME desktop by pressing Ctrl+Alt+F7.
- 12. Close the terminal window.

## Modify Default Access Permissions

If the default settings are not changed, files are created with the access mode 666 and directories with 777.

To modify (restrict) these default access mode settings, you can use the umask command. You use this command with a three-digit numerical value such as 022.

The permissions set in the umask are removed from the default permissions.

For example, entering umask 022 has the result shown in Table 9-5.

|  | Directories |  |  | Files |  |  |
|---|---|---|---|---|---|---|
| Default Permissions | rwx | rwx | rwx | rw- | rw- | rw- |
|  | 7 | 7 | 7 | 6 | 6 | 6 |
| umask | -- | -w- | -w- | -- | -w- | -w- |
|  | 0 | 2 | 2 | 0 | 2 | 2 |
| Result | rwx | r-x | r-x | rw- | r-- | r-- |
|  | 7 | 5 | 5 | 6 | 4 | 4 |

Table 9-5

The following listing shows an example of the effect of different umasks.

```
da10:~ # touch example1
da10:~ # mkdir exampledir1
da10:~ # umask 000
da10:~ # touch example2
da10:~ # mkdir exampledir2
da10:~ # umask 022
da10:~ # touch example3
da10:~ # mkdir exampledir3
da10:~ # ls -l
total 629
-rw-r--r-- 1 root root 0 May 16 11:18 example1
-rw-rw-rw- 1 root root 0 May 16 11:18 example2
-rw-r--r-- 1 root root 0 May 16 11:18 example3
drwxrwxrwx 2 root root 48 May 16 11:18 exampledir1
drwxrwxr-x 2 root root 48 May 16 11:18 exampledir2
drwxrwxr-x 2 root root 48 May 16 11:18 exampledir3
da10:~ #
```

By entering umask 077, you restrict access to the owner and root only; the group and others do not have any access permissions.

umask without any parameters shows the current value of the umask, with a leading zero.

```
da10:~ # umask
0022
da10:~ #
```

To make the umask setting permanent, you can change the value of umask in the systemwide /etc/profile.local configuration file. If you want the setting to be user-specific, enter the value of umask in the .bashrc file in the home directory of the respective user.

## Configure Special File Permissions

The attributes shown in Table 9-6 are used for special circumstances.

| Letter | Number | Name | Files | Directories |
|---|---:|---|---|---|
| t | 1 | Sticky bit | Not applicable | Users can only delete files when they are the owner, when they are root, or when they are the owner of the directory. This is usually applied to the /tmp/ directory. |
| s | 2 | SGID (set GroupID) | When a program is run, this sets the Group ID of the process to the Group ID of the file. | Files created in this directory belong to the group to which the directory belongs and not to the primary group of the user. New directories created in this directory inherit the SGID bit. |
| s | 4 | SUID (set UserID) | Sets the User ID of the process to that of the owner of the file when the program is run. | Not applicable. |

Table 9-6

You set the sticky bit with chmod, either via the permissions of others (such as chmod o+t /tmp) or numerically (such as chmod 1777 /tmp).

![](img/9129877170834ca9d5fdac5319bf5f12_311_0.png)

The sticky bit on older UNIX systems enabled the storing of an executable program in memory after it had been terminated, so it could be quickly restarted. However, with modern UNIX and Linux systems, this only affects directories.

The sticky bit is listed in the permissions for others (t), as in the following:

```
geeko@dal0:~ > ls -ld /tmp
drwxrwxrwt 1000 root root 608 2006-04-06 12:45 /tmp
geeko@dal0:~ >
```

The following is an example for SUID:

```text
geeko@da10:~ > ls -l /usr/bin/passwd
-rwsr-xr-x 1 root shadow 79765 2006-03-24 12:19
/usr/bin/passwd
geeko@da10:~ >
```

Each user is allowed to change his or her password, but the user must have root permission to write the hashed password into the /etc/shadow file.

The following is an example for SGID:

```text
geeko@da10:~ > ls -l /usr/bin/wall
-rwxr-sr-x 1 root tty 10192 2006-03-22 05:24
/usr/bin/wall
geeko@da10:~ >
```

With wall, you can send messages to all virtual terminals. If you use wall, this command is executed with the permissions of the group tty.

If the SUID or SGID attributes are set, the programs are carried out with the privileges the owner (in the example for SUID: root) or the group (in the example for SGID: tty) have.

If root is the owner of the program, the program is carried out with the permissions of root. Unfortunately, there is a security risk in doing this. For example, it could be possible for a user to take advantage of an error in the program, retaining root privileges after the process has ended.

Therefore, this bit should only be set for applications that are well tested and in cases where no other way can be used to grant access to a specific task.

## Ensure File System Security

After a user has logged in to the system, what the user is allowed to do and what the user is not allowed to do is mainly determined by the security settings of the file system.

In Linux, file system security is especially important because every resource available on the system is represented as a file.

For example, when a user tries to access the sound card to play back audio data, the access rights of the sound card are determined by the permission settings of the corresponding device file in the /dev directory.

To ensure basic file system security, you need to know the following:

- - The Basic Rules for User Write Access
- - The Basic Rules for User Read Access

## The Basic Rules for User Write Access

The file systems used in Linux are structurally UNIX file systems. They support the typical file access permissions (read, write, execute, sticky bit, SUID, SGID, etc.).

Apart from additional standard functionalities, such as various time stamps, the access permissions can be administered separately for file owners, user groups, and the rest of the world (user, group, others).
