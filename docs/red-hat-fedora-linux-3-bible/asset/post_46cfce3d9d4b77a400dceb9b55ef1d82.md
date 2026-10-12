
# Connecting to NFS from the command line

You might very well not have any control over how the Linux NFS server is configured. So if the *insecure* option isn't set, you will fail to mount an NFS directory from the Mac's Connect to Server window. A possible workaround is to manually mount the NFS directory from Mac OS X and use a secure root. Here's how:

1. On the Mac OS X computer, gain access to the root user account as follows:
   a. With the Folder icon selected, click Go \rightarrow Applications. The Applications folder appears.
   b. Open the Utilities folder, then the NetInfo Manager utility.
   c. Click on the lock icon on the NetInfo Manager window so that it unlocks.
   d. Click Security \rightarrow Enable Root User. (If you see a NetInfo error, click OK.)
   e. Type in and verify the new root user password, then click Verify. (Remember that password!)
   f. Click the open lock icon to close it and prevent further changes.

2. On the Mac OS X computer, click the Terminal icon to open a shell and log in as root:
   ```shell
   $ su -
   Password: ******
   ```

3. Create a directory that is accessible to the user account of the person who wants to use the shared NFS directory on the Mac. For example, for the user *chris* you might type:
   ```shell
   # mkdir /Users/chris/music
   # chown chris /Users/chris/music
   ```

4. Mount the NFS shared directory on the directory you just created. For example:
   ```shell
   # mount -o "-P" jukelbox.linuxtoys.net:/var/music /Users/chris/music
   ```

   The `-P` says to use a privileged port. Replace `jukelbox.linuxtoys.net` and `/var/music` with the server's name and the shared directory, respectively. The user can now access `/var/music` from the `/Users/chris/music` directory on the Mac OS X client.

# Summary

Because Darwin, a UNIX-like operating system, lies at the heart of the Mac OS X operating system, native Linux and UNIX network servers can be easily connected to these new Macs in a variety of ways. Mac OS X can take advantage of files shared from a Linux server over Samba (Windows file/printer sharing) and NFS (UNIX file/printer sharing).

Instead of just using native Linux server features, you can also configure Linux to act like an AppleTalk file and printer server using the netatalk package. With netatalk, you can set up multiple file servers and protect the volumes (directories) they share with various password and permissions techniques.

# *Part V*

# New Technology

Chapter 27: Adopting the Linux 2.6 Kernel

Chapter 28: Implementing Security Enhanced Linux

# Chapter 27

# Adopting the Linux 2.6 Kernel

## In This Chapter

- Getting to know the 2.6 kernel
- Improvements to desktop performance
- Improvements in laptop support
- Improvements to server performance
- Improvements in hardware support
- Using the 2.6 kernel beyond Fedora Core 3

When the Linux kernel is working well, it should be almost invisible to the people using Linux. External devices should be detected and configured automatically. Applications should be able to read and write data from storage devices, communications cards or any other types of supported hardware. By most accounts, the new 2.6 kernel included with Fedora Core 3 does those jobs well and provides a solid foundation for continued growth of Linux.

The focus of this chapter is on improvements in the 2.6 kernel that relate to how you might use it in Fedora Core 3. For that reason, I’ve broken down descriptions of the 2.6 kernel in much the same way I divided up the book: desktop, server, and administrative features (in this case, represented by a section on supported hardware drivers). After that, I describe features in the 2.6 kernel that relate to how it can be used outside of Fedora Core 3.

## Familiarizing Yourself with the Kernel

The Linux kernel is the software that allows application programs to communicate with the computer hardware and coexist with other running applications on the same system. To do that, the kernel must:

- **Know about the hardware drivers on the computer** — In Linux, the code that lets applications communicate with each piece of computer hardware can either be built into the kernel as drivers or added to the kernel after it is running, using what are called loadable modules.
- **Be able to manage applications** — By performing scheduling functions, the kernel can decide which running processes have access to the computer’s processor and for what duration. Processes are assigned priorities that can slow or speed the completion of those processes' requests.
- **Understand file systems and permissions** — Because the kernel is responsible for letting processes read, write, and execute files that are stored in different types of file systems, the kernel must know about how those file systems are structured. It must also know the permissions each user has to access those files.

There are many other things that a kernel does. However, these three are some of the most obvious functions of the kernel to someone using a Linux system.

One of the best ways to learn about the kernel is to read files that are included with the kernel source code. The location of the kernel source code has changed between Fedora Core 2 and Fedora Core 3, and you have to unzip it and build it yourself. As root user from a terminal window, do the following:

1. Install the kernel source package from the DVD that comes with this book (its name should be something like kernel-2.6.8-1.541.src.rpm from the SRPMS directory).
   ```
   # rpm -Uhv kernel-2.6.8-1.541.src.rpm
   ```

2. Type the following:
   ```
   # rpmbuild -bp --target noarch /usr/src/redhat/SPECS/kernel-2.6.spec
   ```

Now, the kernel source code that you used to be able to find in `/usr/src/linux` is now available in the `/usr/src/redhat/BUILD/kernel-*` directory. Look in that directory for `Documentation` directory. It contains descriptions of many of the drivers and other components in the 2.6 kernel. You can use the code from this package to rebuild the Linux kernel as well.

## Checking your current kernel

If you want to know what kernel your Linux system is currently running, you can type the `uname -a` command as follows:

```
# uname -a
Linux jukedbox.linuxtoybox.net 2.6.8-1.541 #1 Thu Nov 25 12:32:44 EDT 2004
i686 i686 i386 GNU/Linux
```

This example shows the current kernel as 2.6.8-1.541. Because you can have multiple kernels available on your hard disk, each of which may require drivers and modules that are specific to that kernel, the kernel version number is used to store the compatible components. For example, you can look for directories named for your kernel version in:

- `/lib/modules` — Modules that can be loaded as needed to support hardware connected to your computer are stored under the `/lib/modules` directory. One way that modules for the 2.6 kernel are different from the 2.4 kernel counterparts is that they end with a `.ko` extension (as opposed to a `.o` for 2.4 kernel modules). You can use the basename of the modules you find in kernel and unsupported subdirectories with the `modinfo` command to display descriptions of what hardware each driver supports.
- `/usr/src` — If you install the kernel-source package (included on the DVD that comes with this book), a subdirectory of /usr/src is named `linux-2.6.*` (where the asterisk is replaced by the revision level of the kernel), contains source code and documentation for your kernel. The `Documentation` subdirectory of that directory contains a wealth of information about the drivers and components that make up your kernel.

When you get the kernel with Fedora Core 3, it has already been built for you and stored in the `/boot` directory under the name `vmlinuz-2.6.*` (again, replacing the asterisk with the kernel revision level). Red Hat had to make some decisions about what drivers to include in the bootable kernel itself. Drivers that are needed for your particular hardware configuration can be detected after you boot Linux and can be added in the form of loadable modules.

Because there are some inefficiencies from using a kernel that includes drivers you don’t need, and must load drivers you do need, some Linux experts prefer to build their own kernels. In most cases, however, the performance gains are negligible, so most people simply take the small performance hits to load the modules they need at boot time.

If you need to work with modules on your Linux system, you can use tools such as `insmod` (to install a module), `modprobe` (to install/remove a module along with any dependent modules), `lsmod` (to see what modules are installed), `rmmod` (to remove a module), or `modinfo` (to view information about a module). Those tools are described in Chapter 10.

Because, as I mentioned earlier, if the kernel is working well it should be nearly invisible to you, it helps to know what to look for to understand what you are gaining from the 2.6 kernel. The sections in this chapter break down Linux 2.6 kernel features by desktop, server, and other systems.

## Using the /sys directory

The 2.6 kernel includes a centralized approach to viewing the hardware connected to a Linux system. One way in which that centralized approach is reflected is in a new `sysfs` file system type that stores information about the hardware. In Fedora, and other Linux systems, that file system is accessible under the `/sys` directory.

From the /sys directory, application programs (and even humans) can get the same view of devices that the kernel sees. Modifying values in many of the files in the /sys directory can change the way your system performs. Although the kernel itself and some utilities do most of the access and manipulation of the contents of the /sys directory, you can change data in some of those files yourself.

The files in the /sys directory contain such information as IRQ number, block sizes, and power management information. You can list the contents of these files to see how they are set (as in
