
## Missing Configure Script

Sometimes, you will download a package and instantly type cd into its directory and run /`configure`. And you will probably be shocked when you see the message “No such file or directory.” As stated earlier in the chapter, read the README and INSTALL files that are packaged with the software. Typically, the authors of the software are courteous enough to provide at least one of these two files. Source code for packages that you obtain directly from version control systems (such as git, svn, mercurial, and so on) may ship with an autogen.sh script, which you can run instead of configure or to generate the missing configure file.

> TIP: It is common for many of us to jump right in and begin something without first looking at the document, and then to come back hours later to find that a step was missed. The first step you should take when installing software is to read the documentation. It will plainly point out the fact that you need to run something exotic like make first and then make. You get the idea: Always read the documentation first, and then proceed to compiling the software.

## Broken Source Code

No matter what you do, it is possible that the source code you have is simply broken and the only person who can get to it or make any sense of it is its original author or some other software developers. You might have spent countless hours trying to get the application to compile and build before coming to this conclusion and throwing in the towel.

It is also possible that the author of the program has not documented some valuable or relevant information. In cases like this, you could try to use precompiled binaries for the application already exist for your specific Linux distro in the form of RPMs, deb files, and so on.

## Summary

You've explored the common functions of the popular RPM and DPMS. You used various options to manipulate RPM and .deb packages by querying, installing, and uninstalling sample packages.

You learned and explored various software management techniques using purely command-line tools. We also discussed few GUI tools that are used on popular Linux distributions. The GUI tools are similar to the Windows Add/Remove Programs Control Panel app—just point and click. The chapter also touched on other software management systems in Linux distros, namely, DNF, and APT.

Using an available open source program as an example, you went through the steps involved in configuring, compiling, and building software from the raw source code.

As a bonus, you also learned a thing or two about the mechanics of human relationships!

# PART II
Single-Host Administration

## CHAPTER 5 Managing Users and Groups

## Linux Administration: A Beginner's Guide

Linux/UN was designed from the ground up to be a multiuser operating system. But a multiuser operating system would not be much good without users! And this brings us to the topic of managing users in Linux.

On computer systems, a system administrator sets up user accounts, determine who has access to. The ability of a person to access a system is determined by whether that user exists and has the proper permissions to use the system.

Associated with each user is "baggage," which can include files, processes, resources, and other information. When dealing with a multiuser system, a system administrator needs to understand what constitutes a user (and the user's baggage) and a group, how they interact together, and how they affect available resources.

In this chapter, we will examine the technique of managing users on a single host. We'll begin by exploring the account database files that contain information about users. From there, we will examine the system tools available to manage the files automatically.

## What Exactly Constitutes a User?

Under Linux, every file and program must be owned by a user. Each user has a unique identifier called user ID (UID). Each user must also belong to at least one group—a collection of users. Users may belong to multiple groups. Like users, groups also have unique identifiers, called group IDs (GIDs).

The accessibility of a file or program is based on UIDs and GIDs. A running program inherits the rights and permissions of the user who invokes it. (An exception is SetUID and SetGID programs, discussed in "Understanding SetUID and SetGID Programs" in this chapter).

Each user's rights can be defined in one of two ways: as a normal user or a superuser. Normal users can access only what they own or have been given permission to run; permission is granted because the user belongs to the file's group or programs in the system, whether or not he owns the them. A superuser is allowed to access all files and programs. A superuser is a classic example of a superuser and the two words are used interchangeably.

If you are accustomed to Windows, you can draw parallels between system's user management and Linux's user management. Linux UIDs are comparable to Windows SIDs (security identifiers). In contrast to Microsoft Windows, you might find the Linux security model maddeningly simple: Either you're root or you're not.

Normal users do not have root privileges in the same way normal users can be granted administrator access under Windows. Although this approach is a little common, you can implement finer grained access control through the use of access control lists (ACLs) in Linux, as you can with Windows. Which system is better? Depends on what you want and whom you ask.

## CHAPTER 5 Managing Users and Groups

## Where User Information Is Kept

If you're already accustomed to user management in Microsoft Windows Server environments, you're definitely familiar with Active Directory (AD), which takes care of the nitty-gritty details of the user and group database. Among other things, this nitty-gritty includes the SIDs for users, groups, and other objects. AD is convenient, but it makes developing your own administrative tools trickier, the only other way to read or manipulate user information is through a series of Lightweight Directory Access Protocol (LDAP), Kerberos, and programmatic system calls.

In contrast, Linux takes the path of traditional UNIX and keeps all user information in straight text files. This is beneficial for the simple reason that it allows you to make changes to user information without the need of any other tool or text editor. In many instances, larger sites take advantage of these text files by developing their own user administration tools so that they can not create new accounts, but also automatically make additions to the corporate phone book, web pages, and so on.

However, us new to Linux/UNIX may prefer to stick with the basic user management tools that come with most Linux distributions. We will discuss these topics in “User Management Tools” later in this chapter. For now, let's examine the text files that store and group user information in Linux.

> NOTE: This chapter covers the Linux/UNIX methods for storing and managing user information. Chapters 26 and 27 of this book discuss other mechanisms (such as NIS and LDAP) for storing and managing users and groups in Linux-based operating systems.

## The /etc/passwd File

The /etc/passwd file stores the user's login, encrypted password entry, UID, default GID, name (sometimes called GECOS), home directory, and login shell. Each line in the file represents information about a user. The lines are made up of standard fields, with each field delimited by a colon. A sample entry from a passwd file with its various fields is illustrated in Figure 5-1.

The fields of the /etc/passwd file are discussed in detail in the section that follows.

| Username | User ID | GECOS | Shell |
| :--- | :--- | :--- | :--- |
| yyang: x: | 1001: | Ying Yang: | /home/yyang;/bin/bash |
| Password | | Group ID | Directory |

Figure 5-1 Fields of the /etc/passwd file

## Username Field

This field is also referred to as the login field or the account field. It stores the name of the user on the system. The username must be a unique string and uniquely identifies a user to the system. Different sites use different methods for generating login names.

A common method is to use the first letter of the user’s first name and append the user’s last name. This usually works, because the chances are relatively slim that an organization would have several users with the same first and names. For example, for a user whose first name is "Ying" and whose last name is "Yang," a username of "yyang" can be assigned. Of course, several variations of this method are also used.

## Password Field

This field contains the user’s encrypted password. On modern Linux systems, this field contains a x to indicate that shadow passwords are being used (discussed further on, in this chapter). Every regular user or human account on the system should have a password. This is crucial to the security of the—weak passwords make compromising a system just that simpler.

## How Encryption Works

The original philosophy behind passwords is actually interesting, especially since we still rely on a significant part of it today. The idea is: Instead of relying on protected files to keep passwords a secret, the system encrypts the password using an AT&T-developed (and National Security Agency-approved) algorithm called Data Encryption Standard (DES) and leaves the encrypted value publicly viewable. What originally made this secure was that the encryption was computationally difficult to break. The most folks could do a brute-force attack, where automated systems would iterate through a large dictionary or on the natural tendency of users to choose English words for their passwords. Many people tried to break DES itself, but it was an algorithm that anyone could study, and it was much more bulletproof before

When users entered their passwords at a login prompt, the password they entered would be encrypted. The encrypted value would then be compared against the user’s password entry. If the two encrypted values matched, the user was allowed to enter the system. The actual algorithm for performing the encryption was computationally cheap enough that a single encryption wouldn’t take too long. However, the tens of thousands of encryptions that would be needed for a dictionary attack would take prohibitively long.
