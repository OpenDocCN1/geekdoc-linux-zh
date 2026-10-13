Directory names can be made up of a combination of numbers, symbols, and characters. The name of the directory includes the location of the directory in the filesystem relative to the root (/) directory. In other words, the directory name includes the path to follow through the filesystem to get to the directory.

![](bbox=[0.3, 0.28, 0.35, 0.38])

> > The forward slash character (/) is also used to separate directories, subdirectories, and files. The slash character (/) by itself denotes the root directory.

Directories that are nested (contained) within other directories are called subdirectories. A parent/child relationship exists between the two directories. The home directory for your user account is one of these subdirectory branches. It's name begins with the / character, which signifies the root directory. Off the root directory is a subdirectory that contains all the home directories for the system users—the /home directory. Each user has a subdirectory of his or her own in the /home subdirectory.

For example, a user named "rusty" would have a home directory located in the /home/rusty directory path. Notice that there's nothing in front of the / in front of home. This signifies that /home is a subdirectory of the root directory. Because there's no / after /rusty, it could be confusing whether /rusty is a subdirectory of /home or a file stored there. Of course, to end the confusion, you can go ahead and place a / after /rusty to indicate that it is a directory.

The /home directory is not the only directory in the Linux filesystem. The following is a list of directories you'll find when looking around the Linux filesystem:

+   - The base of the operating system is the root (/) directory. It contains all the subdirectories and files in the Linux system. One important item that you'll usually find in the /boot directory is the Linux kernel. If you don't find it here, you'll find it in the / directory.

![](bbox=[0.3, 0.88, 0.35, 0.96])

> > Do not store any files in the / directory. Only system-specific configuration files (such as boot information files) are to be located at the root of the system.