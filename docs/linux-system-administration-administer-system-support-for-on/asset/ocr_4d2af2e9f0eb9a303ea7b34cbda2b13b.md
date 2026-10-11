![](bbox=[0.1, 0.1, 0.19, 0.16])

> Be careful which hosts you define. You could be trusting an unknown user with root access—which could easily invite exploitation.

Say you've got three hosts: a Web host, a main host, and a development host. If you want to enable user *bob* to use your dialup on the Web host, but you want to allow only user *judy* to shut down your main host locally, your *`/etc/sudoers`* file would look something like this:

```
# This file MUST be edited with the 'visudo' command as root.
#
# See the man page for the details on how to write a sudoers file.
#
# Host alias specification
Host_Alias    MAIN=hub:\
                REMOTE=web,devel
# Cmnd alias specification
Cmnd_Alias    PPP=/usr/sbin/ppp-go,/usr/sbin/ppp-off:\
                SHUTDOWN=/etc/halt,/etc/shutdown,/etc/reboot

# User specification
root    ALL=ALL
bob     REMOTE=PPP
judy    MAIN=SHUTDOWN
```

In the *`/etc/sudoers`* file, there is a certain syntax that this file uses. If you are going to be using an alias for either hosts, commands, or users, it must be in all capital letters. The aliases *ALL* and *NONE* are already defined. As in the example just given, *root* is defined for all commands on all hosts. However, *bob* can only run *PPP* commands on *REMOTE* hosts, and *judy* can only run *SHUTDOWN* commands on the *MAIN* host. You can also disable users from having any type of *su* access by denying them with *NONE*.

![](bbox=[0.1, 0.77, 0.19, 0.84])

> Remember that allowing any type of root access to any user other than the administrator can be a possible security problem. If you do so, you are trusting your users with the power to run commands as root, and this power can be exploited by anyone who wants complete root access badly enough. On the upside, the trusting work environment you create by such sharing of responsibility may deter users from trying to get root access. Use your best judgment.