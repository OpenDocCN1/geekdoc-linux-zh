```
[root@lucbn portsentry-1.1]# make linux
SSTYPE=linux
Making
cc -0 -Wall -DLINUX -DSPORFSTSTEALTH -0 ./portsentry ./portsentry.c \
./portsentry.lo.c ./portsentry_util.c
[root@lucbn portsentry-1.1]#
[root@lucbn portsentry-1.1]#
[root@lucbn portsentry-1.4]# make install
Creating psionic directory /usr/local/psionic
Setting directory permissions
Creating portsentry directory /usr/local/psionic/portsentry
Setting directory permissions
chmod 700 /usr/local/psionic/portsentry
Copying files
cp ./portsentry.conf /usr/local/psionic/portsentry
cp ./portsentry.ignore /usr/local/psionic/portsentry
cp ./portsentry /usr/local/psionic/portsentry/portsentry
Setting permissions
chmod 600 /usr/local/psionic/portsentry/portsentry.ignore
chmod 600 /usr/local/psionic/portsentry/portsentry.conf
chmod 700 /usr/local/psionic/portsentry/portsentry

Edit /usr/local/psionic/portsentry/portsentry.conf and change
your settings if you haven't already. (route, etc)

WARNING: This version and above now use a new
directory structure for storing the program
and config files (/usr/local/psionic/portsentry).
Please make sure you delete the old files when
the testing of this install is complete.

[root@lucbn portsentry-1.4]#
[root@lucbn portsentry-1.4]#
```

Figure 1-21 Abacus Port Sentry tries to defend the firewall against attack.

![](bbox=[0.25, 0.59, 0.83, 0.9])

Figure 1-22 Dsniff can be used to sniff for passwords on a system.