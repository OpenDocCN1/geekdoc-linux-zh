# Transferring the Updated Password Files

In all these cases, the updated password file is deposited in a "safe" place (a partition with lots of space), and then a script copies it to /etc/passwd with suitable safety checks. The script could be as simple as the following pseudocode example.

```
if [! -f /etc/ptmp ]; then
cp /some/safe/place/in/root /etc/ptmp
mv /etc/ptmp /etc/passwd
fi
```

That's almost what I've done, but without the race condition. The code is in the client password update script (Listing 15.3).

# Listing 15.3 The client password update script deposits the updated password files in a partition with lots of space, then copies them to /etc/password with suitable safety checks.

```
#!/bin/sh
#
# passwd-update -- update /etc/passwd from a copy of the master.
# Spends most of it's time checking to see if it succeeded.
#
SAFEPLACE=/usr/local/etc/passwd # Place where the master puts it.
SAFEMINIMUM=25 # Smallest allowable /etc/passwd file size, in lines.

if ccopy $SAFEPLACE /etc/ptmp; then
: It was ok.
else
echo "$0: /etc/ptmp exists, therefore the /etc/passwd file"
echo " is locked. Try again later, please."
exit 0
fi
```