# ## Objective 3

# ## Manage User and Group Accounts with YaST

With YaST, you can manage users and groups. To do this, you need to understand the following:

+   - Basics about Users and Groups
+   - User and Group Administration with YaST

# ### Basics about Users and Groups

One of the main characteristics of a Linux operating system is its ability to handle several users at the same time (multiuser) and to allow these users to perform several tasks on the same computer simultaneously (multitasking).

For this reason the system must be able to uniquely identify all users. To achieve this, every user must log in with the following:

+   - A username
+   - A password

Because the operating system can handle numbers much better than strings, users are handled internally as numbers. The number which a user receives is a UID (User ID).

Every Linux system has a privileged user, the user *root*. This user always has the UID 0. This is the administrator of the system.

Users can be grouped together based on shared characteristics or activities. For example:

+   - On SUSE Linux Enterprise Server 10, users by default have the group users as their primary group. (This is different from RHEL, where each user has a group of his own as his primary group.)