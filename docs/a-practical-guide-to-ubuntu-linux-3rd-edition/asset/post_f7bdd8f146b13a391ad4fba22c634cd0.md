
![](img/2344fc4a798f29dca9e8b5ed7288171a_628_0.png)

# **Figure 15-1** The Linux Kernel Configuration window, split view

The **make config** command displays the Linux Kernel Configuration window, which you can view in three configurations: single, split, or full view. Choose a view by clicking one of the three icons to the right of the floppy diskette on the toolbar. Figure 15-1 shows the split view. In this view, the left frame shows the options and the top-right view lists the features for each option. The bottom-right view describes the highlighted option or feature. Figure 15-2 shows the full view.

In any view, you can click the boxes and circles next to the choices and subchoices. An empty box/circle indicates the feature is disabled, a tick indicates it is to be included in the kernel, and a dot means it is to be compiled as a module. With a choice or subchoice highlighted, you can also press **M** for module, **N** for Not included, and **Y** for compiled into the kernel. Select *Menubar: Options->Show All Options* to display all options and features.

![](img/2344fc4a798f29dca9e8b5ed7288171a_628_1.png)

# **Figure 15-2** The Linux Kernel Configuration window, full view

Go through the options and mark the features as you would like them to be configured in the new kernel. At any time during the configuration process, you can store the currently defined configuration to a file, load a configuration from a file, or exit with or without saving your changes. The selections to do so are available in Menu bar: File. When you are done, select Menu bar: File=Save and close the window.

## CLEAnIng THE SOURCE TREE

After generating a .config file, but before compiling or recompiling the kernel, purge the source tree of all potentially stale *.o files using the following command:

```
$ make-kpkg clean
exec make kpkg_version=12.032 -f /usr/share/kernel-package/ruleset/minimal.mk clean
======= Making target minimal_clean [new prereqs: ] ======
This is kernel package version 12.032.
test ! -f .config || cp -pf .config config.precious
test ! -e stamp-building || rm -f stamp-building
test ! -f Makefile || \ \
make ARCH=i386 distclean
make[1]: Entering directory '/usr/src/linux-source-2.6.32'
CLEAN  scripts/basic
CLEAN  scripts/kconfig
CLEAN  include/config
CLEAN  .config include/linux/autoconf.h
make[1]: Leaving directory '/usr/src/linux-source-2.6.32'
test ! -f config.precious || mv -f config.precious .config
rm -f modules/modversions.h modules/kSyms.var scripts/cramfs/cramfsscripts/cramfs/mkcramfs
```

This command ensures that make correctly applies any numbering scheme you use when you compile the kernel. Continue to work as a nonprivileged user.

## COMpIlInG A KERNEL InAGE FILE AnD LOADABLE MODuLES

See “Prerequisites” on page 572 for a list of packages that must be installed to compile the source code. Give the following command to compile the kernel and modules; it generates a .deb file in the parent of the working directory.

```
$ make-kpkg -initrd --rootcmd fakeroot --append-to-version \(date +%s) kernel_image
exec make kpkg_version=12.032 -f /usr/share/kernel-package/ruleset/minimal.mk debian APP ENDO_TO_VERSION=1271202298 INTRO_SYS ROOT_CMD=fakeroot
======= Making target debian/stamp/conf/minimal_debian [new prereqs: ] ======
This is kernel package version 12.032.
test -d debian && rm -rf mdkir debian
test ! -e stamp-building || rm -f stamp-building
... cmdopt -R or=gr
chown -R root:root /usr/src/linux/debian/linux-image-2.6.32.11l+drm33.21271202298
dpkg --build /usr/src/linux/debian/linux-image-2.6.32.11l+drm33.21271202298 ..
dpkg-deb: building package 'linux-image-2.6.32.11l+drm33.21271202298' in '../linux-image-2.6.32.11l+drm 33.21271202298'.
makel[2]: Leaving directory '/usr/src/linux-source-10.00_Custom_1386.deb'
makel[1]: Leaving directory '/usr/src/linux-source-2.6.32'
$ ls ../*.deb ../linux-image-2.6.32.11l+drm33.21271202298-10.00_Custom_1386.deb
```

The `--append-to-version` option allows you to specify a string that uniquely identifies the kernel you are building. This string also helps prevent overwriting existing kernels. You can specify any string you like following this option, using characters from the set of lowercase letters, numbers, , (minus), + (plus), and . (period). The value you specify is placed at the end of the kernel name and release number. You can make note of patches applied to the kernel in this string to help developers track bugs. The preceding example uses command substitution (page 362) to place the number of seconds since the UNIX epoch in the name of the kernel, making easy to tell which of several kernels is newest.

## USING LOADABLE KERNEL MODULES

A loadable kernel *module* (page 1157) (sometimes called a *module* or *loadable module*) is an object file—part of the kernel—that is linked into the kernel at runtime. Modules can be inserted into and removed from a running kernel at almost any time (except when a module is being used). This ability gives the kernel the flexibility to be as small as possible at any given time. Modules are a good way to code some kernel features, including drivers that are not used continually (such as a tape driver). Module filenames end in `.ko` and are stored in subdirectories in `/lib/modules`. Under Ubuntu, kernel modules are compiled along with the kernel as explained in the preceding section.

### FINDING NONSTANDARD MODULES

Many drivers that are not in the main source tree or not free are supplied as *-source* packages. You can use *aptitude* to display a list of available *-source* packages. The following example first updates APT’s cache, then displays a list of *-source* packages, and finally displays a list of packages that pertain to NVIDIA. The dollar sign at the end of the search string (*source$*) ensures that the string matches only the last part of a package name.

```
$ sudo aptitude update
$ aptitude search source$
p acerhkl-source - Source for the acerhkl driver
p acl2-books-source - A Computational Logic for Applicative Common Lisp: library sources
p acl2-infix-source - A Computational Logic for Applicative Common Lisp: infix source
p acl2-source - A Computational Logic for Applicative Common Lisp: source files
...
$ aptitude search source$ | grep -i nvidia
p nvidia-173-kernel-source - Transitional package for nvidia-glx-173-ke
p nvidia-180-kernel-source - Transitional package for nvidia-glx-185-ke
p nvidia-185-kernel-source - Transitional package for nvidia-glx-185-ke
p nvidia-96-kernel-source - Transitional package for nvidia-glx-96-ker
```

### MODULE-ASSISTANT: DOWNLOADING, COMPILING, AND INSTALLING NONSTANDARD MODULES

Once you determine its name, you need to download and install the module source package. You then need to compile, build, and install the Debian module package that corresponds to the source package. Check the prerequisites listed on page 572 before starting this process. The following command uses module-assistant to perform these steps with the nvidia-173-kernel-source package:

```
$ module-assistant --text-mode auto-install nvidia-173-kernel-source
```

The module-assistant utility calls sudo to run apt-get and dpkg. It will fail if you do not have write permission to /usr/src (i.e., if you are not in the src group); sudo may prompt you for your password. You must be a member of the admin group so module-assistant can call sudo successfully. Without the --text-mode option, module-assistant presents a pseudographical interface that requires input.

If you run into problems, you may want to call module-assistant to perform each of the steps in turn. You must run the module-assistant prepare command once before running other module-assistant commands (except auto-install). The following commands use m-a, a link to module-assistant, and -t in place of --text-mode:

```
$ m-a -t prepare
$ m-a -t get nvidia-kernel
$ m-a -t build nvidia-kernel
$ m-a -t install nvidia-kernel
```

The format of a module-assistant command is as follows:

```
module-assistant command [pkg-list]
```

where command is a command from the following list and pkg-list is a list of one or more SPACE-separated module source packages. You do not need to include the -source part of the package name when working with module-assistant. The prepare command does not accept a pkg-list; all other commands require it. See the module-assistant man page for a list of options, more commands, and more information.

- **auto-install pkg-list**
  - Combines the prepare, get, build, and install commands and processes pkg-list. Abbreviate this command as a-i.
- **build pkg-list**
  - Builds pkg-list. Error messages go to /var/cache/modass.
- **get pkg-list**
  - Downloads and installs the source code for pkg-list.
- **install pkg-list**
  - Installs pkg-list. Without pkg-list, installs the last package you built for the kernel running on the local system.
- **list pkg-list**
  - With arguments, lists details about pkg-list. Without arguments, lists all known packages. Abbreviate this command as la (list available).
- **list-installed**
  - Lists details about installed packages. Abbreviate this command as li.
- **prepare**
  - Determines the name of the kernel-header package, installs it and the build-essential package as needed, and creates the /usr/src/linux symbolic link. With the -I option, this command uses the kernel version you specify. Without this option, it uses the version of the kernel running on the local system. You must run this command before you run any other module-assistant commands.
