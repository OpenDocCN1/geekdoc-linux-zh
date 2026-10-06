# Common Configuration Options

The default configuration settings work fine right out of the box, and for basic needs, they may require no further modification. Nevertheless, site administrators may need to customize their web server and/or web sites further.

This section discusses some of the common directives or options that are used in Apache's configuration file.

# ServerRoot

This is used for specifying the base configuration directory for the web server. On Fedora, RHEL, and CentOS distributions, this value, by default, is the /etc/httpd directory. The default value for this in Ubuntu, openSUSE, and Debian Linux distributions is /etc/apache2/

```
Syntax: ServerRoot directory-path
```

# Listen

This is the port(s) on which the web server listens for connection requests. It refers to the venerable port 80 (HTTP ) for everything good and bad on the web is well known!

The Listen can also be used to specify the particular IP addresses over which web server accepts connections. The default value for this is 80 for nonsecure web communications.

```
Syntax: Listen [IP-address:] portnumber
```

For example, to set Apache to listen on its IPv4 and IPv6 interfaces on port 80, you would set the Listen directive to read

```
Listen 80
```

To set Apache to listen on a specific IPv6 interface (such as 2002:c0a8:1::) on port 8080, you would set the Listen directive to read

```
Listen [2002:c0a8:1::]:8080
```

Debian-like systems such as Ubuntu, this default is outside of the /etc/apache2/ports.conf file. The value is usually set in

# ServerName

This directive defines the hostname and port that the server uses to identify itself. At many sites, a single (normally underutilized) server may fulfill multiple purposes and host several services. For example, an intranet web server that isn't getting heavy usage, in a situation, a computer name as “www” (fully qualified domain name, or FQDN=www.example.org) wouldn’t be a good choice, because it suggests that the machine has only one purpose.