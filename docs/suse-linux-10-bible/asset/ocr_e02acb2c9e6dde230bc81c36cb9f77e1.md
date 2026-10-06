# Chapter 2 ✦ Linux Fundamentals 63

The users on a system (provided it does authentication locally) are listed in the file /etc/passwd. Look at your user entry in /etc/passwd; it will look something like this:

```
roger:x:1000:1000:Roger Whittaker:/home/roger:/bin/bash
```

This shows, other things, that the user username roger has the real name Roger Whittaker, and his home directory is /home/roger, and that his default shell is /bin/bash (the bash shell).

There will almost certainly be an entry for the system user postfix looking like this:

```
postfix:x:51:51:Postfix Daemon:/var/spool/postfix:/bin/false
```

This is the postfix daemon, which looks after all. This user can't log in his shell is /var/spool/postfix, and it owns the spool directories in which mail being sent and delivered is held. The fact—it means that any vulnerability in postfix is less likely to lead to a subversion of the whole system. Similar users exist for the web server (the user www) and other services. You often need to consider these, it is important to understand that they exist and the correct ownership of certain files and directories by these users is part of the overall security model of a system.

Each user belongs to one or more groups. The groups are listed in the file /etc/groups. To find out groups you belong to, you can simply type the command groups (alternatively look at the file /etc/group and look for your username). By default, on a WISE system, you will find that you belong to the groups users and also to a few system groups, including the groups dialout and audio. This is to give normal human users the right to use the modem and sound devices (which is arranged through file permissions as you shall see later in this chapter).

# Creating Users and Groups

You can most simply create a new user using YaST's user module. Start YaST and choose the users and groups option. You might want to create a user with the username guest. YaST will create the user according to your instructions and also create a home directory /home/guest for the new user with a skeleton of configuration files in.

This skeleton is copied from the directory /etc/skel has the ownership of the new user (user guest, group users) applied to once the new user's home directory has been created.