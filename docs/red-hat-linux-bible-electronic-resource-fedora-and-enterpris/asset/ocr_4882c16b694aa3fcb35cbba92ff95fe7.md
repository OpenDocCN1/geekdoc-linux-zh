```
# . On SCO (ODT 3) use "User nouser" and "Group nogroup".
# . On HPUX you may not be able to use shared memory as nobody, and
# the suggested workaround is to create a user www and use that user.
# NOTE that some kernels refuse to setgid(Group) or semctl(IPC_SET)
# when the value of (unsigned)Group is above 60000;
# don't use Group #-1 on these systems!
#
User apache
Group apache
```

By default, apache is defined as both the user and group for the server. If you change the User and Group directives, you should specify a nonprivileged entity. This minimizes the risk of damage if your site is compromised. The first daemon process that is started runs as root. This is necessary to bind the server to a low-numbered port and to switch to the user and group specified by the User and Group directives. All other servers run under the user ID (UID) and group ID (GID) defined by those directives.

# Choosing the HTTP port number

Apache listens on particular ports for HTTP requests. The port that is used is set by the Port entry as follows:

```
#
# Port: The port to which the standalone server listens. For
# ports < 1023, you will need httpd to be run as root initially.
#
Port 80
```

Port 80 is the default for HTTP traffic, which is why http://www.apache.org:80/ is the same as http://www.apache.org/. If the server is bound to a different port, the port number must be specified in the URL. Most Web servers run on port 80, although they can accept connections on any port (below 65536) that is not already bound to a particular service (see the /etc/services file for a list of common services/protocols and the ports they use). Only root can run programs that listen for connections on privileged ports (those below 1024).

# Setting an e-mail address

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