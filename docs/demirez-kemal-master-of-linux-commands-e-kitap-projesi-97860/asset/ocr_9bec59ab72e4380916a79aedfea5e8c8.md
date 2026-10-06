# 212 | Master of Linux Commands

We discussed how to list the fields above. Now let's make a similar example, but this time let's list the beginning and ending fields. For example let's find out what's in the beginning and ending fields in the lines of /etc/passwd file, we use awk -F: '{print $1, $NF}' /etc/passwd command.

```
root@kernel:~ awk -F: '{print $1, $NF}' /etc/passwd
root /bin/bash
daemon /usr/sbin/nlogin
bin /usr/sbin/nlogin
sys /usr/sbin/nlogin
sync /bin/sync
games /usr/sbin/nlogin
man /usr/sbin/nlogin
lp /usr/sbin/nlogin
mail /usr/sbin/nlogin
news /usr/sbin/nlogin
uucp /usr/sbin/nlogin
proxy /usr/sbin/nlogin
```

The following three commands do the same thing: gives the total size of the files listed after the command.

+   - ls -l | awk '{sum += $5} END {print sum}'
- ls -l | grep -v '^total' | awk '{sum += $5} END {print sum}'
- ls -l | awk '^total/(getline) {sum += $5} END {print sum}'

```
root@kernel:~ ls -l | awk '{sum += $5} END {print sum}'
45608
root@kernel:~ ls -l | grep -v '^total' | awk '{sum += $5} END {print sum}'
45608
root@kernel:~ ls -l | awk '^total/(getline) {sum += $5} END {print sum}'
45608
root@kernel:-#
```

There are different ways to use our command. Let's give an example. We will work on the /etc / passwd file again. Let's