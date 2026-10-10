> NOTE: This chapter follows the install procedure for Fedora 8, which comes with this book. The procedure is very similar to the Red Hat Enterprise Linux installation process. For details on installing RHEL, refer to the Red Hat Enterprise Linux 5 Installation Guide: www.redhat.com/docs/manuals/enterprise/RHEL-5-manual/Installation_Guide-en-US

# Understanding Fedora Installation Media

In earlier releases, the Fedora Project packaged its Linux operating system as both 5-CD and 1-DVD installation media. Extra software packages could be downloaded from the Fedora Extras repository and installed from over the Internet. Recently, that arrangement has changed in several major ways:

+   - **Fedora Repository** — Instead of separate Fedora Core and Extras repositories, there is just a single Fedora repository that includes all software from those two repositories.
+   
+   - **New Installation Media** — The merged Fedora repository contains too much software to expect the average person to download. Therefore the Fedora Project offers more reasonable-sized installation media that include a single 2.9G installation DVD (Fedora Prime), a GNOME Desktop Live CD, and a KDE Desktop Live CD. Either of the live CDs can also be used to install the Fedora desktop system contained on that CD to hard drive. After the release, look for custom Fedora spins that might include full CD and DVD sets, as well as specialized live CDs for games, art, software development, and other special topics (`http://fedoraproject.org/wiki/CustomSpins`). A *spin* is just a selected grouping of Fedora software into a live or install CD or DVD image.
+   
+   - **New Build Tools** — To help people put together the mass of Fedora software into a form that is useful to them, the Fedora Project created several software tool projects. Using Fedora and optionally other software repositories, Pungi can be used to create a new set of installation media, while livecd-creator can build a live CD or live DVD. (See descriptions of these tools at the end of this chapter.)

With this book, we have included the Fedora GNOME Desktop Live CD and a "Combined" Fedora Installation DVD. The live CD is the exact GNOME Desktop Live CD produced by the Fedora project. The "Combined" DVD includes most of the contents of the Fedora repository, which we put together especially for this book using the Pungi tools just described. (See the "Choosing an Installation Method" section later in this chapter for details about those two media.)

# Using the Fedora 8 Live CD

The official Fedora 8 Desktop Live CD that comes with this book is a great way to try out Fedora before you commit to installing it. In addition to answering the obvious question of "does Fedora run on my PC at all?" the CD itself contains useful tools for examining your hardware and preparing your computer for installation.