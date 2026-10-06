# The init Process and the /etc/initab File 369

# TABLE 15.6 Mount Options (continued)

| Option | Description |
| --- | --- |
| sync | Perform all input and output synchronously. |
| user | Permit an ordinary user to mount the file system. Implies the options noexec, nosuid, and nodev. |

You can modify the contents of the /etc/fstab file using linuxconf, or if you prefer, you can use a text editor. Now try your hand at configuring file systems by completing Exercise 15.4.

# EXERCISE 15.4

# Configuring File Systems

Configuring file systems is an important and common system administration task that is likely to appear on the RHCE exam. To hone your skills in preparation for the exam, modify the /etc/fstab file to specify that a non-root partition will be mounted in read-only mode. Boot the system and verify that your change was correct. Restore the original configuration and reboot the system.

If necessary, you can refer to this book while doing the exercise. Before taking the RHCE exam, be prepared to perform operations such as without the assistance of books or documentation.

# The init Process and the /etc/initab File

The init process is responsible for spawning log-in processes and managing the system runlevel. Its configuration file, /etc/initab, determines the services that should be active at each defined runlevel.