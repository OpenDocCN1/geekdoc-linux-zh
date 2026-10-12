> Note
> 
> Samba will only work on a properly functioning network. To avoid frustration, it is a good idea to first ensure that the client and server systems you will be working on can communicate with each other. Some simple tests using ping and other network tools now will save you hours of hair pulling later.

# The [global] Section

The [global] section specifies parameters for the entire SMB server. This section also provides default values for the other sections.

The first two parameters shown here specify the workgroup to which your computer belongs and how the server will identify itself when queried by clients.

In addition to specifying the workgroup to which your machine belongs, it also specifies the domain name used when the parameter security = domain is specified. The name specified for the workgroup parameter should be limited to no more than nine characters, should have no spaces, and should be entered in all uppercase characters.

The server string parameter is a human-readable string that identifies your server when queried by SMB clients.

```
[global]
    workgroup = MYGROUP
    server string = Samba Server
```

In the default configuration file that comes with Red Hat, the hosts allow line is commented out. If you uncomment this line, access to the Samba server will be restricted to the specified hosts or networks. In the following example, access is limited to the networks 192.168.1.0/24, 192.168.2.0/24, and to localhost. Multiple networks are separated by spaces and a shorthand syntax is allowed. Class C subnets have three numbers and three dots, class B two numbers and two dots, and class A one number and one dot.

```
hosts allow = 192.168.1. 192.168.2. 127.
```

The next few parameters have to do with printing. The default setting in the smb.conf file that is included with your Red Hat Linux system will make available all of the printers defined in /etc/printcap as shared resources to SMB clients on the network. The printing parameter should not be required on Red Hat Linux servers.

```
# if you want to automatically load your printer list rather
# than setting them up individually then you'll need this
```