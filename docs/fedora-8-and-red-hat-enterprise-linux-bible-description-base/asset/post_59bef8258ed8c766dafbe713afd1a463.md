
## Table of HTTP Modules

| Module | Description |
| :--- | :--- |
| mod_negotiation | Provides for the conditional display of documents based on the Content-Encoding, Content-Language, Content-Length, and Content-Type HTTP header fields. |
| mod_proxy | Implements an HTTP 1.1 proxy/gateway server. |
| mod_proxy_ajp | Uses mod_proxy to provide support for Apache JServ Protocol (version 1.3). |
| mod_proxy_balancer | Extension to mod_proxy to handle load balancing. |
| mod_proxy_connect | Extension to mod_proxy to handle CONNECT requests. |
| mod_proxy_ftp | Extension to mod_proxy to handle FTP requests. |
| mod_proxy_http | Extension to mod_proxy to handle HTTP requests. |
| mod_rewrite | Provides a flexible and extensible method for redirecting client requests and mapping incoming URLs to other locations in the file system. |
| mod_setenvif | Conditionally sets environment variables based on the contents of various HTTP header fields. |
| mod_speling | Attempts to correct misspellings automatically in requested URLs. |
| mod_ssl | Implements cryptography using SSL and TLS protocols. |
| mod_status | Provides a summary of the activities of each individual httpd server process, including CPU and bandwidth usage levels. |
| mod_suexec | Lets CGI scripts run with permission of a particular user or group. |
| mod_unique_id | Assigns the UNIQUE_ID environment variable to provide a unique identifier for each request. |
| mod_userdir | Specifies locations that can contain individual users' HTML documents. |
| mod_usertrack | Uses cookies to track the progress of users through a Web site. |
| mod_version | Allows you to use `<IFVersion>` containers to allow version-dependent configuration. |
| mod_vhost_alias | Contains support for dynamically configured mass virtual hosting. |

More information about each module (and the directives that can be defined within it) can be found on your server at `http://localhost/manual/mod/`.

### Including module-specific configuration files

The following lines cause Apache to load configuration files from the `/etc/httpd/conf.d` directory. This directory contains configuration files associated with specific modules.

```
#
# Load config files from the config directory "/etc/httpd/conf.d".
#
Include conf.d/*.conf
```

> **CROSS-REFERENCE:** The "Configuring modules and related services (\etc/httpd/conf.d/\*.conf\*)" section, later in this chapter, describes some of the configuration files in the `conf.d` directory that may interest you.

### Choosing the server's user and group

The `httpd` daemon doesn't have to run as the *root* user; the fact that it doesn't run as *root* by default makes your system more secure. By setting *User* and *Group* entries, you can have the `httpd` daemon run using the permissions associated with a different user and group:

```
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.
#
# User/Group: The name (or #number) of the user/group to run httpd as.
#  . On SCO (ODT 3) use "User nouser" and "Group nogroup".
#  . On HP-UX you may not be able to use shared memory as nobody, and
#    the suggested workaround is to create a user www and use that user.
# NOTE that some kernels refuse to setgid(Group) or setuid(IPC_SET)
# when the value of (unsigned)Group is above 60000;
# don't use Group #-1 on these systems!
#
User apache
Group apache
```

By default, *apache* is defined as both the user and group for the server. If you change the *User* and *Group* directives, you should specify a nonprivileged entity. This minimizes the risk of damage if your site is compromised. The first daemon process that is started runs as *root*. This is necessary to bind the server to a low-numbered port and to switch to the user and group specified by the *User* and *Group* directives. All other processes run under the user ID (UID) and group ID (GID) defined by those directives.

### Setting the main server's configuration

The second section of the `httpd.conf` file relates to directives handled by your main server (the one defined by the *ServerName* directive). In other words, these values are used by the default server and for all virtual hosts, unless they are explicitly changed for a virtual host. To change the same directives for particular virtual hosts, add them within virtual host containers.

### Setting an e-mail address

You can identify an address where users can send e-mail if there is a problem with your server. This is done with the `ServerAdmin` directive:

```
# ServerAdmin: your address, where problems with the server should be
# e-mailed.  This address appears on some server-generated pages, such
# as error documents. e.g. admin@your-domain.com
#
ServerAdmin you@your.address
```

The `ServerAdmin` directive can be set to any valid e-mail address. The default is `root@localhost`.

### Setting the server name

If your server name is anything but your exact registered host or domain name, you should identify your server name here. As the comments point out, the `ServerName` directive can be set to a value other than the actual hostname of your machine. However, this other name should still point to your machine in DNS if the server is to be a public Internet server. Frequently, www is just an alias for the real name of the machine (for example, a machine may respond to `www.linuxtoys.net`, but its real name may be `al.linuxtoys.net`).

```
ServerName jukebox.linuxtoys.net
```

Apache tries to use your hostname as the `ServerName`, if you don’t enter a valid server name. It is recommended that you explicitly enter a `ServerName` here.

### Setting canonical names

Use the `UseCanonicalName` directive to create a self-referencing URL, as follows:

```
# UseCanonicalName: Determines how Apache constructs self-referencing
# URLs and the SERVER_NAME and SERVER_PORT variables.
# When set "Off", Apache will use the Hostname and Port supplied
# by the client.  When set "On", Apache will use the value of the
# ServerName directive.
#
UseCanonicalName Off
```

The `UseCanonicalName` directive provides a form of naming consistency. When it is set to On, Apache uses the `ServerName` and `Port` directives to create a URL that references a file on the same machine (for example, `http://www.linuxtoys.net/docs/`). When `UseCanonicalName` is `Off`, the URL consists of whatever the client specified (for example, the URL could be `http://al.linuxtoys.net/docs/` or `http://al/docs/` if the client is within the same domain).

This can be problematic, particularly when access-control rules require username and password authentication: if the client is authenticated for the host `al.linuxtoys.net` but a link sends him or her to `www.linuxtoys.net` (physically the same machine), the client will be prompted to enter a username and password again. It is recommended that `UseCanonicalName` be set to `On`. In the preceding situation, the authentication would not need to be repeated because any reference to the same server would always be interpreted as `www.linuxtoys.net`.

### Identifying HTTP content directories

There are several directives for determining the location of your server's Web content. The main location for your Web content is set to `/var/www/html` by the `DocumentRoot` directive. (Note that this location has changed from early versions of Red Hat Linux. The location was formerly in `/home/httpd`.)

```
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from the directory, but
# symbolic links and aliases may be used to point to other locations.
DocumentRoot "/var/www/html"
```

### Setting access options and overrides

You can set individual access permissions for each directory in the Web server's directory structure. The default is fairly restrictive. Here is the default:

```
<Directory />
   Options FollowSymLinks
        AllowOverride None
</Directory>
```

This segment sets up a default block of permissions for the `Options` and `AllowOverride` directives. The `<Directory />` … `</Directory>` tags enclose the directives that are to be applied to the `/` directory (which is `/var/www/html` by default, as defined by `DocumentRoot`).

The `Options FollowSymLinks` directive instructs the server that symbolic links within the directory can be followed to allow content that resides in other locations on the computer. None of the other special server features will be active in the `/` directory, or in any directory below that, without being explicitly specified later. Next, the following access options are specifically set for the root of your Web server (`/var/www/html`). (I removed the comments here for clarity.)

```
<Directory "/var/www/html">
   Options Indexes FollowSymLinks
        AllowOverride None
        Order allow,deny
        Allow from all
</Directory>
```

If you have changed the value of `DocumentRoot` earlier in this file, you need to change the `/var/www/html` to match that value. The `Options` set for the directory are `Indexes` and `FollowSymLinks`. Those and other special server features are described in Table 21-2. The
