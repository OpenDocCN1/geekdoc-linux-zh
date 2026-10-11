**WARNING**  Solaris 8 uses 64-bit data types for UID and its group equivalent GIDs. Prior to Solaris 2.5, 32-bit data types were used, which limited these ID numbers to a maximum value of 60,000. Therefore, there are interoperability issues when you use numbers greater than 60,000 with older versions of Solaris and other versions of Unix. Among the problems you may encounter are ID number truncation for a SunOS 4.x NFS server and client, reassignment of the UID for the su command to 60,001 (nobody), access denied to systems running Solaris 2.5, and incorrect UIDs and GIDs displayed in the OpenWindows File Manager when used with the extended file listing option. You will also see problems with the cpio tar and ar command utilities when you create archives, as well as problems with the ps command’s listing when you exceed UID or GID numbers of 60,003.

# The shadow File

Solaris stores users’ passwords in the `/etc/shadow` file, which is an encrypted file that can be read only by someone with root privileges. In addition to the password, the shadow file stores in nine fields user account information that is protected by the operating system. Figure 11.2 shows an /etc/shadow file open in the text editor. You can use the usermod command to modify all of the account information in the shadow file with the exception of the password. Users can modify their password using the passwd command; a superuser or root account can modify all passwords using the passwd command.

![](bbox=[0.07, 0.57, 0.2, 0.61])

![](bbox=[0.29, 0.58, 0.83, 0.86])