# **LISTING 12.3** continued

```
LogFormat "%h %l %u %t "%r" "%s %b" common
LogFormat "%{Referer}i -> %U" referer
LogFormat "%{User-agent}i" agent

#
# The location and format of the access logfile (Common Logfile Format).
# If you do not define any access logfiles within a <VirtualHost>
# container, they will be logged here.  Conversely, if you *do*
# define per-<VirtualHost> access logfiles, transactions will be
# logged therein and *not* in this file.

CustomLog /var/log/httpd/access_log common

#
# If you like to have agent and referer logfiles, uncomment the
# following directives.
#
#CustomLog /var/log/httpd/referer_log referer
#CustomLog /var/log/httpd/agent_log agent

#
# If you prefer a single logfile with access, agent, and referer information
# (Combined Logfile Format) you can use the following directive.
#
#CustomLog /var/log/httpd/access_log combined

#
# Optionally add a line containing the server version and virtual host
# name to server-generated pages (error documents, FTP directory listings,
# mod_status and mod_info output etc., but not CGI generated documents).
# Set to "Email" to also include a mailto: link to the ServerAdmin.
#
# Set to one of:  On | Off | Email

ServerSignature On

#
# Aliases: Add here as many aliases as you need (with no limit).  The format is
# Alias fakename realname
#
# Note that if you include a trailing / on fakename then the server will
# require it to be present in the URL.  So "/icons/" isn't aliased in this
# example, only "/icons/"..
#
Alias /icons/ " /var/www/icons/"

<Directory " /var/www/icons">
    Options Indexes MultiViews
    AllowOverride None
    Order allow,deny
    Allow from all
```