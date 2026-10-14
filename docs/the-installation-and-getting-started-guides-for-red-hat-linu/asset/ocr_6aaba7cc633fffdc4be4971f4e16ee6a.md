Then when you log in at the console, you will be given ownership of the /dev/sga device and the permissions will be 0600 (readable and writable by you only). When you log out, the device will be owned by root and still have 0600 (now: readable and writable by root only) permissions.

# Enabling Console Access for Other Applications

If you wish to make other applications besides shutdown, reboot, and halt accessible to console users, you will have to do just a little bit more work. First of all, console access only works for applications which reside in /sbin or /usr/sbin, so the application that you wish to run must be there. Create a link from the name of your application to the /usr/bin/consolehelper application:

```
cd /usr/bin
ln -s consolehelper foo
```

Create the file /etc/security/console.apps/foo touch /etc/security/console.apps/foo Create a PAM configuration file for the foo service in etc/pam.d/. We suggest that you start with a copy of the shutdown service, then change it if you want to change the behavior:

```
cp /etc/pam.d/shutdown /etc/pam.d/foo
```

Now, when you run /usr/bin/foo, it will call consolehelper, which with the help of /usr/sbin/userhelper will authenticate the user (asking for the users password if /etc/pam.d/foo is a copy of /etc/pam.d/shutdown; otherwise, it will do precisely what is specified in /etc/pam.d/foo) and then run /usr/sbin/foo with root permissions.

# The floppy Group

If, for whatever reason, console access is not appropriate for you, and you need to give non-root users access to your system's diskette drive, this can be done using the floppy group. Simply add the user(s) to the floppy group using the tool of your choice. Here's an example showing how gpasswd can be used to add user fred to the floppy group:

```
[root@bigdog root]# gpasswd -a fred floppy
Adding user fred to group floppy
[root@bigdog root]#
```

User fred will now be able to access the system's diskette drive (using the mtools utility programs, for instance).