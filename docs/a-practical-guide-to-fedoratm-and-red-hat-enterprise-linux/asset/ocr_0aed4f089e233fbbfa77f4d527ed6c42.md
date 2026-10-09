582 CHAPTER 14 BUILDING A LINUX KERNEL

# DOWNLOADING THE SOURCE CODE

**rpmddev-setuptree** After you download the required packages (previous section), run **rpmddev-setuptree**. This utility sets up an SRPM build environment comprising an **rpmbuild** directory hierarchy in your home directory:

```
$ rpmddev-setuptree
$ ls rpmbuild
BUILD    RPMS    SOURCES    SPECS    SRPMS
```

After you compile the kernel, the five directories **rpmddev-setuptree** creates will hold files as follows: **BUILD** holds the results of compiling the kernel, **RPMS** holds compiled RPM files, **SOURCES** holds source and patch files, **SPECS** holds the kernel specification file, and **SRPMS** holds source RPM files, if any.

# Do not work with root privileges

caution
You do not need to\u2014nor should you\u2014work with **root** privileges for any portion of configuring or building the kernel except for installing software packages and installing the kernel (the last step). The kernel README file says, "Don't take the name of **root** in vain."

The sections on building, customizing, and installing the kernel use **su -c** when it is necessary to work with root privileges. This practice helps keep you from working with **root** privileges when you do not mean to. It also provides a better record for you to review in the shell history (page 376) should something go wrong. For more information on **su -c**, refer to "Executing a Single Command" on page 427.

yumdownloader
The easiest way to download the updated kernel source code for the most recently released version of the kernel is to use **yumdownloader**. Work in and download the kernel source code RPM file to your home directory:

```
$ cd
$ yumdownloader --source kernel
Loaded plugins: langpacks, refresh-packagekit
Enabling updates-source repository
Enabling fedora-source repository
...
kernel-3.9.8-300.fc19.src.rpm | 69 MB 00:27
```

# About the examples in this section

tip
The examples in this section show Sam, whose home directory is /home/sam (~sam), working with the kernel named **kernel-3.9.8-300.fc19**. When you build a kernel, you will probably work in your home directory, and the name of the kernel you work with will differ from the name of Sam's kernel. Make the necessary substitutions as you follow the examples.

# INSTALLING THE SOURCE CODE

**yum-builddep** With the kernel source code RPM package file in your home directory, run **yum-builddep** to download and install the packages needed to build the source code package (dependencies). Because you are installing packages, you must work with **root** privileges. Replace **sam** and 3.9.8-300.fc19 in the following example with your username and the name of the kernel you are using to specify the location of the RPM file on the system.