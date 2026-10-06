
# 452 Part IV ♦ Implementing Network Services in SUSE Linux

example can be seen with the Apache module mod_status, which provides dynamic information about the running Apache processes. The dynamic information is mapped to a particular URL, usually /server-status. Since no file exists at a corresponding filesystem location, any directives, as the Order and Deny directives previously mentioned, must be contained within the <Location> container.

```
<Location /server-status>
Order Allow,Deny
Deny from all
</Location>
```

> Why all the fuss about containers representing resources from the point of view of the filesystem or webspace? Generally directives placed in the main configuration file apply to the entire site. Thus, to manage the configuration for only a section or specific resource contained within a site containers such as <Directory>, <Files>, and <Location> are necessary.

# Virtual Hosts

Apache has the capability to serve more than one web site simultaneously. This is known as virtual hosting. To provide this all web server configuration provides the <VirtualHost> container for a web administrator to maintain multiple domains/hosts on server.

At the basic level, the Virtual Host section is simply a reimplementation of the directives defined in the Main Server section, only directed in relation to a specific Virtual Host. Moreover, since the Virtual Hosts inherits, as its default settings, any configurations defined within the Main Server Configuration, the directives within the Virtual Host section simply need to focus on what is different. A look at 16-1.

Listing 16-1: Defining a virtual host

```
# VirtualHost for the subdomain apache.suse.com
<VirtualHost 192.168.2.34>
ServerName apache.suse.com
DocumentRoot /srv/www/apache.suse.com/html
ErrorLog apache.suse.com_error_log
CustomLog logs/apache.suse.com access_log combined

<Directory "/srv/www/apache.suse.com/html">
Options FollowSymLinks
Order Allow,deny
Allow from all
</Directory>
</VirtualHost>
```

# Chapter 16 Setting Up a Web Site with the Apache Web Server 453

This virtual host, which is a web site running under the subdomain apache for suse.com, binding to the IP address 192.168.2.34. Since no port is specified for this virtual host, the default port 80, which would be specified in the Main Server section, is inherited from the default port to this site. On the name of the site is apache.suse.com and the document root, where the main resources in the filesystem can be found for this site, is /var/www/apache.suse.com/html. Moreover the logs for this site will go in the file separate from those used for the Main Server. Finally, the options for access control with the document root are laid out within the Directory counter.

To facilitate the migration of existing websites from Apache 1.3 to 2.0, the ASF programmers learned to minimize the changes that have taken place to the Main Server and Virtual Host configuration sections. This is not to be read as meaning the developers did not change the underlying functionality or code, but simply to mean the group tried to keep complicating migration with a round of completely new directives and syntax. web administrators should be aware that some directives have been eliminated and the behavior of others have changed. Further reading of the Apache documentation is therefore recommended for anyone who is making the switch.

# Security

Security is a big issue when it comes to these days and can mean different things to people. An administrator it can mean the following questions: Is the server locked down and the software up-to-date and free of any vulnerabilities? To an application developer it might mean that the user has verified and that the customer data has been stored in a safe, reusable manner. To the user of the web site it could mean that personal data remains in limited hands and, while transit, is encrypted to limit eavesdropping.

All of these concerns are valid fundamental concerns. However, from the Apache web server's perspective all of these issues come down to three basic concepts: authentication, authorization, and access control.

- ◆ Authentication is any process by which the web site verifies the identity of a user in question, in essence they are who they claim they.
- ◆ Authorization is any process by which someone is allowed to gain access to information that they want to have.
- ◆ Access control is the process of limiting users access to information that they may not have access to.

With the basic web server setup these processes are managed by the Apache modules mod_auth and mod_access. You can use these modules' configuration directives in the main server configuration file, httpd.conf, or in per-directory .htaccess.

# 454 Part IV ♦ Implementing Network Services in SUSE Linux

# Setting Up User Access

The common security issue for a web site is the need to password protect a directory or file. To do this, the first step is the creation of a password file. The password file needs to reside somewhere outside of the webspace. For example, if the web site's directory reside at `/srv/www/htdocs/dir` on the filesystem, then the password file needs to reside somewhere outside of that space, as /etc/httpd-passwd

Creating the file is simple; just use `htpasswd2` utility that comes with the Apache RPM. The utility will ask for a password for the username as a command line option and will ask that the password be re-entered for verification. If all goes well, the file will be created with the new entry.

```
htpasswd2 -c /etc/http-passwd paul
New password:
Re-type new password:
Adding password for user paul
```

In the preceding example, a password file is created (-c) in the `/etc/http-passwd` directory and a user, `paul`, and associated password for that user was entered into the newly created file.

To add names to an existing password file, simply omit the -c

```
htpasswd2 /etc/http-passwd justin
New password:
Re-type new password:
Adding password for user justin
```

After the password file has been properly populated with usernames and passwords, the next step is to configure the server to request a password and tell the server which users are allowed access. If, there is a need to protect a directory, this can be done using the `httpd.conf` file using the `<Directory>` container.

```
<Directory /srv/www/htdocs/private>
AuthType Basic
AuthName "Restricted Directory"
AuthUserFile /etc/http-passwd
Require user paul
</Directory>
```

In the `<Directory>` container:

- The `AuthType` directive selects what method is used to authenticate the user; the most common method is `Basic` and is implemented by `mod_auth`.

# Chapter 16 Setting Up a Web Site with the Apache Web Server 455

![](img/e4e5c9f32e76fb35fabb21a96f1a1e)

The Basic authentication method implemented by the Apache server mod_auth passes the username and password over the network between the client in an encrypted clear text manner. The Apache server supports other authentication methods such as AuthType Digest, which is implemented by the Apache module mod_auth_digest. The Digest authentication type provides a more secure password system by sending only an MD5 hash of the password over the network. However.

- The AuthName directive sets the Realm that is requiring before access. The realm name provides two functions:
- First, the client application presents this information to the user as part of the password dialog box.
- Second, it is used by the client to determine what password to send for given authenticated area should be more than one.
- The UserFile directive sets the path to the password file that was created with htpasswd.
- The Require directive provides the authorization path of the process by defining for the web server, after a valid authentication, the users that are allowed to access the defined realm.

# Setting Up Group Access

The previous example will let only one user in, paul. In most cases this is not very practical, as most sites will need to allow more than one person in. This can be accomplished in two different manners.

- Instead of the Require user directive that will allow only the user paul access to the directory, Require valid-user will allow anyone in the password file access to the directory after entering their password.
- Another option is to create a group file that associates a group name with a list of users in a file. The format of this file is straightforward and can be accomplished with your favorite editor.

GroupName: paul roger

The directory container will need to know where the password file and the group file are located. Since there can be more than one group listed within the group file, which may gain access will also need to be specified.

```
<Directory /srv/www/htdocs/private>
AuthType Basic
AuthName "By Invite Only"
UserFile /etc/http-passwd
```
