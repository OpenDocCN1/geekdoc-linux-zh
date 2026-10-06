# Locating Files 207

than a per-user basis. Setting a limit to 0 (as in the inode limits in the preceding example) eliminates the use of quotas for that value; users may consume as much disk space or create many files as they like, up to the available space on the filesystem.

When using edquota, you can adjust independently for every filesystem for which quotas are enabled and for every user or group. (To edit quotas for a group, use the -g option, as in edquota -g users to adjust quotas for the users group.)

A few more quota-related commands are available. The first is quotacheck, which verifies and updates quota information on quota-enabled disks. This command is normally run as part of the quota package startup script, but you may want to run it periodically (say, once a week) as a cron job (Chapter 7 describes cron jobs). Although theoretically not everything is necessary, quotacheck ensures quota accounting doesn't become inaccurate. The second auxiliary quota command is reportquota, which summarizes the quota information about the filesystem you specify or on all filesystems you pass in the -a option. This tool can be very helpful in keeping track of disk usage. The quota command has a similar effect. It takes a number of options to have modify their outputs. For instance, -g displays group quotas, -1 limits NFS mounts, and -q outputs to filesystems on which usage is over the limit. Consult quota's man page for more obscure options.

# Locating Files

Maintaining your filesystems in perfect health, setting permissions, and so on is pointless if you can't find them. For this reason, Linux provides several tools to locate the files you need to use. The first of these tools is a standard for where files are located; with the right knowledge, you may be able to find files without any of specialized programs. The second class of tools includes just specialized programs, which search a directory tree or a database for whatever meets your criteria.

# The FHS

Linux's placement of files is derived from more than 40 years of Unix history. Given that fact, the structure is remarkably stable and coherent, it's easy for a new administrator to become confused. Some directories exist, on the surface, to fulfill similar or identical roles, but in fact there are subtle but important differences. This section describes the Linux directory standards and provides an overview of what goes where.

# The FSSTND and FHS

Although Linux draws heavily on Unix, its long history has led to numerous splits and variants, starting with the Berkeley Standard Distribution (BSD), which was originally a set of patches and extensions to AT&T's Unix code. As a result of these schemes within the Unix community, early Linux distributions didn't always identical