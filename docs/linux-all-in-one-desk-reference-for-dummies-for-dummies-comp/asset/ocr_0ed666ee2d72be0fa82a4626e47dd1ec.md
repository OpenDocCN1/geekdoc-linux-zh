# **Updating Linux Applications Online**

In a nutshell, assuming the APT sources were configured during Debian installation, you can keep the current collection of software updated with the following two commands, typed in this order:

```
apt-get update
apt-get upgrade
```

The `apt-get update` command checks the current list of packages against the ones available from the locations specified in `/etc/apt/sources.list` file and gathers information about new versions of installed packages.

The `apt-get upgrade` command actually installs any available new versions of the packages installed in your Debian system. You must perform `apt-get upgrade` to install any available upgrades.

![](bbox=[0.14, 0.4, 0.21, 0.48])

To install new packages in Debian, use `apt-cache search` to find the package name in APT’s package cache and then use `apt-get install` to install the package.

# ### Updating Fedora Core Applications

![](bbox=[0.14, 0.5, 0.21, 0.6])

Fedora Core comes with Up2date—a graphical Update Agent that can download any new RPM files your system requires and install those files for you. Up2date is also known as the Red Hat Update Agent because Red Hat developed it for its Red Hat Network, through which Red Hat provides services to its commercial customers.

To update Fedora Core software packages using Up2date, follow these steps:

+   1. **Log in as root, and choose Applications->System Tools->Red Hat Network.** You can also type `up2date` in a terminal window.
+   
+      (If you don’t see Red Hat Network in the menu or you get an error when you type `up2date`, log in as `root`, type `yum install up2*` in a terminal window and then look for it in the menu.) The Update Agent starts, and if you’re using Up2date for the first time, the Red Hat Network Configuration dialog box appears and guides you through the configuration steps. Typically, you can click **OK** to accept the default settings. Another dialog box then prompts you to install a public key in your GPG key ring. (GPG refers to GNU Privacy Guard or GnuPG, a program for encrypting, decrypting, and signing e-mail and other data using the OpenPGP Internet standard.) GnuPG verifies that the package developer has securely signed the package that Up2date has downloaded. If prompted to do so, click **Yes** to install the public key.

+   2. **Up2date displays a window with a welcome message. Click the Forward button to proceed.**