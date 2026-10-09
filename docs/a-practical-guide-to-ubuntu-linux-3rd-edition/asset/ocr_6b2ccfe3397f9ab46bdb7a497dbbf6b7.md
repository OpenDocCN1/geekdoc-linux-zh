and is enabled by default. Two of the most frequently used module binary files are `mod_perl` (part of the `libapache2-mod-perl2` package) and `mod_python` (part of the `libapache2-mod-python` metapackage). The `*.load` files in this directory load modules from the `/usr/lib/apache2/modules` directory (page 941). The `*.conf` files configure the modules for use. See page 905 for information on using `a2enmod` to enable a module.

+   - `/etc/apache2/mods-enabled`—Holds links to files in `mods-available`. Use `a2enmod` to create links and `a2dismod` to remove links (page 905).

Apache configuration files are kept in the `/etc/apache2` hierarchy:

+   - `/etc/apache2/apache2.conf`—Holds configuration directives. This file is the main Apache configuration file. You do not typically make changes to this file, but rather put any configuration directives in `httpd.conf` and other files.
+   
+   - `/etc/apache2/envvars`—Holds variables that modify the environment Apache runs in.
+   
+   - `/etc/apache2/ports.conf`—Holds the `Listen` directive (page 910), which controls which IP address(es) and port(s) Apache listens on.
+   
+   - `/etc/apache2/sites-available`—Holds files containing the code that describes virtual hosts. See page 906 for information on using `a2ensite` to enable a site.
+   
+   - `/etc/apache2/sites-enabled`—Holds links to files in `sites-available`. Use `a2ensite` to create links and `a2dissite` to remove links (page 906).
+   
+   - `/etc/apache2/httpd.conf`—Holds local configuration directives. This file augments the `apache2.conf` file in the same directory. The discussion of configuration directives starts on page 909.
+   
+   - `/etc/apache2/conf.d`—Holds configuration files.

Logs are kept in `/var/log/apache2`:

+   - `/var/log/apache2/access_log`—Logs requests made to the server.
+   - `/var/log/apache2/error_log`—Logs request and runtime server errors.

Web documents (including the Web pages displayed by client browsers), custom error messages, and CGI scripts are kept in `/var/www` by default:

+   - `/usr/lib/cgi-bin`—Holds CGI scripts (page 942). This directory is aliased to `/cgi-bin/`.
+   
+   - `/usr/share/apache2/error`—Holds default error documents. You can modify these documents to conform to the style of your Web site. This directory is aliased to `/error/`. See `ErrorDocument` (page 924).
+   
+   - `/usr/share/apache2/icons`—Holds icons used to display directory entries. This directory is aliased to `/icons/`.
+   
+   - `/usr/share/doc/apache2-doc/manual/index.html`—*Apache HTTP Server Version 2.2 Documentation*. With Apache running and `apache2-doc` installed, point a