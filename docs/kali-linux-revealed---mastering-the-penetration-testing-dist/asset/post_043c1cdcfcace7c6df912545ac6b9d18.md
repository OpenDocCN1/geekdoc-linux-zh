
As you can see, the connection was successful.

## Managing PostgreSQL Clusters

First, it is worth noting that the concept of "PostgreSQL cluster" is a Debian-specific addition that you will not find any reference to this term in the official PostgreSQL documentation. From the point of view of the PostgreSQL tools, such a cluster is an instance of a database server running on a specific port.

That said, Debian's postgresql-common package provides multiple tools to manage such clusters: pg_createcluster, pg_dropcluster, pg_ctlcluster, pg_upgradecluster, pg_renamecluster, and pg_lsclusters. We won't cover all those tools here, but you can refer to their respective pages for more information.

What you must know is when a new major version of PostgreSQL gets installed on your system, it will create a new cluster that runs on the port (usually 5433) and you will keep using the old version until you migrate your databases.

You can retrieve a list of all the clusters and their status with pg_lsclusters. More importantly, you can automate the migration of your cluster to the latest PostgreSQL version with pg_upgradecluster old-version cluster-name. For this to succeed, you might have to remove the (empty) cluster for the new version (with pg_dropcluster new-version cluster-name). The old cluster is not dropped in the process, but it also won't be started automatically. You can drop it once you have checked that the upgraded cluster works.

## 5.3.4. Configuring Apache

A Kali Linux installation includes the Apache web server, provided by the apache2 package. Being a network service, it is disabled by default. You can manually start it with systemctl start apache2.

With and more applications being distributed as web applications, it is important to have some knowledge of Apache in order to host those applications, for local usage or for making them available over the network.

Apache is a modular server and many features are implemented by external modules that the main program loads during its initialization. The default configuration enables only the most common modules, enabling new modules is easily done by running a2enmod module. a2dismod module to disable a module. These programs actually create (or delete) symbolic links in /etc/apache2/mods-enabled/, pointing at the actual files (stored in /etc/apache2/mods-available/).

There are many modules available, but two are worth initial consideration: PHP and SSL. Web applications with PHP are executed by the Apache web server with the module provided by the libapache-mod-php package, and its installation automatically enables the module.

Apache 2 includes the SSL module required for secure HTTP (HTTPS) out of the box. It first needs to be enabled with a2enmod ssl, and the required directives must be added to the configuration files. A configuration example is provided in /etc/apache2/sites-available/default-ssl.conf. See http://httpd.apache.org/docs/2.4/mod/mod_ssl.html for more information.

The full list of Apache modules can be found online at http://httpd.apache.org/docs/2.4/mod/index.html.

With its default configuration, the web server listens on port 80 (as configured in /etc/apache2/ports.conf), and serves pages from the /var/www/html/ directory by default (as configured in /etc/apache2/sites-enabled/000-default.conf).

## Configuring Virtual Hosts

A virtual host is an extra entity for the web (say www.kali.org and www.offensive-security.com) because the HTTP requests embedded both the name of the website requested and the URL localhost (this feature is known as name-based virtual hosts).

The default configuration for Apache 2 enables name-based virtual hosts. In addition, a default virtual host is defined in the /etc/apache2/sites-enabled/000-default.conf file; this virtual host will be used if no host matching the request sent by the client is found.

> Requests concerning unknown virtual hosts will always be served by the first defined virtual host, which is why the package ships a 000-default.conf configuration file, which sorts first among other files that you might create.

Each extra virtual host is described by a file stored in /etc/apache2/sites-available/. The file is usually named the hostname of the website followed by a .conf suffix (for example: www.example.com.conf). You can enable the new virtual host with a2ensite www.example.com. Here is a minimal virtual host:

```apache
<VirtualHost *:80>
    ServerName www.example.com
    DocumentRoot /var/www/html
    CustomLog /var/log/apache2/access.log combined
    ErrorLog /var/log/apache2/error.log
</VirtualHost>
```

## Common Directives

This section briefly reviews some commonly-used Apache directives. The Directory block includes several; for example:

```apache
<Directory /var/www>
    Options FollowSymLinks
    IndexIndex index.html
</Directory>
```

The Options directive lists all options that can be enabled; None value disables all. Available options include:

- ExecCGI: indicates that CGI scripts can be executed.
- FollowSymLinks: tells the server that symbolic links can be followed.
- SymLinksIfOwner: tells the server to follow links, but only when the link and its target have the same owner.
- Includes: enables SSI (Server Side Includes).
- Indexes: tells the server to list the directory contents.
- MultiViews: enables content negotiation.

## Requiring Authentication

In some circumstances, access to part of a website needs to be restricted, so only legitimate users who provide a username and a password are granted access.

The .htaccess file contains access restrictions enforced each time a request connects from the directory where it is stored. These directives are recursive, expanding the scope to all subdirectories. Most of the directives that can occur in a Directory block are also in .htaccess.

### Example 5.3 .htaccess File Requiring Authentication

```apache
Require valid-user
AuthName "Private directory"
AuthType Basic
AuthUserFile /etc/apache2/auth/passwd-private
```

The authentication system used in the example (Basic) has minimal security as the password is in clear text (it is only encoded as base64, which is a simple encoding rather than an encryption method). It should also be noted that documents protected by this mechanism go over the network. If security is important, the entire HTTP session should be encrypted with Transport Layer Security (TLS).

The /etc/apache2/auth/passwd-private file contains a list of users and passwords; it is commonly manipulated by the htpasswd command. For example, the following command is used to add a user or change their password:

```bash
# htpasswd /etc/apache2/auth/passwd-private user
New password:
Re-type new password:
Adding password for user user
```

### Restricting Access

The Require directive controls access restrictions for a directory (and its subdirectories, recursively). It can be used to restrict access based on many criteria; we will stop at access restriction based on the IP address of the client but can be much more powerful than that, especially when Require directives are combined with RequireAll block.

For instance, you could restrict access to the local network with the following directive:

```apache
Require ip 192.168.0.0/16
```
