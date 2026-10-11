
## CHAPTER 11
## User Accounts and Groups

FEATURING:

- Working with users and groups 422
- The user database 423
- Working with user accounts 428
- Working with group accounts 449
- Account management with AdminSuite 3 456
- Administering roles 468

In this chapter, you'll learn how to create and manage user and group accounts. User accounts are used to allow access to Solaris with certain rights and privileges at login. It is also possible to assume another account during a session to get effective rights and privileges. With group accounts, you can assign to one or more users a set of rights and privileges in order to streamline security access. Users, their passwords, and groups are stored locally in a set of database files, and they're stored as part of a naming service in a networked environment. Solaris 8 also supports the creation of roles so that system tasks can be assigned to users without root privileges.

### User and Groups

Users and groups are stored as named accounts in local databases, and each account has a number of important attributes. The system identifies each user account by a user identification number (UID number) and each group account by a group identification number (GID number). Accounts are stored locally in your system, and if you are on a network that uses a naming service, they're stored as part of a domain's directory.

Solaris uses three main files to store user and group accounts locally on a system (each of these three files is documented in detail in this chapter):

- `/etc/passwd` file: The passwd file stores the user database file, with a record for each user account. There is a password field that contains an x as a placeholder.
- `/etc/shadow` file: The shadow file stores additional information about a user account as well as the encrypted password for each account. Access to this file is by the root account only.
- `/etc/group` file: The group file stores the group database file, with a record for each group account. Users associated with each group are shown, although users may be assigned a primary group in the passwd file.

In networked environments, Solaris stores account information in central databases managed by name services such as NIS+ and NIS. A short introduction to the interaction of local user and group accounts with network accounts will be presented in the section "User Account Commands" later in this chapter.

It has been traditional to create, modify, and delete user accounts, group accounts, and passwords using commands at the command line. Many if not most administrators still perform these functions using the commands described in this chapter. However, Solaris 8 provides graphical tools such as the AdminSuite 3 for administering local or remote user accounts and the Admintool (part of the standard distribution) for local account management in the CDE. You can use AdminTool to define users and group accounts as well as set their attributes on a local system. AdminSuite is used to work with user accounts stored on networks.

### The User Database

Solaris stores data concerning a user's security access in the `/etc/passwd` file. It uses the username field to match the data found in the `/etc/passwd` file to the `/etc/shadow` file. Although many programs access the `/etc/passwd` file, to protect passwords, only logins with root privileges can access the `/etc/shadow` file, and even then, the passwords that are stored in the `/etc/shadow` file are encrypted and hidden from view. In the sections that follow, the contents of these two very important system files are described.

#### The passwd File

Although its name suggests that the passwd file stores the actual passwords of individual users, this is no longer the case. Passwords are stored in the `/etc/shadow` file. Figure 11.1 shows an `/etc/passwd` file. Each user's information is stored in a record, which is the information contained between two line endings. Colon characters separate fields in each user's record. The adduser, usermod, and userdel commands are used to add, modify, and delete user accounts in the passwd file, respectively.

##### FIGURE 11.1
The /etc/passwd file

![](img/256e02a6afce528d264a8d911fa0ff20_443_0.png)

The seven fields in the `passwd` file store the following information:

- **Username** A username is the login name for a user account. Usernames should consist of from two to eight alphanumeric characters. The first character must be a letter, and at least one character must be a lowercase letter. No underscore or space characters are allowed in a username.
  - If you are using a name service such as NIS or NIS+, make sure that any username you create is different than any mail aliases used in your domain. If you create a duplicate username, mail may be delivered to the alias in place of the user. You also need to make sure that any account name you create is also not listed in the `/etc/mail/aliases` file, whether you use a name service or not.
- **Password placeholder** You always see an x in this field; the x is a placeholder for the user’s password. In past versions of Solaris, the encrypted password was placed in this field, and the `passwd` file retains this field for backward compatibility. Because many programs used the `passwd` file to determine permissions and needed to be able to access a readable file quickly, Solaris and other versions of Unix moved the encrypted password to the `/etc/shadow` file, which can be read only by users with root privileges.
- **User identification number** The UID number is used to assign file, directory, and process ownership. The UID number is a unique number that is assigned by Solaris to a user account when the account is created. UIDs can have a value of from 0 to 2,147,483,647, with some exceptions. The UIDs from 0 to 100 and from 60,000 to 65,535 are reserved for system use. In large networks, UIDs of 100 to 500 are reserved for daemons such as Web servers or database servers. For example, the anonymous FTP server is typically assigned either UID 10,000 or UID 30,000. Use UIDs in the range of from 0 to 60,000 to preserve backward compatibility with older versions of Solaris.
  - Solaris uses some of the UIDs for special purposes, the so-called built-in user accounts. The users of built-in user accounts are referred to as *pseudo users*. Among the processes taking UIDs are daemons, system maintenance programs, and other functions. Table 11.1 lists some of the system UID assignments.
  - **WARNING** Once you assign a UID to an account, be careful before you reassign it to another account. If you delete the account and don’t change settings such as printer access for that UID, any new user you assign to that UID will inherit the previous user’s settings as well as have access to any of the previous user’s files. It’s a good rule of thumb never to reuse a UID. With 60,000+ numbers to choose from, you will have plenty of numbers left over.
- **Group identification number** The GID number is used by Solaris to see if a user has group access to files, directories, and processes.
- **Comments** The comment field contains the full name of a user. The comment field is also known as the GCOS field and has been used to store comma-delimited information such as phone numbers, department names, and so on.
- **Home directory** The home directory of the user's account is listed in the sixth field.
- **User’s login shell** The seventh field lists the login shell that is called when the user logs in to Solaris. The three most common shells, the ones Solaris ships with, are the Bourne shell (`/bin/sh`), the Korn shell (`/bin/ksh`), and the C shell (`/bin/csh`). You may see other shells in this field if they were installed.

TABLE 11.1: SYSTEM UIDS

| UID | Description |
| :--- | :--- |
| 1–10 | Reserved for daemons and system maintenance pseudo users. |
| 0 | Reserved for root user or superuser. |
| 1 | Used by pseudo user daemon for system server processes. |
| 2 | Used by username bin for ownership of user-initiated programs. |
| 3 | Used by username sys for ownership of system configuration files. |
| 4 | Used by adm for ownership of system accounting logs and files. |
| 5 | Used by username uucp for the Unix-to-Unix Copy Program (UUCP). |
| 9 | Used by username nuucp for the Unix-to-Unix Copy Program (UUCP). |
| 11–99 | Reserved for daemons. |
| 71 | Used by username lp for the line printer (lp) process. |
| 100–60,000 | Assignable accounts for users. |
| 60,001 | Reserved for username nobody, an account with the minimum access privileges. |
| 60,002 | Reserved for username noaccess (analogous to nobody). |
| 60,003–2,147,483,647 | Assignable accounts for users. These numbers are not generally recommended for use. |
| 65,534 | Reserved for username nobody4, as was used in the SunOS 4.x system. Reserved for backward compatibility. |

![](img/256e02a6afce528d264a8d911fa0ff20_445_0.png)
