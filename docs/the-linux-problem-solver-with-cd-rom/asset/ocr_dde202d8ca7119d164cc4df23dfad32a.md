Of course, you should not even think about having the filesystem mounted when using debugfs.
If you modify a filesystem with tune2fs or debugfs, run fsck on the filesystem to get rid of any inconsistencies your change may have brought about.
Relevant man pages: tune2fs (8), debugfs (8)

# Recognizing and Repairing System File Problems

Half of the battle in getting a broken system up and running again is making sure the various files (usually in /etc) are correct, and getting them back into the right format if they aren’t.

# PROBLEM 105

Symptoms: You don’t know the root password. Commands say they don’t know who you are and ignore /etc/passwd.

Problem: You’re having passwd file difficulties (corrupted file, missing entries, incorrect data, and so on).

Fix: If you don’t know the root password, and you’ve got the root filesystem mounted from a rescue CD or some similar medium, you can delete the second field of root’s /etc/passwd entry (but don’t leave it this way for long):

```
root::0:0:Super-User::/bin/bash
```

This change allows you to log in as root without a password (the second field in the passwd file is the encrypted password). Check out /etc/shadow as well if you’re using shadow passwords; you may need to make similar changes there.

If you somehow deleted the passwd file, get one started again with at least this (you can restore the rest later):

```
root::0:0:Super-User::/bin/bash
daemon:*::1:1:daemon:/usr/sbin:/bin/sh
```

Finally, check /etc/nsswitch.conf. You’re probably looking for trouble if you don’t have

```
passwd:  compat
```

or

```
passwd:  files
```

in there.