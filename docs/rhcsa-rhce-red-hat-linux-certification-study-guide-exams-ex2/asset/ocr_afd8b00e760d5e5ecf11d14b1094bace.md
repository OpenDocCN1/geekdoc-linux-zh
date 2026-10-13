**TABLE 14-5**

Default Active Apache-Related SELinux Boolean Settings

| Active Boolean | Description |
|---|---|
| httpd_builtin_scripting | Provides permissions to scripts in httpd_t labeled directories; sometimes used for PHP content. |
| httpd_dbus_avahi | Supports access from HTTP services to automated IP address configuration. |
| httpd_enable_cgi | Allows HTTP services to execute CGI scripts, labeled with the httpd_sys_script_exec_t type. |
| httpd_tty_comm | Enables communication with controlling terminals; useful for SSL certificates. |
| httpd_unified | Supports full read/write/execute access by all httpd_t files. |
| xguest_connect_network | Allows access from secured guests. |

Out of the many other SELinux options, the one of particular interest for this chapter is httpd_enable_homedirs, which supports access to files from user home directories. Other scripts of potential interest relate to interactions with other services, specifically, httpd_enable_ftp_server, httpd_use_cifs, and httpd_use_nfs. These options allow Apache to act as an FTP server, as well as to read shared Samba / NFS directories.

The uses of these and the other unenabled SELinux Apache-related options from Figure 14-4 are summarized in Table 14-6. All descriptions are based on the perspective "what would happen if the boolean were enabled?" For variety, the terms HTTP and Apache are used interchangeably; strictly speaking, Apache is one option for HTTP and HTTPS services.

# Module Management

The Apache web server includes many modular features. For example, it’s not possible to set up SSL-secured web sites without the mod_ssl package, which includes the mod_ssl.so module along with the ssl.conf configuration file.

A number of other similar systems are organized in modules. Loaded modules are included in standard Apache configuration files with the LoadModule directive. A full list of available modules is located in the /usr/lib64/httpd/modules directory (for 32-bit systems, the directory is /usr/lib/httpd/modules). But available modules aren’t used unless they’re loaded with the LoadModule directive in appropriate Apache configuration files.