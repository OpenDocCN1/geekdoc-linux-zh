# Global Server Options

The global server options control how the server interacts with the network and the host machine. Also, many options are available to control the performance of the server.

The directives for these options are in the file `httpd.conf`.

# Changing Server Configuration Files

If, for one reason or another, you need to change the names or locations of the server configuration files, you can do so using the `ServerRoot`, `ResourceConfig`, `AccessConfig`, `TypesConfig`, and `MIMEMagicFile` directives.

The `ServerRoot` directive specifies a base directory for Apache. Any filenames that are specified with the other directives, and do not start with a slash, are appended to the ServerRoot path. This makes it possible to leave all the other filenames alone and just switch the server to use another configuration directory. The default value for ServerRoot is `/usr/local/apache`, but this is commonly reconfigured by distributions to `/home/httpd` (Red Hat/OpenLinux) or `/var/www` (Debian).

The most common reason to change the configuration filenames is when you are running more than one Web server. Obviously, the configuration of the servers must be different for the Web servers to respond on different addresses and serve different documents. You can decide whether you want to keep all the configuration files in one directory and change the names for each set, or whether you just want to make another directory (for example, `/usr/local/apache2/conf`), keep all the filenames the same, and change the value of ServerRoot.

The following list shows the default values for the other configuration file directives:

+   - `ResourceConfig`—`conf/srm.conf`
+   - `AccessConfig`—`conf/access.conf`
+   - `TypesConfig`—`conf/mime.types`
+   - `MIMEMagicFile`—`conf/magic`

If you use these directives, place them in the `httpd.conf` file. For example, to change the name of the access configuration file, edit `httpd.conf` and add a line such as the following:

```
AccessConfig conf/myaccess.conf
```

> **Note**
> 
> Note that `srm.conf` and `access.conf` are generally no longer used, and all configuration directives are placed in `httpd.conf`. It is still legal to split the directives into these three files.

# Changing the Address of the Server

Three directives are used to control the address of the server. Often, your machine has only one IP address, and you use that address with the server. If you have multiple IP addresses, you might want the Web server to respond to requests on any of the machine’s addresses. In these cases you can leave the configuration of the address for your server alone.