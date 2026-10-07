# 614 Chapter 18 Troubleshooting Your Linux System

Exiting will automatically reboot the system.

# exit

# The init Method

Another way to change root's password is to pass a different init parameter to LILO when the system boots. You want to tell the system to mount the root filesystem in read-write mode so that you can write your changes when you run the passwd command and also to prevent the initialization scripts from running. At the boot prompt, enter the following (again assuming that you want to boot a kernel with the label linux):

```
boot: linux init=/bin/sh rw
```

When the system finishes booting, use the passwd command and sync the disks just like before. Now instead of rebooting, use the init command to change run level 6, which is a reboot level:

```
# exec /sbin/init 6
```

# Login Incorrect after Entering Username

If you enter the username at the login prompt and are not prompted for a password but are given a “Login incorrect” error and returned to the login prompt, you have an error in the /etc/pam.d/login file, possibly in the auth line that calls /lib/security/pam_unix.so.

# System Flashes Quick Message and Drops Back to login Prompt

If you try to log in to your system and see a message quickly before you are returned to the login prompt, you probably have an error in /etc/pam.d/system-auth or one of the required session lines. The message that is flashing is “Module is unknown”; it means there is a typing error in the path or name of the PAM library to be accessed, so that the library cannot be found. If the message looks like “Login incorrect”, the error is probably in the pam_unix line of the auth section of /etc/pam.d/system-auth. If you see no message at all, look to the second line of the auth section. We recommend logging in and making changes to /etc/pam.d/login to determine what changes result. Remember to leave one virtual terminal logged in so you don't have to go into rescue mode to fix the file you tampered with.

# Login incorrect Message

If you get this message when attempting to log in remotely as root to a Linux machine, the system is functioning normally; the problem is what you're trying to do. You really