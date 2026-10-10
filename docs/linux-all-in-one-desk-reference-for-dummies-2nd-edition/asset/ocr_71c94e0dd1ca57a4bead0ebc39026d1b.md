# Chapter 2: Managing Users and Groups

# *In This Chapter*

+   ✓ Adding user accounts
+   ✓ Understanding the password file
+   ✓ Managing groups
+   ✓ Exploring the user environment
+   ✓ Changing user and group ownerships of files and directories

Linux is a multiuser system, so it has many user accounts. Even if you are the only user on your system, many servers require a unique username and group name. Take, for example, the FTP server. It runs under the username ftp. A whole host of system users are not for people but just for running specific programs.

Also, users can belong to one or more groups. Typically, each username has a corresponding private group name. By default, each user belongs to that corresponding private group. However, you can define other groups for the purpose of providing access to specific files and directories based on group membership.

User and group ownerships of files are a way to make sure that only the right people (or the right process) can access the right files and directories. Managing the user and group accounts is a typical system administration job. It’s not that hard to do this part of the job, given the tools that come with Linux. I show you how in this chapter.

# Adding User Accounts

You get the chance to add user accounts when you boot your system for the first time after installing Linux. The root account is the only one that you must set up during installation. If you don’t add other user accounts when you start the system for the first time, you can do so later on, using a GUI user account manager or the useradd command to add new users on your system.