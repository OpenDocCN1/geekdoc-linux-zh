
# Samba
CHAPTER 16

hosts allow= overrides any hosts deny= options, which simply deny access to a host or subnet. allow hosts= is a synonym for hosts allow=, and deny hosts= is a synonym for hosts deny=

![](img/cbac72550c7126a22162e94d91a0c360_530_0.png)

## public= and guest ok= (S)

These two are synonyms, with guest ok= preferred in SWAT. The purpose of this option is to allow without a login on the server to access a share. This is a security compromise that sometimes makes sense on a printer. Care must be used to avoid the possibility of allowing a hostile exploit. For that reason the default is no.

## comment= (S) and server string= (G)

These are related in that they both provide human-readable strings to identify Samba resources in an SMB client's user interface. comment= describes a share, while server string= goes in the [global] section and describes the entire Samba server.

## domain logons= (G)

This defaults to no, but if set yes the Samba server is allowed to serve as a domain server for a Windows 95/98 workgroup. This is different from a Windows NT domain.

## encrypt passwords= and smb passwd file= (G)

These options are vital to serving Windows clients and are discussed extensively earlier in this chapter. Defaults are encrypt passwords=no and smb passwd file=/etc/smbpasswd.

## hosts equiv= (G)

This dangerous option points to a file containing hosts and users allowed to log in without password. This is obviously an extreme security risk. The default is none, and the best policy is to leave this option absent from smb.conf.

## interfaces= (G)

This becomes necessary when the server serves multiple subnets. The following is an example:

```
interfaces = 192.168.2.10/24 192.168.3.10/24
```

A /24 is a subnet mask. 24 represents 24 bits of mask, or 255.255.255.0. Thus, the example would serve subnets 192.168.2 and 192.168.3. Normal subnet notations with four dot-delimited numbers can also be used after the slash.

## load printers=(G)

This defaults to yes. A yes value loads all printers in printcap for Samba browsing.

## null passwords=(G)

This option defaults to no, meaning no user with a zero-length password on the server can log into Samba. Setting this to yes is an obvious security risk.

## password level and username level (G)

These determine the level of non-case-sensitivity of username and password comparisons. The default is 0, meaning the client-provided password or username is first compared sensitively against the copy on the server, and if the client username or password is converted to lowercase and compared to the copy on the server if that fails.

In troubleshooting Samba connection problems from Windows clients, it's often handy to set these high (such as 24), to see if that fixes the problem. Although this represents a minor security problem and also slows initial connection, it often solves the problem. After problems have been fixed, an attempt should be made to re-comment these two options to beef up security.

Connection problems from Windows clients also are often solved with the encrypt passwords= smb passwd file= options.

## security=(G)

Default is security=user, which enforces security by user and password. This is generally the best choice, with excellent security and predictability.

security=server security=domain are used primarily when password authentication is actually done by yet another machine. security=domain is used to join Samba to a NT domain. security=share offers less security and less predictable operation, but is sometimes a logical choice in less security-intense situations, such as if most of the client usernames do not exist on the server or if most are printers requiring passwords.

This topic is important, and is discussed further in documents /usr/doc/packages/samba/textdocs/security_level.txt and /usr/doc/packages/samba/textdocs/DOMAIN_MEMBER.txt.

## workgroup=(G)

This is the workgroup in which the server appears and controls the domain name used with the security=domain setting. The default is WORKGROUP, but you are encouraged to change this setting to your preferred workgroup name.

## config file=(G)

This is a method of specifying a Samba configuration file other than /etc/smb.conf. When Samba encounters this option, it reloads all parameters from the specified file.

## smb.conf by Section

We are now going to review the [global], [homes], and [printers] sections of the smb.conf to give you a better understanding of how these various parts work together as a whole.

## The [global] Section

The [global] section controls parameters for the entire SMB server. This section also provides values for the other sections.

```
[global]
# workgroup = NT-Domain-Name or Workgroup-Name
workgroup = MYGROUP
```

workgroup= specifies the workgroup. Try to keep it all uppercase, fewer than nine characters, and without spaces.

```
# server string is the equivalent of the NT Description field
server string = Samba Server
```

server string= specifies a human-readable string used to identify the server in the client's user interface. server string= goes in the [global] section. Note the similarity to the comment=option, which identifies individual shares in the client's user interface.

```
hosts allow = 192.168.1.0 192.168.2.127
```

The hosts allow= line restricts Samba access to certain subnets; a handy security measure. Multiple subnets are separated by spaces. Class C subnets have three numbers and three dots, class B two numbers and two dots, and Class A one number and one dot.

- # You wish to use password encryption.
# ENCRYPTION.txt, Win95.txt and WinNT.txt in the Samba documentation.
# Do not enable this option unless you read those documents

; encrypt passwords = yes
; smb passwd file = /etc/smbpasswd

## The [homes] Section

The [homes] section allows network clients to connect to a user's home directory on your server without having an explicit entry in the smb.conf file. When a service request is made, the Samba server searches the smb.conf file for the specific section corresponding to the service request. If the service is not found, Samba checks whether there is a [homes] section. If the [homes] exists, the Samba password is searched to find the home directory for the user making the request. Once this directory is found, the system shares it with the network:

```
[homes]
comment = Home Directories
browse = no
read only = no
preserve case = yes
short preserve case = yes
path = %h/sbtree
create mode = 0750
```

The comment entry is a human-readable share identification string to be displayed by the client/user interface. Note that comment= is similar to server string=, but the latter is only valid in the [global] section.

The browseable=no entry instructs the SMB client not to list the share in a browser (such as Windows Explorer). However, [homes] is a special case. The user share that it represents will be visible in the client even if [homes] contains browseable=no. If [homes] were to contain browseable=yes, a shared home would actually appear in the client.

The read only parameter controls whether a user can create and change files in the directory. The preserve case and short preserve case instruct the server to preserve the case of any files written to the server. This is important because Windows filenames are not case-sensitive, but Linux filenames are.

Note the path= entry. Because Samba is primarily a file server, %h is a macro indexing the user's home directory, while sbtree is a directory under the home directory. To implement this as a policy, the system administrator must, of course, create a subdirectory upon addition of each user.

# Samba
CHAPTER 16

The final entry sets the file permissions for any files created in the directory.

## The [printers] Section

There are two ways Samba can make printers available. One is to create a specific section with a print ok=yes line, a specific printer specified by a printer name=line, and possibly a list of valid users. The other way is to let the [printers] section do most of the work and list all printcap-defined printers to the client.

Note

This section mentions /etc/printcap, printcap, and printcap printers several times. /etc/printcap is a file defining all the system's printers. A printcap printer is a printer defined by name in /etc/printcap.

For printcap specifics, see the printcap command page.

The following lines allow use of all printcap-defined printers on SMB clients, although it's certainly not ideal in terms of security:

```
[printers]
path = /var/spool/samba
```

The simplest case of a dedicated print share follows:

```
[vals_lp]
print ok = yes
printer name = lp_mine
path = /home/everyone
```

In the dedicated print share, print ok=yes (or the printable=yes synonym) is necessary. It's also necessary to name the printer with the printer name=line. The intent of [printers] is accessibility to all users with valid IDs. The intent of a special printer is to restrict access to a user or group, implying that it would be a good idea to add a valid users= line to the dedicated print share. Beyond that, the [printers] section and dedicated print share function pretty much the same.

The [printers] section defines how printing services are controlled if no specific entries are found in the smb.conf file. As with the [homes] section, if no entry is found for a printing service, Samba uses the [printers] section (if it's present) to allow a user to connect to any printer defined in /etc/printcap:

```
[printers]
```
