# GECOS field

It can be hard to maintain unique UIDs when groups of machines are administered by different people or organizations. The problems are both technical and political. The best solution is to have a central database or directory server that contains a record for each user and enforces uniqueness. A simpler scheme is to assign each group within an organization a range of UIDs and let each group manage its own set. This solution keeps the UID spaces separate but does not address the parallel issue of login names.

LDAP is becoming a popular management tool for UIDs and user account information. It is briefly outlined in this chapter starting on page 202 and is covered more thoroughly in Chapter 19, Sharing System Files, starting on page 728.

# Default GID number

Like a UID, a group ID number is a 32-bit integer. GID 0 is reserved for the group called root or system. With UIDs, the system uses several predefined groups for its own housekeeping. Alas, there is no consistency among vendors. For example, the group bin GID 1 on Red Hat and SUSE GID 2 on Ubuntu, Solaris, HP-UX, and AIX.

In ancient times, when computing power was expensive, groups were used for accounting purposes so that the department could be charged for your seconds of CPU time, minutes of login time, and kilobytes of used disk. Today, groups are used primarily to share access to files.

Theetc/passwd file defines the groups, with the GID field in /etc/passwd providing a default (or "effective") GID at login time. The default GID is not treated specially when access is determined; it is relevant only to the creation of new files and directories. New files are normally owned by your effective group, but if you want to share files with others in a project group, you must then remember to manually change the file's group.

To facilitate collaboration, you can set the setgid (02000) on a directory or mount filesystems with the gridid option. Both of these measures make newly created files of the parent directory.

# GECOS field

The GECO field is used to record personal information about each user. It has no well-defined syntax. You can use any formatting conventions you like, the finger command interprets comma-separated GECO entries in the following:

+   - Full name (often the only field used)
- Office number and building
- Office telephone extension
- Home phone number