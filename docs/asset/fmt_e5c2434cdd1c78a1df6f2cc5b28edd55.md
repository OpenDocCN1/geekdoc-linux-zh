
## 第13章 Web 服务器

### Section 1: Global Environment

```apache
# unless you have overridden these with ResourceConfig and/or
# AccessConfig directives here.
#
# The directives in this section affect the overall operation of Apache,
# such as the number of concurrent requests it can handle or where it
# can find its configuration files.
# ServerType is either inetd, or standalone. Inetd mode is only supported on
# Unix platforms.
ServerType standalone
# ServerRoot: The top of the directory tree under which the server's
# configuration, error, and log files are kept.
ServerRoot "/usr/local/apache"
MinSpareServers 5
MaxSpareServers 10
#
# Number of servers to start initially -- should be a reasonable ballpark
# figure.
#
StartServers 5
#
# Limit on total number of servers running, i.e., limit on the number
# of clients who can simultaneously connect -- if this limit is ever
# reached, clients will be LOCKED OUT, so it should NOT BE SET TOO LOW.
# It is intended mainly as a brake to keep a runaway server from taking
# the system with it as it spirals down....
```

```apache
#
MaxClients 150
# Dynamic Shared Object (DSO) Support
# Example:
# LoadModule foo_module libexec/mod_foo.so
LoadModule rewrite_module libexec/mod_rewrite.so
# Reconstruction of the complete module list from all available modules
# (static and shared ones) to achieve correct module execution order.
# [WHENEVER YOU CHANGE THE LOADMODULE SECTION ABOVE UPDATE THIS, TOO]
ClearModuleList
AddModule mod_env.c
AddModule mod_log_config.c
AddModule mod_mime_magic.c
AddModule mod_mime.c
AddModule mod_negotiation.c
AddModule mod_status.c
AddModule mod_include.c
AddModule mod_autoindex.c
AddModule mod_dir.c
AddModule mod_cgi.c
AddModule mod_asis.c
AddModule mod_imap.c
AddModule mod_actions.c
AddModule mod_userdir.c
AddModule mod_alias.c
AddModule mod_rewrite.c
AddModule mod_access.c
AddModule mod_auth.c
AddModule mod_so.c
AddModule mod_setenvif.c
```

第二个部分定义了“默认”或“主”服务器的设置。主服务器响应所有未由虚拟主机处理的请求。所有虚拟主机的默认设置都在`httpd.conf`文件的这一部分中设置。以下列表是`httpd.conf`文件第二部分的精简版本：

### Section 2: 'Main' server configuration

```apache
#
# The directives in this section set up the values used by the 'main'
# server, which responds to any requests that aren't handled by a
# <VirtualHost> definition. These values also provide defaults for
# any <VirtualHost> containers you may define later in the file.
#
# All of these directives may appear inside <VirtualHost> containers.
# In which case these default settings will be overridden for the
# virtual host being defined.
#
# Port: The port to which the standalone server listens. For
# ports < 1023, you will need httpd to be run as root initially.
#
Port 8080
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.
#
User nobody
Group nobody
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from this directory, but
# symbolic links and aliases may be used to point to other locations.
#
DocumentRoot "/usr/local/apache/htdocs"
# Each directory to which Apache has access, can be configured with respect
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).
#
# First, we configure the "default" to be a very restrictive set of
# permissions.
#
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

# Note that from this point forward you must specifically allow
# particular features to be enabled - so if something's not working as
# you might expect, make sure that you have specifically enabled it
# below.

<Directory "/usr/local/apache/htdocs">

# This may also be "None", "All", or any combination of "Indexes",
# "Includes", "FollowSymLinks", "ExecCGI", or "MultiViews".
# Note that "MultiViews" must be named *explicitly* --- "Options All"
# doesn't give it to you.
```

