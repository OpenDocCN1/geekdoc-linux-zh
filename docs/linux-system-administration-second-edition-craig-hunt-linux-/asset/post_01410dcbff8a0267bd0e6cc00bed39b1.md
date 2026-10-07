
YYYY-MM-DD format as follows:

```
# chage -E 2000-8-12 someuser
```

If the date is passed, the account will be disabled but can be enabled later using the same method. When the user attempts to log in, he or she will see the following message:

Your account has expired; please contact your system administrator

## Deleting User Accounts

If you are sure that you will not need a user’s account again, you can delete it. Deleting an account basically reverses the steps you took to create it. The steps to delete an account are:

- 1. Delete the record for the user in /etc/passwd.
- 2. Back up the user’s files.
- 3. Delete the user’s files.
- 4. Delete the user’s home directory.

You’ll also need to search the system for any other files owned by this user and either remove them or reset their ownership. Removing a user’s account may all be done by hand or via tools as before.

### Manually Deleting an Account

First you’ll want to remove the user’s /etc/passwd entry. When pwconv is run again, the /etc/shadow entry for that user will be automatically removed as well. Next, remove the home directory and all of the files contained therein using an rm command like the following:

```
# rm -r /home/donald
```

The rm command will remove the /home/donald directory and all the files and subdirectories it contains. If you’re confident enough and would rather not be prompted, you can add the -r option to the above command (making it rm -rf /home/donald), which instructs Linux not to prompt you about removing files. This is very dangerous, so you might want to just endure the prompts.

**Tip** It’s a good idea to back up a deleted user’s account before running the rm command. You can do this by archiving the files using the tar backup utility (described in Chapter 9) and storing the files on floppy disk, high-capacity removable disks like Iomega Zip disks, CD-R discs, or tape. Keeping a deleted user’s files on hand in this way can be handy if you discover you’ve deleted the wrong account or if you need to recover a particular file from the ex-user’s account for some reason.

Next you need to search the computer for other files owned by the deleted user and determine what to do with these files. Use the find command for this as follows:

```
# find / -gid 503 -uid 503
```

Assuming Donald’s user ID was 503 and his original group ID had never been changed, this command would generate a list of files by full path that were owned by Donald or had his group ID. You’ll then need to look through the file list and determine what to do with each file. If you decide to keep a file but change its ownership, you can use the chown command, as follows:

```
# chown betty.users /opt/somefile
```

The above command changes the ownership of /opt/somefile to betty, and changes group ownership to the users group. You can omit the period and group name if you don't want to change the group, or add an -R parameter before the username to recursively change every file within a directory. For instance, the following command changes the ownership of the /home/samba/sharefiles directory and all its files and subdirectories to betty, but doesn't change the group associated with the files:

```
# chown -R betty /home/samba/sharefiles
```

## Deleting an Account with Webmin

You can also delete a user using the Webmin utility. To do so, follow these steps:

- 1. Start Webmin as previously described.
- 2. Open Users and Groups.
- 3. Select the account that you'd like to disable. You'll then be presented with the User Information screen, which resembles Figure 5.2.
- 4. Press the Delete button.
- 5. Click Delete User if you want to leave the user's home directory intact or Delete User and Home Directory if you want to remove the user's home directory.
- 6. Wait for the confirmation screen.
- 7. Close the browser.

## Deleting an Account with userdel

The userdel utility will remove a user's entry in the /etc/passwd file and optionally remove that user's home directory and all the files and subdirectories it contains. Any files owned by that user outside the home directory will remain on the system and will appear as owned by the user's ID when displayed via an ls -l command. The userdel command to delete our hypothetical Donald's passwd entry and home directory looks like this:

```
# userdel -r donald
```

You may also choose to delete Donald's /etc/passwd entry but leave all the files in his home directory by omitting the -r.

Use the find command shown earlier to locate all files owned by Donald or in his group. Those files must be handled manually.

## Groups

You saw earlier in the chapter that each user has a default group identity, called a login group, which is assumed upon logging in to the system. Once authenticated by /bin/login, the user assumes the group identity specified in the /etc/passwd file. In Red Hat, a user's default group ID is the same as the user ID; in some other Linux distributions, all users are by default put in a single group, typically called users. Linux administrators can create new groups, associating users for specific purposes such as projects that require certain users to have access to the same set of files. The next sections show how to add and remove groups, and how users can become members of different groups.

### The Function of Groups

Groups are an integral part of Linux security. As described in Chapter 7, every file has an associated permissions string. This string specifies the presence or absence of read, write, and execute permission to each of three classes of users: the file’s owner, the file’s group, and all users on the system (often called *world* permissions). By controlling the group setting for files and by assigning users to particular groups, you can enhance the internal security of your Linux system. For instance, if your system is being used by two different sets of employees, each of which is working on one project, you can create two groups, one for each set of employees. By denying world access to users’ files, you can prevent employees in one group from reading files created by members of the other group. If a few users belong to both groups, you can make those users members of both groups, so they can read both groups’ files.

Because every Linux installation is unique, it’s impossible for a Linux distribution to come with a default group setup that’s appropriate for all environments. The packagers of Red Hat can’t know what groups you’ll need, any more than they can know what users you’ll need. Nonetheless, the account creation tools make certain default assumptions about how you might group your accounts. Different distributions do things in different ways.

In Red Hat, every time a new user is added, a group with the same user ID and numeric ID as that user is created. Say the user is donald again. A user group called donald would be created, and the user donald would be added to that *user private group*. The umask (see Chapter 4) is set to 002, which means that any file created by donald will have read–write permission for him (the owner) and for the donald group and read–only for world. This works well since we know that donald has membership in the group by default. Since Donald is the only member of his user private group, only he and the superuser can access files with the group set to donald. Anyone can be added to the donald group and will then have group access to any files that Donald creates with this umask.

Other distributions don’t always work this way. Some create a single group (generally called users), and place all users in this group. Thus, both the donald and betty accounts by default belong to the users group. Typically, the umask is 022, so users can read each other’s files, but cannot write to them. This is a *shared-group* approach.

On small workstations, both these approaches tend to work well, because workstations tend to have just one or two users, and the implications of group membership have small consequences. At worst, you may need to add one or two users to each other’s groups in the user private group approach, or create a couple of new groups and change default group membership in the shared group approach. On larger systems, though, you’re likely to need to create a more complex configuration. In an academic environment, for instance, you may need to create groups for different courses; and in a work environment, you may need to create groups for different working groups. The tools to do this parallel the tools used to create user accounts in many respects.

### The /etc/group File

Information about each group is contained in the /etc/group file. Just as with /etc/passwd, it is critical that any system administrator clearly understand this important file. Its structure is fairly simple. Listing 5.2 shows an excerpt from a typical /etc/group file.

#### Listing 5.2: A Portion of the /etc/group File

```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
```
