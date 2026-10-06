# 344 Part III ♦ Choosing and Installing a Linux Distribution

♦ Programming tools—A good set of tools for developing software across a variety of programming environments.

KNOPPIX is based on Debian, so a Debian user will be particularly comfortable with the selection and organization of features. KNOPPIX software packages are also in deb format, so you can use apt, dpkg, and related tools to list and manage the packages. A graphical tool for working with software packages that comes with KNOPPIX is KPackage.

> Note Refer to Chapter 9 for information on using apt and dpkg tools for managing software in Debian. Even if you don't install any new software, those tools provide an excellent way to search, list, or even upgrade software packages that are running in KNOPPIX.

# What’s Cool About KNOPPIX

The features just described are ones that come with many Linux distributions. What makes them special with KNOPPIX is that you can be up and using those features within a few minutes — without having to repartion your disk, install software, or do any configuration. For trying out Linux or using it for some special, task such as playing or displaying music, documents, or spreadsheets from a computer's hard disk, KNOPPIX is quite awesome.

Some features, however, are specific to KNOPPIX (as compared to a Linux system you would run from a hard disk). Many of those features are there to help you through issues that relate to the fact that you are not working in a permanent setup. In particular, KNOPPIX includes the following:

+   ♦ Extraordinary hardware detection —The capability to properly detect and configure hardware is one of the best features. During the boot-up procedure, KNOPPIX finds most common PC components and loads the proper modules so it can use them. Its chipset tool relies on the Red Hat libkduzu to identify hardware, load appropriate modules, and create device files.

For hardware that cannot be detected, there are many boot options you can add to properly identify (or skip) over hardware devices. Some of them deal with particularly sticky issues related to video cards and running on laptop computers. (See Tables 11-1 through 11-3).

+   ♦ Automatic desktop startup —Instead of dropping you to a command line, KNOPPIX does its best to start up a complete KDE desktop environment. Along the way, it adds some nice features, such as desktop icons giving you access to your computer’s hard disk partitions.