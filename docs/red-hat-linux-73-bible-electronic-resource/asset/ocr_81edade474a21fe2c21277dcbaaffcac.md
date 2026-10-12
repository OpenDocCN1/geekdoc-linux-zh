```
#LoadModule mime_magic_module modules/mod_mime_magic.so
LoadModule mime_module modules/mod_mime.so
LoadModule negotiation_module modules/mod_negotiation.so
LoadModule status_module modules/mod_status.so
LoadModule info_module modules/mod_info.so
LoadModule includes_module modules/mod_include.so
.
.
.
# Reconstruction of complete module list from all available modules
# (static and shared ones) to achieve correct module execution order.
# [WHENEVER YOU CHANGE THE LOADMODULE SECTION ABOVE UPDATE THIS, TOO]
ClearModuleList
#AddModule mod_mmap_static.c
AddModule mod_vhost_alias.c
<IfDefine HAVE_BANDWIDTH>
AddModule mod_bandwidth.c
</IfDefine>
<IfDefine HAVE_THROTTLE>
AddModule mod_throttle.c
</IfDefine>
AddModule mod_env.c
AddModule mod_log_config.c
AddModule mod_log_agent.c
AddModule mod_log_referer.c
#AddModule mod_mime_magic.c
.
```

Apache modules are included in the list of active modules via the AddModule directive. The ClearModuleList directive removes all entries from the current list of active modules. It is important to synchronize the LoadModule and AddModule blocks above; otherwise, the modules may not be available to the server at run-time. Each of the standard dynamically linked Apache modules is described in Table 21-1.

If a particular module contains features that are not necessary, it can easily be commented out of the above lists. Similarly, you may want to add the features or functionality of a third-party module (for example, mod_perl, which integrates the Perl run-time library for faster Perl script execution, or mod_php, which provides a scripting language embedded within HTML documents) by including those modules in the lists above.