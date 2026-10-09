There must not be SPACES on either side of the comma. Access defaults to the second entry in the pair (Deny,Allow defaults to Allow) if there is no Allow from or Deny from directive that matches the client. If a single Allow from or Deny from directive matches the client, that directive overrides the default. If multiple Allow from and Deny from directives match the client, Apache evaluates the directives in the order specified by the Order directive; the last match takes precedence.

Access granted or denied by this directive applies to the directory hierarchy specified by the container or .htaccess file this directive appears in. Although Ubuntu Linux has a default of Allow,Deny, which denies access to all clients not specified by Allow directives, the next directive in sites-available/default, Allow from all, grants access to all clients:

```
Order allow,deny
Allow from all
```

You can restrict access by specifying Deny,Allow to deny all access and then specifying only those clients you want to grant access to in an Allow directive. The following directives grant access to clients from the example.net domain only and would typically appear within a <Directory> container (page 915):

```
Order deny,allow
Deny from all

Allow from .example.net
```

Contexts: directory, .htaccess
Specify in httpd.conf or sites-available/*
Default: Deny,Allow
Ubuntu: Allow,Deny (for /var/www)

# CONFIGURATION FILES

This section describes the apache2.conf and default configuration files.

# THE UBUNTU apache2.conf FILE

This section highlights some of the important features of the Ubuntu version of the /etc/apache2/apache2.conf file, which is based on the httpd.conf file distributed by Apache. The version of this heavily commented file that is distributed by Apache is broken into three parts, of which Ubuntu uses the first (Section 1: Global Environment) as apache2.conf. Ubuntu distributes the contents of the other two sections among other configuration files, including the sites-available/default configuration file, which is described in the next section.

+   Include directives. See page 906 for information on Include directives in the apache2.conf file.

+   ServerRoot directive. The ServerRoot directive (page 926) is set to /etc/apache2, which is the pathname that Apache prepends to relative pathnames in the configuration files:

```
ServerRoot "/etc/apache2"
```