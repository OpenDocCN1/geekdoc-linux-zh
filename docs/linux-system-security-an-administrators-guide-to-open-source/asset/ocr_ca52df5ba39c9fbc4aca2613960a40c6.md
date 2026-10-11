# Example 9-8 Using sudo -l

```
```
[paul@foghorn]$ sudo -l
You may run the following commands on this host:
        (root, dbmgr) /usr/sbin/lpc; /usr/bin/lprm
        (root, dbmgr) /sbin/shutdown -r *
        (root, dbmgr) /usr/local/db/bin/
[paul@foghorn]$
```
```

execute /sbin/shutdown -r as dbmgr. This is simply due to the fact that running the shutdown command as a user other than root will always result in permission denied.

Now that he knows which command it is, he executes it successfully, as indicated, in Example 9-9. The moral of this story is that the command executed through sudo must match *exactly* that given in /etc/sudoers or as displayed by sudo -l.

# Example 9-9 Successful sudo /usr/sbin/shutdown -r Invocation

```
```
[paul@foghorn]$ sudo /sbin/shutdown -r now
Broadcast message from root (tty0) Wed Mar 10 06:55:39 1999...
        The system is going down for reboot NOW !!
```
```

# OH, BY THE WAY...

Since we compiled sudo with insults (see Example 9-1 on page 177), let's have a look at what that means. In Example 9-10, we show the user paul mistyping his password twice.

Without the --with-insults compile-time option, whenever you enter an incorrect password, you would simply see the message, Sorry, try again. The UNIX operating system used to be full of humorous, insulting, and sometimes offensive error messages. As it has become more commercialized, most of these messages have been sanitized. So, harken back to the days of yore, and compile with insults!

# Example 9-10 Insulting Error Messages

```
```
[paul@foghorn]$ sudo /sbin/shutdown
Password:
        Listen, burrito brains, I don't have time to listen to this trash.
Password:
        Your mind just hasn't been the same since the electro-shock, has it?
Password:
        Sorry, user paul is not allowed to execute "/sbin/shutdown" as root on foghorn.
[paul@foghorn]$
```
```

# General Syntax of /etc/sudoers

Now that we have explored some relatively simple examples associated with the /etc/sudoers file, let's take a look at the full suite of capabilities. The file is broken into two major sections, the alias section and the privilege section. The alias section in the file is largely for convenience. It is the privilege section