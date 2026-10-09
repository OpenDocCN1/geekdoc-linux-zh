
| Directive | Description |
|---|---|
| ServerName | Used to set the hostname, port, and request scheme of a machine hosting the web server while redirecting URLs. The syntax of the ServerName directive is: ServerName alias hostname with the port number. |
| AllowOverride | Used to specify the list of directives that are used in .htaccess files. The directives in the .htaccess file override the earlier configuration directives. If the directive is set to None then the server does not refer to the .htaccess file. The syntax of the AllowOverride directive is: AllowOverride [All \| None | {Any combination of Options, FileInfo, AuthConfig, Limit}]. |
| Addtype | Used to map a MIME-type file name extension to a specified file type. The syntax of the AddType directive is: AddType MIME-type File type. |
| DirectoryIndex | Used to list a set of files that the server needs to look through, when a client requests an index of a directory. The syntax of the DirectoryIndex directive is: DirectoryIndex file name. |
| UserDir | Used to set the location from where the client receives the document as the user’s home directory. The syntax of the UserDir directive is: UserDir file name. |

## The MIME Type Configuration

Multipurpose Internet Mail Extensions (MIME) is a standard Internet format that supports ASCII character sets, non-ASCII character sets, non-text attachments, and multiple parts in a message body. These formats are used in email messages and web pages. The SMTP and HTTP protocols support the MIME formats. The AddType directive is used to configure the MIME types in an Apache server. It supports the email messages sent through the Internet.

## The .htaccess Files

The .htaccess files are used to implement configuration changes in individual directories. They are used to configure a directory that is to be set up for recognizing CGI scripts. The changes made to the directives of a file stored in the directory will be applied to the directory. The .htaccess files follow the same syntax used in the httpd.conf file. The directives to be used in the .htaccess file are determined by the AllowOverride directive, which specifies the value to permit the directive. Information whether the directive is available in the .htaccess file is specified in the respective documentation of the directive.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_628_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_629_0.png)

*Figure 13-4: Configuring a directory to recognize CGI scripts.*

### Syntax for Renaming the .htaccess File

The .htaccess file can be renamed using the **AccessFileName** directive where the syntax is: **AccessFileName new file name**.

### The order Statement

The order statement, which is included in the **mod\_access** module, provides the access control for a system. It operates along with the **Allow** and **Deny** directives. It involves three passes. In the first pass, it processes all the **Allow** or **deny** directives based on their specification. In the second pass, it processes the directive other than the first pass directive. In the third pass, it processes the requests that do not match either the **Allow** or **Deny** directives.

The syntax is:

```
Order Ordering Allow|from hostname|IP address or the IP address range
Deny from hostname|IP address or the IP address range
```

where the ordering value is set to either "Allow, deny" or "Deny, allow".

### The apachectl Command

The Apache HTTP Server Control Interface (**apachectl**) is the interface that allows an administrator to control the functioning of the HTTP service using the **apachectl** command. The **apachectl** command supports various options.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_629_1.png)

| Option | Used To |
|---|---|
| start or apachectl -k start | Start the apache daemon. If the daemon is already running, it displays an error message. |
| stop or apachectl -k stop | Stop the apache daemon. |
| restart or apachectl -k restart | Restart the apache daemon. If the daemon is not running, it starts the daemon. |
| fullstatus | Display the full status report of the services running and requested by clients. It requires the mod_status module to be enabled on the system. |
| status | Display the status report of the services requested by clients. The report does not include the list of running services. |
| configtest or apachectl -t | Run the configuration file test that either reports the success state as “Syntax OK” or displays an error message. It is also used to test the syntax of the ssl.conf file. |
| graceful or apachectl -k graceful | Restart the Apache httpd daemon. It starts the httpd daemon if it is not running. |
| graceful-stop or apachectl -k graceful-stop | Stop the Apache httpd daemon. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_630_0.png)

Figure 13-5: Running the configuration file test for apachectl.

## Syntax

The syntax of the apachectl command is *apachectl* *start*/*stop*/*restart*/*status*/*configtest*.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_631_0.png)

## The httpd Daemon

The httpd daemon is a standalone daemon that runs the Apache service. There are many command line options that can be used with this daemon. Some of the options are listed in the table.

| Option | Description |
| :--- | :--- |
| -h | Displays a list of command line options that are used. |
| -l | Displays a list of modules. |
| -L | Displays a list of directives along with arguments. |
| -S | Displays the settings that are parsed from the config file. |
| -t | Runs the syntax configuration test for the httpd.conf file. It is also used to check the syntax of the ssl.conf file. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_631_1.png)

**Figure 13-6:** PIDs of the httpd daemons running on the system.

## Text-Based Web Browsers

**Definition:**

A **text-based web browser** is an application that is used to access web pages in the CLI mode. It does not support graphics or images and can run either in color or mono mode. The browser requires the URL of a website to be displayed on the screen of a system. The web browser has menus and options that you can use to navigate through web pages.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_632_0.png)

Text-Based Web Browsers

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_632_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_632_2.png)

Contents of a website

*Figure 13-7: Accessing a website using a text-based web browser.*

## ELinks

*ELinks* is a non-GUI, text-based web browser. It supports color text display, table rendering, background downloading, menu-driven configuration interfaces, tabbed browsing, and slim code. It handles local files and works with remote URL protocols such as HTTP, HTTPS, and FTP. The *links* command allows you to open the text-based web browser.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_632_3.png)

ELinks

![](img/477ccb2f05b6ba1b2d563ea74f18c197_633_0.png)

## Syntax

The syntax of the links command is links [options] {URL}.

## The wget Command

The wget command facilitates content retrieval from websites. It supports deriving content via the HTTP, HTTPS, FTP- and TCP/IP-based protocols, recursive downloads, offline viewing of html pages, and proxies. This command is noninteractive and is effective over slow and unstable network connections. If a download does not complete due to a network problem, wget automatically continues the download from where it stopped, until the entire file is retrieved.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_634_0.png)

Figure 13-9: Retrieving web pages using the wget command.

## Syntax

The syntax of the wget command is wget [command options] http://(hostname or IP of the destination).

## The curl Command

![](img/477ccb2f05b6ba1b2d563ea74f18c197_634_1.png)

The curl Command

Curl is a command line tool that is used to transfer data to or from a server, using the URL syntax. It is an open source software that runs on a variety of operating systems. It supports protocols such as FTP, HTTP, FTPS, HTTPS, SCP, SFTP, TELNET, TFTP, LDAP, LDAPS, TFTP, DICT, and FILE. Curl increases file transfer speed by attempting to reuse connections for multiple file transfers to or from the same server.
