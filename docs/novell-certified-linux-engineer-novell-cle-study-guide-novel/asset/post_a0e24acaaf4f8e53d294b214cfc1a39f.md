
## Configuring the hosts File

The next task you need to complete is configuring your system's **hosts** file. Depending on the distribution and version, sometimes the hosts file is written during installation of the operating system in such a way that NNLS is unable to resolve the hostname correctly.

Basically what happens is that an alias for the server hostname is added to the loopback address. For example, it may read something to the effect of

```
127.0.0.1 CLE-1 localhost.localdomain localhost
```

or

```
127.0.0.1 localhost.localdomain localhost CLE-1
```

Check your hosts file, located in /etc, and verify that the hostname of the server doesn't appear in the loopback address line. If you identify this problem in your hosts file, use vi to edit out the server hostname in the loopback address line.

When you're done, it should read as follows:

```
127.0.0.1 localhost.localdomain localhost
```

You should also make sure there is a record in your hosts file that reads as follows:

```
Server_IP_Address   Server_DNS_Name   Server_Hostname (alias)
```

Here's an example:

```
192.168.1.35    CLE1.CLE.com    CLE1
```

When you're done, your hosts file should appear similar to that shown in Figure 5.13.

Once this is done, the next thing you need to do is establish a connection to the Internet.

## Establishing an Active Internet Connection

To install NNLS, you need to have an active Internet connection established prior to starting the installation process. NNLS includes a component called Red Carpet that automatically updates NNLS products (we'll talk a little more about Red Carpet later in this chapter). The Red Carpet daemon must detect an active Internet connection during installation in order for it to configure its network settings.

![](img/c7771e8540507f2b00c088c7a411b57b_171_0.png)

If you don't have an active connection, Red Carpet will still install, but its configuration will not be accurate. Unfortunately, you can't manually edit the configuration. If you install without an active Internet connection, you'll have to uninstall and then reinstall the Red Carpet component of NNLS at a later time when an Internet connection is available.

Once your Internet connection is established, the next thing you need to do is gather information required for installing NNLS.

### Gathering Data Required for Installation

During the installation of NNLS, you will be prompted to provide many pieces of data that will be used to configure the NNLS components; these include usernames and passwords, IP addresses, and various other configuration parameters. Before you start the installation process, it is wise to gather all this information beforehand.

If you do not do this, your installation may have to wait patiently for you while you search for the value of a requested parameter. You should prepare the information shown in Table 5.1.

## NNLS Installation Data

| NNLS COMPONENT | DATA REQUIRED | DESCRIPTION |
| :--- | :--- | :--- |
| **eDirectory** | NICI file location and filename | This is the path and filename of the NICI file you downloaded. You should insert the floppy disk containing this file in your server's floppy drive and mount it to the /media/floppy directory before beginning installation. The NNLS installation script is coded to look in this directory for the file. |
| | Install a new tree or into an existing tree? | You must specify whether you are installing a new eDirectory tree or into an existing tree. |
| | Tree name | The data you provide here is dependent on whether you are installing a new tree or into an existing tree. If you're installing a new eDirectory tree, you must determine a unique name. If you're installing into an existing tree, you must supply its name at this prompt. |
| | Existing server IP address | If you're installing into an existing tree, you need to know the IP address of the server (NetWare, Linux, or Windows) that already resides in the tree. If you're installing into a new tree, you won't be prompted to provide this information. |
| | Admin name with context | Again, the value you supply here is dependent on whether you are installing into a new or an existing eDirectory tree. If you're installing into an existing eDirectory tree, you must provide the typeful name of the tree's admin user (for example, **cn=admin.o=CLE**).<br><br>If you're installing a new tree, you must also provide this information. This information will be used to create the tree's admin user account. |
| | Admin password | This is the password for your admin user. If you are installing into a new tree, the value you provide will be assigned as the admin's password.<br><br>If you're installing into an existing tree, you must provide the password of the existing admin user. |
| | Server context | This parameter specifies where you want your server to reside in the eDirectory tree. If you're installing into a new tree, the context will be automatically created for you. If you're installing into an existing tree, you should use iManager from another server to create the context beforehand. The installation script won't create the context in the tree for you. |
| | LDAP port | This parameter represents the TCP/IP port your LDAP server will use. The default value is **389**. Unless you have a conflict, you should stick with the default. |
| | Secure LDAP port | This parameter represents the secure port the LDAP server will use. The default value is **636**. Again, you should stick with the default value. |
| | HTTP port | This parameter represents the port used by iMonitor. The default is **81**. |
| | Secure HTTP port | This parameter represents the secure port used by iMonitor. The default is **444**. |
| **Linux User Management** | LDAP server IP address | This is the IP address of the eDirectory server running LDAP that LUM will use to authenticate. This could be any server in your tree. In this book, we're going to use the LDAP service on the same server where LUM and eDirectory will be installed. |
| | Admin name and context | This parameter is the admin user for your tree. It's the same user as you specified during the eDirectory portion of the installation.<br><br>You must provide the typeful name of your admin user (for example, **cn=admin.0=CLE**). |
| | Admin password | This parameter is the password assigned to your admin user object. |
| | LDAP port | This parameter specifies which TCP/IP port will be used by LUM to communicate with the LDAP server. The default value is **389**. If you configured your LDAP server to use a different port number, be sure you enter it here. |
| | Secure LDAP port | This parameter specifies the secure TCP/IP port to be used to communicate with the LDAP server in your eDirectory tree. The default value is **636**. If you've configured your LDAP server to use a different secure port number, be sure you enter it here. |
| | Partition root | This parameter specifies the top most context where the LDAP server will begin searching for eDirectory objects. <br>You must supply the typeful name of the container, such as **o=CLE**. |
| | Workstation context | During the installation of LUM, a LUM Workstation object will be created in your tree. <br>This parameter specifies where you want this object created. <br>You must use a typeful name, such as **o=CLE**. <br>This context must be the same as or within the partition root context you specified previously. |
| | PAM services that will use eDirectory | You must decide which services you want to use eDirectory for authentication. You can choose from ftp, su, sshd, rsh, login, rlogin, and passwd. |
| **DirXML** | Tree name | This parameter specifies the name of the tree where DirXML will be installed. In this book, we will use the eDirectory tree we specified previously. |
| | Admin name and context | This parameter specifies the admin user for the tree specified earlier. You must use a typeful name such as **cn=admin.o=CLE**. |
