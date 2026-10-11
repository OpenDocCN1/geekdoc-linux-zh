
![](img/8ad518fddafc7f5e73715a2604b61d50_411_0.png)

Figure 12-6: The default Apache root file

## Configuring the Server

When you have it up and working, it's time to configure the server; handily, most of the server defaults are already enabled. Your configuration files are located in /var/lib/httpd/conf. Your configuration files are as follows:

```
# ls /var/lib/httpd/conf
access.conf httpd.conf mime.types srm.conf-dist
access.conf-dist httpd.conf-dist srm.conf
```

So, when you're configuring access to the server, you'll want to edit the access.conf file. Consider this example:

```
# access.conf: Global access configuration
# Online docs at http://www.apache.org/

# This file defines server settings which affect which types of services
# are allowed, and in what circumstances.

# Each directory to which Apache has access, can be configured with respect
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).

# Originally by Rob McCool

# This should be changed to whatever you set DocumentRoot to.

<Directory /usr/local/etc/httpd/htdocs>
```

Remember the "It worked!" page from http://localhost/? It's located currently in the /var/lib/httpd/htdocs. You may want to change this line to reflect it, or you can move your main Web server pages into that directory. If you want, you can always specify another directory.

```
# This may also be "None", "All", or any combination of "Indexes",
# "Includes", "FollowSymLinks", "ExecCGI", or "MultiViews".

# Note that "MultiViews" must be named *explicitly* -- "Options All"
# doesn't give it to you (or at least, not yet).

Options Indexes FollowSymLinks
```

You can change this to include what other options you want. Options include server side includes, return the listing of the contents of a directory if there is no index.html file, or execute CGI scripts.

```
# This controls which options the .htaccess files in directories can
# override. Can also be "All", or any combination of "Options", "FileInfo",
# "AuthConfig", and "Limit"

AllowOverride None

# Controls who can get stuff from this server.

order allow,deny
allow from all
```

The example just given controls access to the Web server. The way it's currently defined, it seems willing to allow access to anyone. The order is to read the allowed sites first—and then, if they are denied, drop them. You can also define whether you want a particular site to come through, like this:

```
</Directory>

# /usr/local/etc/httpd/cgi-bin should be changed to whatever your ScriptAlias # CGI Directory exists, if you have that configured.

<Directory /usr/local/etc/httpd/cgi-bin>
AllowOverride None
Options None
</Directory>
```

This defines where the CGI binaries are located. The next concern is status reports:

```
# Allow server status reports. With the URL of http://servername/server-status # Change the ".your_domain.com" to match your domain to enable.

#<Location /server-status>
#SetHandler server-status

#Order deny,allow
#deny from all
#allow from .your_domain.com
#</Location>

# There have been reports of people trying to abuse an old bug from pre-1.1
# days. This bug involved a CGI script distributed as a part of Apache.
# By uncommenting these lines you can redirect these attacks to a logging # script on php.apache.org. Or, you can record them yourself, using the script # support/phf_abuse_log.cgi.

#<Location /cgi-bin/phf>*>
#deny from all
#ErrorDocument 403 http://php.apache.org/phf_abuse_log.cgi
#</Location>

# You may place any other directories or locations you wish to have # access information for after this one.
```

The server configuration file is the **httpd.conf** file. This file controls the configurations of the server itself, where the most critical files are located, and network connectivity settings.

```
# This is the main server configuration file. See URL http://www.apache.org/
# for instructions.
# Do NOT simply read the instructions in here without understanding
# what they do. if you are unsure consult the online docs. You have been
# warned.
# Originally by Rob McCool
# ServerType is either inetd. or standalone.
ServerType standalone
```

This defines whether the **httpd daemon** is run from the **inetd super-daemon** if it is run by itself. If you to run it with **inetd**, change **standalone** to **inetd**.

```
# If you are running from inetd. go to "ServerAdmin".
# Port: The port the standalone listens to. For ports < 1023, you will
# need httpd to be run as root initially.
Port 80
```

This is the default port that **httpd** listens on. You can change it if you want to; however, **port 80** is standard for Web traffic.

```
# HostnameLookups: Log the names of clients or just their IP numbers
#   e.g.    www.apache.org (on) or 204.62.129.132 (off)
# You should probably turn this off unless you are going to actually
# use the information in your logs. or with a CGI. Leaving this on
# can slow down access to your site.
HostnameLookups on
```

This process defines whether you are running DNS for hostnames or if you are using the IP address directly. Most Web servers do have access to a nameserver. However, if your system works otherwise, turn HostnameLookups off.

```
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.

# User/Group: The name (or #number) of the user/group to run httpd as.
# On SCO (ODT 3) use User nouser and Group nogroup
# On HP/UX you may not be able to use shared memory as nobody, and the
# suggested workaround is to create a user www and use that user.
User nobody
Group #-1
```

Normally someone accesses your Web server via a user account. The default is nobody with a negative group number. If you want to track Web usage by user account, you can define a user called webuser with properties similar to those of the user nobody. Here’s what it would look like:

```
# The following directive disables keepalives and HTTP header flushes for
# Netscape 2.x and browsers which spoof it. There are known problems with
# these

BrowserMatch Mozilla/2 nokeepalive
```

Common sense tells me to leave this last line alone.

```
# ServerAdmin: Your address, where problems with the server should be
# e-mailed.

ServerAdmin you@your.address
```

Change this address to be your e-mail address or your Web administrator’s e-mail address.

```
# ServerRoot: The directory the server’s config, error, and log files
# are kept in
# NOTE! If you intend to place this on a NFS (or otherwise network)
# mounted file system then please read the LockFile documentation,
# you will save yourself a lot of trouble.

ServerRoot /usr/local/etc/httpd
```

This is where all your server files go. It's currently `/var/lib/httpd/`. Feel free to change this but keep your directories consistent.

```
# BindAddress: You can support virtual hosts with this option. This option
# is used to tell the server which IP address to listen to. It can either
# contain "*", an IP address, or a fully qualified Internet domain name.
# See also the VirtualHost directive.

#BindAddress *
```

This is used for other addresses that come through this server. For example, the Web site http://www.timeoutservices.com goes through the ISP Best Internet. So, in Best's Web server, they have a virtual host of timeouts services.com on their site.

```
# ErrorLog: The location of the error log file. If this does not start
# with /, ServerRoot is prepended to it.

ErrorLog logs/error_log
```

```
# TransferLog: The location of the transfer log file. If this does not
# start with /, ServerRoot is prepended to it.

TransferLog logs/access_log
# PidFile: The file the server should log its pid to
PidFile logs/httpd.pid
```

```
# ScoreBoardFile: File used to store internal server process information.
# Not all architectures require this. But if yours does (you'll know because
# this file is created when you run Apache) then you *must* ensure that
# no two invocations of Apache share the same scoreboard file.
ScoreBoardFile logs/apache_status
```

This is where your log files go. Pay attention to them and what is happening to your server. Many attacks do happen with port 80.

```
# ServerName allows you to set a host name which is sent back to clients for
# your server if it's different than the one the program would get (i.e. use
# "www" instead of the host's real name).
#
# Note: You cannot just invent host names and hope they work. The name you
# define here must be a valid DNS name for your host. If you don't understand
# this, ask your network administrator.

#ServerName new.host.name
```
