He will run the script “in the background.” To submit the job for background use, he uses the “&” (ampersand symbol; Juana calls it a “pretzel”). Here is how he will do it:

```
$ warn_users &<Enter>
```

In October, when the “crunch” comes, this message is what the users will see every five seconds:

Broadcast message from freston (pts/2) Mon Oct 15 14:50:54 2001…  
If you are not active please logout!

Broadcast message from freston (pts/2) Mon Oct 15 10:50:54 2001…  
System will be slow because there are 456 other users logged in.

Broadcast message from freston (pts/2) Mon Oct 15 10:50:59 2001…  
If you are not active please logout!

Broadcast message from freston (pts/2) Mon Oct 15 10:50:59 2001…  
System will be slow because there are 456 other users logged in.

They will hate him for it. But it will work. And everyone will still be able to work.

# **Example 13.16 “Until Looping” to Prevent a System Crash**

Freston could have taken a different approach to the same problem by implementing an *until* script. With this script, *until* the number of users logged in is reduced to 425, the messages will continue to appear. That script would look like the following:

```
$ cat > warn_users <Enter>  
#!/bin/bash  
  
# This script warns users that the system may be slow due to peak usage  
# It will urge them to logout if they aren't active  
  
var4=`w | wc -l`  
until [ $var4 -lt "425" ] ; do  
    wall System will be slow because there are $var4 other users logged in.  
    wall If you are not active please logout!  
sleep 5  
done  
<Ctrl>-d
```