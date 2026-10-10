
Net has no access to your important data (which might otherwise happen in spite of the user/administrator divide). With a little cunning, you can even display a browser and e-mail program running under your “surfing account” among your “normal” programs [1].

Under Linux, every user account is assigned a unique number, the so-called user ID (or UID, for short). Every user account also features a textual user name (such as `root` or `joe`) which is easier to remember for humans. In most places where it counts—e.g., when logging in, or in a list of files and their owners—Linux will use the textual name whenever possible.

![](img/44bdd771e9c9b1353d2401c2892b2459_170_0.png)

The Linux kernel does not know anything about textual user names; process data and the ownership data in the file system use the UID exclusively. This may lead to difficulties if a user is deleted while he still owns files on the system, and the UID is reassigned to a different user. That user “inherits” the previous UID owner’s files.

![](img/44bdd771e9c9b1353d2401c2892b2459_170_1.png)

There is no technical problem with assigning the same (numerical) UID to different user names. These users have equal access to all files owned by that UID, but every user can have his own password. You should not actually use this (or if you do, use it only with great circumspection).

### 13.1.2 Users and Groups

To work with a Linux computer you need to log in first. This allows the system to recognise you and to assign you the correct access rights (of which more later). Everything you do during your session (from logging in to logging out) happens under your user account. In addition, every user has a home directory, where only they can store and manage their own files, and where other users often have no read permission and very emphatically no write permission. (Only the system administrator—`root`—may read and write all files.)

![](img/44bdd771e9c9b1353d2401c2892b2459_170_2.png)

Depending on which Linux distribution you use (cue: Ubuntu) it may be possible that you do not have to log into the system explicitly. This is because the computer “knows” that it will usually be you and simply assumes that this is going to be the case. You are trading security for convenience; this particular deal probably makes sense only where you can stipulate with reasonable certainty that nobody except you will switch on your computer—and hence should be restricted by rights to the computer in your single-person household without a cleaner. We told you so.

Several users who want to share access to certain system resources or files can form a group. Linux identifies group members either fixedly by name or transiently by a login procedure similar to that for users. Groups have no “home directories” like users do, but as the administrator you can of course create arbitrary directories meant for certain groups and having appropriate access rights.

Groups, too, are identified internally using numerical identifiers (“group IDs” or GIDs).

![](img/44bdd771e9c9b1353d2401c2892b2459_170_3.png)

Group names relate to GIDs as user names to UIDs: The Linux kernel only knows about the former and stores only the former in process data or the file system.

Every user belongs to a primary group and possibly several secondary or additional groups. In a corporate setting it would, for example, be possible to introduce project-specific groups and to assign the people collaborating on those projects to the appropriate group in order to allow them to manage common data in a directory only accessible to group members.

¹ Which of course is slightly more dangerous again, since programs running on the same screen can communicate with one another

![](img/44bdd771e9c9b1353d2401c2892b2459_170_4.png)

![](img/44bdd771e9c9b1353d2401c2892b2459_170_5.png)

![](img/44bdd771e9c9b1353d2401c2892b2459_170_6.png)

For the purposes of access control, all groups carry equivalent weight—every user always enjoys all rights deriving from all the groups that he is a member of. The only difference between the primary and secondary groups is that files newly created by a user are usually² assigned to his primary group.

Up to (and including) version 2.4 of the Linux kernel, a user could be a member of at most 32 additional groups; since Linux 2.6 the number of secondary groups is unlimited.

You can find out a user account’s UID, the primary and secondary groups and the corresponding GIDs by means of the *id* program:

```bash
$ id
uid=1000(joe) gid=1000(joe) groups=24(cdrom),29(audio),44(video),1000(joe)
$ id root
uid=0(root) gid=0(root) groups=0(root)
```

With the options *-u*, *-g*, *-G*, *id* lets itself be persuaded to output just the account’s UID, the GID of the primary group, or the GIDs of the secondary groups. (These options cannot be combined.) With the additional option *-n* you get names instead of numbers:

```bash
$ id -G
1000 24 29 44
$ id -Gn
joe cdrom audio video
```

The *groups* command yields the same result as the `id -Gn` command.

You can use the *last* command to find who logged into your computer and when (and, in the case of logins via the network, from where):

```bash
$ last
joe     pts/1      pcjoe.example.c  Wed Feb 29 10:51   still logged in
bigboss pts/0      pc01.example.c   Wed Feb 29 08:44   still logged in
joe     pts/2      pcjoe.example.c  Wed Feb 29 01:17 - 08:44 (07:27)
sue     pts/0      :0               Tue Feb 28 17:28 - 18:11 (00:43)
<reboot>
reboot  system boot 3.2.0-1-amd64      Fri Feb   3 17:43 - 13:25 (4+19:42)
<xxxxxx>
```

For network-based sessions, the third column specifies the name of the *ssh* client computer. “`:0`” denotes the graphical screen (the first X server, to be exact—there might be more than one).

Do also note the *reboot* entry, which tells you that the computer was started. The third column contains the version number of the Linux operating system kernel as provided by `uname -r`.

With a user name, *last* provides information about a particular user:

```bash
$ last joe
joe     pts/1      pcjoe.example.c  Wed Feb 29 10:51   still logged in
joe     pts/2      pcjoe.example.c  Wed Feb 29 01:17 - 08:44 (07:27)
<xxxxxx>
```

² The exception occurs where the owner of a directory has decreed that new files and subdirectories within this directory are to be assigned to the same group as the directory itself. We mention this strictly for completeness.

You might be bothered (and rightfully so!) by the fact that this somewhat sensitive information is apparently made available on a casual basis to arbitrary system users. If you (as the administrator) want to protect your users' privacy somewhat better than your Linux distribution does by default, you can use the

```bash
# chmod o-r /var/log/wtmp
```

command to remove general read permissions from the file that *last* consults for the telltale data. Users without administrator privileges then get to see something like:

```bash
$ last
last: /var/log/wtmp: Permission denied
```

### 13.1.3 People and Pseudo-Users

Besides “natural” persons—the system’s human users—the user and group concept is also used to allocate access rights to certain parts of the system. This means that, in addition to the personal accounts of the “real” users like you, there are further accounts that do not correspond to actual human users but are assigned to administrative functions internally. They define functional “roles” with their own accounts and groups.

After installing Linux, you will find several such pseudo-users and groups in the `/etc/passwd` and `/etc/group` files. The most important role is that of the `root` user (which you know) and its eponymous group. The UID and GID of `root` are 0 (zero).

`root`’s privileges are tied to UID 0; GID 0 does not confer any additional access privileges.

Further pseudo-users belong to certain software systems (e.g., `news` for Usenet news using INN, or `postfix` for the Postfix mail server) or certain components or devices (such as printers, tape or floppy drives). You can access these accounts, if necessary, like other user accounts via the `su` command. These pseudo-users are helpful as file or directory owners, in order to fit the access rights tied to file ownership to special requirements without having to use the `root` account. The same applies to groups; the members of the `disk` group, for example, have block-level access to the system’s disks.

## Exercises

- 13.1 [1] How does the operating system kernel differentiate between various users and groups?
- 13.2 [2] What happens if a UID is assigned to two different user names? Is that allowed?
- 13.3 [1] What is a pseudo-user? Give examples!
- 13.4 [2] (On the second reading.) Is it acceptable to assign a user to group `disk` who you would not want to trust with the `root` password? Why (not)?

## 13.2 User and Group Information

### 13.2.1 The /etc/passwd File

The `/etc/passwd` file is the system user database. There is an entry in this file for every user on the system—a line consisting of attributes like the Linux user name,
