# ## Getting Started with the Desktop

To log in, type your username and press [Enter], and then type your password and press [Enter]. You can log in as either a regular user or as the root user.

+      - **A Regular User —** As someone just using the Linux system, you probably have your own unique username and password. Often, that name is associated with your real name (such as johnb, susan, or djones). If you are still not sure why you need a user login, see the sidebar “Why Do I Need a User Login?” You probably have at least one user account available that was added the first time you booted CentOS.
+      - **The root User —** Every Linux system has a root user assigned when Linux is installed. The root user (literally type the username root) can run programs, use files, and change the computer setup in any way. Because the root user has special powers and can therefore do special damage, you usually log in as a regular user, which allows access only to that user’s files and those that are open to everyone.

> > **CROSS-REF** See Chapter 9 for a description of the root user and Chapter 10 for information on how to set up and use other user accounts. Refer to Chapter 13 for suggestions on how to choose a good password. For information on instances where the root user doesn’t have complete control over the system, refer to the descriptions of SELinux (Security-Enhanced Linux) in Chapter 9.

If your desktop did not start, refer to the “Troubleshooting Your Desktop” section at the end of this chapter. Otherwise, continue on to the next section.

# ### Why Do I Need a User Login?

If you are working on a PC and you are the only one using your Linux computer, you may wonder why you need a user account and password. Unlike Windows, Linux (like its predecessor UNIX) was designed from the ground up to be a multis user system. Here are several good reasons why you should use separate user accounts:

+      - Even as the only person using Linux, you want a username other than root for running applications and working with files so you don’t change critical system files by mistake during everyday computer use.
+      - If several people are using a Linux system, separate user accounts let you protect your files from being accessed or changed by others.
+      - Networking is probably the best reason for using a Linux system. If you are on a network, a unique username is useful in many ways. Your username can be associated with resources on other computers: file systems, application programs, and mailboxes, to name a few. Sometimes a root user is not allowed to share resources on remote Linux systems.

*continued*