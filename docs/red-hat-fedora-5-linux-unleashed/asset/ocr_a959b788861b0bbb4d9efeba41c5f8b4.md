![](bbox=[0.23, 0.1, 0.7, 0.44])

FIGURE 7.4 yumex allows you to handle package installation, removal, and updating in one neat application. It can even edit your repo files!

The benefit to installing and using either of these two applications is that they allow you easy access to and installation of programs that neither Red Hat nor Fedora Core can or will provide (such as multimedia and non-GPL licensed applications). Because the yum mirrors for Fedora all have current Fedora updates, you can be assured of access to the latest versions and security updates. The following sections discuss the yum and pup applications in more detail.

# yum

Some developers believe that although apt is a good tool, using it for .rpm packages is a hack. apt also is believed to be bloated with unnecessary code used for the Debian .deb packages. A new tool, yum, was developed using the Python language because the Fedora installer, anaconda, was written in Python and much of the code could be shared. This decision is what has made yum the choice for integration into the Fedora distribution. It works much the same as apt, but lacks a GUI tool. The Fedora developers have integrated support for yum into the graphical Fedora package management tool, as well as anaconda. Yum is the default package management tool in Fedora, and underpins pirut, pup, and anaconda, making it one of the important technologies in Fedora. The home page of yum can be found at http://linux.duke.edu/projects/yum/.