+   *   There is exactly one primary group for every user
+   *   The primary group of local users is defined by the fourth field in the /etc/passwd file where the group number GID is listed
+   *   New files created by the user are owned by the primary group
+   *   The primary group of a user by default has the same name as that of the user. This is a User Private Group (UPG) and the user is the only member of this group

Supplementary Group:

+   *   A user can be a member of zero or more supplementary groups
+   *   The primary group of local users is defined by the last field in the /etc/group file. For local groups, the membership of the user is identified by a comma separated list of user, which is located in the last field of the group's entry in /etc/group
+   *   groupname: password: GID: list, of, users, in, this, group
+   *   The concept of supplementary groups is in place so that users can be part of more group and in turn have to resources and services that belong to other groups in the system

# ## Getting Superuser Access

In this section, we will learn about what the root user is and how you can be the root or superuser and gain full access over the system.

The root user
There is one user in every operating system that is known as the superuser and has all access and rights on that system. In a Windows-based operating system, you may have heard about the superuser known as the administrator. In Linux based operating