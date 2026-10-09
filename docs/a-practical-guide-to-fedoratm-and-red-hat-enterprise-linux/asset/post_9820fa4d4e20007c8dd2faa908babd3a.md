
## Contexts and Containers

To make it flexible and easy to customize, Apache uses configuration directives, contexts, and containers. Some configuration directives are covered in the previous section. This section discusses contexts and containers, which are critical to managing an Apache server.

### Contexts

Four locations, called *contexts*, define where configuration directives can appear. This chapter marks each configuration directive to indicate which context(s) it can appear in. Table 26-1 describes each of these contexts.

**Table 26-1 Contexts**

| Context | Location(s) directives can appear |
| :--- | :--- |
| **server config** | In the **httpd.conf** file or included files only, but not inside <VirtualHost> or <Directory> containers (next section) unless so marked |
| **virtual host** | Inside <VirtualHost> containers in the **httpd.conf** file or included files only |
| **directory** | Inside <Directory>, <Location>, and <Files> containers in the **httpd.conf** file or included files only |
| **.htaccess** | In .htaccess files (page 939) only |

Directives in files incorporated by means of an Include directive (page 957) are part of the context they are included in and must be allowed in that context.

Putting a directive in the wrong context generates a configuration error and can cause Apache not to serve content correctly or not to start.

### Containers

*Containers*, or *special directives*, are directives that group other directives. Containers are delimited by XML-style tags. Three examples are shown here:

```xml
<Directory> ... </Directory>
<Location> ... </Location>
<VirtualHost> ... </VirtualHost>
```

Look in **httpd.conf** for examples of containers. Like other directives, containers are limited to use within specified contexts. This section describes some of the more frequently used containers.

- **`<Directory>`**
  - **Applies directives to all directories within the specified directory hierarchy.**
  - Syntax: `<Directory directory> ... </Directory>`
  - where *directory* is an absolute pathname specifying the root of the directory hierarchy that holds the directories the directives in the container apply to. The *directory* can include wildcards; a `\*` does not match a `/`.

A `<Directory>` container provides the same functionality as a `.htaccess` file (page 939). While an administrator can use a `<Directory>` container in Apache configuration files, regular users cannot. Regular users must use `.htaccess` files to control access to their own directories.

The directives in the `<Directory>` container shown in the following example apply to the `/var/www/html/corp` directory hierarchy. The Deny directive denies access to all clients, the Allow directive grants clients from the 192.168.10. subnets access, and the AllowOverride directive (page 960) enables Apache to process directives in `.htaccess` files in the hierarchy:

```apache
<Directory /var/www/html/corp>
    Deny From all
    Allow from 192.168.10.
    AllowOverride All
</Directory>
```

The following `<Directory>` container appears in the `httpd.conf` file and sets up a restrictive environment for the entire server filesystem (specified by `/`):

```apache
<Directory />
    AllowOverride None
    Require all denied
</Directory>
```

The AllowOverride directive causes Apache not to process directives in `.htaccess` files. The Require directive (page 961) denies all users access to the entire server filesystem directory. You must explicitly enable less restrictive options if you want them, but doing so can expose the server filesystem and compromise system security. This restrictive `<Directory>` container is followed immediately in `httpd.conf` by one that sets up less restrictive options for `/var/www`.

```apache
<Directory "/var/www">
    AllowOverride None
    Require all granted
</Directory>
```

The previous `<Directory>` container is followed by one that sets up options for the DocumentRoot (`/var/www/html`); this container affects all content. The code in `httpd.conf` is interspersed with many comments. Without the comments it looks like this:

```apache
<Directory "/var/www/html">
    Options Indexes FollowSymlinks
    AllowOverride None
    Require all granted
</Directory>
```

The Indexes option in the Options directive allows Apache to display directory listings and the FollowSymlinks option causes Apache to follow symbolic links. This container is less restrictive than the preceding one, although it still does not allow Apache to follow directives in `.htaccess` files.

Contexts: server config, virtual host

- **`<Files>`**
  - **Applies directives to specified ordinary files.**
  - Syntax: `<Files directory> ... </Files>`
  - where *directory* is an absolute pathname specifying the root of the directory hierarchy that holds the ordinary files the directives in the container apply to. The *directory* can include wildcards; a `*` does not match a `/`. This container is similar to `<Directory>` but applies to ordinary files rather than to directories.

The following directive, from the Fedora/RHEL *httpd.conf* file, denies access to all files whose filenames start with `.ht`, meaning that Apache will not serve the `.htaccess` and `.htpasswd` files.

```apache
<Files ".ht*">
    Require all denied
</Files>
```

Contexts: server config, virtual host, directory, .htaccess

- **`<IfModule>`**
  - **Applies directives if a specified module is loaded.**
  - Syntax: `<IfModule [!module-name] ... </IfModule>`
  - where *module-name* is the name of the module (page 968) Apache tests for. Apache executes the directives in this container if *module-name* is loaded or with *!* if *module-name* is not loaded.

Apache will not start if you specify a configuration directive that is specific to a module that is not loaded.

The following `<IfModule>` container, which is located in the Fedora/RHEL *httpd.conf* file, depends on the *mime_magic_module* module being loaded. If this module is loaded, Apache runs the *MIMEMagicFile* directive, which tells the *mime_magic_module* where its hints file is located.

```apache
<IfModule mime_magic_module>
    MIMEMagicFile conf/magic
</IfModule>
```

Contexts: server config, virtual host, directory, .htaccess

- **`<Limit>`**
  - **Limits access-control directives to specified HTTP methods.**
  - Syntax: `<Limit method [method] ... > ... </Limit>`
  - where *method* is an HTTP method. An HTTP method specifies which action is to be performed on a URL. The most frequently used methods are GET, PUT, POST, and OPTIONS; method names are case sensitive. GET (the default method) sends any data indicated by the URL. PUT stores data from the body section of the communication at the specified URL. POST creates a new document containing the body of the request at the specified URL. OPTIONS requests information about the capabilities of the server.

The `<Limit>` container binds a group of access-control directives to specified HTTP methods: Only methods named by this container are affected by this group of directives.

The following example disables HTTP uploads (PUTs) from systems that are not in a subdomain of example.com:

```apache
<Limit PUT>
    Order deny,allow
    Deny from all
    Allow from .example.com
</Limit>
```

Contexts: *server config, virtual host, directory, .htaccess*

> **Note:** It is safer to use the `<LimitExcept>` container than to use the `<Limit>` container, as the former protects against arbitrary methods. When you use `<Limit>`, you must be careful to name explicitly all possible methods that the group of directives could affect.

- **`<LimitExcept>`**
  - **Limits access-control directives to all except specified HTTP methods.**
  - Syntax: `<LimitExcept method [method] ... ... </LimitExcept>`
  - where *method* is an HTTP method. See `<Limit>` for a discussion of methods.

This container causes a group of access-control directives *not* to be bound to specified HTTP methods. Thus methods *not* named in `<LimitExcept>` are affected by this group of directives.

The access-control directives within the following `<LimitExcept>` container affect HTTP methods other than GET, POST, and OPTIONS. You could put this container in a `<Directory>` container to limit its scope:

```apache
<LimitExcept GET POST OPTIONS>
    Order deny,allow
    Deny from all
</LimitExcept>
```

Contexts: *server config, virtual host, directory, .htaccess*

- **`<Location>`**
  - **Applies directives to specified URIs.**
  - Syntax: `<Location URI> ... </Location>`
  - where *URI* points to content; it specifies a file or the root of the directory hierarchy that the directives in the container apply to. While the `<Directory>` container points within the local filesystem, `<Location>` points outside the local filesystem. The *URI* can include wildcards; a `*` does not match a `/`.

The following `<Location>` container limits access to `http://server/pop` from clients from the example.net domain, where *server* is the FQDN of the server:

```apache
<Location /pop>
    Order deny,allow
    Deny from all
    Allow from .example.net
</Location>
```

Contexts: *server config, virtual host*
