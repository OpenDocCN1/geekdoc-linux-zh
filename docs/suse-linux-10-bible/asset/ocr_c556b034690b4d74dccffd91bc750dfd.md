# Part I ♦ SUSE Linux Basics

At a bare minimum, the files that need to be created are the swap space and a root (/) filesystem. However, for ease of manageability, the creation of a /home partition can help keep your personal data safe from the system partition and also enable you to keep your data in the unlikely event that you want to do a total reinstall of Linux. See the section “Data Partitions” later in this chapter for more information.

In this example you are creating the bare minimum, and root partitions.

# The Root Partition

After the space has been created, you need to configure the root (/) partition (see Figure 1-13). The root (/) partition is the most important data partition on any Linux or Unix system, and it is the only non-swap filesystem that is required to boot a Unix or Linux system. The root partition takes its name from the fact that it is mounted at the root of the Unix/Linux filesystem, which is the directory mounted on which to successfully boot a Linux system. The root filesystem contains core directories required to boot Linux, such as /dev; the directory containing system administration, configuration, and initialization files (/etc); the directory in critical system libraries, kernel modules, security, and informational information located at (/lib); and directories containing system binaries (/bin, /sbin, and so on.

![](bbox=[0.165, 0.543, 0.805, 0.913])

Figure 1-13: Creating the root partition