# **CHAPTER 10**
# Managing Users

+   ### IN THIS CHAPTER
+   
+   - User Accounts
+   - Managing Groups
+   - Managing Users
+   - Managing Permissions
+   - Managing Passwords
+   - Granting System Administrator Privileges to Regular Users
+   - Disk Quotas
+   - Reference

One of the most important things you need to learn while using Fedora is effective user administration. Whether you are setting up a system for use just by yourself, sharing it among a family of five, or even working with a machine that has to handle several thousand different users, it is important that you understand how to effectively assign user permissions and lock down the areas you want to protect. Equally important is the ability to fine-tune user access rights, to enable people to do what they need to do, and not necessarily what they want to!

Managing users includes managing home directories and settings that are unique to each user. You also have to examine how much of the overall system to which you want to give the users access, as well as establish good password practice. This chapter covers all these tasks, as well as others that teach you how to effectively manage the users of your system. It also takes a look at the super-user account so that you can understand why it is so important and also how to let others access some, if not all, of the super-user's power.

# ## User Accounts

Every Fedora installation typically contains three types of accounts: the super user, the day-to-day user, and the system user. Each type is important in its own right, and you must know what each is responsible for. If they didn't work together, Fedora would have a hard time doing anything!

All users must have accounts on the system. Fedora uses the `/etc/passwd` file to hold information on user accounts. Each user, regardless of type, has a one-line entry of account information stored in the `/etc/passwd` text file.