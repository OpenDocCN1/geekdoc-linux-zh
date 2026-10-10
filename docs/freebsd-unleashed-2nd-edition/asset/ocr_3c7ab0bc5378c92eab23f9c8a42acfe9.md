compatibility allows you to do anything up to and including playing back audio/video using Linux software.

# ## Installing from sysinstall

If you have the ports collection installed, you can see a categorized view of all the available software by going to `/usr/ports` and just looking around at the filesystem. Your old friend `/stand/sysinstall`, however, offers an even more direct interface.

From the main menu of the `sysinstall` program, choose Configure and then select Packages. The Packages menu is shown in Figure 14.1. From there, choose CD/DVD as the installation media if you have your FreeBSD install disk handy; if not, and you're on the Net, choose FTP.

![](bbox=[0.26, 0.33, 0.71, 0.49])

**FIGURE 14.1** The Packages menu in the `sysinstall` program.

After you get the package list from whichever medium you choose, you are presented with a menu like the one shown in Figure 14.2. Scroll up and down to see the various categories, and press Enter to go into each one.

# **A Note on Version Branches**

We won't be covering FreeBSD's version-branching system until Chapter 17, "Keeping Up to Date with FreeBSD." For now, however, you should become familiar with at least a few important bits of terminology that are crucial to the proper operation of the packages and ports.

In the Options section of the `sysinstall` program is a field to set the release name you'll be working with. Chances are you will be running a "release" version of FreeBSD (these are the versions that come on CDs). If so, the Release Name field will be set correctly for the version you're running. However, if you've upgraded your system to an interim point on either the `-STABLE` or the `-CURRENT` branch, this field may set to `#.#-STABLE`, where the hash marks (#) stand for major and minor version numbers. That value won't work when you try to open the Packages menu because it's pulled in directly from the output of the `uname` command, which reports information on the kernel version. It doesn't work because the Release Name field specifies the directory on the FTP server where `sysinstall` will look for the packages, and the corresponding directory for the packages that match your system's version doesn't necessarily have the same name.