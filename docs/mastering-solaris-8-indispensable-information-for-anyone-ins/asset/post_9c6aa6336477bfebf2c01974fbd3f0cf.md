
This page intentionally left blank

![](img/256e02a6afce528d264a8d911fa0ff20_311_0.png)

## CHAPTER 8

## Security

**FEATURING:**

- **Passwords and permissions** 292
- **Encryption** 303
- **E-mail security** 305
- **Firewalls** 311
- **Remote access security** 315
- **Login security** 320
- **Virus es** 320

No computer system in today's world is absolutely secure. If there are dial-in lines or if there is public access to terminals and the Internet, there are bound to be security breaches. This chapter will cover the main security issues of the day. It is impossible to cover each one in minute detail simply because every day new security issues crop up with alarming regularity. You will learn, however, to keep security a top priority when using Solaris 8.

Simple methods of establishing permissions, encrypting passwords, and restricting superstar privileges can make for a safer computing environment. How to secure your host and still get information to users, particularly those using remote access, will be discussed. E-mail security and Internet security are of paramount importance because most viruses and worms enter through those mediums. Hackers are quick to spot a weakness in a system and will use it to their advantage. How to be vigilant in spotting weaknesses will be a major point of the chapter. Physical considerations will also be discussed.

### Permissions and Passwords

Security on Solaris 8 needs to be addressed on several different levels. A system connected to a network or with dial-in lines can never be completely secure. A typical user has to consider directories, login names, and passwords. A system administrator or superuser has the potential to create a quagmire if care is not taken in setting up a network and directories, handing out passwords and permissions, and dealing with the Internet. The superuser's password should be kept confidential at all times. If you are a superuser, never let anyone other than a supervisor know your password—and change it frequently.

Ordinary user passwords should also be changed frequently, and the system administrator should keep an up-to-date log of all changes. When choosing passwords, encourage users to mix cases and to use numbers as well as letters. Bear in mind that there are several programs that can crack passwords quite easily. These programs work by repeatedly encrypting words from dictionaries, names, phrases, and other sources. If the encrypted password matches the output of the program, then the program has found the password. Both crack and cops are programs that can detect passwords.

Make certain that no one except the superuser can write to files that are owned by root, which will be run in the setuid (set user ID) mode. It is a good practice to set the -nosuid flag to mount, which will cause the system to treat setuid programs on those file systems as regular programs. Add this option to the flags section in the vfs tab file.

Group write permissions lower security for your files, so delete them out with caution. A free utility named fix-modes can be used to set all directories to more reasonable permissions. If you run this program, it will ask if you want to reset permissions.

Answer no to leave permissions in the more secure mode. If the /etc directory on your computer is writable by group, you will need to run `fix-modes`.

It is necessary to review your own security requirements frequently. The larger the site, the more frequent the reviews should be. There are many types of auditing mechanisms available. They are worth their weight in gold. External auditors are another option. They must have excellent references and credentials, however. Use a firewall if possible. It is one more layer of security on the Internet. The more you layer your security measures, the more difficult you make it for those with malicious intent. The risk assessment you provide for your site should clearly describe known vulnerabilities. Others may surface as time goes on. Imagine the worst-case scenario and have a disaster plan ready. Security policies will shift and change, as does technology itself, but the effort you put into it is more than worth it.

### File Permissions

Files are accessible by their owner, a member of the group to which the owner belongs, and other system users. A user can access a file by reading from it, writing to it, or executing it, depending upon the permissions granted by the owner. The owner of the file has control over which users have permission to access it and how they can access it. Solaris lets you give users access to the files you want to share and yet keeps your private files confidential. You may decide to let some users only read from your files and let others write to them. You may decide that neither option is desirable and choose to protect files or entire directories from being accessed in any form.

The only exception to the access permissions you allow is that anyone who knows the root password can have full access to all files by logging in as the superuser or root. The superuser is usually the person designated as the system administrator. The superuser must have access to certain systemwide powers that the typical user never sees. The superuser is the person in charge of overall security and the administrative tasks that keep the system running at optimal performance. That person will make decisions that affect the overall system. With that responsibility comes the power to change or control some of the restrictions that apply to the general user. The system administrator or superuser can search and create directories and files as well as remove files from any directory. They automatically have read, write, and execute permission on all files, no matter who the owner is. They can change a user's password without knowing the old password. They can halt the system at any time.

> **TIP** See the section "Access Permissions" in Chapter 5, "The File System," for a fuller discussion of the permissions the superuser has.

Because the superuser has the power to change so many things on the system, they also have the potential to do a great deal of harm if they make mistakes. A superuser should log in under their personal account name whenever they are doing routine file access tasks. This will cut down on the possibilities of erashing someone's work or inadvertently bringing down the system.

Standard Solaris file permissions are rather stringent and do not allow you to give file access to more than one group of people, nor do they allow you to give access to more than one person in a group. Access control lists (ACLs) were developed to give you control over who can access a file or directory on an individual basis. Using ACLs, you can give read, write, and execute access to as many users or groups as you wish. By default, an ACL gives everyone read access to a file. You can use the chmod utility to override the ACL permissions. This will be described more fully later.

> **TIP** The options used for granting permissions are r for read, w for writes, and x for execute.

To designate permissions for an individual, you can use the setfacl utility, shown in Figure 8.1. For example, to give read and write permission to a user named Paula, you can use the following syntax. The -m option designates a modification of an existing ACL or creates a new one if one does not already exist:

```
$ setfacl -m o:rw- myfile
```

![](img/256e02a6afce528d264a8d911fa0ff20_314_0.png)

ACLs may or may not work, depending upon your operating system, the network file system, and your remote host. ACLs work with the Network File System (NFS) on any Solaris system over 2.5. File security can be controlled by keeping a comprehensive list of ACL permissions. Be sure to record any changes made when using the *chmod* (change mode) utility. This utility will override ACL permissions if the *chmod* permissions are restrictive. For example, if you wanted to remove the write capability from the user Paula, you would use the following syntax:

```
$ setfacl -m u:paula:r myfile
```

The *chmod* utility is a powerful tool that changes the ways in which a file can be accessed. It uses an absolute or symbolic expression to specify the access mode. Tables 8.1 and 8.2 describe the absolute and symbolic expressions and their meanings when *chmod* is used to change access permissions.

### TABLE 8.1: SYMBOLIC CLASSES OF USERS

| Letter | Class | Meaning |
| :--- | :--- | :--- |
| u | user | Owner of the file |
| g | group | Group to which the owner belongs |
| o | others | All other users |
| a | all | Users and groups, replaces ugo |

### TABLE 8.2: SYMBOLIC OPERATORS

| Symbol | Meaning |
| :--- | :--- |
| + | Add permission for the user class. |
| - | Remove permission for the user class. |
| = | Set permission for the user; reset all other permissions for the user class. |
| r | Set read permission. |
| w | Set write permission. |
| x | Set execute permission. |
| \ | Enable mandatory locking. |
| s | Give the *setuid* or *setgid* *permission* to the owner of the file being executed or to the group the owner belongs to. |
| t | Set the sticky bit for the superuser only. |
| u | Match the permissions you are setting with the owners. |
| g | Match the permissions you are setting with the groups. |
| o | Match the permissions you are setting with the others. |
