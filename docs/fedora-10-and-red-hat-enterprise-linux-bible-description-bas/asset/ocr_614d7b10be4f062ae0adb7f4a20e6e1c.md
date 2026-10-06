# 24 Part I: Getting Started in Fedora and RHEL

NOTE: This chapter follows the install procedure for Fedora 10, which comes with this book. The procedure is very similar to the Red Hat Linux installation process. For details on installing RHEL, refer to the Red Hat Enterprise Linux 5 Installation Guide: http://www.redhat.com/docs/manuals/enterprise/RHEL-5-manual/Installation_Guide-en-US.

# Understanding Fedora Installation Media

In earlier releases, the Fedora Project packaged its operating system as both 5-CD and 1-DVD installation media. Extra software packages could be downloaded from the Fedora Extras repository and installed over the Internet. In the past few releases, that arrangement has changed in several major ways:

+   - Fedora Repository — Instead of separate Core and Extras repositories, there is just a single Fedora repository that includes all the software.

+   - New Installation Media — The merged Fedora repository contains too much software to expect the average user to download. The Fedora Project offers reasonable-sized installation media that include a 3.5G installation DVD , a Desktop Live CD, and a KDE Desktop Live CD. Either of the live CDs can be used to install the Fedora desktop system on CD hard drive. After the release, look for custom Fedora spins that might include CD and DVD sets, as well as specialized live CDs for games, software development, and other special topics (http://spins.fedaproject.org/). A spin is just a grouping of Fedora software into a live CD or DVD image.

+   - New Build Tools — To help put together the mass of Fedora software into a form that is useful to them, the Fedora Project created several software tool projects. Using Fedora and optionally other software repositories, Pungi can be used to create a new set of installation media, which-creator can build a live CD or live DVD. (See descriptions of these tools at the end of this chapter.)

With this book, we have included the official Fedora KDE Desktop Live CD and the official Fedora Installation DVD.

# Using the Fedora 10 Live CD

The official Fedora 10 KDE Live CD that comes with this book is a great way to try out Fedora before you commit to installing. In addition to answering the obvious question of "does Fedora run on your PC at all?" the CD itself contains useful tools for examining your hardware and preparing your computer for installation.

A live CD is a bootable media (usually a CD, but other removable media, such as DVDs or USB flash drives can be used the same way) that contains an entire operating system. In most cases, you can boot the live CD without touching the contents of your hard drive.