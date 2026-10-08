# redhat Chapter 6.

# Users and Groups

Control of users and groups is a core element of Red Hat Linux system administration.

Users can be either people, meaning accounts tied to physical users, or accounts which exist for specific applications to use.

Groups are logical expressions of organization, tying users together for a common purpose. Users within the same group can read, write, or execute files owned by the group.

Each user and group have a unique identification number called a userid (UID) and a groupid (GID) respectively.

When a file is created, it is assigned to a user and group owner. It is also assigned separate read, write, and execute permissions for the owner, the group, and everyone else. The group to which a file belongs, as well as the access permissions on the file, can be changed by the root user, or by the creator of the file.

Proper management of users and groups, and effective management of file permissions are among the most important tasks a system administrator undertakes. For a detailed look at strategies for managing users and groups, refer to the chapter titled Managing Accounts and Group in the Red Hat Linux System Administration Primer.

# 6.1. User and Group Management Tools

Managing users and groups can be a tedious task, but Red Hat Linux provides tools and conventions to make their management easier.

The easiest way to manage users and groups is through the graphical application, User Manager (redhat-config-users). For more information, refer to the chapter titled User and Group Configuration in the Red Hat Linux Customization Guide.

The following command tools can also be used to manage users and groups:

+   - useradd, usermod, and userdel — Industry-standard methods of adding, deleting and modifying user accounts.
- groupadd, groupmod, and groupdel — Industry-standard methods of adding, deleting, and modifying user groups.
- gpasswd — Industry-standard method of administering the /etc/passwd file.
- pwck, grpck — Tools for verifying the password, group, and associated shadow files.
- pwconv, pwunconv — Tools for the conversion to shadow passwords and back to standard words.

For an overview of users and group management, see the Red Hat Linux System Administration Primer. For a detailed look at command line tools for managing users and groups, see the chapter titled User and Group Configuration in the Red Hat Linux Customization Guide.

# 6.2. Standard Users

Table 6-1 lists the users configured in the /etc/passwd file by an "Everything" installation. The groupid (GID) in this table is the primary group for the user. See Section 6.3 Standard Groups for a listing of standard groups.