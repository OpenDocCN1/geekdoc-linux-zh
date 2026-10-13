
```
mthorne has UID=500 and GID=500
mdella has UID=501 and GID=501
taylor has UID=502 and GID=502
```

By convention, UIDs lower than 100 are system accounts or system IDs and should be ignored. The only exception is UID=0, which is the root or superuser account. You want to keep track of that because anyone with that ID can ignore all file permissions and edit, change, and even delete any file they'd like.

3. A simple awk command to use occasionally to keep track of these UID=0 accounts—since a sysadmin can always set up any number of different accounts with a given UID, and UID=0 is obviously the most important to watch—is

```
awk -F: '{ if ($3 == '0') print $0 }' /etc/passwd
```

Your output should be a single line: the root account. If there are other matches, you need to immediately look into it and ascertain why there's another superuser account. (We'll explore this issue further in Hour 5, "Working with User Accounts.")

4. To change the owner UID of a file or directory, use the chown command. To demonstrate, let's try to change the ownership of the testfile file created earlier to games (which you can see in the earlier listing is UID=12):

```
$ chown games testfile
chown: changing ownership of 'testfile': Operation not permitted
```

This error is good news, in fact. This means that Red Hat Linux 7.2 is one of the Unix systems available that prevents users from changing the ownership of their own files. Why? Because otherwise there's a really sneaky way that users can circumvent quotas. They could change the ownership of a very large file (an MP3 archive, for example) to a+rwx (giving everyone read, write, and execute access), then changing ownership to another user ID. When the quota system analyzes disk usage by UID, the huge file shows up as being owned by someone else. When the user wants to return to their ownership, they copy it into a new filename (which they own by default), and delete the version that had been recorded as owned by the other user. Tricky, eh?

![](img/5ced0c78d748bd190e9027e5549a3622_88_0.png)

> Both Solaris and Darwin have a similar restriction on chown usage by regular users, so this sneaky trick must be more popular than I thought!

Good news or not, this means that it's time to become root to be able to change ownership. This can be done a variety of different ways, but I typically use su, which, without any arguments, spawns a subshell as UID=0, after prompting for the root account password.

```
$ su
Password:
bash-2.05# chown games testfile
bash-2.05# ls -lAF
total 176
drwxr-x--- 4 taylor coders 4096 Jan 7 21:47 ./
drwxr-x--- 13 taylor coders 4096 Jan 7 22:27 ../
-rw-rw---- 1 taylor coders 263 Dec 5 05:12 snapshot.sh
-rw-rw---- 1 taylor coders 153600 Dec 5 05:12 sourcefiles.cpio
drwxr-xr-x 2 taylor coders 4096 Dec 5 05:12 Src/
drwxrwxr-x 2 taylor coders 4096 Jan 7 21:47 testdir/
-rw-rw-r-- 1 games coders 0 Jan 7 21:47 testfile
```

As you can see, as root I can change ownership of a file with nary a complaint or warning.

5. An interesting observation is that although the Unix system displays the UID by account name, it's really only storing it by account ID. Which means, if user medella were to ask me, as sysadmin, to change his login account name to marcos, all I'd have to do is change the first word of the account-information line in /etc/passwd, and all the file listings would magically change as well.

For example, if I change taylor to davet in the password file:

```
davet:x:502:502:Dave Taylor:/home/taylor:/bin/bash
```

then the very same ls command has different results:

```
# ls -lAF
total 176
drwxr-x--- 4 davet coders 4096 Jan 7 21:47 ./
drwxr-x--- 13 davet coders 4096 Jan 7 22:27 ../
-rw-rw---- 1 davet coders 263 Dec 5 05:12 snapshot.sh
-rw-rw---- 1 davet coders 153600 Dec 5 05:12 sourcefiles.cpio
drwxr-xr-x 2 davet coders 4096 Dec 5 05:12 Src/
drwxrwxr-x 2 davet coders 4096 Jan 7 21:47 testdir/
-rw-rw-r-- 1 games coders 0 Jan 7 21:47 testfile
```

Working with account IDs in Unix is fairly straightforward, and if you're already working on a Unix system, it was doubtless a simple review. Unix handles groups in a way that is quite helpful, but understood much less. That's what we'll explore next.

## Understanding Unix Groups and /etc/group

To fully understand Unix groups, it's helpful to take some time to talk about the historical roots of the Unix operating system. Unix was developed at AT&T Bell Telephone Labs (also known as Bell Labs, now a core part of Lucent Corporation) during a period when all computers were shared by multiple users. In the jargon of the time, Unix is a multiuser, multitasking operating system.

One of the challenges of multiuser systems is file permission, and a popular research operating system at the time that had gained considerable attention at Bell Telephone Labs (BTL) was Multics. Developed originally by BTL, the Massachusetts Institute of Technology, and General Electric (BTL later dropped out of the project), Multics was an astonishingly complex multiuser system that had a highly sophisticated security model, based on concentric circles of access to files, peripherals, and applications.

Brian Kernighan and Ken Thompson, the inventors of the Unix system, had helped with Multics before BTL quit, and although they liked many of its capabilities, they disliked its complexity. The Unix security model, therefore, has an approximately similar concept of circles of access, but in a much simpler manner.

> It's worth mentioning that the name Unix is a bit of a poke at Multics. UN-IX, MULTI-ICS. The saying at Bell Labs used to be "Unix is one of whatever Multics was many of." Learn more, if you're curious, at http://www.multicians.org/

On first glance, the Unix security model seems to be three levels of access: owner, group, and everyone else. A glimmer of how this can be more complex was suggested earlier when I used the id command and learned that I was in two groups, not one. Therefore, although files, programs, or directories can only have a single owner and group, a user can be a member of many groups and thereby end up with access privileges that represent the union of all the individual permissions.

> It's not entirely true that files can only have one owner and group. Creating a hard link to a file can enable the new name to be assigned a different owner and/or group. Yet there's still only one file on the system, so no additional disk space has been consumed. This is a very important concept for system administrators who are going to develop more sophisticated access control methods on their system.

For our purposes, let's start by exploring standard Unix groups, then go from there.

## Task 4.3: Groups and the /etc/group file

Every user account is assigned what's called a default group. On many modern Unix systems, the use of groups has become so uncommon that by default every user gets his own group, effectively negating a powerful characteristic of the Unix operating system itself.

1. Look at the last ten lines of the /etc/passwd file for a moment, running it through the awk filter, shown earlier in this hour:

```
$ awk -F ':' '{print $1" has UID="$3" and GID="$4}' < /etc/passwd | tail
```

radvd has UID=75 and GID=75
postgres has UID=26 and GID=26
apache has UID=48 and GID=48
squid has UID=23 and GID=23
named has UID=25 and GID=25
pcap has UID=77 and GID=77
mthorne has UID=500 and GID=500
mdella has UID=501 and GID=501
taylor has UID=502 and GID=502

Notice that every UID has a corresponding GID, and that no two accounts share a default group.

I think this is somewhat silly. It's akin to buying a Ferrari and never putting it in high gear, or a multifunction stereo and only listening to AM radio. (Well, maybe that's a bit of an exaggeration!)

Since mthorne and taylor are both administrators, it would actually make more sense to have them in the same administrative group on this system. mdella, by contrast, is a regular user and should not be included in the sysadmin group.

2. To change who is in what group, it's time to delve into the /etc/group file. Let's start by examining the file (which does have a tendency to vary in format from flavor to flavor, in case yours isn't exactly the same):

```
$ head /etc/group
```

root:x:0:
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon,taylor
tty:x:5
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8:
kmem:x:9:

As you can see, the file format is quite similar to the /etc/passwd file examined earlier. In this case, the format for each line is

account name : encrypted password : group ID : member list

The first thing to notice is that an encrypted password value of x denotes that there's a shadow password file stored elsewhere on the system—for security reasons—that has the actual encrypted password string. The next hour explores the password's /etc/shadow file, but for groups, the relevant group file is

![](img/5ced0c78d748bd190e9027e5549a3622_91_0.png)
