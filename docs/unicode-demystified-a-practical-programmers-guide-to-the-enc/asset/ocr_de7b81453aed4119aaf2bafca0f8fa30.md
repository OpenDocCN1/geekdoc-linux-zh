# rpm: Red Hat Package Manager

The rpm (Red Hat Package Manager) utility works only with software packages that have been built for processing by rpm; it installs, uninstalls, upgrades, queries, and verifies rpm packages. Because Red Hat released rpm under the GPL (page 7), rpm is used by several distributions. Together with information contained within software packages assembled for use with rpm (named *.rpm), the rpm utility keeps track of where software packages should be installed, the versions of packages that you have installed, and the dependencies between the packages.

Source rpm packages are frequently in a directory SRPMS (source rpms), whereas object rpm packages are in RPMS. When you download object packages, make sure that they are relevant to your operating system (both distribution and release—for example, redhat 7.2) and were compiled on the appropriate architecture (i386 for all Intel and most AMD-based systems, i586 class processors and above, $390 is for IBM System/390, ia64 for the 64-bit Intel processor, alpha is for the DEC/Compa Alpha chip, athlon denotes the AMD Athlon family, pcs is for the Power PC chip, and spares covers the Sun Spar processor).\¹⁵ The name of the rpm file contains almost all the necessary information. Each of the following lines from a search for sendmail on www.rpmfind.get you the information you need:

![](bbox=[0.285, 0.398, 0.858, 0.418])

+   15. Many rpm packages run on releases and even distributions other than the ones they were compiled on.