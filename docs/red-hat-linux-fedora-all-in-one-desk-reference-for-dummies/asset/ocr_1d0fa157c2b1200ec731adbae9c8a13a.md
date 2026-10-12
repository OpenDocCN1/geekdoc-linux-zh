server to respond to both `www.big.org` and `www.tiny.com` and serve a unique home page for each host name. A server with this capability is known as a *multi-homed* Web server, a *virtual* Web server, or a server with *virtual host support*.

As you might guess, Internet service providers (ISPs) use the virtual host feature of Apache Web server to offer virtual Web sites to their customers. You need the following to support virtual hosts:

+   - The Web server must be able to respond to multiple IP addresses (each with a unique domain name) and must enable you to specify document directories, log files, and other configuration items for each IP address.
+   - The host system must be able to associate multiple IP addresses with a single physical network interface. Red Hat Linux can do so.
+   - Each domain name associated with the IP address must be a unique, registered domain name with proper DNS entries.

For the latest information on how to set up virtual hosts in an Apache HTTP server, consult the following URL:

```
http://httpd.apache.org/docs-2.0/vhosts
```

The Apache HTTP server can respond to different host names with different home pages. You have two options when supporting virtual hosts:

+   - **Run multiple copies of the `httpd` program, one for each IP address.** In this case, you create a separate copy of the `httpd.conf` configuration file for each host and use the `Listen` directive to make the server respond to a specific IP address.
+   - **Run a single copy of the `httpd` program with a single `httpd.conf` file.** In the configuration file, set `Listen` to a port number only (so the server responds to any IP address associated with the host), and use the `VirtualHost` directive to configure the server for each virtual host.

Run multiple HTTP daemons only if you don’t expect heavy traffic on your system; the system may not be able to respond well because of the overhead associated with running multiple daemons. However, you may need multiple HTTP daemons if each virtual host has a unique configuration need for the following directives:

+   - `UserId` and `GroupId` (the user and group ID for the HTTP daemon)
+   - `ServerRoot` (the root directory of the server)
+   - `TypesConfig` (the MIME type configuration file)