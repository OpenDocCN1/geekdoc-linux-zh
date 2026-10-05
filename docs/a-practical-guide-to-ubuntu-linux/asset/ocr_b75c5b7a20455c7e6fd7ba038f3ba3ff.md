# SETTING UP DNS SERVER 847

```
server 1.2.3.4 {
# 1.2.3.4 is the IP address of the other server using this key
keys {
  "keyname"
};
```

Each server must have a Server clause, each containing the IP address of the other server. The servers will now communicate with each other if they first authenticate each other using the secret key.

# RUNNING BIND IN a chroot JAIL

To increase security, you can run BIND in a chroot jail. See page 466 for information about the security advantages of, and how to set up, a chroot jail. The bind-chroot shell script (below), which sets up BIND to run in a chroot jail, creates a directory /var/lib/named that takes the place of the root directory (/) for ALL BIND files. The bind-chroot.sh installs the bind9 and resolveconf packages if they are not already installed and runs the bind9 and resolveconf scripts to start named. It adds the -t option to the options in /etc/default/bind9 so named chroots to the /var/lib/named directory before it reads its configuration files. The daemon is already set up to run as the user bind (-u bind).

After creating the necessary directories in /var/lib/named, the script moves the files from /etc/bind to /var/lib/named, creates a symbolic link from /var/lib/named back to /etc/bind, and creates and sets permissions on devices BIND may need. Next, bind-chroot.sh disables apparmor protection for named. Finally, the script starts named and resolveconf, and displays the end of the syslog file.

```
# cat bind-chroot.sh
!/bin/bash

# install -y stop bind
ptitude -y install bind9
service bind9 stop

# install and stop resolveconf
ptitude -y install resolveconf
service resolveconf stop

# add -t /var/lib/named to OPTIONS in /etc/default/bind9
sed -i 's:OPTIONS=(.*):OPTIONS=\1 -t /var/lib/named": /etc/default/bind9

# make the chroot directories
mkdir -p /var/lib/named/{etc,dev,var/cache/bind,var/run/bind,run}

# move the configuration to the chroot and link back to /etc
mv /etc/bind /var/lib/named/etc
ln -s /var/lib/named/etc/bind /etc/bind
```