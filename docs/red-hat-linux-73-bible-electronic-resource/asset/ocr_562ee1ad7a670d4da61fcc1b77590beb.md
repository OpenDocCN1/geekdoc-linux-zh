I recommend using these commands — and the security arrangement I’m about to describe — between computers within an organization in which the other computers are trusted and there are no connections to the outside world. They provide a great way for people who work on multiple computers to exchange data and execute commands among those computers.

One of the main problems with the “r” commands is that its security mechanism simply believes that you are who you say you are. For example, suppose permission is open to allow joe from the computer named maple to run any program as though he were the local user named joe. Any computer with access to your network could claim to be that computer and user to gain access to your computer. Even the basic password mechanism is bypassed.

# Setting up rhosts security

Let’s say you have a private network at your place of business and you want your employees to be able to draw on resources from many of those computers. You give each user a login account to several different computers (using the same login name on each). For a user to be able to freely exchange information among the computers, you or the user can simply change a configuration file to enable the user to run the rlogin, rcp, and rsh commands freely.

> **CAUTION:** The reason the security measures described here are not terribly secure is that they rely on the computer on the networks to supply user names. There is no guarantee that the names supplied are real user names. For that reason, you should use this method only among trusted machines.

An individual user can create a .rhosts file in the user’s home directory. That file can contain a list of host computers on which the user has accounts of the same name. For example, a user named mike on the machine named pine also has a user login (of the same name) on computers named maple, spruce, and fig. He adds the following entries to a .rhosts file that looks like the following in the home directory on each computer:

```
maple
spruce
fig
pine
```

After the files are added, mike can use the rlogin, rsh, and rcp commands between the four computers without having to type a password. For each command, mike will have permission to copy files, access files and directories, and execute programs with the permission available on the computer being accessed.

Instead of using the .rhosts files, a system administrator can add similar contents to the /etc/hosts.equiv file. A /etc/hosts.equiv file that had those four computer names in it would enable any users with the same user name on those computers to exchange information between them without entering a password. Besides host names, the /etc/hosts.equiv file can limit the user names that can use “r” commands without passwords. Here’s an example of a /etc/hosts.equiv file: