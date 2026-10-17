
### Unix users to deny (from /etc/ftpusers)

This is simply a list of users to deny access to the server to. This information is drawn from the `/etc/ftpusers` file. Adding to this list will add to the file. Note that if the next two sets of options are used to precisely control access to the FTP server (i.e., by blocking all access except for explicitly permitted users), then the `ftpusers` file becomes unnecessary.

### Unix users and UIDs to deny and Unix groups and GIDs to deny

Here you can enter any users or groups you would like to deny access to. These options configure the `deny-uid` and `deny-gid` directives.

### Unix users and UIDs not to deny and Unix groups and GIDs not to deny

These options can be used to negate the above options, if you chose to disallow all access from all users and groups. In this way, you could allow only explicitly configured users to access the server.

## Messages and Banners

WU-FTPD provides a simple mechanism for informing users of important information regarding the server, or files on the server. As in the previous section, this page configures certain aspects of the `ftpaccess` (Figure 9-3).

### Message files

This option configures the messages that will be displayed on login to the server. The default on many systems is to display a message contained in the file `welcome.msg` in the root FTP directory, if it exists, as soon as someone logs in. Also, when entering a directory the server will check for the existence of a file called `.message` in the new directory. If it exists, it will be displayed. Both of these are optional, and the names and actions can be changed at will. This option configures the `message` directive.

![](img/d84604054810a13cacfdac212ebee2f7_179_0.png)

Figure 9-3: Messages and Banners

### README files

Here, you can configure the behavior of the server with regard to README files. This, too, is set up by default on most systems. In this case, any file beginning `README` will be displayed to the user, both on logging into the server, and upon entering a new directory. This option configures the `readme` directive.

### Greeting level

Here you can select how much information about your server will be presented to the user. This can include the host name, the server version, and nothing. This can be a mild security risk, as the first step to cracking a box is to figure out what software and version is running. However, if the system is kept up to date (religiously), and the system is otherwise secured, this should not be an issue. Many paranoid types (and there’s no harm in being paranoid in a world where script kiddies are a dime a dozen) will disable all specific software and version information on all of their publicly accessible services. This option configures the `greeting` directive.

### Pre-login banner

Here you configure a banner that will be displayed before the user is prompted for a user name and password. This option can cause problems with non-compliant FTP client software. This option configures the `banner` directive.

### Hostname for messages

This will be the host name that is printed in the greeting message, and anytime the host name is inserted into a message for the user. This option configures the `hostname` directive.

### Owner's email address

Here you can set the email address of the servers maintainer. This will be presented as the contact email for this server. This option configures the `email` directive.

## Limits and Access Control

This page provides access to various resource limits, as well as provides system level access controls. If you wish to limit the system or network resources your server uses, this is the page to start with.

### Deny access from

Here you may deny access to the server from any number of IP addresses, and you can provide a filename of a text error message file to send the client in the event they have been denied access based on this rule. This option configures the `deny` directive.

### Concurrent user limits
