# Chapter 14 • INTERNAL COMMUNICATION

RCS checks out most recent version of a by default, but if you have a specific version in mind, you can check it out using the -r flag, as follows:

```
$ co -r1 httpd.conf
RCS/httpd.conf,v --> httpd.conf
revision 1.2 (locked)
done
```

![](bbox=[0.093, 0.206, 0.153, 0.246])

# No Space Between -r and Version Number

Never put a space between the -r flag and the version number. Otherwise, RCS will try to check out a file by the name of your version.

# Breaking Locks

Occasionally a user might forget to check in a file—or might go on vacation in the middle of editing a checked-out file! When a file remains checked out, the file is locked and other users are prevented from editing the file. Fortunately, RCS provides a mechanism for breaking the lock on a file; RCS -u breaks the lock on a file, but it asks you to supply a reason for the break; RCS -u then sends mail to the user holding the original lock, as shown:

```
$ bash -u httpd.conf
RCS file:httpd.conf,v
Revision 1.2 is already locked by jeff.
Do you want to break the lock? [ny](n): y
State the reason for breaking the lock:
(terminate with single './' or end of file)
>> need to add a virtual server for a client
>> .
1.2 unlocked
done
```

The message sent to the original user looks like this:

Date: Sat, 6 Apr 2002 12:56:00 -0500
From: mike
Subject: Broken lock on httpd.conf,v

Your lock on revision 1.2 of file /usr/local/apache/conf/RCS/httpd.conf,v
has been broken by mike for the following reason:

need to add a virtual server for a client

![](bbox=[0.093, 0.803, 0.153, 0.843])

# Check with the Lock Owner Before Breaking Locks

Always check with the owner of an RCS lock before breaking it. Someone could have made significant changes to a file and simply stepped out for a bite to eat. By breaking the lock and making your changes to that file, you could effectively erase or obsolete the other person's changes.