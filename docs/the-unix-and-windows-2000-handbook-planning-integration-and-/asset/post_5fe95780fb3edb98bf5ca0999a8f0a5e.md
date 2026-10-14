
Operating system upgrades need not invoke nightmares and late-night trips to the local copy center to update your resume. Upgrades are generally a useful and productive way to improve system performance. Operating system developers have designed upgrades to add functionality, eliminate bugs and quirks, and increase performance and reliability. While many of us may question the value of past upgrades, in general, operating system programmers don’t start out to be sadistic people who only want to make your life unbearable.

Upgrading in an integrated environment adds the complexity of cross-operating system dependency. Various integration tools, like SAMBA and LDAP, require the administrator to confirm compatibility after the upgrade. Something that works fine with Red Hat Linux 6.0 and NT 4.0 may not work with Linux 5.1 and Windows 2000, or vice versa.

An informed administrator will understand the key elements of an operating system upgrade, and will develop a plan for successful implementation. In the sections that follow, we will give the tips and tools necessary to evaluate, plan, and install your next operating system upgrade. With these tools, your chance of success should increase, while your stress and blood pressure levels should decrease.

## UPGRADING VS. RE-INSTALLING

If you are an experienced administrator, you are most likely the survivor of many system upgrades and re-installations. However, the terms “upgrade” and “re-installation” may not be the words you have used to describe your processes. It is important to understand the difference, as your strategies for maintaining your systems change based on which method you choose to use.

Upgrading an operating system is the act of adding and deleting elements from the existing system to create a new operating system. A good example of this is when you upgraded from Windows 95 to Windows 98. Once you finished, you had a new operating system (Windows 98), but many core elements from the previous operating system were still intact (from Windows 95). You also didn’t have to re-install any of your programs or hardware, and once you completed the upgrade, your task was finished.

Re-installation consists of taking the new version of the operating system and installing it as if the data on your hard drive didn’t exist. Basically, you are installing the operating system from scratch, with the outcome of a complete new and virgin operating system when you are finished. However, after the installation is complete, you still have a lot of work to do. Sometimes re-installing is the only way to get to the new operating system version (Windows 95 to Windows 2000, or SunOS to Solaris), so in some cases, you may not have a choice.

### Table 5.1 Pros of Upgrading and Re-installing

| Advantages of Upgrading | Advantages of Re-Installing |
|---|---|
| System files remain intact; little or no post-upgrade work is necessary. | New installation is much faster than upgrade process. |
| Upgrades provide finer granularity when modifying the operating system as less changes are required per upgrade compared to a complete re-installation. | Allows the administrator to reconfigure hardware without affecting the system configuration. |
| In many cases, it is possible to back out of an upgrade and revert to the old operating system. | Clean, virgin copy of new operating system. |

Cases can be made for both upgrading and re-installing, as seen in Table 5.1. By completing an upgrade, you have little post-upgrade work to do, as upgrading generally does not disturb application software or operating system modifications. Also, in many cases, you get the added peace of mind that you can back out, and uninstall the upgrade, and revert to your previous operating system level. With a new installation, you’ll find that the amount of time needed to install a new operating system is two to three times faster then attempting an upgrade. Also, you get a fresh, new copy of the operating system, so you are sure what you are working with.

While upgrading and re-installing each have positives, looking at the negatives of each choice is just as important. Table 5.2 shows some of the negatives for each procedure.

Re-installing a system has relatively few drawbacks. The most time-consuming task is that you need to spend time after the operating system has been transferred to disk. Basically, re-installing the OS is the same as installing the system from scratch—a new install. Given that you have a solid installation procedure, re-installation should be a piece of cake. The only other issue with a re-installation is that you don’t have an on-line backout path if the new operating system has problems. However, as long as you have good backups, you should be able to recover from any disaster.

When choosing an upgrade route, you must install each new version of the new operating system if you wish to progress to the future version. For operating systems that don’t change very often, this isn’t an issue, but if your operating system changes two or three times a year, do you really want the
