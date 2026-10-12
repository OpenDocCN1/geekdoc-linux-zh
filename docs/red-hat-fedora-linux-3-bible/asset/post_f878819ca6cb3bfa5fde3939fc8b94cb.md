
## The `ServerAdmin` Directive

The `ServerAdmin` directive can be set to any valid e-mail address. The default is `root@localhost`.

## Setting the server name

If your server name is anything but your exact registered host or domain name, you should identify your server name here. As the comments point out, the `ServerName` directive can be set to a value other than the actual host name of your machine. However, this other name should still point to the machine in DNS if the server is to be a public Internet server. Frequently, **www** is just an alias for the real name of the machine (for example, a machine may respond to `www.linuxtoys.net`, but its real name may be `al.linuxtoys.net`).

```
ServerName juicebox.linuxtoys.net
```

Apache tries to use your host name as the `ServerName` if you don't enter a valid server name. It is recommended that you explicitly enter a `ServerName` here.

## Setting canonical names

Use the `UseCanonicalName` directive to create a self-referencing URL, as follows:

```
# UseCanonicalName: Determines how Apache constructs self-referencing
# URLs and the SERVER_NAME and SERVER_PORT variables.
# When set "Off", Apache will use the Hostname and Port supplied
# by the client. When set "On", Apache will use the value of the
# ServerName directive.
#
UseCanonicalName Off
```

The `UseCanonicalName` directive provides a form of naming consistency. When it is set to **On**, Apache uses the `ServerName` and `Port` directives to create a URL that references a file on the same machine (for example, `http://www.linuxtoys.net/docs/`). When `UseCanonicalName` is **Off**, the URL consists of whatever the client specified (for example, the URL could be `http://al.linuxtoys.net/docs/` or `http://al/docs/` if the client is within the same domain).

This can be problematic, particularly when access-control rules require user name and password authentication: if the client is authenticated for the host `al.linuxtoys.net` but a link sends him or her to `www.linuxtoys.net` (physically the same machine), the client will be prompted to enter a user name and password again. It is recommended that `UseCanonicalName` be set to **On**. In the preceding situation, the authentication would not need to be repeated, because any reference to the same server would always be interpreted as `www.linuxtoys.net`.

## Identifying HTTP content directories

There are several directives for determining the location of your server's Web content. The main location for your Web content is set to `/var/www/html` by the `DocumentRoot` directive. (Note that this location has changed from versions of Red Hat Linux prior to Red Hat Linux 7. The location was formerly in /home/http.)

```
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from the directory, but
# symbolic links and aliases may be used to point to other locations.
DocumentRoot "/var/www/html"
```

## Setting access options and overrides

You can set individual access permissions for each directory in the Web server's directory structure. The default is fairly restrictive. Here is the default:

```
<Directory />
  Options FollowSymLinks
  AllowOverride None
</Directory>
```

This segment sets up a default block of permissions for the *Options* and *AllowOverride* directives. The `<Directory />…</Directory>` tags enclose the directives that are to be applied to the / directory (which is /var/www/html by default, as defined by *DocumentRoot*).

The *Options FollowSymLinks* directive instructs the server that symbolic links within the directory can be followed to allow content that resides in other locations on the computer. None of the other special server features will be active in the / directory, or in any directory below that, without being explicitly specified later. Next, the following access options are specifically set for the root of your Web server (/var/www/html). (I removed the comments here for clarity.)

```
<Directory "/var/www/html">
  Options Indexes FollowSymLinks
  AllowOverride None
  Order allow,deny
  Allow from all
</Directory>
```

If you have changed the value of *DocumentRoot* earlier in this file, you need to change the /var/www/html to match that value. The *Options* set for the directory are *Indexes* and *FollowSymLinks*. Those and other special server features are described in Table 21-2. The *AllowOverride None* directive instructs the server that an .htaccess file (or the value of *AccessFileName*) cannot override any of the special access features. You can replace *None* with any of the special access features described in Table 21-3.

> NOTE: Remember that unless you specifically enable a feature described in Tables 21-2 and 21-3, that feature is not enabled for your server (with the exceptions of *Indexes* and *FollowSymLinks*).

| Feature | Description |
|---|---|
| ExecCGI | The execution of CGI scripts is permitted. |
| FollowSymLinks | The server will traverse symbolic links. |
| Includes | Server-Side Includes are permitted. |
| IncludesNOEXEC | Server-Side Includes are permitted, except the #exec element. |
| Indexes | If none of the files specified in the DirectoryIndex directive exists, a directory index will be generated by mod_autoindex. |
| MultiViews | The server allows content negotiation based on preferences from the user's browser, such as preferred language, character set, and media type. |
| SymLinksIfOwnerMatch | The server will traverse symbolic links only if the owner of the target is the same as the owner of the link. |
| None | None of the features above are enabled. |
| All | All the features above are enabled, with the exception of MultiViews. This must be explicitly enabled. |

| Feature | Description |
|---|---|
| AuthConfig | Enables authentication-related directives (AuthName, AuthType, AuthUserFile, AuthGroupFile, Require, and so on). |
| FileInfo | Enables MIME-related directives (AddType, AddEncoding, AddLanguage, LanguagePriority, and so on). |
| Indexes | Enables directives related to directory indexing ( FancyIndexing, DirectoryIndex, IndexIgnore, HeaderName, AccessFileName, AddIcon, AddDescription, and so on). |
| Limit | Enables directives controlling host access (Allow, Deny, and Order). |
| Options | Enables the Options directive (as described in Table 21-5). |
| None | None of the access features above can be overridden. |
| All | All the access features above can be overridden. |

## Disabling indexes in root directory

The following directives disable indexing for the root directory (probably /var/www/html), so that your index.html, or the default one put there by the Fedora Project, is displayed when that directory is requested. (The default way of listing the contents of directories on your Apache Web server is defined in the “Defining Indexing” section later in this chapter.)

```
# # Disable autoindex for the root directory, and present a
# default Welcome page if no other index page is present.
#
<LocationMatch "\*/$">
    Options -Indexes
    ErrorDocument 403 /error/noindex.html
</LocationMatch>
```

## Identifying user directories

If you have multiple users on your server and you want each to be able to publish their own Web content, it is common practice to identify a directory name that users can create in their own home directories to store that content. When you identify the name that is appended to a user’s home directory, that directory is used to respond to requests to the server for the user’s name(~user). This directory name used to be set to public_html by default; however, it is now turned off by default.

To allow access to your users’ personal Web pages, add a comment character (#) to the UserDir disable line. Then remove the # from the UserDir public_html line to make users’ personal public_html directories accessible through the Web server. After removing extra comment lines, the following text shows what the enabled section looks like:

```
# UserDir: The name of the directory which is appended onto a user’s
# home directory if a ~user request is received.

<IfModule mod_userdir.c>
#  UserDir disable
    UserDir public_html
</IfModule>
```

Besides uncommenting the UserDir public_html line shown in the previous example, you must make both the user’s home directory and public_html directory executable by everyone in order for the UserDir directive to allow access to a particular user’s public_html directory. For example, the user cjb could type the following to make those directories accessible.

```
$ chmod 711 /home/cjb
$ mkdir /home/cjb/public_html
$ chmod 755 /home/cjb/public_html
```
