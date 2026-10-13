
```
chmod 755 $homedir
chown $login $homedir
echo "Please enter a default initial password for $login now:"
passwd $login
```

In a small nutshell, those six lines accomplish almost all that the adduser command requires. In a bit, you'll see how we can deal with the shadow file issue. The only two steps missing are to manipulate the /etc/group file appropriately (which many adduser scripts skip), and copy across any default cshrc, login, or profile files.

## 5. Adding the new user in the /etc/group file is easy if each user gets her own group. It's accomplished with one line:

```
echo "$login:x:${gid}:${login}" >> /etc/group
```

Where things get more difficult is if we're adding the new user to an existing group. Then we need to extract the group line from the /etc/group file, append the user name, then write it back to the file:

```
grep -v "$groupname": /etc/group > /tmp/group.tmp.$$
grep "$groupname": /etc/group > /tmp/group
echo "$groupline,$login" >> /tmp/group.tmp.$$
mv /tmp/group.tmp.$$ /etc/group
chmod 644 /etc/group
```

This no doubt looks odd, but we copy every line but the matching group line to a temp file; then set groupl ine to the matching line that's been extracted, append the new login, and then move the temp group file to the master group file and change its mode to our required default (644).

## 6. Finally, to copy default configuration files across, Linux includes the standard /etc/skel directory, which contains prototypical default files for new home directories:

```
$ ls -la /etc/skel
total 15
drwxr-xr-x 3 root root 1024 Nov 21 14:48 ./
drwxr-xr-x 50 root root 4096 Jan 10 06:12 ../
-rw-r--r-- 1 root root 24 Jul 9 2001 .bash_logout
-rw-r--r-- 1 root root 191 Jul 9 2001 .bash_profile
-rw-r--r-- 1 root root 124 Jul 9 2001 .bashrc
-rw-r--r-- 1 root root 820 Jul 30 03:03 .emacs
-rw-r--r-- 1 root root 118 Aug 9 17:15 .gtkrc
drwxr-xr-x 3 root root 1024 Nov 21 14:40 .kde/
-rw-r--r-- 1 root root 3511 Aug 3 09:53 .screenrc
```

Because there's a subdirectory (for KDE, the K Desktop Environment) we'll want to use the -R flag to cp when we copy these files across.

Now, with all that, here’s the complete second half of the script, built with the assumption that every user gets his own group.

```
echo "Setting up account $login for $fullname..."
echo "$login:x:$uid:$gid:$fullname:$homedir:$shell" >> /etc/passwd
echo "$login:*::11647:0:99999:7:::" >> /etc/shadow
echo "$login:x:$gid:$login" >> /etc/group
#uncomment below if your system is using group shadow files too
#echo "$login::::" >> /etc/gshadow
mkdir $homedir
cp -R /etc/skel/[a-zA-Z]* $homedir
chmod 755 $homedir
find $homedir -print | xargs chown $login
echo "Please enter a default initial password for $login now:"
passwd $login
exit 0
```

Notice that because this version of Unix is working with shadow password files, we need to include new entries for the account in /etc/shadow, and for the group in /etc/gshadow.

![](img/5ced0c78d748bd190e9027e5549a3622_115_0.png)

> Solaris doesn’t use the gshadow file. Instead the encrypted passwords for groups are saved in the /etc/group file regardless of whether shadow passwords are enabled on the system overall.

![](img/5ced0c78d748bd190e9027e5549a3622_115_1.png)

```
# sh adduser.sh
Add new user account to staging.intuitive.com
login: testdude
full name: The Test Dude
shell: /bin/bash
Setting up account testdude for The Test Dude...
Please enter a default initial password for testdude now:
Changing password for user testdude
New password:
Retype new password:
passwd: all authentication tokens updated successfully
```

That’s all that’s required. Simple, succinct, and the resultant account is ready to go with default files from /etc/skel and everything.

This has been a long and involved script that has demonstrated a variety of sophisticated shell script techniques. It also is written in a completely portable fashion, can be run easily on any system that supports shadow passwords, and, with a few small tweaks, even on systems that don't have /etc/shadow enabled.

To have the adduser script work with an NIS-compatible system like Solaris, I'd recommend making the adduser script a front end to the built-in useradd utility. Darwin, with NetInfo, is a proverbial horse of a different color, as the next section will succinctly detail.

## Adding Users in a NetInfo World

The earlier shell script for adding users directly manipulated the /etc/passwd file, but as was demonstrated earlier, systems running NetInfo or another NIS descendant require new users to be added to the NIS database. This sounds harder than it is, though, because that's exactly what the niutil command does.

## Task 5.4: The Darwin Version of adduser

The world of NetInfo not only changes how we need to examine the user account data, but also forces significant changes on how new accounts are created. That's the bad news. The good news is that Darwin includes a variety of different command-line NetInfo utilities, most notably including the general purpose niutil.

There are two modes to niutil that we're interested in for this task: -create specifies that a new entry should be made in the database, then -createprop adds specific properties and assigns the specified values within the specified record.

- 1. To start out, we'll have to recode the section that calculates the highest UID in use.
- To do this, we'll use nireport and sort -n:
```
uid1=`nireport . /users uid | sort -n | tail -1`
uid=`expr $uid1 + 1`
```
- The next step is to actually create a new user account record. This can be done with niutil, using the -create option:
```
niutil -create . /users/$login
```
- 2. Each individual property of the user record must be defined and have a value assigned to it. It's a bit more work than a single line output to /etc/passwd:
```
niutil -createprop . /users/$login passwd
niutil -createprop . /users/$login uid $uid
niutil -createprop . /users/$login gid $gid
niutil -createprop . /users/$login realname "$fullname"
niutil -createprop . /users/$login shell $shell
niutil -createprop . /users/$login home $homedir
```

There shouldn't be any surprises in the name/value pairs but it's worth highlighting that fullname is the only variable that might have spaces, hence the quotes in the script.

- 3. For the Darwin version of the script, we're also going to add all users to the home-team group rather than give them each unique groups. This is done by using the niutil command to modify the field users for the specified group:

niutil -appendprop . /groups/hometeam users $login

Other than those changes, the rest of the script is identical to the Linux version.

Here's the entire Darwin adduser script:

```
#!/bin/sh

# ADDUSER - add a new user to the system, including building their
#           home directory, copying in default config data, etc.

progname=`basename $0`
dgroup="hometeam"
dgid=101
hdir="/Users"

if [ "`whoami`" != "root" ] ; then
  echo "$progname: Error: You must be root to run this command."
  # exit 0
fi

echo "Add new user account to `hostname`"
echo -n "login: "  ; read login

uid1=`nireport . /users uid | sort -n | tail -1`
uid=`expr $uid1 + 1`
homedir=$hdir/$login

# we are putting all users into the $dgroup group, which has a fixed GID
gid=$dgid

echo -n "full name: " ; read fullname
echo -n "shell: "   ; read shell

echo "Setting up account $login for $fullname..."

niutil -create      . /users/$login
niutil -createprop . /users/$login passwd
niutil -createprop . /users/$login uid $uid
niutil -createprop . /users/$login gid $gid
niutil -createprop . /users/$login realname "$fullname"
niutil -createprop . /users/$login shell $shell
niutil -createprop . /users/$login home $homedir
```

```
niutil -createprop . /users/$login _shadow_passwd ""
# adding them to the $dgroup group...
niutil -appendprop . /groups/$dgroup users $login

mkdir $homedir

if [ -d /etc/skel ] ; then
  cp -R /etc/skel/.[a-zA-Z]* $homedir
fi

chmod 755 $homedir
find $homedir -print | xargs chown $login

echo "Please enter a default initial password for $login now:"
passwd $login

exit 0
```

4. Let's test it out by creating an account!

```
$ adduser
adduser: Error: You must be root to run this command.
```

Oops! Use the su command to switch to root (you'll need to enter your administrative password) and try again:

```
# adduser
Add new user account to ds1-132.ds1designs.com
login: tintin
full name: Tintin, Boy Reporter
shell: /bin/tcsh
Setting up account tintin for Tintin, Boy Reporter...
Please enter a default initial password for tintin now:
Changing password for tintin.
New password:
Retype new password:
```

And verify its existence and proper creation:

```
# ni report . /users name realname
nobody Unprivileged User
root System Administrator
daemon System Services
unknown Unknown User
www World Wide Web Server
taylor Dave Taylor
badguy Test Account
tintin Tintin, Boy Reporter
```

Welcome to the world of Darwin, Mr. Tintin! All looks good.
