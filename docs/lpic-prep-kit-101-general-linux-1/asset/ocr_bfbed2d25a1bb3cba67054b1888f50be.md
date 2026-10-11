Each distribution has some differences in where files are stored and how the directory structure should be organized. Over time, these differences have resulted in problems with software installation or going from one distribution to another, especially regarding where configuration files are stored.

As a result, an effort toward standardization has been undertaken. It is defined by the Filesystem Hierarchy Standard, which can be viewed at http://linuxpowerred.com/html/tutorials/fhs/fhs-toc.html. Although this standard was first defined to cover the Linux filesystem, it has been expanded to apply to other UNIX systems.

For the exam, you will need to know the standard locations for files. On the distribution-specific exam, you will need to know the locations specific to that distribution.

# Hierarchy

There are some directories that always should be present and that contain specific types of files. A good place to start is root, which is represented by * / . This is the top or beginning of your directory structure.

The / is the container for various other directories. Think of it as the glue that holds your system together. As a rule, this directory should not contain other files. Table 6.9 shows the major directories, what they contain, and their purposes. These are the directories that you should be familiar with for the exam.

**Table 6.9 The Contents of the Root Directory and the Purpose of Each**

| Directory | Contents and Use |
| :--- | :--- |
| bin | Contains binaries that are required for system startup. |
| boot | Contains the kernel and any configuration files necessary for the boot loader. |
| dev | Contains files necessary for accessing all types of peripheral devices, not just those present on your system. |
| etc | Contains the system configuration files and scripts such as shell startup scripts. |
| etc/skel | Contains skeleton user files to be placed in user's home directory when his account is created. See Chapter 7 for more information on this directory. |
| etc/X11 | Contains X Window configuration files. |
| etc/rc.d | Contains startup scripts and the rc directories. See Chapter 2, "Booting Linux," for more information on the use and structure of this directory. |
| home | Contains subdirectories for each user except root to be used as home directories; every regular user needs a home directory to be able to log in. Additional subdirectories can be used to further classify users. |...continues