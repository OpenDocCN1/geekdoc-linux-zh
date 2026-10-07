change to the superuser is:

```
$ su
```

Using the su command without specifying a user name implies root. You will be prompted for the root password and must properly authenticate to be granted root access. Failure to do so will send a message to the root user about a failed su attempt.

If you successfully authenticate, you will retain the environment of your original user account but will be allowed to change into directories owned by the root user, execute binaries that would not be executable by your normal account, create files in directories that are restricted to root, and much more. Your PATH will remain as it was with your normal user, so many of the more dangerous commands will not be accessible unless you specify their full path.

# **su – [username]**

Adding the – parameter starts a root login shell wherein the environment of the root user is assumed as well. The command for this would be:

```
$ su –
```

You will be prompted for the root password, and failure to authenticate will leave you as your own user and send a message of the failed su to the root user. If you authenticate successfully, however, your working directory will be changed to root’s home directory. From this point on, you are effectively root, although your identity is still known.

# **Starting an X Session as Root**

If your network uses the X Window System GUI interface (discussed in Chapter 13, "The X Window System"), you can run an entire X session as root by changing to the root user and then starting X. Everything done in that session will be performed as if you had logged in as root from the original login prompt, although again your true identity will be recorded. It is easy to forget that you have assumed superuser privileges, so this session should be handled with special care. One method of ensuring that you don’t forget that you started an X session as root is to use a totally different X environment for the root user than for the other users. You might make the background of the root user’s X session red or yellow to flag the session as initiated by the superuser.

Because of the potential for disaster that is associated with doing general work as the superuser, it’s better to use your normal user account to log in and to initiate the X session. Once you have the X session up and running, you can then bring up a terminal and use the su command to "become" root within that terminal and perform the required tasks. As soon as you’ve finished, exit from the superuser identity and proceed as your normal user. This method is far less dangerous.

# **sudo**

sudo (which stands for "superuser do") is a Linux command that system administrators commonly use to grant "superuser" or root privileges to a user or group of users temporarily so that they can perform specific operations they would not otherwise be allowed to do.

sudo logs its use, keeping track of who used it and what was done. It also sends e-mail to the superuser if someone tries to invoke sudo who does not have the necessary access to do so. Once authenticated, sudo grants the requested privilege for five minutes at a time (this default is configurable), and each command issued gets its own five minutes. The command looks like this: