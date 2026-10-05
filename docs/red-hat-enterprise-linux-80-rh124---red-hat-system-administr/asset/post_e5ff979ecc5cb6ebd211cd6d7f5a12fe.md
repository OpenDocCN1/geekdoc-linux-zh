
## CHAPTER 6 | Managing Local Users and Groups

### 4. Switch to root in a login shell and explore the new shell environment.

4.1. Run sudo su - at the shell prompt to become the root user.

```
[student@servera ~] sudo su
[root@servera #]
```

Notice the difference in the shell prompt compared to that of sudo su in the preceding step.
sudo may or not prompt you for the student password, depending on the time-out period of sudo. The default time-out period is five minutes. If you have authenticated to sudo within the last five minutes, sudo will not prompt you for the password. If it has been more than five minutes since you authenticated to sudo, you need to enter student as the password to get authenticated to sudo.

4.2. Run id to view the current user and group information.

```
[root@servera #] id
uid=0(root) gid=0(root) groups=0(root)
context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

4.3. Run pwd to display the working directory.

```
[root@servera #] pwd
root
```

4.4. Print the values of the HOME and PATH variables to determine the home directory and the user executables path, respectively.

```
[root@servera #] echo HOME
/root
[root@servera #] echo PATH
/usr/local/sbin:/usr/local/bin:/usr/bin:/root/bin
```

In the preceding step, after sudo reset the PATH variable from the settings of student's shell environment, the su - command ran the shell login scripts for root and set the PATH variable to yet another value. The su command without the (-) did not do that.

4.5. Exit the root user's shell to return to the student user's shell.

```
[root@servera #] exit
logout
[student@servera ~]$
```

5. Verify that the operator1 user is configured to run any command as any user with sudo.

```
student@servera ~]$ sudo cut /etc/sudoers.d/operator1
operator1-ALL=(ALL)
```

6. Become operator1 and view the contents of /var/log/messages. Copy /etc/motd to /etc/motd and remove it (/etc/motd). These operations require administrative rights so you use sudo to run these commands as the superuser. Do not switch to root with sudo su or sudo su -.

### 6.1. Switch to operator1.

```
[student@servera ~]$ su - operator1
Password: redhat
[operator1@servera ~]
```

6.2. Attempt to view the five lines of /var/log/messages without using sudo. This should fail.

```
[operator1@servera ~]$ tail -5 /var/log/messages
tail: cannot open '/var/log/messages' for reading: Permission denied
```

6.3. Attempt to view the five lines of /var/log/messages with sudo. This should succeed.

```
[operator1@servera ~]$ sudo tail -5 /var/log/messages
[sudo] password for operator1: redhat
Jan 23 15:53:36 server su(2394): FAILED SU (to operator1) student on pts/1
Jan 23 15:53:51 servera su(2310): FAILED SU (to operator1) student on pts/1
Jan 23 15:53:58 servera su(2310): FAILED SU (to operator1) student on pts/1
Jan 23 15:54:12 server su(2322): (to operator1) student on pts/1
Jan 23 15:54:25 servera su(2853): (to operator1) student on pts/1
```

> NOTE
> The preceding output may differ on your system.

6.4. Attempt to make a copy of /etc/motd as /etc/motd without using sudo. This should fail.

```
[operator1@servera ~]$ cp /etc/motd /etc/motd
cp: cannot create regular file '/etc/motd': Permission denied
```

6.5. Attempt to make a copy of /etc/motd as /etc/motd with sudo. This should succeed.

```
[operator1@servera ~]$ sudo cp /etc/motd /etc/motd
[operator1@servera ~$]
```

6.6. Attempt to delete /etc/motd without sudo. This should fail.

```
[operator1@servera ~$] rm /etc/motd
rm: remove write-protected regular empty file '/etc/motd'
rm: cannot remove '/etc/motd': Permission denied
[operator1@servera ~$]
```

6.7. Attempt to delete /etc/motd with sudo. This should succeed.

```
[operator1@servera ~$] sudo rm /etc/motd
[operator1@servera ~$]
```

6.8. Exit the operator1's shell to return to the student user's shell.

```
[operator1@servera ~$] exit
logout
[student@servera ~]$
```

6.9. Log off from server.

```
[student@servera ~]$ exit
logout
Connection to server closed.
```

### Finish.

On workstation, run lab-finish to complete the exercise.

## CHAPTER 6 | Managing Local Users and Groups

### MANAGING USER ACCOUNTS

### OBJECTIVES
After completing this section, you should be able to create, modify, and delete user accounts.

## MANAGING USERS

### Creating Users from the Line
- The useradd command creates a new user. It sets up the home directory and account information. At this point the account does not have a valid password set.
- The useradd --help displays the basic options that can be used.

### Modifying Existing Users from the Line
- The usermod --help displays the basic options that can be used:

| OPTIONS | USAGE |
| :--- | :--- |
| -c, --comment | Add the real name to the comment field. |
| -g, --group | Specify the primary group for the user. |
| -G, --groups | Specify a comma-separated list of supplementary groups. |
| -a, --append | Used with -G to add the supplementary groups instead of replacing the set. |
| -d, --home_DIR | Specify a particular home directory for the user. |
| -m, --move-home | Move the user's home directory to a new location. Must be used with -d. |
| -s, --shell | Specify a particular login shell for the user account. |
| -L, --lock | Lock the account |

### Deleting Users from the Line
- The userdel username removes the details of username from /etc/passwd, but leaves the user's home directory intact.
- The userdel -r username removes the details of username from /etc/passwd and also deletes the user's home directory.

> WARNING
> When a user is removed with userdel without the -r option, the system will have files that are owned by anassigned UID. This can also happen when a file, having a deleted user as its owner, exists outside that user's home directory. This can lead to information leakage and other security issues. Red Enterprise Linux 7 and Red Enterprise Linux 8, the useradd command assigns the first free UID greater than or 1000, unless you specify it using the -u option. This is how information leakage can occur. If the first free UID has been previously assigned to a user account that has since been removed, the old user's UID will be reassigned to the new user, giving the new user ownership of the old user's files.

### Setting Pass from the Command Line
- The password username command sets the initial password or changes the existing password of username.
