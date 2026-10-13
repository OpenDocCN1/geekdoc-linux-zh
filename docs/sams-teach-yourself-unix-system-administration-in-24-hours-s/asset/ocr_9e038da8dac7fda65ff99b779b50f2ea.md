```
$ passwd badguy
Changing password for badguy.
New password:
Retype new password:
$ ni report . /users name passwd | grep badguy
badguy Hk4IS.3eeh69.
```

Looks like things are safe again!

In some sense, NetInfo is a great application, managing the various databases that comprise the Unix system world, including printers, Internet services, user accounts, and network connections. It also has a venerable pedigree, coming from the Network Information Service (NIS) and Yellow Pages (YP) services originally developed by Sun Microsystems. (More in a minute about those services.)

However, NetInfo is also a bit of an oddball in the Unix world. Not only is it not a part of the popular Linux distributions, it's also not included in any of the major commercial Unix distributions either (other than Mac OS X). NetInfo is therefore very incompatible and platform- and version-specific.

Ordinarily, I'd recommend that you shy away from using the utility for just this reason, but if you're running Darwin or another NIS/YP-enabled (NetInfo) Unix system, you must go through the NetInfo facility or your changes will be ignored. As an example, the /etc/passwd file on the test Darwin platform includes the following few lines at its end:

```
$ tail -3 /etc/passwd
www::70:70:World Wide Web Server:/Library/WebServer:/noshell
unknown::*99:99:Unknown User:/nohome:/noshell
testme::0:0:Unknown Root User:/var/root:/bin/tcsh
```

Yet you'll notice that the testme account never showed up in the NetInfo listings if you flip back and look. That's because it was added to the password file, but not to the NetInfo database.

# Adding Users and the adduser Script

Putting Darwin, BSD, and the NetInfo weirdness aside for a bit, let's breathe some fresh air and go back to "regular Unix" (whatever that means!), okay?

There are a couple of steps required for creating a new user account, more than just creating a new entry in the /etc/passwd file. These steps are as follows:

+   1. Add the user to the /etc/passwd file.
+   2. Add the user to the /etc/group file.
+   3. Create their home directory.