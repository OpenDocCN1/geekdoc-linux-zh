# VOCABULARY

Cache A temporary storage system used to speed up frequent data access when the usual access method is expensive (performance-wise). This concept can be applied in numerous situations and at different scales, from the core of microprocessors up to high-end storage systems.

In the case of APT, the reference Packages files are located on Debian mirrors. That said, it would be very ineffective to push every search through the online package databases. That is, if APT stores copies of all files (in /var/lib/apt/lists/) and searches are done within those files. Similarly, /var/cache/apt/archives/ contains a cached copy of already downloaded packages to avoid downloading them if you need to reinstall them.

To avoid excessive disk usage when you upgrade frequently, you should regularly sort through /var/cache/apt/archives/ directory. Two commands can be used for this: apt clean (or apt-get clean) entirely removes the directory; apt autoclean (apt-get autoclean) only removes packages that can no longer be downloaded because they have disappeared from the mirror and Note that the configuration parameter APT:Clean-Installed can be used to prevent the removal of .dev files that are currently installed. Also, note that apt drops downloaded files once they have been installed, so this matters when you use other tools.

The apt-cache command can do keyword-based package searches with apt-cache search word. It can also display the headers of the package's available versions with apt-cache search package. This command provides the package's description, its dependencies, and the name of its maintainer. This feature is particularly useful in determining the packages that are installed via meta-packages, such as kali-linux-wireless, kali-linux-web, and kali-linux-gpu. Note that apt search, apt soft, aptitude search, and aptitude search work in the same way.

# Alternative: axi-cache

apt-cache search is a very rudimentary tool, basically implementing grep on package descriptions. It often returns many too results or no at all, when many keywords are included.

axi-cache search term, on the other hand, provides better results, sorted by relevancy. It uses the Xapian search engine and is part of the apt-xapian package, which indexes all package information (and more, like the .desktop files from all Debian packages). It knows about that and results in matter of milliseconds.

# $ axi-cache search forensics graphical

5 results found:

+   100% autopsy - graphical interface to SleuthKit
82% forensics-colorize - show differences between files using color graphics
73% diff - Powerful, efficient and modular digital forensic framework

+   53% gpart - Guess PC disk partition table, find lost partitions