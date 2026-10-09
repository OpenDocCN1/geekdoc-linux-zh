
The `/etc/passwd` file must be readable by all system users; it is how programs on the system get information about users, including their usernames and their home directories.

```bash
# ls -l /etc/passwd
-rw-r--r-- 1 root security 989 Apr 21 11:24 /etc/passwd
```

Though the password stored in the file is encrypted, the encryption is done via an algorithm that is easily cracked through the power of today's computers. AIX solves this problem by putting a placeholder character in the password field and storing the actual encrypted password in another file, readable only by root. This file is `/etc/security/passwd`.

```bash
# ls -l /etc/security/passwd
-rw------- 1 root security 508 Apr 21 11:24 /etc/security/passwd
```

The entries in this file for the preceding user accounts are

```text
root:
    password = m1lnz0ois8rdw
    lastupdate = 1015529254
    flags =

daemon:
    password = *
    ...

jdoe:
    password = LW94qd/8zKd.c
    lastupdate = 1019416125
    flags =

jane:
    password = QVvyzV3vkSwcY
    lastupdate = 1019416076
    flags = ADMCHG
```

There are several items of note in the preceding `/etc/security/passwd` excerpt:

- The password for the daemon account is a single asterisk. Since it is impossible for the encrypted value of any password to ever be a single asterisk, this account has a password that cannot be typed and can never be logged into (though root can su to the account).
- The flag ADMCHG is indicated for **jane**. This flag signifies that the most recent password change for the user **jane** was performed by root, and so **jane** will have to immediately enter a new password upon her next login. No one, including root, should ever know the unencrypted password of a user.

## Password Restrictions and Aging

Rarely are users inclined to use strong passwords, and they do not, in general, like to change their passwords more than once in a lifetime. These inclinations break the golden rules of account security. Fortunately, AIX provides a mechanism both for forcing users to change their password and for guiding them in the creation of strong passwords.

Table 23-1 presents the options that are available for enforcing the quality of user passwords, and the frequency with which they must be changed. These options can be set on a per-user basis when creating the account (SMIT FastPath mksuser) or at any point after, via the SMIT FastPath passwdattrs. They can also be set on a system-wide basis by editing the following fields in the /etc/security/user file. Table 23-1 shows a quick map of these user attributes to the SMIT options. Use SMIT Help for a complete description of each attribute.

| User Attributes | SMIT mksuser or passwdattrs Options |
|---|---|
| pwdwarntime | Days to warn user before password expires |
| pwdchecks | Password check methods |
| dictionary | Password dictionary files |
| histsize | Number of passwords before reuse |
| histexpire | Weeks before password reuse |
| maxexpired | Weeks between password expiration and lockout |
| maxage | Password maximum age |
| minage | Password minimum age |
| minlen | Password minimum length |
| minalpha | Password minimum alpha characters |
| minother | Password minimum other characters |
| maxrepeats | Password maximum repeated characters |
| mindiff | Password minimum different characters |

Table 23-1. User Attributes to SMIT Options Map

## ALTERNATE AUTHENTICATION METHODS

In addition to the standard local username/password combination, there exist a number of additional methods for authenticating users. Some of these methods are designed to improve the security of the login process, while other methods have as their goal to create a common authentication service for multiple systems spread out over different networks. AIX 5L provides several facilities for incorporating these alternative authentication schemes.

### Adding Custom Authentication Methods

The file /usr/lib/security/methods.cfg contains a block of text, commented out by default, that allows the system administrator to define an alternative authentication method:

```text
auth_method:
    program = /any/program
```

By specifying the path to a custom authentication program on the program line, the administrator enables that program to be used to validate the user. The most common use for this is NIS and DCE (already present in this file with AIX 5L). The following trivial example of an auth_method will request from the user a secret word. If the user enters the proper word, the program exits with a zero code. If the correct word is not entered, the program exits with a nonzero code.

```bash
#!/bin/ksh -
# trivial alternate auth_method

read secret "Who goes there? "
if [ $secret = "itisme" ]; then
  exit 0
else
  exit 1
fi
```

If the preceding program is saved as /usr/local/auth/whogoesthere, the following stanza should be added to /usr/lib/security/methods.cfg:

```text
whogoesthere:
   program = /usr/local/auth/whogoesthere
```

To use the new authentication method, it must be specified in the /etc/security/user file. If listed in the default stanza, the new method will apply to all users:

```text
default:
  auth1 = SYSTEM,whogoesthere
  auth2 = NONE
```

When the user **nancy** tries to log in, she will be presented with

```text
login: nancy
nancy's Password: <nancy's password>
Who goes there? Idontknow
3004-007 You entered an invalid login name or password.
```

If she then enters the proper secret word, the login process continues successfully.

### Kerberos

Kerberos is the name of a system designed by MIT and provided by IBM on the AIX 5L for POWER V5.1 Expansion Pack CD. Kerberos is a network authentication protocol, designed to provide strong authentication for client/server applications by using secret-key cryptography.

In a “Kerberized” environment, all systems and applications are assumed to be untrustworthy, except for the authentication server itself. Users obtain an authentication credential, called a *ticket*, from the authentication server, and that ticket is presented to other systems and applications. By using this system, the transmission of the user’s password over the network is minimized. A ticket is valid for a limited amount of time, and so even if it is captured and cracked, it contains no information that might be useful to someone trying to break into a system.

Kerberos requires a significant amount of setup before it is useful, and any application that wishes to use this authentication method must be written to support Kerberos. Kerberos is used extensively as the authentication method for the distributed computing environment (DCE) and the Andrew File System (AFS), as well as with IBM SP systems.

### Installing Kerberos

The implementation of Kerberos included with AIX 5L is called the “IBM Network Authentication Service”, and can be found on volume one of the AIX 5L for POWER V5.1 Expansion Pack. Each system that will be using Kerberos authentication must have the filesel **krb5.client.rte** installed. This filesel contains the Kerberos libraries and the user commands. On the system that has been designated as the Key Distribution Center (KDC), and on any “slave” KDCs, you must also install the **krb5.server.rte** filesel.

Note that the preceding filesels install the commands into `/usr/krb5/bin` and `/usr/krb5/sbin`. This is done to avoid the mixing and possible overwriting of commands already installed into the standard locations. These commands are also used in the DCE, but are incompatible implementations. Therefore, if you want to use the Network Authentication Service, ensure that the `/usr/krb5` directories are before `/usr/bin` and `/usr/sbin` in the *PATH*. Also, since Kerberos is highly dependent on the accurate time synchronization of all client and server systems, it is recommended that either *ntpd* or *timed* be used to ensure the proper clock settings.

### Configuring the Server

To configure the master KDC and Kerberos administration server, use the command `/usr/sbin/config.krb5`, with the following flags and arguments:

| Flag | Example Argument | Meaning |
|---|---|---|
| -s | none | Indicates that the configuration is for a server. |
| -d | domain.tld | Specifies the DNS domain containing this realm. |
| -r | REALM.DOMAIN.TLD | Specifies the name of the Kerberos realm being defined. |
| -S | hostname.domain.tld | Specifies the fully qualified domain name of the host being configured. Not currently supported. |

So, to set up the KDC and administration server on the host named **kdc.srv**, located in the domain `osborne.com`, for the realm BOOKS.OSBORNE.COM, you would execute this command:

```bash
# /usr/sbin/config.krb5 -S -d osborne.com \
         -r BOOKS.OSBORNE.COM
```

The most overlooked part of the Kerberos configuration is synchronizing the system clock. The following **setclock** command will be sufficient for this example but you may need to give this more thought for an enterprise solution:

```bash
# setclock timeserver.osborne.com
                              # Synchronize the system clock
```

### Configuring the Clients

Each client must be configured as a member of the Kerberos realm; this is also done with the **config.krb5** command, with the following flags and arguments:

| Flag | Example Argument | Meaning |
|---|---|---|
| -C | none | Indicates that the configuration is for a client. |
| -c | hostname.domain.tld | Specifies the fully qualified domain name for the realm's KDC. |
| -d | domain.tld | Specifies the DNS domain containing this realm. |
| -r | REALM.DOMAIN.TLD | Specifies the Kerberos realm. |
| -S | domain.tld | Specifies the fully qualified domain name for the realm's administration server. |

Thus, to configure a client to use the Kerberos realm defined in the previous section, execute this command:

```bash
# /usr/sbin/config.krb5 -C -c kdc.srv.osborne.com \
          -d osborne.com -r BOOKS.OSBORNE.COM \
          -S kdc.srv.osborne.com

# setclock timeserver.osborne.com
                              # Synchronize the system clock
```
