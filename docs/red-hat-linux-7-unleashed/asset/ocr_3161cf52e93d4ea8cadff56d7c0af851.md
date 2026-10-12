# **LISTING 12.3** continued

```
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
```