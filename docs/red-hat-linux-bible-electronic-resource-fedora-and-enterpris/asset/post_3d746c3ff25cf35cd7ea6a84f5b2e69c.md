
# . On SCO (ODT 3) use "User nouser" and "Group nogroup".
# . On HPUX you may not be able to use shared memory as nobody, and
# the suggested workaround is to create a user www and use that user.
# NOTE that some kernels refuse to setgid(Group) or semctl(IPC_SET)
# when the value of (unsigned)Group is above 60000;
# don't use Group #-1 on these systems!
#

User apache
Group apache

By default, apache is defined as both the user and group for the server. If you change the User and Group directives, you should specify a nonprivileged entity. This minimizes the risk of damage if your site is compromised. The first daemon process that is started runs as root. This is necessary to bind the server to a low-numbered port and to switch to the user and group specified by the User and Group directives. All other servers run under the user ID (UID) and group ID (GID) defined by those directives.

## Choosing the HTTP port number

Apache listens on particular ports for HTTP requests. The port that is used is set by the Port entry as follows:

```
#
# Port: The port to which the standalone server listens. For
# ports < 1023, you will need httpd to be run as root initially.
#
Port 80
```

Port 80 is the default for HTTP traffic, which is why http://www.apache.org:80/ is the same as http://www.apache.org/. If the server is bound to a different port, the port number must be specified in the URL. Most Web servers run on port 80, although they can accept connections on any port (below 65536) that is not already bound to a particular service (see the /etc/services file for a list of common services/protocols and the ports they use). Only root can run programs that listen for connections on privileged ports (those below 1024).

## Setting an e-mail address

You can identify an address where users can send e-mail if there is a problem with your server. This is done with the ServerAdmin directive:

```
#
# ServerAdmin: Your address, where problems with the server should be
# e-mailed. This address appears on some server-generated pages, such
# as error documents.,e.g. admin@your-domain.com
#
ServerAdmin you@your.address
```

The ServerAdmin directive can be set to any valid e-mail address. It can direct mail to a user account (on the same or another machine) or redirect mail to an alias (such as Webmaster) that could distribute mail to several individuals. The default is root@localhost.

## Setting the server name

If your server name is anything but the exact registered host/domain name, you should identify your server name here. As the comments point out, the ServerName directive can be set to a value other than the actual host name of your machine. However, this other name should still refer to your machine in DNS if the server is to be a public Internet server. Frequently, www is just an alias for the real name of the machine (for example, a machine may respond to www.linuxtoys.net, but its real name may be al.linuxtoys.net).

```
ServerName jukebox.linuxtoys.net
```

Apache tries to use your host name as the ServerName if you don't enter a valid server name. It is recommended that you explicitly enter a ServerName here.

## Setting canonical names

Use the UseCanonicalName directive to create a self-referencing URL, as follows:

```
## UseCanonicalName: Determines how Apache constructs self-referencing
# URLs and the SERVER_NAME and SERVER_PORT variables.
# When set "Off", Apache will use the Hostname and Port supplied
# by the client.  When set "On", Apache will use the value of the
# ServerName directive.
#
UseCanonicalName Off
```

The UseCanonicalName directive provides a form of naming consistency. When it is set to on, Apache uses the ServerName and Port directives to create a URL that references a file on the same machine (for example, http://www.linuxtoys.net/docs/). When UseCanonicalName is Off, the URL consists of whatever the client specified (for example, the URL could be http://al.linuxtoys.net/docs/ or http://al/docs/ if the client is within the same domain).

This can be problematic, particularly when access-control rules require user name/password authentication: if the client is authenticated for the host al.linuxtoys.net but a link sends him or her to www.linuxtoys.net (physically the same machine), the client will be prompted to enter a user name and password again. It is recommended that UseCanonicalName be set to on. In the preceding situation, the authentication would not need to be repeated, as any reference to the same server would always be interpreted as www.linuxtoys.net.

## Identifying HTTP content directories

There are several directives for determining the location of your server's Web content. The main location for your Web content is set to /var/www/html by the DocumentRoot directive. (Note that this location has changed from versions of Red Hat Linux prior to Red Hat Linux 7. The location was formerly in /home/http.)

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

This segment sets up a default block of permissions for the Options and AllowOverride directives. The `<Directory />...</Directory>` tags enclose the directives that are to be applied to the / directory (which is /var/www/html by default).

The Options FollowSymLinks directive instructs the server that symbolic links within the directory can be followed to allow content that resides in other locations on the computer. None of the other special server features will be active in the / directory, or in any directory below that, without being explicitly specified later. Next, the following access options are specifically set for the root of your Web server (/var/www/html). (I removed the comments here for clarity.)

```
<Directory "/var/www/html">
    Options Indexes FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

If you have changed the value of DocumentRoot earlier in this file, you need to change the /var/www/html to match that value. The Options set for the directory are Indexes and FollowSymLinks. Those and other special server features are described in Table 21-2. The AllowOverride None directive instructs the server that the .htaccess file (or the value of AccessFileName) cannot override any of the special access features. You can replace None with any of the special access features described in Table 21-3.

> NOTE: Remember that unless you specifically enable a feature described in Tables 21-2 and 21-3, that feature is not enabled for your server (with the exceptions of Indexes and FollowSymLinks).

### Table 21-2: Special Server Features for the Options Directive

| Feature | Description |
| :--- | :--- |
| ExecCGI | The execution of CGI scripts is permitted. |
| FollowSymLinks | The server will traverse symbolic links. |
| Includes | Server-Side Includes are permitted. |
| IncludesNOEXEC | Server-Side Includes are permitted, except the #exec and #include elements. |
| Indexes | If none of the files specified in the DirectoryIndex directive exists, a directory index will be generated. |
| MultiViews | The server allows a content-based filename pattern-matching search. |
| SymLinksIfOwnerMatch | The server will traverse symbolic links only if the owner of the target is the same as the owner of the link. |
| None | None of the features above are enabled. |
| All | All the features above are enabled, with the exception of MultiViews. This must be explicitly enabled. |

### Table 21-3: Special Access Features for the AllowOverride Directive

| Feature | Description |
| :--- | :--- |
| AuthConfig | Enables authentication-related directives (AuthName, AuthType, AuthUserFile, AuthGroupFile, Require, and so on). |
| FileInfo | Enables MIME-related directives (AddType, AddEncoding, AddLanguage, LanguagePriority, and so on). |
| Indexes | Enables directives related to directory indexing (FancyIndexing, DirectoryIndex, IndexOptions, IndexIgnore, HeaderName, ReadmeName, AddIcon, AddDescription, and so on). |
| Limit | Enables directives controlling host access (Allow, Deny, and Order). |
| Options | Enables the Options directive (as described in Table 21-5). |
| None | None of the access features above can be overridden. |
| All | All the access features above can be overridden. |

## Disabling indexes in root directory

The following directives disable indexing for the root directory (probably /var/www/html), so that your index.html, or the default one put there by Apache, is displayed when that
