
## Cross-Reference

The “Configuring Modules and Related Services (/etc/httpd/conf.d\*.conf)” section, later in this chapter, describes some of the configuration files in the `conf.d` directory that may interest you.

## Choosing the server’s user and group

The `httpd` daemon doesn’t have to run as the root user; the fact that it doesn’t **run** as root by default makes your system more secure. By setting **User** and **Group** entries, you can have the `httpd` daemon run using the permissions associated with a different user and group:

```
User apache
Group apache
```

By default, **apache** is defined as both the user and group for the server. If you change the **User** and **Group** directives, you should specify a nonprivileged entity. Doing so minimizes the risk of damage if your site is compromised. The first daemon process that is started runs as root. This is necessary to bind the server to a low-numbered port and to switch to the user and group specified by the **User** and **Group** directives. All other processes run under the user ID (UID) and group ID (GID) defined by those directives.

## Setting the main server’s configuration

The second section of the `httpd.conf` file relates to directives handled by your main server (the one defined by the **ServerName** directive). In other words, these values are used by the default server and for all virtual hosts, unless they are explicitly changed for a virtual host. To change the same directives for particular virtual hosts, add them within virtual host containers.

## Setting an e-mail address

You can identify an address where users can send e-mail if they encounter a problem with your server. This is done with the **ServerAdmin** directive:

```
ServerAdmin you@your.address
```

The **ServerAdmin** directive can be set to any valid e-mail address. The default is `root@localhost`.

## Setting the server name

If your server name is anything but your exact registered host or domain name, you should identify your server name here. As the comments point out, the **ServerName** directive can be set to a value other than the actual hostname of your machine. However, this other name should still point to your machine in DNS if the server is to be a public Internet server. Frequently, `www` is just an alias for the real name of the machine (for example, a machine may respond to `www.linuxtoys.net`, but its real name may be `al.linuxtoys.net`).

```
ServerName jukebox.linuxtoys.net
```

Apache tries to use your hostname as the *ServerName* if you don't enter a valid server name. I recommend that you explicitly enter a *ServerName* here.

## Setting canonical names

There may be times when you need to configure how the server determines its own name and port. To do this, you can alter the `UseCanonicalName` directive to create a self-referencing URL. This allows Apache to use the hostname and port specified to construct the canonical name for the server. The value resulting from `UseCanonicalName` is used in all self-referential URLs and for the values of `SERVER_NAME` and `SERVER_PORT` in CGI. You can set the `UseCanonicalName` directive to `On`, `Off`, or `DNS`.

To allow Apache to form self-referential URLs using the hostname and port, set the `UseCanonicalName` directive as follows:

```
UseCanonicalName Off
```

Using the `UseCanonicalName` directive can make the names that identify the server more consistent. When the directive is set to `On`, Apache uses `ServerName` and `Port` directives to create URLs that reference files on the same machine (for example, `http://www.linuxtoys.net/docs/`). When `UseCanonicalName` is set to `Off`, the URL consists of whatever the client specified (for example, the URL could be `http://abc.linuxtoys.net/docs/` or `http://abc/docs/` if the client is within the same domain).

This can be problematic, particularly when access-control rules require username and password authentication: If the client is authenticated for the host `abc.linuxtoys.net` but a link sends him or her to `www.linuxtoys.net` (physically the same machine), the client will be prompted to enter a username and password again. I recommend that `UseCanonicalName` be set to `On` so that in a situation like the one just described, the authentication would not need to be repeated because any reference to the same server would always be interpreted as `www.linuxtoys.net`.

The last option, `UseCanonicalName DNS`, can be configured when you want to deploy a virtual hosting environment to support older clients that do not provide a `Host:` header. With this option Apache does a reverse DNS lookup on the server's IP address that the client connected to in order to figure out self-referential URLs.

## Identifying HTTP content directories

There are several directives for determining the location of your server's Web content. The main location for your Web content is set to `/var/www/html` by the `DocumentRoot` directive. Notice that the trailing slash is not used on the path name.

```
DocumentRoot "/var/www/html"
```

(Note that this location has changed from early versions of Red Hat Linux. The location was formerly `/home/http`. Moving the Web content out of `/home` has helped keep user directories in `/home` separate from system files.)

## Setting access options and overrides

You can set individual access permissions for each directory in the Web server’s directory structure. The default (following) is fairly restrictive.

```
<Directory />
   Options FollowSymLinks
   AllowOverride None
</Directory>
```

This segment sets up a default block of permissions for the `Options` and `AllowOverride` directives. The `<Directory />...</Directory>` tags enclose the directives that are to be applied to the `/` directory (which is `/var/www/html` by default, as defined by `DocumentRoot`).

The `Options FollowSymLinks` directive instructs the server that symbolic links within the directory can be followed to allow content that resides in other locations on the computer. None of the other special server features will be active in the `/` directory, or in any directory below that, without being explicitly specified later. Next, the following access options are specifically set for the root of your Web server (`/var/www/html`). (I removed the comments here for clarity.)

```
<Directory "/var/www/html">
   Options Indexes FollowSymLinks
   AllowOverride None
   Order allow,deny
   Allow from all
</Directory>
```

If you have changed the value of `DocumentRoot` earlier in this file, you need to change `/var/www/html` to match that value. The `Options` set for the directory are `Indexes` and `FollowSymLinks`. Those and other special server features are described in Table 20-2. The `AllowOverride None` directive instructs the server that an `.htaccess` file (or the value of `AccessFileName`) cannot override any of the special access features. You can replace `None` with any of the special access features described in Table 20-3.

## Table 20-2: Special Server Features for the Options Directive

| Feature | Description |
| --- | --- |
| ExecCGI | The execution of CGI scripts is permitted. |
| FollowSymLinks | The server will traverse symbolic links. |
| Includes | Server-Side Includes are permitted. |
| IncludesNOEXEC | Server-Side Includes are permitted, except the #exec element. |
| Indexes | If none of the files specified in the DirectoryIndex directive exists, a directory index will be generated by mod_autoindex. |
| MultiViews | The server allows content negotation based on preferences from the user’s browser, such as preferred language, character set, and media type. |
| SymLinksIfOwnerMatch | The server will traverse symbolic links only if the owner of the target is the same as the owner of the link. |
| None | None of the features above are enabled. |
| All | All the features above are enabled, with the exception of MultiViews. This must be explicitly enabled. |

## Table 20-3: Special Access Features for the AllowOverride Directive

| Feature | Description |
|---|---|
| AuthConfig | Enables authentication-related directives (AuthName, AuthType, AuthUserFile, AuthGroupFile, Require, and so on). |
| FileInfo | Enables MIME-related directives (AddType, AddEncoding, AddLanguage, LanguagePriority, and so on). |
| Indexes | Enables directives related to directory indexing (FancyIndexing, DirectoryIndex, IndexOptions, IndexIgnore, HeaderName, ReadmeName, AddIcon, AddDescription, and so on). |
| Limit | Enables directives controlling host access (Allow, Deny, and Order). |
| Options | Enables the Options directive (as described in Table 20-2). |

> NOTE: Remember that unless you specifically enable a feature described in Tables 20-2 and 20-3, that feature is not enabled for your server (with the exceptions of Indexes and FollowSymLinks).

## Identifying user directories

If you have multiple users on your server and you want them to be able to publish their own Web content, it is common practice to identify a directory name that users can create in their own home directories to store that content. When you identify the name that is appended to a user’s home directory, that directory is used to respond to requests to the server for the user’s
