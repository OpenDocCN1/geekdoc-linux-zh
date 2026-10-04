# Access Control Lists

Access control lists (ACLs) are an extension of file system permissions. They are typically specific to the file system implemented with the particular Unix, and provide a more granular method of control within the system. The method works usually similarly to the traditional file system permissions model used in Unix with the read, write, and execute bit.

However, ACLs differ in that they allow one to specify exactly which users or groups, if any, may have any of these permissions. Because they are so granular, ACLs are often useless useless. Addition of a single user to the system requires going through the entire system and adding the user into access control lists for binaries that the user will require execute permissions over. However, for smaller tasks, ACLs may be exactly what is needed.

# Access Control Lists and Commercial Unix

In Solaris, ACLs are manipulated using the setfac(1) program. The setfac command can be used to manually set ACL entries on a specific file, or the path to a configuration file containing ACL entries can be specified with a command line flag to automatically apply the permissions in the configuration file. This feature can allow you to apply specific access control requirements to a number of files using one centralized configuration.

Access control list entries are displayed using the getfac(1) program. The getfac program is simple to use and provides only two options when executed. One option allows the user of getfac to see the file name, owner, group, and ACL of the file. The other option displays the same information, except instead of displaying the current ACL, it displays the default ACL for the given file.

In HP-UX, access control lists are manipulated with a single program. HPUX uses the swacl program to perform all ACL actions. AIX uses three programs to manipulate ACLs, the aclget, aclput, and acledit commands.

# Access Control Lists and Linux

Linux requires additional patches to the kernel to provide access control list functionality. One source of information is the Linux Access Control Lists Project, reachable via the Web at http://sourceforge.net/projects/linux-acl. A few other projects exist that also provide this functionality, such as the grssecurity.net project. It is rumored that the 2.6 kernel will provide this functionality natively.