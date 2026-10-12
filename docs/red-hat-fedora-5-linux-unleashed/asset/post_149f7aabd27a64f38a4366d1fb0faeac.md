
## DocumentRoot

Set this directive to the absolute path of your document tree, which is the top directory from which Apache serves files. By default, it’s set to `/var/www/html/usgsa`. If you built the source code yourself, DocumentRoot is set to `/usr/local/apache/htdocs` (if you didn’t choose another directory when you compiled Apache). Prior to version 1.3.4, this directive appears in srm.conf.

## UserDir

The `UserDir` directive disables or enables and defines the directory (relative to a local user’s home directory) where that user can put public HTML documents. It’s relative because each user has her own HTML directory. This setting is disabled by default but can be enabled to store user web content under any directory.

The default setting for this directive, if enabled, is public_html. Each user can create a directory called public_html under her home directory, and HTML documents placed in that directory are available as `http://servername/~username`, where username is the user-name of the particular user. Prior to version Apache version 1.3.4, this directive appears in srm.conf.

## DirectoryIndex

The `DirectoryIndex` directive indicates which file should be served as the index for a directory, such as which file should be served if the URL `http://servername/SomeDirectory/` is requested.

It’s often useful to put a list of files here so that if index.html (the default value) isn’t found, another file can be served instead. The most useful application of this is to have a CGI program run as the default action in a directory. You can have users who make their web pages on Windows, you might want to add index.htm as well. In that case, the directive would look like `DirectoryIndex index.html index.cgi index.htm`. Prior to version 1.3.4, this directive appears in srm.conf.

## Apache Multiprocessing Modules

Apache version 2.0 and greater now uses a new internal architecture supporting multiprocessing modules (MPMs). These modules are used by the server for a variety of tasks, such as network and process management, and are compiled into Apache. MPMs enable Apache to work much better on a wider variety of computer platforms, and they can help improve server stability, compatibility, and scalability.

Apache can use only one MPM at any time. These modules are different from the base set included with Apache (see the “Apache Modules” section later in this chapter), but are used to implement settings, limits, or other server actions. Each module in turn supports numerous additional settings, called directives, which further refine server operation.

The internal MPM modules relevant for Linux include:

- mpm_common—A set of 20 directives common to all MPM modules
- prefork—A nonthreaded, preforking web server that works similar to earlier (1.3) versions of Apache
- worker—Provides a hybrid multiprocess multithreaded server

MPM enables Apache to be used on equipment with fewer resources yet still handle massive numbers of hits and provide stable service. The worker module provides directives to control how many simultaneous connections your server can handle.

> **NOTE**
> Other MPMs are available for Apache related to other platforms, such as mpm_netware for NetWare hosts and mpm_winnt for Windows NT platforms. An MPM named perchild, which provides user ID assignment to selected daemon processes, is under development. For more information, browse to the Apache Software Foundation’s home page at http://www.apache.org/.

## Using .htaccess Configuration Files

Apache also supports special configuration files, known as .htaccess files. Almost any directive that appears in httpd.conf can appear in an .htaccess file. This file, specified in the AccessFileName directive in httpd.conf (or srm.conf prior to version 1.3.4) sets configurations on a per-directory (usually in a user directory) basis. As the system administrator, you can specify both the name of this file and which of the server configurations can be overridden by the contents of this file. This is especially useful for sites in which there are multiple content providers and you want to control what these people can do with their space.

To limit which server configurations the .htaccess files can override, use the AllowOverride directive. AllowOverride can be set globally or per directory. For example, in your httpd.conf file, you could use the following:

```
# Each directory to which Apache has access can be configured with respect
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).
#
# First, we configure the 'default' to be a very restrictive set of
# permissions.
#
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

### Options Directives

To configure which configuration options are available to Apache by default, you must use the Options directive. Options can be *None*, *All*, or any combination of *Indexes*, *Includes*, *FollowSymLinks*, *ExecCGI*, and *MultiViews*. *MultiViews* isn't included in *All* and must be specified explicitly. These options are explained in Table 21.2.

| Switch | Description |
| :--- | :--- |
| *None* | None of the available options are enabled for this directory. |
| *All* | All the available options, except for *MultiViews*, are enabled for this directory. In the absence of an *index.html* file or another *DirectoryIndex* file, a listing of the files in the directory is generated as an HTML page for display to the user. |
| *Indexes* | Server-side includes (SSI) are permitted in this directory. This can also be written as *IncludesNoExec* if you want to allow includes but don't want to allow the *exec* option in them. For security reasons, this is usually a good idea in directories over which you don't have complete control, such as *UserDir* directories. |
| *Includes* | Allows access to directories that are symbolically linked to a document directory. You should never set this globally for the whole server and only rarely for individual directories. This option is a potential security risk because it allows web users to escape from the document directory and could potentially allow them access to portions of your file system where you really don't want people poking around. |
| *FollowSymLinks* | CGI programs are permitted in this directory, even if it isn't a directory defined in the *ScriptAlias* directive. |
| *ExecCGI* | This is part of the *mod_negotiation* module. When a client requests a document that can't be found, the server tries to figure out which document best suits the client's requirements. See http://localhost/manuals/mod/mod_negotiation.html for your local copy of the Apache documentation. |
| *MultiViews* | |

> **NOTE**
> These directives also affect all subdirectories of the specified directory.

### AllowOverride Directives

The *AllowOverride* directives specify which configuration options *.htaccess* files can override. You can set this directive individually for each directory. For example, you can have different standards about what can be overridden in the main document root and in *UserDir* directories. This capability is particularly useful for user directories, where the user doesn't have access to the main server configuration files.

*AllowOverride* can be set to *All* or any combination of *Options*, *FileInfo*, *AuthConfig*, and *Limit*. These options are explained in Table 21.3.

| Switch | Description |
| :--- | :--- |
| **Options** | The `.htaccess` file can add options not listed in the Options directive for this directory. |
| **FileInfo**<br>**AuthConfig** | The `.htaccess` file can include directives for modifying document type information. The .htaccess file might contain authorization directives. |
| **Limit** | The .htaccess file might contain allow, deny, and order directives. |

## File System Authentication and Access Control

You're likely to include material on your website that isn't supposed to be available to the public. You must be able to lock out this material from public access and provide designated users with the means to unlock the material. Apache provides two methods for accomplishing this type of access: authentication and authorization. You can use different criteria to control access to sections of your website, including checking the client's IP address or hostname, or requiring a username and password. This section briefly covers some of these methods.

> **CAUTION**
> Allowing individual users to put web content on your server poses several important security risks. If you're operating a web server on the Internet rather than on a private network, you should read the WWW Security FAQ at http://www.w3.org/Security/Faq/www-security-faq.html.

### Restricting Access with allow and deny

One of the simplest ways to limit access to website material is to restrict access to a specific group of users, based on IP addresses or hostnames. Apache uses the allow and deny directives to accomplish this.

Both directives take an address expression as a parameter. The following list provides the possible values and use of the address expression:

- all can be used to affect all hosts.
- A hostname or domain name, which can either be a partially or a fully qualified domain name; for example, test.gnuiix.org or gnuiix.org.
- An IP address, which can be either full or partial; for example, 212.85.67 or 212.85.67.66.
- A network/netmask pair, such as 212.85.67.0/255.255.255.0.
- A network address specified in classless inter-domain routing (CIDR) format; for example, 212.85.67.0/24. This is the CIDR notation for the same network and netmask that were used in the previous example.
