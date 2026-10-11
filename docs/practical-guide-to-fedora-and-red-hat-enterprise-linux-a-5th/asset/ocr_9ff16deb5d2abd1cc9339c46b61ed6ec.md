# MODULES

Apache is a skeletal program that relies on external modules, called dynamic shared objects (DSOs), to provide most of its functionality. This section lists these modules and discusses some of the more important ones. In addition to the modules included with Fedora/RHTEL, many other modules are available. See httpd.apache.org/modules for more information.

# MODULE LIST

Following is a list of some of the modules that are available under Apache:

+   **access** (*mod_access.so*) Controls access based on client characteristics.
+   
+   **actions** (*mod_actions.so*) Allows execution of CGI scripts based on the request method.
+   
+   **alias** (*mod_alias.so*) Allows outside directories to be mapped to DocumentRoot.
+   
+   **asis** (*mod_asis.so*) Allows sending files that contain their own headers.
+   
+   **auth** (*mod_auth.so*) Provides user authentication via *htaccess*.
+   
+   **auth_anon** (*mod_auth_anon.so*) Provides anonymous user access to restricted areas.
+   
+   **auth_dbm** (*mod_auth_dbm.so*) Uses DBM files for authentication.
+   
+   **auth_digest** (*mod_auth_digest.so*) Uses MD5 digest for authentication.
+   
+   **autoindex** (*mod_autoindex.so*) Allows directory indexes to be generated.
+   
+   **cern_meta** (*mod_cern_meta.so*) Allows the use of CERN **httpd** metafile semantics.
+   
+   **cgi** (*mod_cgi.so*) Allows the execution of CGI scripts.
+   
+   **dav** (*mod_dav.so*) Allows Distributed Authoring and Versioning.
+   
+   **dav_fs** (*mod_dav_fs.so*) Provides a filesystem for mod_dav.
+   
+   **dir** (*mod_dir.so*) Allows directory redirects and listings as index files.
+   
+   **env** (*mod_env.so*) Allows CGI scripts to access environment variables.
+   
+   **expires** (*mod_expires.so*) Allows generation of Expires HTTP headers.
+   
+   **headers** (*mod_headers.so*) Allows customization of request and response headers.
+   
+   **imap** (*mod_imap.so*) Allows image maps to be processed on the server side.
+   
+   **include** (*mod_include.so*) Provides server-side includes (SSIs).
+   
+   **info** (*mod_info.so*) Allows the server configuration to be viewed.
+   
+   **log_config** (*mod_log_config.so*) Allows logging of requests made to the server.
+   
+   **mime** (*mod_mime.so*) Allows association of file extensions with content.
+   
+   **mime_magic** (*mod_mime_magic.so*) Determines MIME types of files.
+   
+   **negotiation** (*mod_negotiation.so*) Allows content negotiation.
+   
+   **proxy** (*mod_proxy.so*) Allows Apache to act as a proxy server.
+   
+   **proxy_connect** (*mod_proxy_connect.so*) Allows connect request handling.
+   
+   **proxy_ftp** (*mod_proxy_ftp.so*) Provides an FTP extension proxy.
+   
+   **proxy_http** (*mod_proxy_http.so*) Provides an HTTP extension proxy.
+   
+   **rewrite** (*mod_rewrite.so*) Allows on-the-fly URI rewriting based on rules.
+   
+   **setenvif** (*mod_setenvif.so*) Sets environment variables based on a request.
+   
+   **speling** (*mod_speling.so*) Auto-corrects spelling if the requested URI has incorrect capitalization and one spelling mistake.
+   
+   **status** (*mod_status.so*) Allows the server status to be queried and viewed.