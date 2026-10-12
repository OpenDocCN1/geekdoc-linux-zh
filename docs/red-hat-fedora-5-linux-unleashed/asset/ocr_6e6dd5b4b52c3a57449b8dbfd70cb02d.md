![](bbox=[0.21, 0.11, 0.85, 0.47])

FIGURE 14.1 Just check the box to add a user to a group.

# # Managing Users

We have mentioned users previously, but in this section we examine how the sysadmin can manage the users. Users must be created, assigned a UID, provided a home directory, provided an initial set of files for their home directory, and assigned to groups so that they can use the system resources securely and efficiently. The system administrator might elect to restrict a user’s access not only to files, but to the amount of disk space they use as well. (You can learn more about that in the “Managing Disk Quotas” section of Chapter 7, “Managing Software.”)

# ## User Management Tools

Fedora provides several command-line tools for managing users as well as graphical tools. Many experienced sysadmins prefer the command-line tools because they are quick and easy to use and they can be included in scripts if the sysadmin desires to script a repetitive task. Here are the most commonly used commands used to manage users:

useradd—This command is used to add a new user account to the system. Its options permit the sysadmin to specify the user’s home directory and initial group or to create the user with the default home directory and group assignments.

useradd -G—This command sets the system defaults for creating the user’s home directory, account expiration date, default group, and command shell. See the specific options in man