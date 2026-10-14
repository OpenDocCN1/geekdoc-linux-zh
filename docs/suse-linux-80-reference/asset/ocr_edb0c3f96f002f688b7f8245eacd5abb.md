> > **Caution**
> >
> > Be careful if you try to make a logical Linux partition bootable by installing LILO onto it. Success is not guaranteed for version 8.0, even if your other boot manager is able to launch logical partitions.

Try it if you like. The safest way is to try it with a tiny Linux installation to see if it will work. Perhaps you will be lucky. The recommended way is still to create a primary and bootable Linux partition.

# ## Configuring LILO

LILO is a flexible boot manager that offers many ways of adapting a configuration to your needs. The most important options and meanings are described below. For more detail, look at [Alm94].

LILO is configured in `/etc/lilo.conf`. If you are installing LILO for the first time, use YaST to configure LILO. Fine-tune by editing `/etc/lilo.conf` later stage.

> > **Note**
> >
> > `/etc/lilo.conf` should only be readable for root, as it could contain passwords (see Section *Other LILO Configuration Options* on page 99). This is the default setting with SuSE Linux. If in doubt, check by running `chmod 0600 /etc/lilo.conf` as root.

It is recommended to keep any existing old and working `lilo.conf` files backed up in a safe place. Your settings only take effect when you reinstall LILO after changing `/etc/lilo.conf` (see Section *Installing and Uninstalling LILO* on page 103).

# ### Structure of lilo.conf

`/etc/lilo.conf` starts with a global section followed by one or more system sections for each operating system LILO should start. A new section is started by a line beginning with either `image` or `other`.

The order of entries in `/etc/lilo.conf` only matters in that the first one in the list is booted by default if no user interaction is taken — this can be set to delay and timeout.