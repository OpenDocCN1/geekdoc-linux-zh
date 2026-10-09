I discuss both types of information in the following sections.

# ## Accessing configuration information with mod_info

System configuration information can be accessed via the `mod_info` module. This module provides a comprehensive overview of the server configuration, including all installed modules and directives in the configuration files. This module is contained in the `mod_info.c` file. It is not compiled into the server by default. You have to compile it using the `--enable-info` option with the `configure` script. For example:

```
```
./configure --prefix=/usr/local/apache \
            --with-mpm=prefork \
            --enable-info
```
```

This command configures Apache to be installed on `/usr/local/apache` directory, configures the source to run as a preforking server, and enables the `mod_info` module. Run `make` and `make install` to compile and install the newly built Apache server.

After you have installed this module in the server, you can view server configuration information via the Web by adding the following configuration to the `httpd.conf` file:

```
```
<Location /server-info>
    SetHandler server-info
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1 .domain.com
</Location>
```
```

This allows the localhost (`127.0.0.1`) and every host on your domain to access the server information. Do not forget to replace the `.domain.com` with your top-level domain name. For example, if your Web site is `www.nitec.com`, you need to add:

```
```
Allow from 127.0.0.1 .nitec.com
```
```

The dot in front of the domain name enables any host in the domain to access the server information. However, if you wish to limit this to a single host called `sysadmin.domain.com`, then change the Allow from line to:

```
```
Allow from 127.0.0.1 sysadmin.domain.com
```
```

After the server is configured and restarted, the server information is obtained from the localhost (that is, running a Web browser such as lynx on the server itself) by accessing `http://localhost/server-info`.