```
$post

# add comment to /etc/motd
echo "Kickstart-installed Red Hat Linux `date`" > /etc/motd

# add another nameserver
echo "nameserver 10.10.0.2" >> /etc/resolv.conf
```

This section creates a message-of-the-day file containing the date the kickstart installation took place, and gets around the network command's "one name server only" limitation by adding another name server to /etc/resolv.conf.

> **Please Note**
> Note that the post-install script is run in a chroot'ed environment; therefore performing tasks such as copying scripts or RPMs from the installation media will not work.

# --nochroot

Allows you to specify commands that you would like to run outside of the chroot'ed environment.