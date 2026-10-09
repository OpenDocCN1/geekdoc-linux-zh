# LAB 37

# Use RPM and YUM Package Management: YUM

**Lab Objective:**
Learn how to use the YUM package manager to install, upgrade, search for, and uninstall packages.

**Lab Purpose:**
The YUM package manager is a collection of tools meant for RedHat-based distros to install and manage RPM-based packages.

> **IMPORTANT:** YUM is not pre-installed with Ubuntu and it may not install correctly. In that case, we recommend setting up another VM with a RedHat-based distro, such as CentOS.

**Lab Tool:**
A RedHat-based distro such as CentOS. Ubuntu is not recommended for this lab.

**Lab Topology:**
A single Linux machine, or virtual machine

# Lab Walkthrough:

*Task 1:*
Open the Terminal and run:

```
• grep -r -v -e ^# -e $ /etc/yum.conf{,.d/*}
• cat /etc/yum.repos.d/*
```

These files determine which repos will be used by YUM. There are many reputable third-party repos (and many unreputable ones), which you can enable by adding to one of these files, but we'll stick with the defaults for now.

Let's start by running all system updates: `sudo yum -y update`

If you chose Fedora, you will be using a newer tool: `sudo dnf -y update`