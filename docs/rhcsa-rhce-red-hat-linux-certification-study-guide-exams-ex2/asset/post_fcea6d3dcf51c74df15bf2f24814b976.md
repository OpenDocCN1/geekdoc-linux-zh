
In other words, the umask value of 002 is given to users with UIDs of 200 and above. A umask value of 022 is given to users with UID of 199 and below.

- 4. Change the first umask statement to exclude all permissions for groups and others. In other words, replace the umask of 002 with a umask of 077.
- 5. Save and exit the file.
- 6. Log in as a regular nonprivileged user. Use the touch command to make a new empty file. Use ls -l to verify the permissions on that file.
- 7. Log in as root. Again, use the touch command to make a new empty file and use ls -l to verify the permissions on that new file. You have just changed the default umask for all regular users. While this is an excellent option for security, it would affect the steps used in other chapters. Therefore, one final step is important:
- 8. Restore the original version of /etc/bashrc from the backup created in Step 1.

## Shell Configuration Files in User Home Directories

As described earlier, each user gets a copy of all files from the /etc/skel directory. Most of them are hidden, revealed only with commands like ls -a. As users start working with their accounts, more configuration files may be added to their home directories. Some users may work primarily with the default bash shell, while others include additional configuration in configuration files related to their GUI desktop environments such as GNOME.

The default Linux shell is bash, and until recently, it was specifically included as the only shell described in associated Red Hat exam objectives. While bash is no longer specifically included in the objectives, it is the default for RHEL 6.

## Login, Logout, and User Switching

While this may seem like a "no-brainer" topic for Linux users with even a couple of days of experience, one of the RHCSA topics is to "Log in and switch users in multi-user runlevels." It includes concepts from different chapters. As discussed in Chapter 5, the multi-user runlevels are 2, 3, 4, and 5. Command-line logins are available at all of these runlevels. For the first RHEL 6 release, command-line logins appear as follows:

```
Red Hat Enterprise Linux Server release 6.0 (Santiago)
Kernel 2.6.32-71.el6.x86_64 on an x86_64

server1 login:
```

The hostname, as well as the versions of RHEL 6 and the kernel, will vary. But that's irrelevant to actual logins; all you need to do is type in a username, press ENTER, and type in a password when prompted.

Logouts from the command line are even simpler; the exit, logout, and CTRL-D commands all perform logouts from the command line. Of course, once you've logged out from a system, the login prompt just shown will appear.

As discussed earlier in this chapter, there's a different way to switch user accounts. For example, to switch from the current account to user donna's account, run the following command:

```
$ su - donna
```

The same exit, logout, and CTRL-D commands can be used to exit from user donna's account.

Of course, users can log in to and log out of the GUI. While the steps vary a bit by desktop environment, they are as simple as the steps required to log in to and log out of any other operating system.

## CERTIFICATION OBJECTIVE 8.04

## Users and Network Authentication

By default, access to a Linux computer requires a valid username and password. One problem with a large network of Linux systems is that without some central database, each user would require an account on every Linux computer.

Several services are available that can be used as a central authentication database.

> exam watch
> 
> In the RHCSA objectives, the only requirement is to be able to connect a client to a LDAP server. You're not required to actually create an LDAP server. In addition, NIS is no longer part of the objectives.

One now-obsolete option for the Red Hat exams is the Network Information Service (NIS). In contrast, the Lightweight Directory Access Protocol (LDAP) is specifically listed in the RHCSA objectives. Other services are available, namely Samba, which can be configured to support access by Linux systems and users to networks governed by a Microsoft database. In any of these cases, one database of passwords and usernames exists for a network.

The focus of this section is LDAP as a client. You'll configure an RHEL 6 system as an LDAP client, set up authentication in the name service switch file, and repeat the process with Red Hat network authentication tools. First, I'll show you how you can configure LDAP clients using the command line interface and then use the Red Hat Authentication Configuration tool to repeat the process. So you'll know two methods for configuring LDAP clients.

In contrast to NIS, LDAP services can be configured on a variety of platforms. Of course, LDAP servers can be configured on RHEL 6, but they are not part of the current RHCSA or RHCE exam objectives. LDAP authentication databases can even be configured on Microsoft-based Active Directory (AD) services.

> *LDAP directory services and authentication is the focus of Red Hat's RH423 course. While Red Hat allows students with "equivalent experience" to take RH423, the RHCE is an acceptable prerequisite. So you're not expected to know LDAP servers for the RHCSA exam. If you want to set up a simplified LDAP server, explore the FreeIPA (Identity, Policy, and Audit) project at www.freeipa.org.*

## LDAP Client Configuration

To configure a RHEL computer as an LDAP client, you'll need the openldap-clients, openldap, and nss-pam-ldapd RPM packages. The openldap-clients and nss-pam-ldapd RPMs are both optional parts of the Directory Client package group. The openldap package, as a mandatory part of the Server package group, should be installed by default on the RHEL 6 systems for this book.

To configure an LDAP client, you'll need to configure various LDAP configuration files, namely /etc/pam_ldap.conf and /etc/openldap/ldap.conf. While the files can get quite complex, you don't have to reconfigure a lot just to set up an LDAP client.

### /etc/pam_ldap.conf

The default version of the /etc/pam_ldap.conf file includes a number of different commands and comments. Standard changes required to set up a basic LDAP client are based on several directives shown in Table 8-10. Encryption-related directives in this file may be associated with both the Secure Sockets Layer (SSL), and its successor, Transport Layer Security (TLS). If TLS is shown, the SSL directives work with them.

### TABLE 8-10

Client Configuration Parameters in /etc/pam_ldap.conf

| Directive | Description |
|---|---|
| host 127.0.0.1 | Specifies the IP address for the LDAP server. This command assumes the LDAP server is on the local computer. Should be changed to the actual IP address of the LDAP server. |
| base dc=example,dc=com | Sets the default base distinguished name, in this case, example.com. Should be changed to the domain of the network that is being served. |
| ssl start_tls | Required if TLS support is used to encrypt passwords that are sent to the LDAP server. |
| pam_password | Supports encryption schemes for passwords; options include crypt, nds (Novell Directory Services), and ad (Active Directory). |
| nss_initgroups ignoreusers root, ldap | Assumes no supplemental groups in the LDAP directory server. |

As suggested by the name of the file, the pam_ldap.conf file applies Pluggable Authentication Modules to LDAP authentication. It is almost identical to the /etc/ldap.conf file from RHEL 5; the differences do not affect the successful configuration of an LDAP client.

Related directives are included at the end of the file; they may include the following. First, the Uniform Resource Identifier, as specified by the uri, should redirect the client to the actual address of the LDAP server.

```
uri ldap://127.0.0.1/
```

If secure communication is used, you may change ldap to ldaps; if you're also configuring the LDAP server, that corresponds to TCP/IP ports 389 and 636, respectively. An LDAP server won't work if a firewall blocks these ports (unless they are otherwise reassigned). Of course, if secure communication is being used to LDAP, you'd want to change this to ssl yes:

```
ssl no
```

Of course, to enable secure connections, LDAP needs access to appropriate certificates. While TLS is the successor to SSL, it's commonly used in concert with SSL directives. The following directive specifies the directory with those certificates:

```
tls_cacertdir /etc/openldap/cacerts
```
