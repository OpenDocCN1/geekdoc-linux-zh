After Frank has used **keyinit** to set up his S/Key mechanism and has added an entry for his login to `/etc/skeykeys`, you must create the file `/etc/skey.access` (if it doesn't already exist) and add the following line:

```
```
deny user frank
```
```

The `/etc/skey.access` file tells FreeBSD under what conditions a remote user is permitted to use his regular Unix password, and under what conditions he must use an S/Key one-time password. A line in `skey.access` specifies a rule beginning with **permit** (allowing either an S/Key or Unix password) or **deny** (requiring an S/Key password), followed by as many conditions as you like. These conditions can specify certain users, groups, remote hostnames or networks, or login terminals (you can read a full description of the conditions in `man skey.access`). The sample line you just saw requires that when Frank tries to log in, only an S/Key password is permitted—not his Unix password.

The next time Frank uses Telnet to connect to your system, his login prompt will look like this:

```
```
# telnet stripes.somewhere.com
Trying 64.41.131.102...
Connected to stripes.somewhere.com.
Escape character is '^]'.

FreeBSD/i386 (stripes.somewhere.com) (tty2)

login: frank
s/key 99 st28077
Password:
```
```

> **NOTE**
> 
> As mentioned earlier, S/Key provides a way to make even clear-text Telnet logins secure. However, if you have a tight security policy, you should require your users to use SSH and disable Telnet logins altogether. If Frank were to use SSH to connect, the S/Key behavior would be the same as in the example, although the output lines would look somewhat different.

Frank must now use the **key** program (or its equivalent) on his own machine to figure out what password to enter. He has to feed it the challenge information presented by the server: the iteration count (99 in this case, meaning that there are 99 logins left before Frank must run **keyinit** again), followed by the “seed” string (st28077 here, the same as you saw in the **keyinit** example). These numbers, combined with Frank's secret password, generate an S/Key password made up of six short, uppercase English words:

```
```
# key 99 st28077
Reminder - Do not use this program while logged in via telnet or rlogin.
```
```