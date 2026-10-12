+   • **ServerTokens OS** – provides the following information:

```
Apache/2.0.41 (Unix)
```

It is recommended to use the **ServerTokens Prod** option so that a possible attacker does not gain any valuable information about your system.

![](bbox=[0.09, 0.192, 0.16, 0.292])

# IMPORTANT

Do not remove the **IncludeNoExec** directive. By default, the **Server-Side Includes (SSI)** module cannot execute commands. It is recommended that you do not change this setting unless absolutely necessary, as it could, potentially, enable an attacker to execute commands on the system.

# Removing httpd Modules

In certain scenarios, it is beneficial to remove certain **httpd** modules to limit the functionality of the HTTP Server. To do so, edit configuration files in the `/etc/httpd/conf.modules.d` directory. For example, to remove the proxy module:

```
echo '# All proxy modules disabled' > /etc/httpd/conf.modules.d/00-proxy.conf
```

Note that the `/etc/httpd/conf.d/` directory contains configuration files which are used to load modules as well.

# httpd and SELinux

For information, see the The Apache HTTP Server and SELinux chapter from the Red Hat Enterprise Linux 7 SELinux User's and Administrator's Guide.

# 4.3.8.2. Securing NGINX

NGINX is a high-performance HTTP and proxy server. This section briefly documents additional steps that harden your NGINX configuration. Perform all of the following configuration changes in the **server** section of your NGINX configuration files.

# Disabling Version Strings

To prevent attackers from learning the version of NGINX running on your server, use the following configuration option:

```
server_tokens    off;
```

This has the effect of removing the version number and simply reporting the string **nginx** in all requests served by NGINX:

```
$ curl -sI http://localhost | grep Server
Server: nginx
```

# Including Additional Security-Related Headers

Each request served by NGINX can include additional HTTP headers that mitigate certain known web application vulnerabilities: