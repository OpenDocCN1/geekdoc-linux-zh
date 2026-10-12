By default, the kernel-related packages are not automatically downloaded, so there should already be an entry in the skip list. You can add additional exceptions if you wish, but don’t do this unless you have a good reason. The whole point of this tool is to keep your system up to date.

> **NOTE**
> You can also initiate system upgrades via the RHNI web interface at http://rhni.redhat.com. The systems will need to be entitled and running the `rhnsd` daemon for this to work properly, but it can be more convenient than having to touch each of many systems to perform updates. Of course, running `rhnsd` itself may have security implications, but if you’ve got to choose, `rhnsd` is the lesser of two evils.

# ### Manually Performing Security Updates

You don’t have to be a Red Hat Network subscriber or use the **up2date** command to keep your system up to date. Instead, you can track Red Hat Linux 8.0 security updates from Red Hat’s web site at https://rhni.redhat.com/errata/rh8-errata.html. Follow these steps to update your system the manual way:

+   1.  Find the packages you need on the web site.
+   2.  Download them from the web site to your system.
+   3.  Verify their authenticity by checking their GNU Privacy Guard keys using the `rpm -K *.rpm` command in the download directory.
+   4.  Run the package upgrades as described in Module 4.

# **Project 9-1** ## Getting Your System up2date

You’ve seen the screens in this module; now see them on your very own Linux server’s screen. In the course of this project, you will create a Red Hat Network account, register your computer, and update its packages. Even if you have already burned your one demonstration run of `up2date`, you can make this project a reality by registering another account name.

# ### Step by Step

+   1.  Run the **up2date** program to set up your account and register your Red Hat Linux 8.0 system (if you haven’t already).
+   2.  Select at least one, but not all, of the available packages for download.
+   3.  Once the packages have been downloaded, install them.