+   • **LDAP** This is an option that many Linux administrators are starting to adopt more and more. Instead of storing user accounts in a file in the file system, user accounts are stored in a directory service and accessed via the Lightweight Directory Access Protocol (LDAP). Unlike local authentication, which stores accounts in a simple flat file, the directory service is hierarchical in nature, allowing you to sort and organize your user accounts by location, function, or department. The directory database can also be replicated among several different Linux systems, providing fault tolerance. The key benefit of this option is that it allows you to maintain a single set of user accounts that can be used to authenticate to many different Linux systems.

![](bbox=[0.16, 0.3, 0.24, 0.35])

> **NOTE** Essentially, the LDAP option moves Linux in the direction of other server operating systems that use local authentication, such as Novell's eDirectory or Microsoft's Active Directory.

+   • **NIS** This option stands for *Network Information Service*. NIS is also designed to provide centralized user account management when you have multiple systems that all need the same user accounts. To do this, NIS configures systems to all use a common passwd and shadow file.
+   • **Windows Domain** If you have a Windows domain controller in your network (or another Linux server running the Samba service), you can configure your Linux system to use the user accounts in the domain to authenticate to the local system.

![](bbox=[0.16, 0.58, 0.24, 0.63])

> **EXAM TIP** For your LPIC-1/CompTIA Linux+ exam, you need to be concerned with the Local option. All Linux distributions can use the `/etc/passwd` and `/etc/shadow` files for authentication.

Which of these options is best? It depends on what you need your system to do. If the system is a stand-alone workstation, the Local option is usually sufficient. You could also optionally use the LDAP option.

If your system is going to participate on a network where lots of different users will need access to your system, then you may want to consider using LDAP, NIS, or Windows Domain authentication.

For our purposes here, we're going to focus on the Local option. This option stores user and group information in the following files in the file system:

+   • `/etc/passwd` This file contains the user account information for your system.
+   • `/etc/shadow` This file contains passwords for your user accounts.
+   • `/etc/group` This file contains your system's groups. (We'll discuss groups later in this chapter.)

Let's look at the `/etc/passwd` file first.