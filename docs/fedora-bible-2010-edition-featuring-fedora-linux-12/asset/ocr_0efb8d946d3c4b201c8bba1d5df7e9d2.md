# # Chapter 10
# Setting Up and Supporting Users

# **In This Chapter**

+   - Creating user accounts
+   - Setting user defaults
+   - Extending user authentication
+   - Creating portable desktops
+   - Providing support to users
+   - Deleting user accounts
+   - Checking disk quotas
+   - Sending mail to all users

One of the more fundamental and important tasks of administering a Linux system is setting up and supporting user accounts. Computers, after all, are tools to be used by people. Apocalyptic science fiction plots aside, computers have no purpose without users.

> When you install Fedora, you automatically create an account, called the root user account, to administer the system. The first time you boot Fedora, you are asked to create a regular user account, using any name you choose. Several other administrative user accounts that you will probably never use directly are set up automatically as well (such as apache, rpm, and lp). **CROSS-REFERENCE**: For a description of the root user account and how to use it, see Chapter 9.

This chapter discusses the basics of setting up user accounts and offers tips on easing the burden of supporting a large number of Linux users.

# ## Creating User Accounts

Every person who uses your Fedora system should have a separate user account. Having a user account provides each person with a dedicated area in which to securely store files. A user account also defines which files and directories a user is permitted to create, modify, or delete throughout the computer’s file system.