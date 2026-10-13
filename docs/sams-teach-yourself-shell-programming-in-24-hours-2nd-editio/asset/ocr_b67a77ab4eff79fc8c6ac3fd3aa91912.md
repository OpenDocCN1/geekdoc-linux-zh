Some of the new features added to UNIX in System V are

+   - A new boot system
+   - A networking subsystem known as STREAMS
+   - A process-to-process communication and memory sharing system
+   - Standardized system administration tools
+   - A prepackaged software installation and removal system

System V UNIX also changed the layout of the file system. Table 23.1 lists the BSD directories and their System V equivalents.

Table 23.1 System V Equivalents of BSD Directories

| BSD | System V |
|---|---|
| /bin | /usr/bin |
| /sbin | /usr/sbin |
| /usr/adm | /var/adm |
| /usr/mail | /var/mail or /var/spool/mail |
| /usr/tmp | /var/tmp |

The directories /bin and /sbin still exist on some System V-based UNIX versions.

On Solaris, these directories are links to /usr/bin and /usr/sbin, respectively. On HP-UX, these directories still contain some commands essential at boot time. The commands stored in these directories are not the same commands as in BSD. Most vendors who have switched from BSD to System V still provide BSD versions in the directory /usr/ucb.

In addition to these changes, many System V-based UNIX versions have introduced the directory /opt in an attempt to standardize the installation locations of prepackaged software products. On older systems, many different locations, including /usr, /usr/contrib, and /usr/local, were used to install optional software packages.

# Linux

Linux can be considered as a third version of UNIX. It was developed independent of either the BSD or the System V source code. Linux was written by Linus Torvalds at the University of Helsinki in the early 1990s. It incorporates the best features found in both System V and BSD. The commands and the networking layer in Linux are similar to BSD, whereas the standardized tools for system configuration and installation of prepackaged software are similar to System V. Some of the major vendors of Linux are Caldera, Debian, Mandrake, Red Hat, Slackware, and SuSE.