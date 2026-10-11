major file system hierarchy, containing many of the same subdirectories you find on the /root itself. Figure 5.7 shows the /usr directory.

# FIGURE 5.7
The /usr directory contains optional program installations and related files.

![](bbox=[0.31, 0.2, 0.8, 0.57])

The various /usr directories that start with the letter X refer to different settings and aspects of the X Window system. The X and the xpg4 directories are two examples. Inside the X directory, for example, are folders that store documents (//docs), programs (/bin), libraries (//lib), man pages (/man), and so forth. (Keep in mind that the X directory is a symbolic link to the openwin directory described later in this chapter.) One important directory is the /usr/local directory and its subdirectories. Any files specific to the type of workstation or server that is in use locally are stored in this directory tree.

Many people use the /usr/local directory to install applications that they have compiled for the system. It's taken from the BSD method of using / and /usr for system installed files and using /usr/local for software additions the user makes. Most software downloaded from SunSites (like sunsite.uns.edu) install to the /usr/local directory even though they are Solaris packages.