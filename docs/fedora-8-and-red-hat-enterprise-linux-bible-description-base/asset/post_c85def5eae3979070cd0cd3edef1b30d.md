
## Chapter 16: Setting Up a Proxy Server

### Debugging Squid
### Setting Up Proxy Clients
#### Configuring Firefox to use a proxy
#### Configuring Internet Explorer to use a proxy
#### Configuring other browsers to use a proxy

## Chapter 17: Setting Up a Print Server

### Common UNIX Printing Service
### Setting Up Printers
#### Using the Printer configuration window
#### Using Web-based CUPS administration
#### Configuring the CUPS server (cupsd.conf)
#### Configuring CUPS printer options
### Using Printing Commands
#### Using lpr to print
#### Listing status with lpc
#### Removing print jobs with lprm
### Configuring Print Servers
#### Configuring a shared CUPS printer
#### Configuring a shared Samba printer

## Chapter 18: Setting Up a File Server

### Goals of Setting Up a File Server
### Setting Up an NFS File Server
#### Sharing NFS file systems
#### Using NFS file systems
#### Unmounting NFS file systems
#### Other cool things to do with NFS
### Setting Up a Samba File Server
#### Getting and installing Samba
#### Configuring a simple Samba server
#### Configuring Samba with SWAT
#### Working with Samba files and commands
#### Setting Up Samba clients
#### Troubleshooting your Samba server

## Chapter 19: Setting Up a Mail Server

### Introducing SMTP and sendmail
#### Installing and Running sendmail
#### Starting sendmail
#### Other programs
#### Logging performed by sendmail
### Configuring sendmail
#### Getting a domain name
#### Configuring basic sendmail settings (sendmail.mc)
#### Defining outgoing mail access
#### Configuring virtual servers
#### Configuring virtual users
#### Adding user accounts
#### Starting sendmail and generating database files
#### Redirecting mail
### Introducing Postfix
### Stopping Spam with SpamAssassin
#### Using SpamAssassin
#### Setting up SpamAssassin on your mail server
#### Setting e-mail readers to filter spam
### Getting Mail from the Server (POP3 or IMAP)
#### Accessing mailboxes in Linux
#### Configuring IMAP and POP3 with dovecot
### Getting Mail from Your Browser with SquirrelMail
### Administering a Mailing List with mailman

## Chapter 20: Setting Up an FTP Server

### Understanding FTP Servers
#### Attributes of FTP servers
#### FTP user types
#### Using the Very Secure FTP Server
#### Quick-starting vsFTPd
#### Configuring vsFTPd
### Getting More Information about FTP Servers

## Chapter 21: Setting Up a Web Server

### Introduction to Web Servers
#### The Apache Web server
#### Other Web servers available for Fedora and RHEL
### Quick Starting the Apache Web Server
### Configuring the Apache Server
#### Configuring the Web server (httpd.conf)
#### Configuring modules and related services (/etc/httpd/conf.d/*.conf)
### Starting and Stopping the Server
### Monitoring Server Activities
#### Displaying server information
#### Displaying server status
#### Further security of server-info and server-status
#### Logging errors
#### Logging hits
#### Analyzing Web-server traffic

## Chapter 22: Setting Up an LDAP Address Book Server

### Understanding LDAP
### Defining information in schemas
### Structuring your LDAP directories
### Setting Up the OpenLDAP Server
#### Installing OpenLDAP packages
#### Configuring the OpenLDAP server (slapd.conf)
#### Starting the OpenLDAP service
### Setting Up the Address Book
### More Ways to Configure LDAP
### Accessing an LDAP Address Book from Thunderbird

## Chapter 23: Setting Up a DHCP Server

### Using Dynamic Host Configuration Protocol
### Setting Up a DHCP Server
#### Opening your firewall for DHCP
#### Configuring the /etc/dhcpd.conf file
#### Starting the DHCP server
### Setting Up a DHCP Client

## Chapter 24: Setting Up a MySQL Database Server

### Finding MySQL Packages
#### Getting More MySQL Packages
### Configuring the MySQL Server
#### Using mysql user/group accounts
#### Adding administrative users
#### Setting MySQL options
#### Using sample my.cnf files
### Starting the MySQL Server
### Checking That MySQL Server Is Working
### Working with MySQL Databases
#### Starting the mysql command
#### Creating a database with mysql
#### Adding data to a MySQL database table
#### Understanding MySQL Tables
#### Displaying MySQL Databases
##### Displaying all or selected records
##### Displaying selected columns
##### Sorting data
#### Making Changes to Tables and Records
##### Altering the structure of MySQL tables
##### Updating and deleting MySQL records
