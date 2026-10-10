# The Linux Directory Structure

**Directory What's In It**

**/mnt** A folder for other mount points, usually other partitions not used directly by Linux, including those for other operating systems.

**/proc** Process and system information. Be extremely careful of changes to /proc while you are logged in as the root user, because they can easily bring the system down.

**/root** The home directory for the root user.

Home directories for other users are generally sub-directories of /home.

**/sbin** System binary files. Some of these are usable-only by the root user.

Other executables are in /bin.

**/usr** Programs and system files that are shared by all users. A common location for free software or for third-party software. Important sub-directories include /usr/local and /usr/share.

**/var** Data files whose content changes frequently, such as caches, spools, log files and user mailbox files.