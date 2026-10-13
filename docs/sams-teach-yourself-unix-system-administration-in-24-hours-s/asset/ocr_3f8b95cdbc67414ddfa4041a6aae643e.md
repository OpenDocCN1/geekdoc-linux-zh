```
if [ "`who | grep $1`" != "" ] ; then
sid=`ps -U $1 | awk '{print $3}' | tail -1`
kill -HUP $sid
echo "$1 was logged in. Just logged $1 out."
fi
```

If you force the logout of a user while he's logged in, be prepared for an emotional response! A better way to code this is to have the script warn him, then give him a few seconds to promptly exit his apps before being booted off.

To send a message to a user on the system, there's a faster solution than sending e-mail that might be ignored: Write information directly to the user's terminal device. Consider the second field in the output of the who command:

```
$ who
taylor pts/0 Jan 14 05:09 (dsl-132.dsidesigns.com)
testdude pts/1 Jan 14 05:11 (dsl-132.dsidesigns.com)
```

That's the terminal device address if you preface it with /dev/ (so testdude is logged in to /dev/pts/1). Obtain that information and you can write a message to the user's screen directly (then sleep $secs seconds):

```
tty=`who | grep $1 | tail -1 | awk '{print $2}'`
cat << "EOF" > /dev/$tty
**************************************************
URGENT NOTICE FROM THE ADMINISTRATOR:
This account is being suspended by the request of management.
You are going to be logged out in $secs seconds. Please
shut down any processes you have running immediately.
If you have any questions, please contact your supervisor or
Jane Mansmith, director of corporate computing.
**************************************************
EOF
echo "(Warned $1, now sleeping $secs seconds)"
sleep $secs
```

Another step I like to take when suspending accounts is to close off the user's home directory. This is also easy:

```
chmod 000 $homedir/$1
```

3. In total, and with some useful comments added, the suspend script looks like this:

```
#!/bin/sh

## Suspend - suspend a user account for the indefinite future

secs=10 # seconds before user is logged out (if logged in)
homedir="/home" # home directory for all users
```