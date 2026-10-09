
## DOWNLOADING THE SOURCE CODE

**rpmddev-setuptree** After you download the required packages (previous section), run **rpmddev-setuptree**. This utility sets up an SRPM build environment comprising an **rpmbuild** directory hierarchy in your home directory:

```
$ rpmddev-setuptree
$ ls rpmbuild
BUILD    RPMS    SOURCES    SPECS    SRPMS
```

After you compile the kernel, the five directories **rpmddev-setuptree** creates will hold files as follows: **BUILD** holds the results of compiling the kernel, **RPMS** holds compiled RPM files, **SOURCES** holds source and patch files, **SPECS** holds the kernel specification file, and **SRPMS** holds source RPM files, if any.

### Do not work with root privileges

> **caution** You do not need to—nor should you—work with **root** privileges for any portion of configuring or building the kernel except for installing software packages and installing the kernel (the last step). The kernel README file says, "Don't take the name of **root** in vain."

The sections on building, customizing, and installing the kernel use **su -c** when it is necessary to work with root privileges. This practice helps keep you from working with **root** privileges when you do not mean to. It also provides a better record for you to review in the shell history (page 376) should something go wrong. For more information on **su -c**, refer to "Executing a Single Command" on page 427.

**yumdownloader** The easiest way to download the updated kernel source code for the most recently released version of the kernel is to use **yumdownloader**. Work in and download the kernel source code RPM file to your home directory:

```
$ cd
$ yumdownloader --source kernel
Loaded plugins: langpacks, refresh-packagekit
Enabling updates-source repository
Enabling fedora-source repository
...
kernel-3.9.8-300.fc19.src.rpm | 69 MB 00:27
```

### About the examples in this section

> **tip** The examples in this section show Sam, whose home directory is /home/sam (~sam), working with the kernel named **kernel-3.9.8-300.fc19**. When you build a kernel, you will probably work in your home directory, and the name of the kernel you work with will differ from the name of Sam's kernel. Make the necessary substitutions as you follow the examples.

## INSTALLING THE SOURCE CODE

**yum-builddep** With the kernel source code RPM package file in your home directory, run **yum-builddep** to download and install the packages needed to build the source code package (dependencies). Because you are installing packages, you must work with **root** privileges. Replace **sam** and 3.9.8-300.fc19 in the following example with your username and the name of the kernel you are using to specify the location of the RPM file on the system.

```
$ su -c 'yum-builddep /home/sam/kernel-3.9.8-300.fc19.src.rpm'
Password:
Loaded plugins: langpacks, refresh-packagekit
Getting requirements for kernel-3.9.8-300.fc19.src
...
Install  15 Packages (+37 Dependent packages)

Total download size: 36 M
Installed size: 108 M
Is this ok [y/d/N]: y
...
Complete!
```

Finally, working from your home directory as a nonprivileged user, use `rpm` to install the kernel source code in the `rpmbuild` directory hierarchy in your home directory:

```
$ rpm -Uvh kernel-3.9.8-300.fc19.src.rpm
  1:kernel    warning: user mockbuild does not exist -- using root
warning: group mockbuild does not exist -- using root
warning: user mockbuild does not exist -- using root
...
  1:kernel-3.9.8-300.fc19   ##################################################  [100%]
```

You can ignore errors, such as those shown above, about groups and users that do not exist.

### Preparing the Source Code

The final step before you can work with the source code is to prep it. Prepping unpacks compressed files and applies patches. The following `rpmbuild` command uses the `-bp` option to prep the source code:

```
$ cd /home/sam/rpmbuild/SPECS
$ rpmbuild -bp --target {arch} kernel.spec
Building target platforms: x86_64
Building for target x86_64
Executing(%prep): /bin/sh -e /var/tmp/rpm-tmp.qGVQ0c
+ umask 022
+ cd /home/sam/rpmbuild/BUILD
...
```

If `rpmbuild` cannot find a package it needs to prep the code, it displays a message such as the following:

```
error: Failed build dependencies:
  elfutils-libelf-devel is needed by kernel-3.9.8-300.fc19.x86_64
  zlib-devel is needed by kernel-3.9.8-300.fc19.x86_64
  binutils-devel is needed by kernel-3.9.8-300.fc19.x86_64
```

In this case, install the needed packages (you might have to install different packages than those in the example):

```
$ su -c 'yum install elfutils-libelf-devel zlib-devel binutils-devel'
```

After you install the packages, give the preceding `rpmbuild` command again. With the kernel source code installed and prepped on the local system, you can configure, compile, and install it.

## CONFIGURING AND COMPILING THE LINUX KERNEL

This section describes how to configure and compile the kernel.

> **tip** **Where are the kernel source code and the kernel specification file?** After installing and prepping the source code as described in the previous section, Sam’s source code is in /home/sam/rpmbuild/BUILD/kernel-3.9.fc19/linux-3.9-300.fc19.x86_64/, and his kernel specification file is in /home/sam/rpmbuild/SPECS. Your source code will be in a similarly named directory (~rpmbuild/BUILD/kernel-*linux*) and your kernel specification file will be in the directory named ~rpmbuild/SPECS. 

Most of the work in this section is done in the directory in which the source code is located (Linux*). Labelling and installing the kernel is done in the SPECS directory.

### LABELING THE KERNEL

To prevent overwriting existing kernel files and to identify various compilations of the kernel, you can change the **buildid** variable in the *kernel.spec* file. This variable is initially set to .local. Whatever value you assign to this variable is placed at the end of the kernel name and release number to identify the kernel. You can make note of patches applied to the kernel in this string to help people track down problems later. Use **cd** to change directories to ~rpmbuild/SPECS, edit kernel.spec, and change local in the line

```
# %define buildid .local
```

to a value that identifies the kernel you are building. You must also remove the leading hash mark (#), the space following the hash mark, and the space between % and define:

```
%define buildid .sam1307021000
```

### .config: Configures the Kernel

Before you can compile the code and create a Linux kernel, you must decide on and specify which features you want the kernel to support. You can configure the kernel to support most features in one of two ways: by building the feature into the kernel or by specifying the feature as a loadable kernel module (page 589), which is loaded into the kernel only as needed. In deciding which method to use, you must weigh the size of the kernel against the time it takes to load a module. Make the kernel as small as possible while minimizing how often modules have to be loaded.

The .config file in the ~rpmbuild/BUILD/kernel-*linux* directory controls which features the new kernel will support and how it will support them. The next section provides instructions for replacing an existing custom kernel. “Customizing a Kernel” on page 586 explains how to create a default version of the .config file if it does not exist and how to edit the file if it does exist.

### REPLACING A CUSTOM KERNEL

If you have already configured a custom kernel, you might want to replace it with a similarly configured, newer kernel. Each kernel potentially has new configuration options, however—which explains why it is poor practice to use an old **.config** file for compiling a new kernel. This section explains how to upgrade an existing **.config** file so it includes options that are new to the new kernel and maintains the existing configuration for the old options.

Work in the `~/rpmbuild/BUILD/kernel*/linux*` directory. The system keeps a copy of the configuration file for the kernel the local system is running in `/boot`. The following command copies this file to **.config** in the working directory:

```
$ pwd
/home/sam/rpmbuild/BUILD/kernel-3.9._fc19/linux-3.9._8-300._fc19.x86_64
$ cp /boot/config-$(uname -r) .config
```

In this command, the shell executes `uname -r` and uses command substitution (page 410) to replace `$(uname -r)` with the output of the command, which is the name of the release of the kernel running on the local system.

Next give the command `make oldconfig` to patch the **.config** file with options from the new kernel that are not present in the old kernel. This command displays each kernel option that is the same in the new and old kernels and automatically sets the state of the option in the new kernel the same way it was set in the old kernel. It stops when it finds an option that appears in the new kernel but not in the old kernel. It then displays a prompt, which is similar to [N/y/?] (NEW), showing possible responses and indicating that this option is new. The prompt shows the default response as an uppercase letter; you can type this letter (uppercase or lowercase) and press RETURN, or just press RETURN to select this response. In the example, the Tickless System option is new, and the default response is Y for yes, *include the option in the new kernel*. To select a nondefault response (**n** means *no, do not include the option*, and **m** means *include the option as a module*), you must type the letter and press RETURN. Enter ? followed by RETURN to display more information about the option.

```
$ make oldconfig
scripts/kconfig/conf --oldconfig Kconfig

* Linux Kernel Configuration
*
* Code maturity level options
*
* Prompt for development and/or incomplete code/drivers (EXPERIMENTAL) [Y/n/?] y
*
* General setup
*
* Local version - append to kernel release (LOCALVERSION) []
* Automatically append version information to version string (LOCALVERSION_AUTO) [N/y/?] n
...
```
