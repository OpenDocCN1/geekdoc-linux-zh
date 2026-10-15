For example, to change kernel.msgmni to 1024, enter the following command:

```
sysctl -w kernel.msgmni=1024
```

However, these settings will not remain after the next reboot unless they are saved in the /etc/sysctl.conf file.

# Modifying 2.4.x series kernel parameters on SuSE

Modifying kernel parameters on SuSE is a little different than Red Hat. These instructions will explain how to update the kernel.shmmax, kernel.sem, and kernel.msgmni parameters and set them for reboot.

+   1. Log in as a user with root authority.
+   2. Some SuSE distributions do not have a /etc/sysctl.conf file. If that is the case, you need to create one manually using a text editor.
+   3. In the /etc/sysctl.conf file, add the following entries:
+      kernel.shmmax=268435456
+      kernel.msgmni=1024
+      fs.file-max=8129
+      kernel.sem="250 32000 32 1024"
+   4. Run sysctl -p to load in sysctl settings from the default file /etc/sysctl.conf.
+      sysctl -p
+   5. Next, you need to add sysctl -p to a system initialization file to set kernel parameters after each reboot. To do this, write a script and configure it to run automatically at runlevel 5. Specifically, you need to create an executable file in /etc/init.d, then add pointers to this script in /etc/init.d/rc5.d. Follow our example:

In /etc/init.d, we created an executable file named kerneld b2. This file contains the following script:

```
#!/bin/sh
#
# /etc/init.d/kerneld b2
#
### END INIT INFO
touch /var/lock/subsys/kerneld b2
/sbin/sysctl -p >> /var/lock/subsys/kerneld b2
```

Then in /etc/init.d/rc5.d, we added pointers to the kerneld b2 script by entering the following commands:

```
bash# cd /etc/init.d/rc5.d
bash# ln -s ../kerneld b2 S99kerneld b2
bash# ln -s ../kerneld b2 K99kerneld b2
```