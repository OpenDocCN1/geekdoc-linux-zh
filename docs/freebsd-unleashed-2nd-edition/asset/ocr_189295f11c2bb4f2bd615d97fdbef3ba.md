Users never really access their files directly. Everything a user does to his or her files by giving commands is effectively done by executing processes, running with the user's assigned permissions. Those processes then operate on files and other processes, as illustrated in Figure 9.1. The processes owned by user1 can only operate on the files and processes owned by user1; permission would be denied if any of those processes tried to change any of user2's files or processes in any way. In the simplest setup, each user can change only those files and processes that he or she owns.

![](bbox=[0.2, 0.26, 0.8, 0.47])

**FIGURE 9.1** A user executes processes, which then operate on files and other processes.

Imagine what would happen if user1 were the super-user. That user's processes would have absolute power over any other user's files and processes. If one of user1's processes is, for instance, a program that reads a configuration file and then modifies items on the system specified in that file, imagine what would happen if an unauthorized user managed to modify the configuration file. The system would be vulnerable to complete annihilation. This is why most system processes, except those that are absolutely trusted, run under the ownership of one of the automated pseudo-users instead of running as root.

# ## Why Use Groups?

Every user belongs to some primary group, generally a group of one that has the same name as the user. This can be changed as you see fit; for instance, you may decide to have all users belong to the “users” group as their primary group. However, having a different group for every user gives you more flexibility, as you'll see a little later. It's also a more secure model. More information on unique “personal” groups can be found in man adduser.

Each user can also belong to any other groups in the system, such as other users' “personal” groups, the wheel group, or any other group you create (by adding the user to the /etc/group file, as you'll see later). However, the super-user is the only one who can control who belongs to what groups.