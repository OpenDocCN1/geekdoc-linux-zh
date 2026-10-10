Next, as root, use the quotacheck command to initialize quota use on your system like this:

```
# quotacheck -avug
Scanning /dev/hda12 [/] done
Checked 6100 directories and 104649 files
Using quotafile /quota.user
```

To assign a quota for a particular user, implement the edquota command, along with its -u option, followed by a username (or -g, followed by a group's name), like this:

```
# edquota -u bbai
```

After you press Enter, you will be presented with a screen in which to enter quota settings. Following this, you should also use the edquota command with its -t option to set soft limits (limits that, when reached, issue a warning to the user).

> You must use a Linux kernel that has quota use enabled. According to SuSE, this is the default with its stock PowerPC Linux kernels. LinuxPPC 2000 Q4 does not ship with a kernel that enables use of quotas, so you will have to rebuild the default kernel in order to use quotas.

![](bbox=[0.83, 0.4, 0.96, 0.51])

# Resources

+   http://mm.ii.uni-miskolc.hu/Data/texts/Linux/SAG/node76.html.
+   A history of Linux filesystems.
+   
+   http://www.coda.cs.cmu.edu/. Home page for the CODA filesystem.
+   
+   http://linas.org/linux/raid.html. A Web site with information about using RAID and Linux.
+   
+   http://www-ccm.stanford.edu/Students/hargrove/HFS/index.html.
+   Home page for the Linux kernel HFS filesystem support, where you will find the latest kernel modules aimed at supported Mac OS HFS volumes.
+   
+   http://sourceforge.net/projects/linux-hfsplus/. The development page for support of HFS+ in Linux 2.4-series kernels.
+   
+   http://www.ca.us.vergenet.net/linux/redundant_content/related/linux-ha/High-Availability-HOWTO.html. One site providing the Linux High-Availability HOWTO, with essential information on providing great uptimes and service.