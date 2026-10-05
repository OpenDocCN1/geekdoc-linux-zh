# LISTING 11.2 CONTINUED

```
#n# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, in addition to the default. See also the <VirtualHost>
# directive.
#Listen 3000
#Listen 12.34.56.78:80
```

```

# BindAddress: You can support virtual hosts with this option. This directive
# is used to tell the server which IP address to listen to. It can either
# contain "*", an IP address, or a fully qualified Internet domain name.
# See also the <VirtualHost> and Listen directives.
#BindAddress *
```

```

# Dynamic Shared Object (DSO) Support
# To be able to use the functionality of a module which was built as a DSO you
# we have to place corresponding 'LoadModule' lines at this location so the
# directives contained in are actually available _before_ they are used.
# Please read the README.DSO in the Apache 1.3 distribution for more
# details about the DSO mechanism and run 'httpd -l' for the list of already
# built-in (statically linked and thus always available) modules in your httpd
# binary.
# Note: The order by which modules are loaded is important. Don't change
# the order below without expert advice.

# Example:
# LoadModule foo_module libexec/mod_foo.so
LoadModule mmap_static_module /usr/lib/apache/mod_mmap_static.so
LoadModule env_module /usr/lib/apache/mod_env.so
LoadModule config_log_module /usr/lib/apache/mod_log_config.so
LoadModule agent_log_module /usr/lib/apache/mod_log_agent.so
LoadModule referer_log_module /usr/lib/apache/mod_log_referer.so
LoadModule mime_magic_module /usr/lib/apache/mod_mime_magic.so
LoadModule mime_module /usr/lib/apache/mod_mime.so
LoadModule negotiation_module /usr/lib/apache/mod_negotiation.so
LoadModule status_module /usr/lib/apache/mod_status.so
LoadModule info_module /usr/lib/apache/mod_info.so *
```