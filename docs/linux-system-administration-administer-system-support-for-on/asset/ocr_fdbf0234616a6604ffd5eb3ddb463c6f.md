**ATTRIBUTES** Attributes are added similarly to symbolic notation in `chmod`. A plus adds the attributes, a minus removes them, and an equals sign overrides any previous existing condition.

+   * A   Don’t update a time, decreases disk I/O
+   * S   Synchronous updates
+   * a   Can only append to file, not delete or change
+   * c   Compressed, file is stored as compressed; viewed or edited as uncompressed
+   * i   File cannot be modified—immutable
+   * d   Will not backup when dump is run
+   * s   Secure deletion. When deleted blocks are zeroed and written back to the disk
+   * u   Undeletable, if it is accidentally deleted, it can be recovered

So, securing the /etc, /bin, /dev, and /usr directories is always a good idea. You can do this as root by typing

```
# chattr -R su /etc /bin /dev /usr /home zImage
```

This way if anything accidentally happens to the files, you’ve protected yourself. You’ll also want to shield your binaries by making them non-writable. This can help protect you from Trojan horses.

```
# chattr -R +i /usr/bin /bin /usr/sbin
```

You may have additional directories you’ll want to protect. These files are a starting point.

# # Summary

It is very important to have good account maintenance. As a system administrator, make sure that you give accounts to only users who need it on the system. For example, you should have many accounts on a mail server since they are designed for users. Whereas a firewall is not designed to be a user host, you should have as few accounts on it as possible.

In addition to giving an account on your system, a user may need some additional super powers that root can give to ordinary users. This includes network connectivity through PPP, mounting disks, and even shutting down a host. If you feel someone needs that access but does not need entire root access, you can use the `sudo` command to divide up root accessibility. Or, if someone needs root access, they can use the `su` command. However, only one or two people at most should