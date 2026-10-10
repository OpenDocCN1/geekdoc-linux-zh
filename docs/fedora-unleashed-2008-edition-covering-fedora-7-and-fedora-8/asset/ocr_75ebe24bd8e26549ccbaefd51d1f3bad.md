Here’s another access control example, again using the previous `server-status` example. This time, you combine access methods so that all users from the `gnulix` domain are allowed access and those from outside the domain must identify themselves before gaining access. You can do so with the following:

```
```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from gnulix.org
    AuthType Basic
    AuthName "Server status"
    AuthUserFile "/etc/apache2/.htpasswd"
    Require valid-user
    Satisfy Any
</Location>
```
```

There are more ways to protect material on your web server, but the methods discussed here should get you started and are probably more than adequate for most circumstances. Look to Apache’s online documentation for more examples of how to secure areas of your site.

# Apache Modules

The Apache core does relatively little; Apache gains its functionality from modules. Each module solves a well-defined problem by adding necessary features. By adding or removing modules to supply the functionality you want Apache to have, you can tailor the Apache server to suit your exact needs.

Nearly 50 core modules are included with the basic Apache server. Many more are available from other developers. The Apache Module Registry is a repository for add-on modules for Apache, and it can be found at http://modules.apache.org/. The modules are listed in the `modules` directory under `/etc/httpd/`, but the following directory is a link to the `/usr/lib/httpd/modules` directory where the modules reside (your list might look different):

|              |                  |                       |                  |
|--------------|------------------|-----------------------|------------------|
| mod_access.so | mod_cern_meta.so | mod_log_config.so     | mod_setenvif.so  |
| mod_actions.so| mod_cgi.so       | mod_mime_magic.so     | mod_speling.so   |
| mod_alias.so  | mod_dav_fs.so    | mod_mime.so           | mod_ssl.so       |
| mod_asisl.so  | mod_dav.so       | mod_negotiation.so    | mod_status.so    |
| mod_auth_anon.so| mod_dir.so     | mod_perl.so           | mod_suexec.so    |
| mod_auth_dbm.so | mod_env.so      | mod_proxy_connect.so  | mod_unique_id.so |
| mod_auth_digest.so| mod_expires.so| mod_proxy.so          | mod_userdir.so   |
| mod_auth_mysql.so | mod_headers.so | mod_proxy_http.so     | mod_ustrack.so   |
| mod_auth_pgsql.so | mod_imap.so    | mod_proxy.so          | mod_whois_alias.so|
| mod_auth.so   | mod_include.so   | mod_python.so         | mod_autoindex.so |
|              |                  |                       |                  |
| mod_info.so   | mod_rewrite.so   |                       |                  |