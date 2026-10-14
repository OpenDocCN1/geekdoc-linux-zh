# WINDOWS 2000 GROUPS

Windows 2000 also provides the ability to organize users into groups. You can use these groups to grant/deny access to resources and to create an organizational structure. This section will provide you with an overview of groups in Windows 2000 and describe how to create a group on your Windows 2000 domain controller.

# Overview of Groups

Simply put, a group is a collection of users, or rather, user accounts. You can use groups to assign permissions to groups of users instead of individual users. When working with groups, keep the following in mind:

+   - Users can be members of multiple groups.
+   - Each user account is assigned a “primary” group (the default is Domain Users).
+   - Members inherit group permissions.
+   - Groups themselves can be members of other groups.

You must also understand two things about groups: type and scope. Table 12.12 describes the different types of groups, and Table 12.13 describes the different group scopes.

By properly organizing your users into groups, you can make system administration much easier. Instead of assigning permissions to users, you can assign permissions to groups, thus reducing the administrative overhead required when user accounts are added and removed from the domain. Now that you understand the different types of groups and the scopes they cover, we can discuss creating groups.

| Table 12.12 Windows 2000 Group Types |  |
|---|---|
| Group Type | Description |
| Security Group | Windows 2000 uses security groups to assign permissions to groups of users. Security groups can also be used as distribution groups. |
| Distribution Group | Distribution groups are used by applications for non-security-related functions, such as sending mail. You cannot use distribution groups for assigning permissions. |