```
# passwd
Changing local password for root
New Password:
Retype New Password:
#
```

> **NOTE**
> You'll notice that you weren't asked for the old root password. In single-user mode, you're automatically root, and passwd(8) doesn't ask root for any password.

Or, if you find that there’s a typo in /etc/fstab that confuses the system and makes it unbootable, you can mount the root partition with the device name and then edit /etc/fstab to resolve the issue.

If you have a program that panics the system on boot and you need to stop that program from starting again, you can either edit /etc/rc.conf to disable the program or set the permissions on the startup script so that it can’t execute.

```
# chmod a-x /usr/local/etc/rc.d/program.sh
```

We’ll discuss third-party programs (ports and packages) in Chapter 15.

You need to understand single-user mode to be a successful sysadmin, and we’ll refer to it throughout this book. For now, though, let’s look at the loader prompt.

# **SYSTEM FAILURES VERSUS HUMAN FAILINGS**

There’s a reason all of these examples involve recovering from human errors. Hardware failures aren’t common, and FreeBSD failures, even less so. If it weren’t for human error, our computers would almost never let us down. As