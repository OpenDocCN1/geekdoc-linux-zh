# CHAPTER 6 Booting and Shutt Down 171

4. Copy or move the script to a directory where your startup scripts will find it;
we'll use the /usr/local/sbin/ directory:
`[root@fedora-server ~]# mv carpald.sh /usr/local/sbin/`

5. Notice that the carpald.sh script references a mailx command (to the last
line). Therefore, you will have the mailx utility available or installed on the
system so it can be used within the script.
On our sample Fedora/CentOS/RHEL system, you can use dnf to install
mailx—if you do not already have it. Type the following:
`[root@fedora-server ~]# dnf -y install mailx`

If you don't have mailx on a Debian-based system like Ubuntu, you can use the\apt-get program to install it by running:
`master@ubuntu-server:~# sudo apt-get -y install mailutils`

![](bbox=[0.088, 0.398, 0.165, 0.443])

# Creating the Startup Script

Here you will create the actual script that will be executed during system
startup and shutdown. The file you create will be called carpald. The file will be
chkconfig-enabled. This means that if you want, you can use the chkconfig utility
to control the runs at which the program starts and stops. This is a useful and
time-saving functionality.

+   1. Launch any text editor of your choice, and type the following text:
```bash
#!/bin/sh
#Carpald
#
#chkconfig:    35 99 01
# description: Carpald is a program that wakes up every 1 hour and
# tells us that we need to take a break from the keyboard
# or we'll lose all functionality of our wrists and never
#
# be able to type again as long as we live.
# Source function library.
/etc/init.d/functions
```