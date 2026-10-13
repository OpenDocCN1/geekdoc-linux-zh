```
for account in `passwd -sa | grep NP | awk '{print $1}'`
do
  shell=`egrep "^${account}:!:" /etc/passwd | cut -d: -f7`
  if [ "$shell" != "/sbin/nologin" ] ; then
    echo "*** WARNING: Account $account has no password and login shell $shell"
  fi
done

exit 0
```

When it's run, the results are what you would hope:

```
# checkpw.sh
*** WARNING: Account testdude has no password and login shell
/bin/sh
```

# 5. Let's lock testdude out with the passwd -l option:

```
# passwd -l testdude
# passwd -s testdude
testdude LK
```

No feedback was given on the first command, but the -s summarizes the new state as LK (locked), which is correct. To unlock the account again, use passwd testdude, then enter an appropriate new password value.

# 6. One more quick examination of the userdel command for comparison's sake proves that it's 100% identical to the Linux version shown earlier. Hurray!

```
# man userdel
Maintenance Commands
userdel(1M)
```

NAME
userdel - delete a user's login from the system

SYNOPSIS
userdel [ -r ] login

DESCRIPTION
The userdel utility deletes a user account from the system and makes the appropriate account-related changes to the system file and file system.

OPTIONS
The following options are supported: