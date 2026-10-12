
# SESSION 29

![](img/5fe8f856723cde0b366f73584b9e64b8_314_0.png)

# Maintaining System Security

**Session Checklist**

- Establishing a security policy
- Securing your system
- Monitoring system security

![](img/5fe8f856723cde0b366f73584b9e64b8_314_1.png)

As a system administrator, you have to worry about your Linux system's security. For a stand-alone system or a system used in an isolated local area network (LAN), you must ensure that a user does not intentionally or inadvertently modify, delete, or destroy system files. If your Linux system is connected to the Internet, you must also secure the system from unwanted accesses. Intruders, also known as *crackers*, typically impersonate a user, steal or destroy information, and even deny you access to your own system (known as *denial of service*). This session only briefly covers some key aspects of securing your Linux system. As you'll see, Red Hat Linux already includes the tools you need to maintain system security.

> To learn more about Linux security, consult the *Linux Security HOWTO* at http://metalab.unc.edu/pub/linux/docs/HOWTO/Security-HOWTO. Another good resource is the *Linux Administrator’s Security Guide*, which you can read online at http://www.securityportal.com/lasg.

## Establishing a Security Policy

The first step in securing your Linux system is to set up a security policy. A *security policy* establishes the principles and rules that determine what you enable users (as well as visitors over the Internet) to do on the Linux system. The level of security depends on how you use the Linux system and how much is at risk if someone gains unauthorized access to your system.

If you are a system administrator for Linux systems at an organization of any sort, you probably want to involve the management as well as the users in setting up the security policy. Obviously, you cannot create such an imposing policy that no one can do any work on the system. On the other hand, if the users are creating or using data that's valuable to the organization, you have to set up a policy that aims to protect the data from disclosure to outsiders. In other words, the security policy should strike a balance between the users' needs and the necessity of protecting the system.

For a stand-alone Linux system or a home system that you occasionally connect to the Internet, the security policy can be just a listing of the Internet services that you want to run on the system and the user accounts you plan to set up on the system. For any larger organization, you probably have one or more Linux systems on a LAN connected to the Internet, preferably through a *firewall*, which is a device that controls the flow of Internet Protocol (IP) packets between the LAN and the Internet. These days, with the widening availability of broadband Internet access for home users (typically through DSL or cable service), home users should also consider using a firewall. In these cases, the security policy typically addresses the following areas:

- **Authentication:** Who gets access to the system? What is the minimum length and complexity of passwords? How often must you change passwords? How long can a user be idle before that user is logged out automatically?
- **Authorization:** What can different classes of users do on the system? Who can have the root password?
- **Data Protection:** What data has to be protected? Who has access to the data?
- **Internet Access:** What are the restrictions on users (from the LAN) accessing the Internet? What Internet services (such as access to the Web, Internet Relay Chat (IRC), and so on) can the users access? Are incoming e-mails and attachments scanned for viruses? Is there a network firewall?
- **Internet Services:** What Internet services are allowed on each Linux system? Are there any file servers? Mail servers? Web servers? What services run on each type of server? What services, if any, run on Linux systems used as desktop workstations?
- **Responsibilities:** Who is responsible for maintaining security? Who monitors log files and any audit trails for signs of unauthorized access? If any security breach occurs, who must be informed?
- **Security Audits:** What tests whether the security is adequate? How often is the security tested? How are problems found during security testing handled?

The remainder of this session shows you some of the ways in which you can enhance and maintain the security of your Red Hat Linux system.

## Securing the System

Once you have a security policy defined, you can proceed to secure the system according to the policy. The exact steps depend on what you want to do with the system, whether it is a server or a workstation, and how many users must access the system. The general steps for securing the system and maintaining the security are as follows:

- Select only those package groups that you need for your system when installing Red Hat Linux. Do not install any unnecessary software. For example, if your system is a workstation, you do not need to install most of the server packages, such as the Web server, news server, e-mail server, and so on.
- Create initial user accounts and make sure that all passwords are strong ones that password-cracking programs cannot guess. As you will learn in the next section, “Securing Passwords,” Red Hat Linux includes the tools to enforce strong passwords.
- Enable only those Internet services that you need on a system. In particular, do not enable services that are not properly configured. Later in this session, in the section titled “Securing Internet Services,” you learn about enabling and disabling Internet services.
- Check various log files periodically for signs of any break-ins or attempted break-ins. These log files are in the /var/log directory of your system.
- Check security news by regularly visiting and installing updates from Red Hat once a fix becomes available.

## Securing Passwords

Historically, UNIX passwords were stored in the /etc/passwd file, which any user could read. For example, a typical old-style /etc/passwd file entry for the root user looks like this:

```
root:t6T7NWDLK1K8u:0:0:root:/root:/bin/bash
```

The fields are separated by colons (:) and the second field contains the password in encrypted form. To check if a password is valid, the login program encrypts the plain-text password entered by the user and compares it with the contents of the /etc/passwd file. If there is a match, the user is allowed to log in.

Password-cracking programs work just like the login program except that these programs pick one word at a time from a dictionary, encrypt the word, and compare the encrypted word with the encrypted passwords in the /etc/passwd file for a match. To crack the password, the intruder needs the /etc/passwd file. Often, crackers use weaknesses of various Internet servers (such as mail and FTP) to get a copy of the /etc/passwd file.

Recently, several improvements have been made to UNIX passwords to make them more secure. These include shadow passwords and pluggable authentication modules, described in the next two sections.

![](img/5fe8f856723cde0b366f73584b9e64b8_316_0.png)

![](img/5fe8f856723cde0b366f73584b9e64b8_317_0.png)

### Shadow Passwords

Instead of storing the passwords in the /etc/passwd file, which any user can read, passwords are now stored in a shadow password file. On Red Hat Linux, the shadow passwords are in the /etc/shadow file. Only the super user (root) can read this file. For example, here is the entry for root in the new-style /etc/passwd file:

```
root:x:0:0:root:/root:/bin/bash
```

As you can see, the second field contains an x instead of an encrypted password. The encrypted password is now stored in the /etc/shadow file where the entry for root is like this:

```
root:$1$AAAAAr/ybW5tE8HbzUp9cf0olPf810S0:1077:0:99999:7:-1:13454340356
```

The format of the /etc/shadow entry controls when the password expires. You do not need to interpret or change these entries in the /etc/shadow file. Instead, you should use the chage command to change the password expiration information. For starters, you can check a user's password expiration information by using the chage command with the -l option as follows (in this case, you have to be logged in as root):

```
chage -l root
   Minimum: 0 
   Maximum: 99999 
   Warning: 7 
   Last Change: -1 
   Password Expires: Never 
   Password Inactive: Never 
   Account Expires: Never
```

In this case, the output shows various expiration information: you can change the root password any time—that's what zero minimum time means. The root password lasts for 99,999 days, and the root user gets a warning seven days before the password expires.

If you want to ensure that the password changes every 90 days, you can use chage's -M option to set the maximum number of days the password stays valid. For example, to make sure that user kwall is prompted to change the password in 90 days, you would log in as root and type the following command:

```
chage -M 90 kwall
```

You can do this for each user account to ensure that all passwords expire and all users must pick new passwords.

### Pluggable Authentication Modules

In addition to improving the password file's security by using the shadow passwords, Red Hat Linux also enhances the actual encryption of the passwords stored in the /etc/shadow file. Password encryption is now done using the MD5 message-digest algorithm to convert
