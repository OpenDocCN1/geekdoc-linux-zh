
# Finish

On workstation, run **lab rhcsa-rh124-review4 finish** to complete the comprehensive review. This script deletes the files and directories created during the start of the comprehensive review and ensures that the environment on **serverb** is clean.

```
[student@workstation ~]$ lab rhcsa-rh124-review4 finish
```

This concludes the comprehensive review.

# MOUNTING FILESYSTEMS AND FINDING FILES

In this review, you will mount a file system and locate files based on different criteria.

# OUTCOMES
You should be able to:

- Mount an existing file system.
- Find files on the basis of the file name, permissions and size.

# BEFORE YOU BEGIN
Log in workstation as student using student as the password.

On workstation, run lab rhcsa-rh124-review5 start to start the comprehensive review. This script creates the necessary file system, user accounts and group accounts.

```
[student@workstation ~]$ lab rhcsa-rh124-review5 start
```

# INSTRUCTIONS
Accomplish the tasks on serverb to complete the exercise.

- On serverb, a block device containing the XFS file system exists but is not mounted. Determine the block device and mount it on the /review5-disk directory. Create the /review5-disk directory, if necessary.
- On serverb, locate the file called review5-path. Create a file named /review5-disk/review5.txt that contains a single line consisting of the absolute path to the /review5 file.
- On serverb, locate all the files having contractor1 and contractor as the owning user and group, respectively. These files must also have the octal permissions of 640. Save the list of these files in /review5-disk/review5-perms.txt.
- On serverb, locate all files 100 bytes in size. Save the absolute paths of these files in /review5-disk/review5-size.txt.

# Evaluation

On workstation, run the lab rhcsa-rh124-review5 grade command to confirm success of this exercise.

```
[student@workstation ~]$ lab rhcsa-rh124-review5 grade
```

# Finish

On workstation, run rhcsa-rh124-review5 finish to complete the comprehensive review. This script deletes the file system, user accounts, and group accounts created during the start of the comprehensive review and ensures that the environment on serverb is clean.

```
[student@workstation ~]$ lab rhcsa-rh124-review5 finish
```

This concludes the comprehensive review.

# MOUNTING FILESYSTEMS AND FINDING FILES

In this review, you will mount a file system and locate files based on different criteria.

# OUTCOMES

You should be able to:

- Mount an existing file system.
- Find files on the basis of the file name, permissions and size.

# BEFORE YOU BEGIN

Log in to workstation as student using student as the password.

On workstation, run lab rhca5-rh124-reviews5 to start the comprehensive review. This script creates the necessary file system, user accounts and group accounts.

```
[student@workstation ~]$ lab rhca5-rh124-reviews5 start
```

# INSTRUCTIONS

Accomplish the following tasks on server to complete the exercise.

- On server, a block device containing the XFS file system exists but is not mounted. Determine the block device and mount it on the /review5-disk directory. Create the /review5-disk directory, if necessary.
- On server, locate the file called review5-path. Create a file named /review5-disk/review5.txt that contains a single line consisting of the absolute path to the review5 file.
- On server, locate all the files having contractor1 and contractor as the owning user group, respectively. The files must also have the octal permissions of 640. Save the list of these files in /review5-disk/review5-perms.txt.
- On server, locate all 100 bytes in size. Save the absolute paths of these files in /review5-disk/review5-size.txt.

1. On server, mount the block device containing the XFS file system on the /review5-disk directory.

1.1. From workstation, open an SSH session to server as student.

```
[student@workstation ~]$ ssh student@server
...output omitted...
[student@server ~]$
```

1.2. Use the lsblk -fs command to determine the idle block device containing the XFS file system.

```
$student@server ~$ lsblk -fs
NAME FSTYPE LABEL UUID MOUNTPOINT
...output omitted...
vdb1 xfs 
    3d97c5ef-23e7-4c1c-a9be-d5c47b5d0d5
└─vdb
...output omitted...
```

From the preceding output, note that the vdb1 block device contains the XFS system, which is not mounted on any directory.

1.3. Use the sudo mkdir command to create the /review5-disk directory as the superuser. When the sudo command prompts you for a password, give the password student.

```
$student@server ~$ sudo mkdir /review5-disk
[sudo] password for student: student
```

1.4. Use the sudo mount command to mount the vdb1 device on the /review5-disk as the superuser.

```
$student@server ~$ sudo mount /dev/vdb1 /review5-disk
```

1.5. Verify that the vdb1 device is mounted on the /review5-disk directory.

```
$student@server ~$ df -Th
Filesystem     Type  Size  Used Avail Use% Mounted on
/dev/vdb1      xfs   XXG   XX  XXG XX% /review5-disk
```

2. On server, locate the file called review5-path. Create a file named /review5-disk/review5.txt that contains a single line consisting of the absolute path to the review5 file.

2.1. Use the find command to locate review5-path. Redirect all errors to /dev/null.

```
$student@server ~$ find / -name review5-path 2>/dev/null
/home/student/review5-path
```

2.2. Create /review5-disk/review5.txt. Record the absolute path to the review5-path file in the file.

```
$student@server ~$ echo "/home/student/review5-path" > /review5-disk/review5.txt
```

3. On server, locate all the files having contractor1 and contractor as the owning user and group, respectively. The files must also have the octal permissions of 640. Save the list of these files in /review5-disk/review5-perms.txt.

3.1. Use the find command to locate these files. Redirect all errors to /dev/null and save the output to the file.

```
$student@server ~$ find / -user contractor1 -group contractor -perm 640 2>/dev/null > /review5-disk/review5-perms.txt
```

4. On server, locate all files 100 bytes in size. Save the absolute paths of these files in /review5-disk/review5-size.txt.

4.1. Use the find command to locate all files 100 bytes in size. Redirect all errors to /dev/null and save the output to the file.

```
$student@server ~$ find / -size 100c 2>/dev/null > /review5-disk/review5-size.txt
```
