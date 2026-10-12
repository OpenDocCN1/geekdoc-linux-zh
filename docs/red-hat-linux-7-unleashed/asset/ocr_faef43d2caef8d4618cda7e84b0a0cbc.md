# **LISTING 12.3** *continued*

```
```text
DefaultType text/plain

# The mod_mime_magic module allows the server to use various hints from the
# contents of the file itself to determine its type. The MIMEMagicFile
# directive tells the module where the hint definitions are located.
# mod_mime_magic is not part of the default server (you have to add
# it yourself with a LoadModule [see the DSO paragraph in the “Global
# Environment” section], or recompile the server and include mod_mime_magic
# as part of the configuration), so it’s enclosed in an <IfModule> container.
# This means that the MIMEMagicFile directive will only be processed if the
# module is part of the server.
<IfModule mod_mime_magic.c>
    MIMEMagicFile share/magic
</IfModule>

# HostnameLookups: Log the names of clients or just their IP addresses
# e.g., www.apache.org (on) or 204.62.129.132 (off).
# The default is off because it’d be overall better for the net if people
# had to knowingly turn this feature on, since enabling it means that
# each client request will result in AT LEAST one lookup request to the
# nameserver.

HostnameLookups Off

# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here.  If you *do* define an error logFile for a <VirtualHost>
# container, that host’s errors will be logged there and not here.
ErrorLog /var/log/httpd/error_log

# LogLevel: Control the number of messages logged to the error_log.
# Possible values include: debug, info, notice, warn, error, crit,
# alert, emerg.
LogLevel warn

# The following directives define some format nicknames for use with
# a CustomLog directive (see below).
LogFormat "%h %l %u %t "%r" "%s" %b "%{Referer}i" "%{User-Agent}i"
```
continued
```