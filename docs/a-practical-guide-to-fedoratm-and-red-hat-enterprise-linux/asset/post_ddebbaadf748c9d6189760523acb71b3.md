
## Include
IncludeOptional

Loads directives from files.

`Include \ IncludeOptional` *filename* \ *directory*

where *filename* is the relative pathname of a file that contains directives. Apache prepends ServerRoot (page 955) to *filename*. The directives in *filename* are included in the file holding this directive at the location of the directive. Because *filename* can include wildcards, it can specify more than one file.

The *directory* is the relative pathname that specifies the root of a directory hierarchy that holds files containing directives. Apache prepends ServerRoot to *directory*. The directives in ordinary files in this hierarchy are included in the file holding this directive at the location of the directive. The *directory* can include wildcards.

Whereas Include displays an error when wildcards do not match a file or directory, IncludeOptional does not display an error when there is no match for a wildcard.

The Apache installer puts configuration files for modules, which have a filename extension of conf, in the conf.d and conf.modules.d directories within the ServerRoot directory. The Include directives in the Fedora/RHEL httpd.conf file incorporate module configuration files for whichever modules are installed.

- Contexts: server config, virtual host, directory
- Default: none
- Fedora/RHEL: conf.d/\*.conf conf.modules.d/\*.conf

## LoadModule

Loads a module.

`LoadModule` *module* *filename*

where *module* is the name of an external DSO module and *filename* is the relative pathname of the named module. Apache prepends ServerRoot (page 955) to *filename* and loads the external module specified by this directive. For more information refer to “Modules” on page 968.

- Context: server config
- Default: none; nothing is loaded by default if this directive is omitted
- Fedora/RHEL: loads many modules; refer to the configuration files

## Options

Controls server features by directory.

`Options` [+] *option* [!] *option* ...]

This directive controls which server features are enabled for a directory hierarchy. The directory hierarchy is specified by the container this directive appears in. A + or the absence of a – turns an option on, and a – turns it off.

The *option* might be one of the following:

- **None**—None of the features this directive can control are enabled.
- **All**—All of the features this directive can control are enabled, except for MultiViews, which you must explicitly enable.
- **ExecCGI**—Apache can execute CGI scripts (page 969).
- **FollowSymLinks**—Apache follows symbolic links.
- **Includes**—Permits SSI (server-side includes). SSI is are containers embedded in HTML pages that are evaluated on the server before the context is passed to the client.
- **IncludesNOEXEC**—The same as Includes but disables the #exec and #exec cgi commands that are part of SSI. Does not prevent the #include command from referencing CGI scripts.
- **Indexes**—Generates a directory listing if DirectoryIndex (page 944) is not set.
- **MultiViews**—Allows MultiViews (page 963).
- **SymLinksIfOwnerMatch**—The same as FollowSymLinks but follows the link only if the file or directory being pointed to has the same owner as the link.

The following Options directive from the Fedora/RHEL httpd.conf file sets the Indexes and FollowSymLinks options and, because the <Directory> container specifies the /var/www/html directory hierarchy (the document root), affects all content. The AllowOverride None directive causes Apache to ignore directives in .htaccess files (page 960).

```
<Directory "/var/www/html">
    Options Indexes FollowSymLinks
    AllowOverride None
</Directory>
```

- Context: directory
- Default: All
- Fedora/RHEL: Indexes, FollowSymLinks

## ScriptAlias
Maps a URL to a directory or file and declares the target to be a server (CGI) script.

```
ScriptAlias alias pathname
```

where alias must match part of the URL the client requested to invoke the ScriptAlias. The pathname is the absolute pathname of the target of the alias, usually a directory. Similar to the Alias directive, this directive specifies that the target is a CGI script (page 969).

The following ScriptAlias directive from the Fedora/RHEL httpd.conf file maps client requests that include /cgi-bin/ to the /var/www/cgi-bin directory (and indicates that these requests will be treated as CGI requests):

```
ScriptAlias /cgibin/ "/var/www/cgi-bin/"
```

- Contexts: server config, virtual host
- Default: none
- Fedora/RHEL: /cgi-bin/ "/var/www/cgi-bin"

## User
*Sets the UID of the processes that run the servers.*
*User* **#userid** \| *username*

where **#userid** is a UID value, preceded by #, and *username* is the name of a local user. The processes that Apache spawns are run as the user specified by this directive.

Apache must start with **root** privileges to listen on a privileged port. For reasons of security, Apache’s child processes (servers) run as nonprivileged users. The default UID of −1 does not map to a user under Fedora/RHEL. Instead, the Fedora/RHEL **httpd** package creates a user named **apache** during installation and sets User to that user.

- Context: server config
- Default: #−1
- Fedora/RHEL: apache

**Do not set User to root or 0**

**security** For a more secure system, do not set User to **root** or **0** (zero) and do not allow the **apache** user to have write access to the DocumentRoot directory hierarchy (except as needed for storing data), especially not to configuration files.

# SECURITY DIRECTIVES

## Allow
*Specifies which clients can access specified content.*
*Allow* from *All* \| *host* [**host** ...] \| *env*=*var* [**env**=*var* ...]

This directive, which must be written as **Allow from**, grants access to a directory hierarchy to the specified clients. The directory hierarchy is specified by the container or .htaccess file this directive appears in. See the Order directive (page 961) for an example.

- **All**—Serves content to any client.
- **host**: Serves content to the client(s) specified by *host*, which can take several forms: an FQDN, a partial domain name (such as *example.com*), an IP address, a partial IP address, or a network/netmask pair.
- **var**: Serves content when the environment variable named *var* is set. You can set a variable with the SetEnvIf directive.

- Contexts: **directory**, .htaccess
- Default: none; default behavior depends on the Order directive
- Fedora/RHEL: none

## AllowOverride
*Specifies whether Apache examines .htaccess files and which classes of directives in those files it processes.*

AllowOverride All | None | *directive-class* [*directive-class* ...]

This directive specifies whether Apache examines .htaccess files in the directory hierarchy specified by its container. If Apache does examine .htaccess files, this directive specifies which classes of directives within .htaccess files Apache processes. See the tip on page 973 for performance considerations.

- **All**—Processes all classes of directives in .htaccess files.
- **None**—Ignores directives in .htaccess files. However, Apache will still serve the content of .htaccess files, possibly exposing sensitive information. This choice does not affect .htpasswd files. The example in the description of the <Files> container (page 947) shows how to prevent Apache from serving the content of files whose names begin with .ht.

The *directive-class* is one of the following directive class identifiers:

- **AuthConfig**—Class of directives that control authorization (AuthName, AuthType, Require, and so on). This class is used mostly in .htaccess files to require a username and password to access the content. For more information refer to “Authentication Modules and .htaccess Files” on page 972.
- **FileInfo**—Class of directives that controls document types (DefaultType, ErrorDocument, SetHandler, and so on).
- **Indexes**—Class of directives relating to directory indexing (DirectoryIndex, FancyIndexing, IndexOptions, and so on).
- **Limit**—Class of client-access directives (Allow, Deny, and Order).
- **Options**—Class of directives controlling directory features.

- Context: **directory**
- Default: **All**
- Fedora/RHEL: **None**

## Deny
*Specifies which clients are not allowed to access specified content.*

Deny from All | *host* [*host* ...] | *env*=*var* [*env*=*var* ...]

This directive, which must be written as Deny from, denies access to a directory hierarchy to the specified clients. The directory hierarchy is specified by the container or .htaccess file this directive appears in. See the Order directive (next) for an example.

- **All**—Denies content to all clients.
- **host**: Denies content to the client(s) specified by *host*, which can take several forms: an FQDN, a partial domain name (such as example.com), an IP address, a partial IP address, or a network/netmask pair.
