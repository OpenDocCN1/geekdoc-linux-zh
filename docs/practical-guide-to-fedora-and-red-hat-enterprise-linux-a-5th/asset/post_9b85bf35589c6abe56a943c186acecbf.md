
absent or when none of the files specified by this directive exists in the specified directory, Apache displays a directory listing as specified by the IndexOptions directive (page 863).

For example, you could provide the following DirectoryIndex directive:

```
DirectoryIndex index.php index.html index.htm index.shtml
```

This directive would cause Apache to return from the specified directory the file named **index.php**, **index.html**, **index.htm**, or **index.shtml**.

The **index.php** is the name of a PHP document; **index.html** and **index.htm** are the names of the standard, default HTML documents; and **index.shtml** is a secure HTML document. If you supply CGI documents, you may want to add the **index.cgi** value to this directive. The name **index** is standard but arbitrary.

A **.var** filename extension denotes a content-negotiated document that allows Apache to serve the Apache manual and other documents in one of several languages as specified by the client. If you are not providing content in different languages, you can omit this filename extension from the DirectoryIndex directive.

- Contexts: server config, virtual host
- Default: index.html
- Fedora/RHEL: index.html index.html.var

## Contexts and Containers

To make it flexible and easy to customize, Apache uses configuration directives, contexts, and containers. Configuration directives were covered in the previous section. This section discusses contexts and containers, which are critical to managing an Apache server.

### Contexts

Four locations, called *contexts*, define where a configuration directive can appear. This chapter marks each configuration directive to indicate which context(s) it can appear in. Table 26-1 describes each of these contexts.

Table 26-1 Contexts

| Context | Location(s) directives can appear in |
| :--- | :--- |
| **server config** | Directive can appear in the **httpd.conf** file only, but not inside <VirtualHost> or <Directory> containers (next section) unless so marked |
| **virtual host** | Directive can appear inside <VirtualHost> containers in the **httpd.conf** file only |
| **directory** | Directive can appear inside <Directory>, <Location>, and <Files> containers in the **httpd.conf** file only |
| **.htaccess** | Directive can appear in **.htaccess** files (page 850) only |

Directives in files incorporated by means of the Include directive (page 866) are part of the context they are included in and must be allowed in that context. Putting a directive in the wrong context generates a configuration error and can cause Apache not to serve content correctly or not to start.

## Containers

Containers, or special directives, are directives that group other directives. Containers are delimited by XML-style tags. Three examples are shown here:

```
`<Directory> ... </Directory>`
`<Location> ... </Location>`
`<VirtualHost> ... </VirtualHost>`
```

Look in **httpd.conf** for examples of containers. Like other directives, containers are limited to use within specified contexts. This section describes some of the more frequently used containers.

# <Directory>

*Applies directives to directories within specified directory hierarchies.*
`<Directory directory> ... </Directory>`

where *directory* is an absolute pathname specifying the root of the directory hierarchy that holds the directories the directives in the container apply to. The *directory* can include wildcards; a *`*`* does not match a *`/`*.

A `<Directory>` container provides the same functionality as a `.htaccess` file. While an administrator can use a `<Directory>` container in the **httpd.conf** file, regular users cannot. Regular users can use `.htaccess` files to control access to their own directories.

The directives in the `<Directory>` container shown in the following example apply to the */var/www/html/corp* directory hierarchy: The Deny directive denies access to all clients, the Allow directive grants clients from the 192.168.10. subnet access, and the AllowOverride directive (page 869) enables the use of `.htaccess` files in the hierarchy:

```apache
<Directory /var/www/html/corp>
  Deny From all
  Allow From 192.168.10.
  AllowOverride All
</Directory>
```

Contexts: **server config**, **virtual host**

# <Files>

*Applies directives to specified ordinary files.*
`<Files directory> ... </Files>`

where *directory* is an absolute pathname specifying the root of the directory hierarchy that holds the ordinary files the directives in the container apply to. The *directory* can include wildcards; a `*` does not match a `/`. This container is similar to <Directory> but applies to ordinary files and not to directories.

The following directive, from the Fedora/RHEL `httpd.conf` file, denies access to all files whose filenames start with `.ht`. The tilde (`~`) changes how Apache interprets the following string. Without a tilde, the string is a simple shell match that interprets shell special characters (page 243). With a tilde, Apache interprets the string as a regular expression (page 1023):

```
`<Files ~ "^\.ht">`  
`Order allow,deny`  
`Deny from all`  
`</Files>`
```

> Contexts: server config, virtual host, directory, .htaccess

```
`<IfModule>`
```

> Applies directives if a specified module is loaded.

```
`<IfModule [!1]module-name> ... </IfModule>`
```

where `module-name` is the name of the module (page 876) that is tested for. Apache executes the directives in this container if `module-name` is loaded or with `!` if `module-name` is not loaded.

Apache will not start if you specify a configuration directive that is specific to a module that is not loaded.

The following <IfModule> container from the Fedora/RHEL `httpd.conf` file depends on the `mod_mime_magic.c` module being loaded. If this module is loaded, Apache runs the `MIMEMagicFile` directive, which tells the `mod_mime_magic.c` module where its hints file is located.

```
`<IfModule mod_mime_magic.c>`  
`MIMEMagicFile conf/magic`  
`</IfModule>`
```

See page 871 for another example of the <IfModule> container.

> Contexts: server config, virtual host, directory, .htaccess

```
`<Limit>`
```

> Limits access-control directives to specified HTTP methods.

```
`<Limit method [method] ... > ... </Limit>`
```

where `method` is an HTTP method. An HTTP method specifies which action is to be performed on a URL. The most frequently used methods are GET, PUT, POST, and OPTIONS; method names are case sensitive. GET, the default method, sends any data indicated by the URL. PUT stores data from the body section of the communication at the specified URI. POST creates a new document containing the body of the request at the specified URL. OPTIONS requests information about the capability of the server.

This container binds a group of access-control directives to specified HTTP methods: Only methods named by the `<Limit>` container are affected by this group of directives.

The following example disables HTTP uploads (PUTs) from systems that are not in a subdomain of **example.com**:

```
<Limit PUT> 
    order deny,allow
    deny  from all
    allow from .example.com
</Limit>
```

# Use `<LimitExcept>` instead of `<Limit>`

- **caution** It is safer to use the `<LimitExcept>` container instead of the `<Limit>` container, as the former protects against arbitrary methods. When you use `<Limit>`, you must be careful to name explicitly all possible methods that the group of directives could affect.
- It is safer still not to put access-control directives in any container.

Contexts: **server config**, **virtual host**, **directory**, **htaccess**

# `<LimitExcept>` Limits *access-control* directives to *all* except *specified* HTTP *methods*.

```
<LimitExcept method [method] ... > ... </LimitExcept>
```

where **method** is an HTTP method. See `<Limit>` for a discussion of methods.

This container causes a group of access-control directives *not* to be bound to specified HTTP methods: Methods *not* named in `<LimitExcept>` are affected by this group of directives.

The access-control directives within the following `<LimitExcept>` container affect HTTP methods other than GET and POST. You could put this container in a `<Directory>` container to limit its scope:

```
<LimitExcept GET POST OPTIONS> 
    Order deny,allow
    Deny  from all
</LimitExcept>
```

Contexts: **server config**, **virtual host**, **directory**, **htaccess**

# `<Location>` Applies directives to *specified* *URIs*.

```
<Location URI> ... </Location>
```

where **URI** points to content and specifies a file or the root of the directory hierarchy that the directives in the container apply to. While the `<Directory>` container points within the local filesystem, `<Location>` points outside the local filesystem. The **URI** can include wildcards; a `*` does not match a `/`.
