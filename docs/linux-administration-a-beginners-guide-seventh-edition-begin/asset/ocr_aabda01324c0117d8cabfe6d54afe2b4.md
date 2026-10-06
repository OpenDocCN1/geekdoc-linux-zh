# CHAPTER 5 Managing Users and Groups

# 123

# Where User Information Is Kept

If you're already accustomed to user management in Microsoft Windows Server environments, you're definitely familiar with Active Directory (AD), which takes care of the nitty-gritty details of the user and group database. Among other things, this nitty-gritty includes the SIDs for users, groups, and other objects. AD is convenient, but it makes developing your own administrative tools trickier, the only other way to read or manipulate user information is through a series of Lightweight Directory Access Protocol (LDAP), Kerberos, and programmatic system calls.

In contrast, Linux takes the path of traditional UNIX and keeps all user information in straight text files. This is beneficial for the simple reason that it allows you to make changes to user information without the need of any other tool or text editor. In many instances, larger sites take advantage of these text files by developing their own user administration tools so that they can not create new accounts, but also automatically make additions to the corporate phone book, web pages, and so on.

However, us new to Linux/UNIX may prefer to stick with the basic user management tools that come with most Linux distributions. We will discuss these topics in “User Management Tools” later in this chapter. For now, let's examine the text files that store and group user information in Linux.

> NOTE This chapter covers the Linux/UNIX methods for storing and managing user information. Chapters 26 and 27 of this book discuss other mechanisms (such as NIS and LDAP) for storing and managing users and groups in Linux-based operating systems.

# The /etc/passwd File

The /etc/passwd file stores the user's login, encrypted password entry, UID, default GID, name (sometimes called GECOS), home directory, and login shell. Each line in the file represents information about a user. The lines are made up of standard fields, with each field delimited by a colon. A sample entry from a passwd file with its various fields is illustrated in Figure 5-1.

The fields of the /etc/passwd file are discussed in detail in the section that follows.

| Username | User ID | GECOS | Shell |
| --- | --- | --- | --- |
| yyang: x: | 1001: | Ying Yang: | /home/yyang;/bin/bash |
| Password | | Group ID | Directory |

Figure 5-1 Fields of the /etc/passwd file