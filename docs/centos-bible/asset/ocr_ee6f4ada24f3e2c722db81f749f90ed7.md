```
/usr/sbin/tmpwatch 720 /var/tmp
for d in /var/(cache/man,catman)/|cat2,X11R6/cat2,.local|cat2]; do
if [ -d " $d" ]; then
/usr/sbin/tmpwatch " $flags" -f 30d $d
fi
done
```

Each day, this tmpwatch script runs to delete temporary files that haven't been used for some time. The flags (-umc) indicate that time access is based on the file's access time (u), modification time (m), and inode change time (c). It starts by identifying files that are not to be deleted (tmpwatch -x). Files such as those in the /tmp/X11-unix directory represent sockets for active X servers and would make an active GUI inaccessible if they were deleted. All other files from the /tmp and /var/tmp directories are removed after 10 and 30 days of not being accessed, respectively. Temporary man page files stored in /var/cache subdirectories are also checked and deleted after 30 days of disuse.

# ## Sending Mail to All Users

Occasionally, you need to send messages to all users on your system. Warning users of planned downtime for hardware upgrades is a good example. Sending e-mail to each user individually is extremely time-consuming and wasteful; this is precisely the kind of task that e-mail aliases and mailing lists were invented for. Keeping a mailing list of all the users on your system can be problematic, however. If you are not diligent about keeping the mailing list current, it becomes increasingly inaccurate as you add and delete users. Also, if your system has many users, the mere size of the alias list can become unwieldy.

The following script, called *maillfile*, provides a simple method of working around these problems. It grabs the login names from the /etc/passwd file and sends e-mail to all users.

> > **NOTE** Because regular user accounts begin with UID 500 in CentOS, the script excludes all UIDs under 500 that are typically administrative accounts. It also skips UID 65,534, which is the anonymous NFS user account.

```
#!/bin/bash
# maillfile: This script mails the named file to all regular
# users of the system. It skips all administrative
# accounts (accounts under UID 500) as well as the
# anonymous NFS user (UID 65534).
#
#
# USAGE: maillfile "Subject goes here" filename.txt
#
# Check for a subject
#
# Get the subject of the message
subject=$1
```