All access to a Linux system is through a user account. Every user must be set up by the system administrator, with the sole exception of the root account (and some system accounts that users seldom, if ever, use). While many Linux systems only have one user, that user should not use the root account for daily access. Most systems allow several users to gain access, either through multiple users on the main console, through a modem or network, or over hard-wired terminals. Knowing how to set up and manage user accounts and their associated directories and files is an important aspect of Linux system administration.

This chapter looks at the the following subjects:

+   - The root (superuser) account
- How to create new users
- The files a new user requires
- What is a group of users
- Managing groups

# # The Superuser Account

When the Linux software is installed, one master login is created automatically. This login, called root, is known as the *superuser* because there is nothing the login can’t access or do. While most user accounts on a Linux system are set to prevent the user from accidentally destroying all the system files, for example, the root login can blow away the entire Linux operating system with one simple command. Essentially, the root login has no limitations.

> **WARNING**

The sheer power of the root login can be addictive. When you log in as root you don’t have to worry about file permissions, access rights, or software settings. You can do anything at anytime. This power is very attractive to newcomers to the operating system, who tend to do everything while logged in as root. It’s only after the system has been damaged that the root login’s problems become obvious: There are no safeguards! As a rule, you should only use the root login for system maintenance functions. Do not use the superuser account for daily usage!