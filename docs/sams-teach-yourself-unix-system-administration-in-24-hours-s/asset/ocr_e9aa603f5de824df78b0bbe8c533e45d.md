2. The second step required is to remove the user's home directory and all its contents within a script, assuming that $1 is the user's account name:

```
rm -rf $homedir/$1
```

There's a nuance to this, however, because the user might very well have files elsewhere on the system.

3. Finding these stray files is a job for the find command, which will search throughout the file system for any remaining files or directories that are owned by the user.

For example:

```
$ find / -uid 501 -print
```

/var/spool/mail/mdella

In this case, you can see that though you've stripped all the files in the /home directory, there was still an e-mail mailbox lingering in the spool directory.

One ramification of adding this check for files outside the user's home directory is that you need to grab the UID of the account before deleting it. This is done with the line

```
uid="`egrep "^$1\(:" /etc/passwd | cut -d: -f3`"
```

4. Here's the full script with the exception of stripping the account information out of shadow files. Notice that the first step is to call the suspend script to ensure that the user can't log in and is logged out if needed. No reason to duplicate that code here!

```
#!/bin/sh

## Delete - delete a user account without a trace...

homedir="/home"

if [ "$1" = "" ] ; then
 echo Usage: `basename $0` account; exit 0
fi
if [ "`whoami`" != "root" ] ; then
 echo `basename $0`: Error. You must be 'root' to run this command.
 exit 0
fi

suspend $1  # suspend their account while we do the dirty work

uid=`egrep "^$1\(:" /etc/passwd | cut -d: -f3`

egrep -v "^$1\(:" /etc/passwd > /tmp/newpasswd
mv /tmp/newpasswd /etc/passwd
chmod 655 /etc/passwd

rm -rf $homedir/$1
```