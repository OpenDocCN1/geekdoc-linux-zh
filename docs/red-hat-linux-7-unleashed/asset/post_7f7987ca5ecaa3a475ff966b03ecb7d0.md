
## LISTING 12.3

#
# ServerType is either inetd, or standalone. Inetd mode is only supported on
# Unix platforms.
#
ServerType standalone

#
# ServerRoot: The top of the directory tree under which the server's
# configuration, error, and log files are kept.
#
# NOTE! If you intend to place this on an NFS (or otherwise network)
# mounted filesystem then please read the LockFile documentation
# (available at <URL:http://www.apache.org/docs/mod/core.html#lockfile>);
# you will save yourself a lot of trouble.
#
# Do NOT add a slash at the end of the directory path.
#
ServerRoot "/etc/httpd"

#
# The LockFile directive sets the path to the lockfile used when Apache
# is compiled with either USE_FCNTL_SERIALIZED_ACCEPT or
# USE_FLOCK_SERIALIZED_ACCEPT. This directive should normally be left at
# its default value. The main reason for changing it is if the logs
# directory is NFS mounted, since the lockfile MUST BE STORED ON A LOCAL
# DISK. The PID of the main server process is automatically appended to
# the filename.
#
LockFile /var/lock/httpd.lock

#
# PidFile: The file in which the server should record its process
# identification number when it starts.
#
PidFile /var/run/httpd.pid

#
# ScoreBoardFile: File used to store internal server process information.
# Not all architectures require this. But if yours does (you'll know because
# this file will be created when you run Apache) then you *must* ensure that
# no two invocations of Apache share the same scoreboard file.
#
ScoreBoardFile /var/run/httpd.scoreboard

#
# In the standard configuration, the server will process this file,
# srm.conf, and access.conf in that order. The latter two files are
# now distributed empty, as it is recommended that all directives
# be kept in a single file for simplicity. The commented-out values
# below are the built-in defaults. You can have the server ignore
# these files altogether by using "/dev/null" (for Unix) or
# "nul" (for Win32) for the arguments to the directives.
#
#ResourceConfig conf/srm.conf
#AccessConfig conf/access.conf

#
# Timeout: The number of seconds before receives and sends time out.
#
Timeout 300

#
# KeepAlive: Whether or not to allow persistent connections (more than
# one request per connection). Set to "Off" to deactivate.
#
KeepAlive On

#
# MaxKeepAliveRequests: The maximum number of requests to allow
# during a persistent connection. Set to 0 to allow an unlimited amount.
# We recommend you leave this number high, for maximum performance.
MaxKeepAliveRequests 100

#
# KeepAliveTimeout: Number of seconds to wait for the next request from the
# same client on the same connection.
#
KeepAliveTimeout 15

#
# Server-pool size regulation. Rather than making you guess how many
# server processes you need, Apache dynamically adapts to the load it
# sees ... that is, it tries to maintain enough server processes to
# handle the current load, plus a few spare servers to handle transient
# load spikes (e.g., multiple simultaneous requests from a single
# Netscape browser).
#
# It does this by periodically checking how many servers are waiting
# for a request. If there are fewer than MinSpareServers, it creates
# a new spare. If there are more than MaxSpareServers, some of the
# spares die off. The default values are probably OK for most sites.
#
MinSpareServers 5
MaxSpareServers 20

#
# Number of servers to start initially --- should be a reasonable ballpark
# figure.
StartServers 8

#
# Limit on total number of servers running, i.e., limit on the number
# of clients who can simultaneously connect ... if this limit is ever
# reached, clients will be LOCKED OUT, so it should NOT be set TOO LOW.
# It is intended mainly as a brake to keep a runaway server from taking
# the system with it as it spirals down...
MaxClients 150

# MaxRequestsPerChild: the number of requests each child process is
# allowed to process before the child dies. The child will exit so
# as to avoid problems after prolonged use when Apache (and maybe the
# libraries it uses) leak memory or other resources. On most systems, this
# isn't really needed, but a few (such as Solaris) do have notable leaks
# in the libraries. For these platforms, set to something like 10000
# or so; a setting of 0 means unlimited.
#
# NOTE: This value does not include keepalive requests after the initial
# request per connection. For example, if a child process handles
# an initial request and 10 subsequent "keepalive" requests, it
# would only count as 1 request towards this limit.
MaxRequestsPerChild 100

# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, in addition to the default. See also the <VirtualHost>
# directive.
#
#Listen 3000
#Listen 12.34.56.78:80
Listen 80

#
# BindAddress: You can support virtual hosts with this option. This directive
# is used to tell the server which IP addresses to listen to. It can either
# contain "*", an IP address, or a fully qualified Internet domain name.
# See also the <VirtualHost> and Listen directives.
#
#BindAddress *

#
# Dynamic Shared Object (DSO) Support
#
# To be able to use the functionality of a module which was built as a DSO you
# have to place corresponding 'LoadModule' lines at this location so the
# directives contained in it are actually available_before they are used.
# Please read the file README.DSO in the Apache 1.3 distribution for more
# details about the DSO mechanism and run 'httpd -l' for the list of already
# built-in (statically linked and thus always available) modules in your httpd
# binary.
#
# Note: The order in which modules are loaded is important. Don't change
# the order below without expert advice.
#
# Example:
# LoadModule foo_module modules/mod_foo.so

#LoadModule mmap_static_module    modules/mod_mmap_static.so
LoadModule vhost_alias_module     modules/mod_alias.so
LoadModule env_module             modules/mod_env.so
LoadModule config_log_module      modules/mod_log_config.so
LoadModule agent_log_module      modules/mod_log_agent.so
LoadModule referer_log_module    modules/mod_log_referer.so
#LoadModule mime_magic_module    modules/mod_mime_magic.so
LoadModule mime_module            modules/mod_mime.so
LoadModule negotiation_module    modules/mod_negotiation.so
LoadModule status_module          modules/mod_status.so
LoadModule info_module            modules/mod_info.so
LoadModule includes_module        modules/mod_include.so
LoadModule autoindex_module       modules/mod_autoindex.so
LoadModule dir_module             modules/mod_dir.so
LoadModule cgi_module             modules/mod_cgi.so
LoadModule asis_module            modules/mod_asis.so
LoadModule imap_module            modules/mod_imap.so
LoadModule action_module          modules/mod_actions.so
#LoadModule speling_module       modules/mod_speling.so
LoadModule userdir_module         modules/mod_userdir.so
LoadModule aliases_module         modules/mod_aliases.so
LoadModule rewrite_module         modules/mod_rewrite.so
LoadModule access_module          modules/mod_access.so
#LoadModule auth_module           modules/mod_auth.so
#LoadModule anon_auth_module      modules/mod_auth_anon.so
#LoadModule db_auth_module        modules/mod_auth_db.so
#LoadModule digest_module         modules/mod_digest.so
#LoadModule proxy_module          modules/libproxy.so
#LoadModule cern_meta_module      modules/mod_cern_meta.so
LoadModule expires_module         modules/mod_expires.so
LoadModule headers_module         modules/mod_headers.so
#LoadModule usertrack_module     modules/mod_usertrack.so
#LoadModule example_module       modules/mod_example.so
#LoadModule unique_id_module     modules/mod_unique_id.so
LoadModule setenvif_module        modules/mod_setenvif.so

#LoadModule bandwidth_module    modules/mod_bandwidth.so
#LoadModule put_module          modules/mod_put.so
<IfDefine HAVE_PERL>
LoadModule perl_module           modules/libperl1.so
</IfDefine>
<IfDefine HAVE_PHP>
LoadModule php_module           modules/mod_php.so
</IfDefine>
<IfDefine HAVE_PHP3>
LoadModule php3_module          modules/libphp3.so
</IfDefine>
<IfDefine HAVE_PHP4>
LoadModule php4_module          modules/libphp4.so
</IfDefine>
<IfDefine HAVE_DAV>
LoadModule dav_module           modules/libdav.so
</IfDefine>
<IfDefine HAVE_ROAMING>
LoadModule roaming_module       modules/mod_roaming.so
</IfDefine>
<IfDefine HAVE_SSL>
LoadModule ssl_module           modules/libssl.so
</IfDefine>

# Reconstruction of the complete module list from all available modules
# (static and shared ones) to achieve correct module execution order.
# [WHENEVER YOU CHANGE THE LOADMODULE SECTION ABOVE UPDATE THIS, TOO]
ClearModuleList
AddModule mod_mmap_static.c
AddModule mod_vhost_alias.c
AddModule mod_env.c
AddModule mod_log_config.c
AddModule mod_log_agent.c
AddModule mod_log_referer.c
#AddModule mod_mime_magic.c
AddModule mod_mime.c
AddModule mod_negotiation.c
AddModule mod_status.c
AddModule mod_info.c
AddModule mod_include.c
AddModule mod_autoindex.c
AddModule mod_dir.c
AddModule mod_cgi.c
AddModule mod_asis.c
AddModule mod_map.c
AddModule mod_actions.c
#AddModule mod_speling.c
AddModule mod_userdir.c
AddModule mod_alias.c
