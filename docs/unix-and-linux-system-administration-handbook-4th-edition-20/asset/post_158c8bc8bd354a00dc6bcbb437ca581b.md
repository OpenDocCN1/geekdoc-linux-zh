
## 6.7 EXERCISES

- **E6.1** What is a umask? Create a umask that would give no permissions to the group or the world.
- **E6.2** What is the difference between hard links and symbolic (soft) links? When is it appropriate to use one or the other?
- **E6.3** What steps would be needed on your system for a Windows NTFS partition to be automatically mounted from a local hard disk? What's the most appropriate mount point for such a partition according to your system's conventions and the conventions at your site?
- **E6.4** When installing a new system, it is important to set up the system volumes that each filesystem (/var, /usr, etc.) has adequate space for current and future needs. The Foobar Linux distribution uses the following defaults:

| Path | Size |
| :--- | :--- |
| / | 2GB |
| /var | 100MB |
| /boot | 100MB |
| <swap> | 2GB |
| /usr | remaining space |

What are some potential problems with this arrangement on a busy server box?
- **E6.5** Why is it a good idea to put partitions (such as /var, /home, and swap) on a separate drive from other data files and programs? What about /tmp? Give specific reasons for each of the filesystems.
- **E6.6** Write a script that finds all the hard links on a filesystem.
- **E6.7** Give commands to accomplish the following tasks:
    - a) Set the permissions on the file README to read/write for the owner and read for everyone.
    - b) Turn on a file's setuid without changing (or knowing) the permissions.
    - c) List the contents of the current directory, sorting by modification time and the most recently modified file.
    - d) Change the group of a file called shared from “user” to “friends”.
- **E6.8** By convention, the /tmp directory is available to all users who care to create files. What prevents one user from reading or deleting another's temporary files? What's to prevent a disgruntled user from filling up /tmp with junk files? What would be the consequences of such an attack?

## 7 Adding New Users

Adding and removing users is a routine chore on most systems. These tasks are simple, but they are also boring; most administrators tweak the tools provided with the operating system to automate the process and then delegate the actual work to an assistant or operator.

These days we are seeing a resurgence of centralized servers with login accounts for hundreds of people in addition to the distributed server with as few as two users. Administrators need a thorough understanding of the user account system in order to manage network services and to configure accounts appropriately for the local computing environment. Often, account management on servers is just one piece of the account-provisioning puzzle for an entire enterprise.

Today's enterprise environments need not just a tool for adding users to specific machines, but also a tool for managing users and their myriad accounts and passwords across the entire computing environment—an identity management system such as Microsoft's Active Directory, OpenLDAP, and Fedora Directory Server are in widespread use, so we'll detail how these systems affect account management tasks. (As usual, myopic Microsoft does not play well with others unless you let Active Directory be in charge. Sigh.)

## Adding New Users

Some sites' needs may exceed the capabilities of even these systems. We do not cover the commercial identity management systems but will point you to a few candidates. They are probably the right solution for a very large site, especially where compliance with regulatory regimes such as HIPAA or Sarban-Oxley (in the United States) is required. See page 203.

Account hygiene is a key determinant of system security. Frequently used accounts are prime targets for attackers, as accounts with easily guessed passwords. If you use your system's automated tools to add and remove users, it is important to understand the changes the tools are making. For this reason, we start our discussion of account management with the flat files you must modify to add users to a single machine.

We examine the automated tools distributed with each of our example systems and the configuration files that control their behavior. Surprisingly (or perhaps confusingly), the user management tools are called **useradd**, **usedel**, and **usermod** on each of our example systems, even though the programs are not necessarily the same. (In addition, AI achieves this naming conformity with its native **mkuser**, **rmuser**, and **chaser** tools with driver scripts.)

The default useradd tool is actually quite good and should be sufficient for most sites' needs. Unfortunately, **usedel** is not always thorough as we would like.

Most systems also use simple GUI tools for adding and removing users, although these tools don't implement a batch mode or advanced localization. They are straightforward enough that we don't think it's helpful to review their operation in detail, but we'll point you to the vendors' documentation for each tool.

In this chapter, we focus specifically on adding and removing users. Many topics associated with user management actually live in other chapters and are only referenced here. For example:

- Pluggable authentication modules (PAM) for password encryption and the enforcement of strong passwords are covered in Chapter 22, *Security*. See the material on page 908.
- Password vaults for managing passwords are described in Chapter 4, *Access Control and Rootly Powers* (see page 117).
- Directory services as NIS and OpenLDAP are outlined in Chapter 19, *Sharing System Files*, starting on page 728. Some comments on Active Directory can also be found in Chapter 30, *Cooperating with Windows*, on page 1154.
- Finally, policy and regulatory issues are major topics of Chapter 23, *Management, Policy, and Politics*.

That said, the next three sections present an overview of the primary files involved in user management.

### 7.1 THE /ETC/PASSWD FILE

The /etc/passwd file is a list of users recognized by the system. It can be extended or replaced by a directory service, so it is complete and authoritative only on standalone systems.

The system controls /etc/passwd at login time to determine a user' UID and home directory, among other things. Each line in the file represents one user and contains seven fields separated by colons:

- Login name
- Encrypted password placeholder (see page 179)
- UID (user ID) number
- Default GID (group) ID number
- "GECOS" information: full name, office, extension, home phone
- Login shell

For example, the following lines are all valid /etc/passwd entries:

```
root:x:0:0:/bin/sh
jlim:x:100:0:Jime Lane,ECOT8-3;:/staff/j:/bin/sh
dotty:x:101:20:/home/dotted:/bin/sh
```

Encrypted passwords used in the second field, but that is no longer safe; with fast hardware, they can be cracked (decrypted) in minutes. All versions of UNIX and Linux now hide the encrypted passwords by placing them in a separate file that is not world-readable. The passwd file contains an x in the encrypted password field on Linux, Solaris, and HP-UX an a * on AIX. (On Unix systems, * as a placeholder disables the account.)

The actual encrypted passwords are stored in /etc/shadow on Linux, Solaris, and HP-UX in /etc/security/passwd on AIX. The formats vary.

If accounts are shared through a directory service such as NIS or LDAP, you might see entries in the passwd file that begin with + or -. These entries tell the system how to integrate the directory service's data with the contents of /etc/passwd. This integration can also be set up in /etc/nsswitch.conf file (/etc/ncontrol on AIX).

The following sections discuss the /etc/passwd fields in more detail.

# Login name

Login names (also known as usernames) must be unique, and depending on the operating system, may have length and character set restrictions. Table 7.1 shows the rules for our example systems. Login names can never contain colons or newlines because these characters are used as field separators and entry separators.
