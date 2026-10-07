```
if grep "^${USER?:"Unable to determine user"}" /etc/
asswd > /dev/null
then print "You have a local account on this system."
else print "You have a network account for accessing this system."
fi
```