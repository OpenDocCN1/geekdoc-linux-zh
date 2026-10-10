+   • Managing system software. When the time comes to remove old software and install new packages, knowing what to do can save a lot of trouble. Adding a new device driver or upgrading the Linux kernel can make all the difference in the world.
+   • Managing users and passwords. How do you want to handle users on your system? Are there certain rules you want in place for guests? How can you limit access to system resources, such as RAM or hard drive space, or portions of your directory tree?

Fortunately, Linux includes the software tools you need to administer your system. Some distributions include specialized graphical tools that can make the job a lot easier. This chapter provides an introduction for the use of these tools (and command-line equivalent actions), but the rest will be up to you. Learning system administration can take some effort, but the time spent will be well rewarded.

# Graphical Administrative Tools

Every Linux distribution, especially those from commercial vendors, touts a toolbox of graphical software tools aimed at making Linux management easier. Early software tools were in the form of shell scripts, but as Linux has matured, commercial distributors such as Red Hat, Inc. wrapped various system administration tools in graphical interfaces. To Red Hat’s credit, many of these original tools survive today in the Yellow Dog Linux and LinuxPPC 2000 Q4 distributions.

SuSE, Inc. includes a text-based console administrative tool named YaST, and another setup tool named Yet, which has a legacy stemming back to 1995. More recently, SuSE has included a graphical, X-based version, the YaST2 client. These tools can be used by SuSE PPC Linux users, in the same way the Yellow Dog Linux and LinuxPPC 2000 linuxconf clients are—to control nearly every aspect of a Linux system.

Keep in mind however, that you will still benefit from learning how to manually configure your system. Relying on X-based administrative tools can lead to an inconvenient situation, especially if you are suddenly dropped into single-user mode, or have to reboot your system to a runlevel that does not support X and networking.

# Using Legacy Red Hat Tools

Red Hat, Inc.’s version of Linux has had a profound impact on nearly all Linux distributions for Intel-based PCs, Sun SPARC workstations, and Alpha-based