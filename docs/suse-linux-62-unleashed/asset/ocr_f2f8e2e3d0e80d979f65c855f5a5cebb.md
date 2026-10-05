# workgroup=(G)

This is the workgroup in which the server appears and controls the domain name used with the security=domain setting. The default is WORKGROUP, but you are encouraged to change this setting to your preferred workgroup name.

# config file=(G)

This is a method of specifying a Samba configuration file other than /etc/smb.conf. When Samba encounters this option, it reloads all parameters from the specified file.

# smb.conf by Section

We are now going to review the [global], [homes], and [printers] sections of the smb.conf to give you a better understanding of how these various parts of work together a whole.

# The [global] Section

The [global] section controls parameters for the entire SMB server. This section also provides values for the other sections.

[global]

```
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
hosts allow = 192.168.1. 192.168.2.127.
```

The hosts allow= line restricts Samba access to certain subnets; a handy security measure. Multiple subnets are separated by spaces. Class C subnets have three numbers and three dots, class B two numbers and two dots, and Class A one number and one dot.

+   # You wish to use password encryption.
# ENCRYPTION.txt, Win95.txt and WinNT.txt in the Samba documentation.
# Do not enable this option unless you read those documents