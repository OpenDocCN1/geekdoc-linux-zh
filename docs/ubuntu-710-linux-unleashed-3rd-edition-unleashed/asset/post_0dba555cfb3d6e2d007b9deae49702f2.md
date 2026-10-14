
However, Cedega is a popular and up-to-date product with support for recent releases such as Elder Scrolls IV: Oblivion and World of Warcraft. Because the state of Cedega is constantly changing, TransGaming Technologies has a subscription service, which means that you get updates for the code when they are released—ensuring that you are able to enjoy not only the games of today, but also those of tomorrow.

So, if you cannot wait for Linux to become more popular with game developers, use Cedega as a stop-gap until they can be persuaded to support Linux directly.

> **TIP**
> 
> The keys to successful gaming in Linux are to always read the documentation thoroughly, always investigate the Internet resources thoroughly, and always understand your system. Installing games is a great way to learn about your system because the reward of success is so much fun.

## Reference

- http://www.transgaming.com/—The official TransGaming Technologies website provides details of games that are directly supported under Cedega.
- http://www.linuxgames.com/—A good source of up-to-date information about the state of Linux gaming.
- http://zerowing.idsoftware.com/linux/doom/—Includes a complete how-to and troubleshooting guide for running DOOM 3 under Linux.
- http://www.unrealtournament.com/—The official site of Unreal Tournament.
- http://www.nvnews.net/vbulletin/forumdisplay.php?f=14—The Official Nvidia Linux driver support forum.
- http://www.nvidia.com/object/linux.html—Home page for the Nvidia Linux drivers.
- http://tinyurl.com/3pm2v—Home page for the ATI Linux drivers (courtesy of tinyurl.com).

This page intentionally left blank

## PART III

## System Administration

## IN THIS PART

- CHAPTER 10 Managing Users 195
- CHAPTER 11 Automating Tasks 219
- CHAPTER 12 System-Monitoring Tools 275
- CHAPTER 13 Backing Up 287
- CHAPTER 14 Networking 311
- CHAPTER 15 Remote Access with SSH and Telnet 355

This page intentionally left blank

## CHAPTER 10
## Managing Users

If it weren’t for users, system administrators would have a quiet life! However, it’s impossible for you have a system with absolutely no users, so it is important that you learn how to effectively manage and administer your users as they work with your system. Whether you are creating a single user account or modifying a group that holds hundreds of user accounts, the fundamentals of user administration are the same.

User management and administration includes looking after allocating and managing home directories, putting in place good password policies, and applying an effective security policy including disk quotas and file and directory access permissions. We will take a look at all of these areas within this chapter, as well as the different types of user that you are likely to find on an average Linux system.

### User Accounts

You can normally find three types of users on all Linux systems: the super user, the day-to-day user, and the system user. Each type of user is essential to the smooth running of your system and learning the differences between the three is essential if you are to work efficiently and safely within your Linux environment.

All users who access your system must have accounts on the system itself. Ubuntu uses the /etc/passwd file to store information on the user accounts that are present on the system. All users, regardless of their type, have a one-line entry in this file that contains their username (typically used for logging in to the system), a password field (which contains an x to denote that a password is present), a User ID (commonly referred to as the UID), and a Group ID

- User Accounts
- Managing Groups
- Managing Users
- Managing Passwords
- Granting System Administrator Privileges to Regular Users
- Disk Quotas
- Reference

(commonly referred to as the GID). The last two fields show the location of the home directory (usually /home/username) and the default shell for the user (/bin/bash is the default for new users).

> NOTE
> Just because the password field contains an x doesn't mean that this is your password! All passwords are actually encrypted and stored in /etc/shadow for safe keeping. Ubuntu automatically refers to this file whenever a password is required.

In keeping with other UNIX-based operating systems, Linux and Ubuntu make use of the established UNIX file ownership and permission system. All files (which can include directories and devices) can be assigned one or more of read, write, and/or execute permissions. These three "flags" can also be assigned to the owner of the file, a member of a group, or anyone on the system. The security for a file is drawn from these permissions and also file ownership. As the system administrator (more commonly referred to as the super user), it is your responsibility to manage these settings effectively and ensure that the users have proper UIDs and GIDs. Perhaps most importantly, you will need to lock away sensitive files from users who should not have access to them, through file permissions.

### The Super User/Root User

No matter how many system administrators there are for a system, there can ever only be one super user account. The super user account, more commonly referred to as the root user, has total and complete control over all aspects of the system. They can go anywhere in the filesystem, grant and revoke access to files and directories, and can carry out any operation on the system, including destroying it if they so wish. The root user is unique in that it has a UID of 0 and GID of 0.

As you can probably guess by now, the root user has supreme power over your system. With this in mind, it's important that you do not work as root all the time as you may inadvertently cause serious damage to your system, perhaps even making it totally unusable. Instead, you should rely on root only when you need to make specific changes to your system that require root privileges. As soon as you've finished your work, you can switch back to your normal user account to carry on working.

Within Ubuntu, you execute a command with root privileges by way of the sudo command like so:

```
$sudo apt-get update
```

You will be prompted for your password so you should enter this. Ubuntu will then carry out the command (in this case, updating information about available software) as if you were running it as root.
