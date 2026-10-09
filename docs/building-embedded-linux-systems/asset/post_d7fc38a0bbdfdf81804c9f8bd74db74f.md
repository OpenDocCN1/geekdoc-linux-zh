
Since version 1.3, the choice of a compiler or a cross-compiler is no longer made in the configuration file, but instead in the same way as in the Linux kernel, with the same `ARCH` and `CROSS_COMPILE` settings. This was explained in detail in Chapter 5.

Once BusyBox is configured, you can compile and install it. When linking with glibc, use the following command:

```bash
$ make ARCH=mips CROSS_COMPILE=mipsel-linux- \
> CONFIG_PREFIX=${PRJROOT}/rootfs install
```

`CONFIG_PREFIX` is set to the root filesystem base directory. The *Makefile* will install all BusyBox's components within this directory.

To build BusyBox with uClibc instead of the GNU C library, use the following command:

```bash
$ make ARCH=mips CROSS_COMPILE=mipsel-uclibc- \
> CONFIG_PREFIX=${PRJROOT}/rootfs install
```

BusyBox is now installed on your target's root filesystem and ready to be used.

### Usage

To understand how best to use BusyBox, let's first take a look at the components BusyBox's build process installs on the target's root filesystem. As expected, only one executable was installed, */bin/busybox*. This is the single binary with support for the configured commands. This binary is never called directly; however, instead, symbolic links bearing the original commands' names have been created to */bin/busybox*. Such symbolic links have been created in all the directories in which the original commands would be found, including */bin*, */sbin*, */usr/bin*, and */usr/sbin*.

When you type a command during the system's normal operation, the *busybox* command is invoked via the symbolic link. In turn, *busybox* determines the actual command you were invoking, using the name being used to run it. */bin/ls*, for instance, points to */bin/busybox*. When you type *ls*, the *busybox* command is called and it determines that you were trying to use the *ls* command, because *ls* is the first argument on the command line.¹

Although this scheme is simple and effective, it means you can't use arbitrary names for symbolic links. Creating a symbolic link called */bin/dir* to either */bin/ls* or */bin/busybox* will not work, because *busybox* does not recognize the dir command.

Note that, although symbolic links are the usual way of linking commands to */bin/busybox*, BusyBox can also be instructed to create hard links instead of symbolic ones during its installation. Its behavior at runtime is the same, regardless of the type of links used.

> ¹ Like many other application, *busybox*'s *main()* function is passed to the command line used to invoke it.

The documentation on the project’s website, which is also provided with the package, describes all the options available for each command supported. In most cases, the options supported by BusyBox have the same functions as the options provided by the original commands. For instance, using the -al options with BusyBox’s ls will have the same effect as using the same options with the original ls.

When using one of the shells provided in BusyBox, such as ash, hush, lash, or msh, you will find it convenient to use a `/etc/profile` file to define a few global variables for all shell users. Here is a sample `/etc/profile` file for a single-user target:

```bash
# Set path
PATH=/bin:/sbin:/usr/bin:/usr/sbin
export PATH
```

In addition to setting the path, you could set the LD_LIBRARY_PATH environment variable, which is used during the startup of each application to locate the libraries it depends on. Though the default location for libraries is /lib, your system may have libraries located in other directories. If that is the case, you can force the dynamic linker to look for the other libraries by adding the appropriate directory paths to LD_LIBRARY_PATH. As with the PATH environment variable, you can add more directories to the library path by placing colons between directory paths.

Note that on a workstation or a server, LD_LIBRARY_PATH would actually be used only as a temporary holding place for new library paths. To permanently add another library path, the administrator would edit `/etc/ld.so.conf` and run the `ldconfig` command to consult that file and generate `/etc/ld.so.cache`, which is itself read by the dynamic linker to find libraries for dynamically linked applications. Although `ldconfig` was generated when we compiled glibc in Chapter 4, it is a target binary and cannot be run on the host to generate a target `ld.so.cache`. So, you can expect many embedded systems to have no `/etc/ld.so.conf` and instead rely on the LD_LIBRARY_PATH technique.

## TinyLogin: BusyBox logging utilities

TinyLogin used to be another collection of utilities maintained by the developers of BusyBox. A single binary like BusyBox, it implemented the following commands: addgroup, adduser, delgroup, deluser, getty, login, passwd, su, sulogin, and vlock. There were several reasons to keep the TinyLogin functionality separate from BusyBox. The main one was that many of the commands implemented in TinyLogin had to run with root privileges, which in turn required that the TinyLogin binary file belong to the root user and have its “set user” permission bit enabled, a configuration commonly known as “setuid root.” Since TinyLogin used symbolic links in the same way BusyBox does, a single binary containing the functionality of both packages would also result in having commands such as ls and cat run as root, which increased the likelihood that a programming error in any one command could be exploited to gain root privileges.

However, as you can see from the original TinyLogin website, http://tinlogin.busybox.net, the project hasn't been updated since 2003. These logging utilities are now actively maintained in BusyBox.

To address the setuid security issues, BusyBox drops its root privileges for applets that don't require root access. It can also be configured to check the /etc/busybox.conf configuration file specifying those privileged applets. For the most paranoid users, the safest solution is still to build two separate BusyBox binaries, one for privileged applets and one for unprivileged applets.

Among the options you can configure, pay special attention to the CONFIG_FEATURE_SHADOWPASSWD, CONFIG_USE_BB_SHADOW, and CONFIG_USE_BB_PWD_GRP configuration options, which are documented in the configuration interface. The most important one is CONFIG_FEATURE_SHADOWPASSWD, which adds support for passwords encrypted in a separate etc/shadow file.

Traditionally, /etc/passwd could be read by anyone in the system, and this in turn became a security risk as more and more programs for cracking passwords were available. Hence, the use of so-called shadow passwords became the norm. When in use, the password fields in /etc/passwd contain only filler characters. The real encrypted passwords are stored in /etc/shadow, which can be read only by a process running with root privileges. Note that if you configure uClibc without shadow password support, enabling CONFIG_FEATURE_SHADOWPASSWD and linking with uClibc will result in a failed build.

You should enable CONFIG_USE_BB_SHADOW to let BusyBox use its own shadow functions for accessing shadow passwords, unless you plan to use glibc's NSS libraries with a properly configured /etc/nsswitch.conf file.

If you enable CONFIG_USE_BB_PWD_GRP, the logging utilities will directly use the /etc/passwd and /etc/group files instead of using the password and group functions provided by glibc. Otherwise, you will also need the C library NSS libraries and a /etc/nsswitch.conf file.

Note that you will not need to create and manage the /etc/group, /etc/passwd, and /etc/shadow files by hand, as the addgroup, adduser, delgroup, and deluser commands take care of creating or updating these files.

For more information on the creation and manipulation of group, password, or shadow password files, as well as system administration in general, see the Linux System Administrator's Guide (O'Reilly, also available from the Linux Documentation Project [LDP]), Running Linux, and the Linux From Scratch book (mentioned earlier in "Complete Standard Applications").

## embutits

embutits is another set of miniaturized and optimized replacements for mainstream Unix commands. Although embutits groups some of the commands in a single binary,
