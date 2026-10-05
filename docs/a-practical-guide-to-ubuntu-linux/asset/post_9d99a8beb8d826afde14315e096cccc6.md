
AuthConfig: Class of directives that control authorization (AuthName, AuthType, Require, and so on). This class is used mostly in .htaccess files to require a username and password to access the content. For more information refer to "Authentication Modules and .htaccess" on page 945.

FileInfo: Class of directives that controls document type (DefaultType, Error-Document, SetHandler, and so on).

Indexes: Class of directives relating to directory indexing (DirectoryIndex, Fancy-Indexing, IndexOptions, and so on).

Limit: Class of client-access directives (Allow, Deny, and Order).

Options: Class of directives controlling directory features.

Context: directory

Specify in httpd.conf or sites-available/*

Default: All

Ubuntu: various

Deny Specifies which clients are not allowed to access specified content.

Deny All \ host [ ... ] \ env=var [env=var ... ]

This directive, which must be written as Deny from, denies access to a directory hierarchy by the specified clients. The directory hierarchy is specified by the container or .htaccess file this directive appears in. See the Order directive (next) for an example.

All: Denies content to all clients.

host: Denies content to the client(s) specified by *host*, which can take several forms: an FQDN, a partial domain name (such as example.com), an IP address, a partial IP address, or a network/mask pair.

var: Denies content when the environment variable named *var* is set. You can set a variable with the SetEnvIf directive.

Contexts: directory, .htaccess

Specify in mods-available/proxy.conf, httpd.conf, and sites-available/*

Default: none

Ubuntu: All

Order Specifies the default access and the order in which Allow and Deny directives are evaluated.

Order Deny,Allow | Allow,Deny

Allow,Deny: Allows access by default; denies access only to clients specified in Deny directives. (First evaluates Deny directives, then evaluates Allow directives).

Allow,Deny: Denies access by default; allows access only to clients specified in Allow directives. (First evaluates Allow directives, then evaluates Deny directives).

There must not be SPACES on either side of the comma. Access defaults to the second entry in the pair (Deny,Allow defaults to Allow) if there is no Allow from or Deny from directive that matches the client. If a single Allow from or Deny from matches the client, directive overrides the default. If Multiple Allow from or Deny directives match the client, Apache evaluates the directives in the order specified by the Order directive; the last match takes precedence.

Access granted or denied by this directive applies to the directory hierarchy specified by the container or .htaccess file directive appears in. Although Ubuntu Linux has a default of Allow,Deny, which denies access to all clients not specified by Allow directives, the next directive in sites-available/default, Allow from all, grants access to all clients:

- - Order allow,deny
- Allow from all

You can restrict access by specifying Deny,Allow to deny all access and specifying only those clients you want to grant access to an Allow directive. The following directives grant access to clients from the example.net domain only and would typically appear within a <Directory> container (page 915):

- - Order deny,allow
- Deny from all
- Allow from .example.net

Contexts: directory, .htaccess
Specify in httpd.conf or sites-available/*
Default: Deny,Allow
Ubuntu:Allow,Deny(for /var/www)

# CONFIGURATION FILES

This section describes the apache.conf and default configuration files.

# THE UBUNTU apache2.conf FILE

This section highlights some of the important features of the Ubuntu version of the /etc/apache2/apache2.conf file, which is based on the httpd.conf file distributed by Apache. The version of this heavily commented file that is distributed by Apache is broken into three parts, of which Ubuntu uses the first (Section 1: Global Environment) as apache2.conf. Ubuntu distributes the contents of the other sections among other configuration files, including the sites-available/default configuration file, which is described in the next section.

Include directives See page 906 for information on Include directives in the apache2.conf file.

ServerRoot The ServerRoot directive (page 926) is set to /etc/apache2, which is the pathname that Apache prepends to relative paths in the configuration files:

```
ServerRoot "/etc/apache2"
```

# Do not modify apache.conf

**tip** Typically, when you configure Apache, you do not make changes to **apache.conf**; instead, modify files that are specified in Include directives (page 906). You can also use the configuration tools described on page 905. This setup allows Apache to change **apache2.conf** without affecting the server.

The `<IfModule>` containers (page 916) allow you to use the same **apache2.conf** file with different multiprocessing modules (MPMs, page 947). Apache executes the directives in an `<IfModule>` container only if the specified module is loaded. The **apache2.conf** file holds two `<IfModule>` containers that configure Apache, depending on which module—*prefork* or *worker*—is loaded. Ubuntu ships with the more efficient *worker* MPM loaded.

```
## Server-Pool Size Regulation (MPM specific)
<IfModule mpm_prefork_module>
StartServers 5
MinSpareServers 5
MaxSpareServers 10
MaxClients 150
MaxRequestsPerChild 0
</IfModule>

<IfModule mpm_worker_module>
StartServers 2
MinSpareThreads 25
MaxSpareThreads 75
ThreadLimit 64
ThreadsPerChild 150
MaxRequestsPerChild 0
</IfModule>
```

For more information refer to “Multiprocessing Modules (MPMs)” on page 947.

The User directive causes Apache to run as the user specified by APACHE_USER. In the `/etc/apache2/envvars` file, the APACHE_USER variable is assigned a value of www-data:

```
export APACHE_USER=www-data
```

The TypesConfig directive specifies the file that defines MIME (page 934) types that Apache uses for content negotiation (page 935).

```
TypesConfig /etc/mime.types
```

DefaultType defines the content-type Apache sends if it cannot determine a type.

```
DefaultType text/plain
```

# CHAPTER 26 APACHE: SETTING UP A WEB SERVER

Instead of having a lot of LoadModule directives in the apache2.conf file, Ubuntu puts the following Include directives in file:

```
Include /etc/apache2/mods-enabled/*.load
Include /etc/apache2/mods-enabled/*.conf
```

These directives include all the *.load and *.conf files in the mods-enabled directory. For more information on how to enable modules, see the discussion of a2enmod on page 905.

There are many more directives in the apache2.conf file; the comments in the file provide a guide as to what they do. There is nothing you need to change as you get started with Apache.

# THE UBUNTU DEFAULT CONFIGURATION

This section highlights some of the important features of the Ubuntu configuration file, which is located in the /etc/apache2/sites-available directory.

ServerAdmin ServerName As Ubuntu Linux is shipped, the ServerAdmin directive is set to webmaster@localhost. Add a ServerName directive and change ServerAdmin to a useful value as suggested under ServerAdmin (page 912) and ServerName (page 912).

DocumentRoot The DocumentRoot directive (page 913) appears as follows:

```
DocumentRoot: /var/www/
```

Modify this directive only if you want to put content somewhere other than /var/www/ directory.

The <Directory> container (page 915) sets up a restrictive environment for the entire local filesystem (specified by /):

```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

The Options directive (page 928) allows Apache to follow symbolic links but allows many options. The AllowOverride directive (page 930) causes Apache not to process directives in .htaccess files. You must explicitly enable less restrictive if you want them, but be aware that doing so expose the root filesystem and compromise system security.

Next, another <Directory> container sets up less restrictive options for the DocumentRoot (/var/www/). The code in default is interspersed with many comments. Without the comments it looks like this:

```
<Directory /var/www/>
Options Indexes FollowSymLinks MultiViews
AllowOverride None
Order allow,deny
allow from all
</Directory>
```
