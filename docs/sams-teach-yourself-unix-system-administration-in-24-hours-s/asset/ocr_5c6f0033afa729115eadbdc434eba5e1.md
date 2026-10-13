```
# This only runs on Linux systems with the '-S' flag to 'passwd'
temp="/tmp/tocheck.$$"

trap "/bin/rm -f $temp" 0  # remove the file upon exit

for name in `cut -d: -f1 /etc/passwd`
do
  echo "$name" | passwd -S $name | tail -1 | \
  egrep -v "(Locked|encryption)" | awk '{print $1}' >> $temp
done

for account in `cat $temp`
do
  shell=`egrep "^${account}:" /etc/passwd | cut -d: -f7`
  if [ "$shell" != "/sbin/nologin" ] ; then
    echo "*** WARNING: Account $account has no password and login shell $shell"
  fi
done
exit 0
```

Nothing too fancy in this script, but notice that we've had to resort to a temporary file for intermediate output. The results are quite helpful and could easily become part of a daily system status report:

```
# checkpw.sh
*** WARNING: Account sync has no password and login shell /bin/sync
*** WARNING: Account shutdown has no password and login shell /sbin/shutdown
*** WARNING: Account halt has no password and login shell /sbin/halt
*** WARNING: Account news has no password and login shell /bin/sync
*** WARNING: Account testdud has no password and login shell /bin/bash
```

The shells sync, shutdown, and halt are indicative of shortcuts available at the login prompt. Type in shutdown as the account name and—remember that there's no password—the system will probably be shut down. You might want to disable those accounts if you don't think you'll ever need them.

> In more than 20 years of working with Unix systems, most of which had these three administrative logins, I've never used them in this manner. I always shut these accounts off when I install a new system.