# 1032  **Appendix C: RHEL 5 Features**

+   - **Virtualization** — In RHEL 5, virtualization features are based on XenSource technology (www.xensource.com). The concept of virtualization is to allow multiple operating systems to run on a single computer. For RHEL 5, this includes the ability to run multiple instances of *RHEL 5* on one machine (in what is called *para-virtualization*) or to run guest operating systems, such as Microsoft Windows. In most cases, special virtualized hardware is needed, such as Intel Virtualization Technology or AMD Virtualization processors.
+   
+   Virtualization is seen as an important feature for enterprise computing, where often a single machine is configured to run only a single application. With virtualization, a large enterprise can have multiple virtualized operating systems each running a single application and sharing the same computer hardware. As demand increases or decreases for a particular service, the entire virtualized OS can be moved to a different computer or duplicated to handle more load.

+   - **Security** — Security Enhanced Linux (SELinux) continues to be one of the main features that Red Hat offers to distinguish itself from other Enterprise players. With tools such as the SELinux Troubleshooter and SELinux Management Tool, it has become easier for systems administrators to lock down security on many of the most important services. These include Web service (httpd), name service (bind), network information service (ypbind), and DHCP (dhcpd).

+   - **Software Package Management** — With RHEL 5, the yum facilities have become the backbone of the software installation and maintenance features. Improvements to anaconda allow RHEL 5 servers to install from multiple yum-enabled software repositories. Graphical tools such as Package Updater (pup) and Package Manager (pirtu) make it easy to get updates, search for packages, and add and remove software.

Other features of RHEL 5 desktop and server systems include (but aren’t limited to):

+   - **Linux 2.6 Kernel** — The 2.6 kernel is part of both the latest Fedora and RHEL distributions. Features in the 2.6 kernel that make it particularly valuable in RHEL are its ability to handle more processors, larger memory pools, more devices, larger file systems, and higher-bandwidth networks, now could the previous major kernel release (2.4).

+   - **GNOME and KDE desktops** — Like Fedora, RHEL 5 offers both GNOME and KDE desktop software, with GNOME installed by default. Aside from logos and backgrounds being different, you can follow most of the descriptions of Fedora desktop features in Chapter 3 to learn about how the RHEL 5 desktops work.

+   - **Applications** — Hundreds of desktop applications for creating documents, using the Internet, working with graphics, and playing with sound and video are included with RHEL 5.

+   - **Extras** — To offer RHEL customers the same range of software available to Fedora users, Red Hat created the Extra Packages for Enterprise Linux (EPEL) software repository. This project has been spearheaded by the Fedora project, providing ports of