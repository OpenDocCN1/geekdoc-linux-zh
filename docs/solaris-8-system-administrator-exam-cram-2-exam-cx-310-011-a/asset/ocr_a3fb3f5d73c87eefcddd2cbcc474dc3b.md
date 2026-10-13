This chapter covers system security and file permissions. In particular, system security involves controlling access to the system by use of passwords and restricting/monitoring the use of administrative user accounts. The file permissions portion of the chapter addresses controlling access to the data in files by using both basic and extended access controls. Most of the *Security* test objectives are covered in this chapter.

# System Security

Unix system security is based on controlling access to files (programs and data). You control access by defining user and group accounts and granting these accounts different levels of file access. The user accounts are protected by passwords.

Administrative accounts are given access to system data and tools that allow them to perform system maintenance. These accounts include root, sys, bin, and adm.

Several account administration files are used to store information associated with user and group accounts, such as account names and passwords.

# The Superuser (Root) Account

The root, or superuser, account is a special administrative account that provides the ultimate in access to data and services because it can override any file permissions on the system. To enforce good system security, you must restrict access to the superuser account and monitor it as closely as possible. Solaris 8 provides several ways to restrict and monitor the superuser account, discussed in the following sections.

# Restricting and Monitoring the Superuser Account

You can restrict the root account so that it cannot log in to the system remotely; instead, it must log in from the system console. This restriction can be enforced by the following entry in the /etc/default/login file:

```
```text
CONSOLE=/dev/console
```
```

By default, the root account is restricted. To disable this feature, edit the /etc/default/login file and put the shell comment character (#) at the beginning of the entry.

Restricting the root login to the console forces anyone accessing the superuser account remotely to log in with a regular system account and then use