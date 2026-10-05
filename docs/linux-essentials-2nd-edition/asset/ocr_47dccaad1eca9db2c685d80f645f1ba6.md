# Understanding Package Management

risky even when they use the same package type. This is because a non-native package age may have dependencies that conflict with the needs of native packages.

Originally, package systems worked locally. To install a package on your computer, you would have to first download a package file from the Internet or in some other way. Then you could use a local command to install the package. This approach, however, can be tedious when a package has many dependencies; you might attempt an installation, find unmet dependencies, download several more packages, find that one or more of them has unmet dependencies, and so. By the time you've rolled down all of these depended-upon packages, you might need to install a dozen or more.

Modern distributions provide network-enabled tools to help automate the process. These tools rely on software repositories, from which the tools can download packages automatically. The network-enabled tools vary from one to another, particularly among RPM-based distributions.

In practice, managing software in Linux using text-mode or GUI tools to interface with a software repository. A typical software installation works something like this:

+   1. You issue a command to install a program.
2. The software locates dependencies of the specified program and notifies you of any additional software that must be installed.
3. You issue a final approval for software installation (or decide against it, in which the case process stops).
4. The software downloads all of the necessary packages.
5. The software installs all the packages.

Upgrading software works in a similar way, although upgrades are less likely to require downloading depended-upon packages. Removing software can be done entirely locally, of course. Many distributions automatically check with their repositories from time to time and notify you when updates are available. Thus you can keep your system up-to-date by clicking a few buttons when you're prompted to do so. As an example, Figure 9.1 shows the Software Update utility in Fedora 21, which shows a list of available packages.

Package management necessarily involves root access, which is described in more detail in Chapter 13, “Creating Users and Groups.” If you follow the auto-matic prompts to update your software, you can keep the system up-to-date by entering the root password, or your regular password on some distributions, when the update software prompts for it.

Table 1.1 in Chapter 1, "Selecting an Operating System" summarizes features of several popular Linux distributions, including the package system each uses.

Certification Objective

> You can configure most distributions to use local media instead in addition to Internet repositories.

> Immediately after installing a distribution, you may find that many updates are available.