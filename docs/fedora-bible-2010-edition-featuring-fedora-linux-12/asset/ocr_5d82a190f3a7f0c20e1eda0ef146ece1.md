Some user accounts are automatically created when you install your Linux system.  
Administrative user accounts (originally UID 0-99, although now UIDs up to 499 are used) are created to maintain separate control of system files and services from regular user accounts. Of the administrative user accounts, you will probably use only root (when some system administration is required).

Regular user accounts are created using any names you choose, starting (by default) with a user ID (UID) of 500. Regular users you add to your Fedora system typically fall into one of two categories:

+   - **Desktop users** — A desktop user is one whom you expect to use your computer via a graphical interface (typically GNOME or KDE). Create this kind of user account for yourself and anyone else you want to be able to log in directly to your computer (or from a thin client over the network). Most of this section describes how to add this type of user.
+   - **Server users** — If you are configuring Fedora as a server (Web, mail, FTP, and so on), you may want to add accounts for users who should have only limited access to your system. You may want those users to be able to add content to a Web server or access a mail server but have only a shell login account (or possibly no login account). See the section “Adding user accounts to servers” later in this chapter for information on adding these types of accounts.

> **CROSS-REFERENCE:** If you have multiple users, you’ll also need to be concerned about backup and recovery issues for those users. See Chapter 12 for more information.

You can add user accounts to your Fedora system in several ways. This chapter describes how to use the useradd command to add user accounts to Fedora from the command line, and how to use the User Manager window to add users from the desktop.

# ### Adding users with useradd

The most straightforward method for creating a new user from the shell is with the useradd command. After opening a Terminal window with root permission, simply invoke the useradd command at the command prompt, with details of the new account as parameters.

The only required parameter to useradd is the login name of the user, but you will probably want to include some additional information. Each item of account information is preceded by a single-letter option code with a dash in front of it. Table 10-1 lists the options that are available with the useradd command.