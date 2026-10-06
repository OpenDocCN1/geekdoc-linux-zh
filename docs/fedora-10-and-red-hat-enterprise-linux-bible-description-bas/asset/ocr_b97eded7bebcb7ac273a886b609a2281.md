# Part IV: Fedora and RHEL Network and Server Setup

```
# by the client. When "On", Apache will use the value of the
# ServerName directive.
#nUseCanonicalName Off
```

The UseCanonicalName directive provides a form of naming consistency. When it is set to
On, Apache uses the ServerName and Port directives to create a URL that references a file
on the same machine (for example, http://www.linuxtoys.net/docs/). When
UseCanonicalName is Off, the URL consists of whatever the client specified (for example,
the URL could be http://al.linuxtoys.net/docs/ or http://al/docs/ if the
client is within the same domain).

This can be problematic; when access-control rules require username and
password authentication: if the client is authenticated for host.linuxtoys.net but a
link sends him or her to www.linuxtoys.net (physically the same machine), the client will
be prompted to enter a username and password. It is recommended that
UseCanonicalName be set to On. In the preceding situation, the authentication would not
need to be repeated because the same server would be interpreted as
www.linuxtoys.net.

# Identifying HTTP content directories

There are several directives for determining the location of your server's content. The
main location for your web content is set to /var/www/html by the DocumentRoot
directive. Note that the trailing slash is not on the path name.

> (Note that location has changed from early versions of Red Linux. The location was
formerly in /home/http.)

```
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from the directory, and
# symbolic links and aliases may be used to point to other locations.
DocumentRoot "/var/www/html"
```

# Setting access options and overrides

You can set access permissions for each directory in the web server's directory
structure. The default is fairly restrictive. Here is the default:

```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

This segment up a default block of permissions for the Options and AllowOverride
directives. The <Directory /...</Directory> tags enclose the directives that are to
be applied to the directory (which is /var/www/html by default, as defined by
DocumentRoot).