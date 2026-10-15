system is set up in a standard way. If you try to improve upon the default structure, you are asking for trouble.

The root filesystem includes the root directory and a minimal set of files and subdirectories. The file that contains the OS kernel usually lives somewhere within the root filesystem, but it has no standard name or location; under Solaris, it is not really even a single file so much as a set of components.

Also part of the root filesystem are /etc for critical system and configuration files, /sbin and /bin for important utilities, and sometimes /tmp for temporary files. /dev is usually a real directory that's included in the root filesystem, but some or all of it may be overlaid with other filesystems if your system has virtualized its device support. (See page 419 for more information about this topic.)

Some systems keep shared library files and a few other odd things such as the C preprocessor in the /lib directory. Others have moved these items into /usr/lib, sometimes leaving /lib as a symbolic link.

See Chapter 13 for more information about configuring the kernel.

The directories /usr and /var are also of great importance. /usr is where most standard programs are kept, along with various other booty such as on-line manuals and most libraries. It is not strictly necessary that /usr be a separate filesystem, but for convenience in administration it often is. Both /usr and /var must be available to enable the system to come up all the way to multiuser mode.

See page 231 for some reasons why partitioning might be desirable and some rules of thumb to guide it.

/var houses spool directories, log files, accounting information, and various other items that grow or change rapidly and that vary on each host. Since /var contains log files, which are apt to grow in times of trouble, it's a good idea to put /var on its own filesystem if that is practical.

Home directories of users are often kept on a separate filesystem, usually one that's mounted in the root directory. Dedicated filesystems can also be used to store bulky items such as source code libraries and databases.

Some of the more important standard directories are listed in Table 6.2. (Alternate rows have been shaded to improve readability.)

On many systems, a hier man page (filesystem man page on Solaris) outlines some general guidelines for the layout of the filesystem. Don't expect the actual system to conform to the master plan in every respect, however. The Wikipedia page for "UNIX directory structure" is a good general reference as well.

![](bbox=[0.15, 0.88, 0.22, 0.95])

For Linux systems, the Filesystem Hierarchy Standard (pathname.com/fhs) attempts to codify, rationalize, and explain the standard directories. It's an excellent resource to consult when you're trying to figure out where to put something.

We discuss some additional rules and suggestions for the design of local hierarchies on page 407.