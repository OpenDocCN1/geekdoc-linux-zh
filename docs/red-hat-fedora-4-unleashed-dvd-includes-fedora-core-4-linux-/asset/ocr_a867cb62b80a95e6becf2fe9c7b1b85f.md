Fedora Core, as the next generation of Red Hat Linux, is slated for upgrades two or three times a year, according to the Fedora Project. In reality, however, work never ceases on the distribution because open-source developers, along with Red Hat engineers, cross-pollinate Red Hat’s Enterprise Linux and Fedora with software package upgrades, security updates, and bug fixes. Fedora’s free, online upgrade system will be available via the Internet.

Red Hat uses a 12- to 18-month release cycle for Enterprise Linux. This cycle is required to provide third-party application developers time to test, deploy, and market products. In the past, Red Hat has used a 6-month release schedule for the consumer version of Red Hat Linux, with a 3- to 4-month beta cycle for development and testing. Fedora Core will have a similar schedule; the Fedora Project has stated it intends to “produce time-based releases of Fedora Core about two to three times a year.”

As a Fedora user, you will be able to obtain the latest software for your system at any time using a variety of commands and software management tools:

+   yum—The Yellowdog Updater Modified, an automated software package manager based on RPM technology that resolves RPM dependencies.

+   apt-get—The APT command-line software package tool from The Debian Project, it’s used to upgrade, install, check, or remove software.

+   system-config-packages—Red Hat’s graphical package manager, it’s used to install or remove applications (refer to Table 1.1).

+   rpm—The Red Hat Package Manager, which uses a database of installed packages to manage software on your system.

+   up2date—Red Hat’s Red Hat Network update manager.

# Distribution Version and Kernel Numbering Schema

There is a specific numbering system for Linux kernels, kernel development, and Fedora’s kernel versions. Note that these numbers bear no relation to the version number of your Fedora Linux distribution. Fedora distribution version numbers are assigned by the Fedora Project, whereas most of the Linux kernel version numbers are assigned by Linus Torvalds and his legion of kernel developers.

To see the date your Linux kernel was compiled, use the uname command with its -v command-line option. To see the version of your Linux kernel, use the -r option. The numbers, such as 2.6.7-1, represent the major version (2), minor version (6), and patch level (7). The final number, (1), is the developer patch level and is assigned by the Fedora Project.

Even minor numbers are considered “stable” and generally fit for use in production environments, while odd minor numbers (such as a Linux 2.7 source tree) represent versions of the Linux kernel under development and testing. You will only find stable versions of the Linux kernel included with this book. You can choose to download and install a beta (test) version of the kernel, but this is not recommended for a system destined for everyday use. Most often, beta kernels are installed to provide support and testing of new hardware or operating system features.