many files and directories of an operating system such as Red Hat Linux. The benefit of the FHS standard lies in compatibility with other FHS-compliant systems. For example, if a software developer wishes to support both Red Hat Linux and another FHS compliant Linux distribution, he or she can simply make the installation program use a standard directory for installing the software. This makes life easier for both developers and users of the software. The details of the FHS standard are available at www.pathname.com/fhs.

The top directories of a FHS system are shown in Table 8-1.

# Table 8-1 Top Directories of an FHS System

| Directory | Purpose |
|---|---|
| / | The root directory. |
| /bin | Contains essential command binaries. |
| /boot | Contains boot loader files. |
| /dev | Contains device files. |
| /etc | Contains system configuration files. |
| /lib | Contains kernel modules and shared library files. |
| /mnt | Usually used for storing mount point directories for removable media such as CD-ROM, floppy drive, etc. |
| /opt | Contains third-party applications. |
| /sbin | Contains system binaries. |
| /tmp | Temporary space for all users. |
| /usr | This is a separate directory structure of its own. It is discussed in Table 8-2. |
| /var | Variable data space used by programs to store logs, spools, etc. |

The /usr directory structure is very important because it is (usually) available throughout the entire file system for all users. The /usr directory structure is shown in Table 8-2.