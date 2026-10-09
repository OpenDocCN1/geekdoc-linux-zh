# # CHAPTER 6
# Administrative Tasks

# ## CHAPTER OBJECTIVES

+   - Install and uninstall applications after installing the operating system
- Validate newly installed applications
- Reconfigure the boot loader
- Work with the tar program
- Perform and verify a backup and restore
- Program basic shell scripts

# ### PACKAGES

The Linux operating system gets its name from the Linux kernel. The total operating system is made up of many other programs that do everything from providing the user interface to retrieving the time from remote time servers. These programs are presented in the form of packages to install on the specific Linux distribution you are using.

The term *packages* in Linux operating systems refers to applications bundled into an archive and ready to install. This section discusses packages in general terms, but covers Red Hat Package Manager (RPM) in detail. RPM is used by many Linux installations, including Red Hat, SuSE, Mandrake, and others.

# #### Package Concepts

A package is an archive of files. Archived files in Windows typically use the *zip* format. Linux packages are similar in functionality, but a little different in implementation. An RPM file, for example, when installed will first check to make sure dependencies are in place. In other words, the RPM package will check that any files it depends on are installed first.

Packages contain precompiled software that is ready to install on a Linux operating system; however, some applications for Linux are distributed as source code. Source code must be compiled into binary code before it can be run on a Linux system. Packages are compiled for different Linux distribution versions and are ready to install. Precompiled programs are generally smaller than the source code, making them easier to transfer over a network.

Without packages that are configured for your specific computer and operating system, you would have to compile the programs and then install them into the correct locations. If you later decide to update the programs, it is up to you to make sure all files are updated, in the correct location, and not duplicated.

Binary files are compiled to work with specific computer resources. Resources include the processor and system libraries. Processors are designed with a unique micro-code that controls all the functions of the computer system. Each processor type must have source code compiled with the system libraries designed specifically for that processor.

One of the most important day-to-day jobs of an administrator is managing packages. When a new program update is released the administrator must find the program, determine the version, and install the update if needed. Packages and package management programs make the job of managing the software much easier.