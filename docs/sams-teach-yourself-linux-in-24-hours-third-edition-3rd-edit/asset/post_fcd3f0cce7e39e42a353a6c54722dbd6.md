
5. What should you do if your printer is not listed in the printtool utility?

Select a printer that closely matches your printer. You could try another printer from the same manufacturer. You may also try to check the printer documentation to see if there is a printer that your printer will emulate.

6. What tools do you use to manage print jobs once you have sent them off to the print spool?

To check on the status of the files in the print spool, use the lpq command. This command displays the jobs that are being processed by the printer and those jobs that are waiting to be processed. To delete a job from the print spool, use the lprm command. When you use the lprm command, you'll need to specify the number of the print job that you want removed from the print spool. You can find this number by using the lpq command.

## Exercises

- 1. Find new ways to use your computer system efficiently and conservatively. Read the Linux Ecology HOWTO. This HOWTO contains some good ideas on saving power, paper, and ink. It also contains some good hints on extending the life of your computer hardware and on how to turn off the lights in your home by remote control.
- 2. Remember the three R's? Reduce, reuse, and recycle. Let's add another subject— compost. If your community sponsors a recycling program for bottles, plastics, and old newspapers, do your part to participate. Put a tree box in your home office or small business in which you can toss those mistakes that come off the printer. You can always use this scrap paper to make notes. Alternatively, you can learn how to compost in your backyard (start with the composting guide at www.vegweb.com/composting/resources.shtml). It's a great way to enrich your garden soil and to save landfill space.

## Hour 12

### Sharing Files with Other Users on the System

Because Linux is a multi-user operating system, several people can share the same machine without interfering with the home directories and related files of other users. However, those several people can also use the same multi-user system to allow the sharing of selected files with another user or a group. You can do this while maintaining your home directory autonomy and keeping your personal files private.

In this hour, you will

- Manage user accounts on the system
- Create group accounts to facilitate file sharing
- Transfer ownership of a file to other system users
- Determine who can access a file and the type of access they will be permitted

![](img/782ecfdc0b083a767896cc983e10427f_210_0.png)

### Maintaining User Accounts

In Hour 5, "Getting Acquainted with the Shell," you learned how to use the adduser command to create an unprivileged user account that you could use to experiment with your Linux system. You can use this command to create as many user accounts as you need. Ideally, you should create an account for each person who uses the computer and the Linux operating system. To see the list of system users, open the /etc/passwd file (shown in Figure 12.1).

> Please be careful when viewing and editing the files mentioned during this hour. One typographical error could cause you many headaches. One way to avoid problems is to make a backup copy of the file before you attempt to make changes. Then, if you make a mistake, you can revert back to the original file. If you feel uncomfortable editing these files, you might want to explore LinuxConf, which is covered in Appendix B, "Introducing GNOME and LinuxConf."

FIGURE 12.1
The /etc/passwd file lists all the users who have been set up in the system.

![](img/782ecfdc0b083a767896cc983e10427f_211_0.png)

You’ll notice that there are three types of users set up on the system. These are:

- Superuser—The root account is for the superuser. This account should only be used to perform system maintenance and configuration tasks.
- Individual—Unprivileged user accounts are assigned to the individuals who use the system. Each person has a username and password that are different from those of other users on the system.
- Fictitious User—System daemon accounts are accounts that are set up by the operating system and are not used by individuals. These accounts perform special tasks (such as retrieving the mail and sending files to the printer) and need access to files on the system. You can think of these system daemon accounts as fictitious users.

Each user has a separate entry in the /etc/passwd file that contains seven fields. Each field is separated by the colon (:) character. In order of appearance, these fields are

- The username is the name that the user types to log in to his account.
- The password is indicated by the letter x. This means that the passwords are encrypted so that someone can't look in the /etc/passwd file and learn everyone's passwords.

![](img/782ecfdc0b083a767896cc983e10427f_212_0.png)

> If you want to prevent a user from being able to access his account, place an asterisk (*) at the front of the password field.

- The user identification number (uid) is a unique number that is assigned to each account. The system uses this number to identify the user when dealing with file permissions.
- The group identification number (gid) identifies the primary group to which the user belongs. A user can belong to more than one group, but only the primary group is listed in the /etc/passwd file. You'll learn about group accounts later in the hour.
- Miscellaneous information (gecos) about the user can also be placed in the file. This could contain the user's real name and location information (such as an office number or phone number).
- The user's home directory (homedir) is where the user stores personal files. This is also the default working directory when the user logs in to his account.
- The shell that runs when the user logs in to his account is the last field in the entry. The default for most Linux distributions is /bin/bash.

When a user will no longer be using the system, you will want to delete his account. You have two options: You can delete the account and the user's home directory (along with its contents), or you can delete the account and leave the home directory in place. To delete a user's account and home directory, type

```
userdel -r username
```

To delete the user's account and leave his home directory in place, type

```
userdel username
```

![](img/782ecfdc0b083a767896cc983e10427f_213_0.png)

> You must be logged in to the root account to do this, and you cannot delete a user account while the user is logged in.

### Task: Changing Your Password

It is very important that each user (and the superuser) account has a password and that the password is changed on a regular basis. Here's how to change the password for your user account:

- 1. Log in to your user account.
- 2. Type `passwd` and press Enter. You will be prompted for the current account password.
- 3. Type the password and press Enter. You will be prompted for the new password.
- 4. Type the new password and press Enter. You will be asked to verify the password.
- 5. Type the new password (again) and press Enter.

Here are a few rules about changing passwords:

- As a general rule of thumb, change your password (and the root account password) on a regular cycle, such as once a month or every three months.
- If the password becomes known by someone who does not need access to the account, change the password.
- When someone who was responsible for maintaining the system is no longer in charge of the system, change the superuser password. Some reasons for the change might be that the former system administrator has been transferred to another department, or has left the company.

### Setting Up Group Accounts

In addition to setting up user accounts on your Linux system, you might want to consider setting up group accounts. Group accounts are useful when several users need to share the same files. You can create as many group accounts as needed and assign any combination of users to the group. Users can even belong to more than one group. To see the list of groups that are already set up on your system, look at the `/etc/group` file (shown in Figure 12.2).
