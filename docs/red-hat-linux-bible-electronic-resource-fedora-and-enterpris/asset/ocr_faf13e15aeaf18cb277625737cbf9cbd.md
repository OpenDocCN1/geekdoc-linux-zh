# Setting the server name

If your server name is anything but the exact registered host/domain name, you should identify your server name here. As the comments point out, the ServerName directive can be set to a value other than the actual host name of your machine. However, this other name should still refer to your machine in DNS if the server is to be a public Internet server. Frequently, www is just an alias for the real name of the machine (for example, a machine may respond to www.linuxtoys.net, but its real name may be al.linuxtoys.net).

```
ServerName jukebox.linuxtoys.net
```

Apache tries to use your host name as the ServerName if you don't enter a valid server name. It is recommended that you explicitly enter a ServerName here.

# Setting canonical names

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

# Identifying HTTP content directories

There are several directives for determining the location of your server's Web content. The main location for your Web content is set to /var/www/html by the DocumentRoot directive. (Note that this location has changed from versions of Red Hat Linux prior to Red Hat Linux 7. The location was formerly in /home/http.)

```
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from the directory, but
```