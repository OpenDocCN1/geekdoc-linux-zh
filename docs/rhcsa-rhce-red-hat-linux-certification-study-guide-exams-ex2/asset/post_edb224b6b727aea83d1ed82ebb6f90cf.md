
This command creates a file_contexts.local file in the /etc/selinux/targeted/contexts/files directory. If there's also a cgi-bin/ subdirectory, you'll want to set up appropriate contexts for that subdirectory as well with the following command:

```
# semanage fcontext -a -s system_u -t httpd_sys_script_exec_t \
/www/cgi-bin/
```

## Apache and SELinux Boolean Settings

Boolean settings are more extensive. For display purposes, I've isolated them in the SELinux Administration tool, as shown in Figure 14-4. Only a few SELinux boolean settings are enabled by default, and they're described in Table 14-5.

FIGURE 14-4 Apache-related SELinux boolean settings

![](img/9139201cfcaf4292284a0eed074928e5_775_0.png)

### TABLE 14-5

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

## Module Management

The Apache web server includes many modular features. For example, it’s not possible to set up SSL-secured web sites without the mod_ssl package, which includes the mod_ssl.so module along with the ssl.conf configuration file.

A number of other similar systems are organized in modules. Loaded modules are included in standard Apache configuration files with the LoadModule directive. A full list of available modules is located in the /usr/lib64/httpd/modules directory (for 32-bit systems, the directory is /usr/lib/httpd/modules). But available modules aren’t used unless they’re loaded with the LoadModule directive in appropriate Apache configuration files.

### TABLE 14-6 Default Inactive Apache-Related SELinux Boolean Settings

| Inactive Boolean | Description |
|---|---|
| allow_httpd_anon_write | Allows the web server to write to files labeled with the public_content_rw_t file type. |
| allow_httpd_mod_auth_ntlm_winbind | Supports access to Microsoft authentication databases, if the mod_auth_ntlm_winbind module is loaded. |
| allow_httpd_mod_auth_pam | Enables access to PAM authentication modules, if the mod_auth_pam module is loaded. |
| allow_httpd_sys_script_anon_write | Configures write access by scripts to files labeled with the public_content_rw_t file type. |
| httpd_can_check_spam | Works with web-based e-mail applications to check for spam. |
| httpd_can_network_connect | Supports Apache access to connections on remote ports; normally disabled to minimize risk of attacks on other systems. |
| httpd_can_network_connect_cobbler | Allows Apache to connect to the Cobbler installation server; should not be activated simultaneously with httpd_can_network_connect. |
| httpd_can_network_connect_db | Allows Apache to connect to a database server. |
| httpd_can_network_memcache | Enables HTTP memory caching access; originally set up for a translation server. |
| httpd_can_network_relay | Supports the use of the HTTP service as a proxy. |
| httpd_can_sendmail | Allows the use of HTTP-based e-mail services; does not require the use of the sendmail SMTP server described in Chapter 13. |
| httpd_enable_homedirs | Configures access via HTTP to files in user home directories. |
| httpd_execmem | Supports operation of executable programs that require executable and writable memory addresses; normally disabled to minimize risk of buffer overflows. |
| httpd_read_user_content | Enables access to scripts from user home directories. |
| httpd_setrlimit | Allows Apache to modify maximum number of file descriptors. |
| httpd_ssi_exec | Allows Apache to access Server Side Include (SSI) scripts; similar to httpd_enable_cgi. |
| httpd_tmp_exec | Supports those Apache-based scripts that require access to the /tmp directory. |
| httpd_use_cifs | Enables Apache access to shared Samba directories, when labeled with the cifs_t file type. |
| httpd_use_gpg | Allows access to systems that require GPG encryption. |
| httpd_use_nfs | Enables Apache access to shared Samba directories, when labeled with the nfs_t file type. |

## Security Within Apache

You’ve read about (and hopefully tested) Apache security options related to iptables-based firewalls as well as SELinux. Now you’ll examine the security options available in the main Apache configuration file, httpd.conf. That file can be modified to secure the entire server or to configure security on a directory-by-directory basis. Directory controls secure access by the server, as well as users who connect to the web sites on the server. To explore the basics of Apache security, start with the first default active line in httpd.conf:

```
ServerTokens OS
```

This line looks deceptively simple; it limits the information displayed about a web server you navigate to a nonexistent page to the following message:

```
Apache/2.2.15 (Red Hat) Server at localhost Port 80
```

Contrast that output with what happens with a ServerTokens Full line:

```
Apache/2.2.15 (Red Hat) DAV/2 mod_ssl/2.2.15 OpenSSL/1.0.0-fips mod_wsgi/3.2
Python/2.6.5 mod_perl/2.0.4 Perl/v5.10.1 Server at localhost Port 80
```

In other words, with one option, outsiders can see whether modules such as Perl, Python, and PHP have been loaded, along with their version numbers. As not everyone updates their software in a perfectly timely manner, what happens when a cracker sees a version that has been compromised, your servers will face additional risks.

Next, you can restrict access to the directory defined by the ServerRoot directive as shown here:

```
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>
```

This configures a very restrictive set of permissions. The Options FollowSymLinks line supports the use of symbolic links for web pages. The AllowOverride None line disables any .htaccess files. The ServerRoot directive points to /etc/httpd, which contains Apache configuration files. Without the AllowOverride None line, a cracker who inserts a malicious .htaccess file can configure permissions that allows any user to change such configuration files.

However, there’s an appropriate use for .htaccess files. For example, when placed in a subdirectory such as /www/html/project, then it can be used to permit access to a group, and such changes would apply only to that directory.

You can improve this by limiting access to all but explicitly allowed users, by adding the following commands to the desired <Directory> container:

```
Order deny,allow
Deny from all
```

The next <Directory> container example limits access to /var/www/html, which corresponds to the default DocumentRoot directive (while these directives are divided by numerous comments, they are all in the same stanza):

```
<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

The Options directive is different; the Indexes setting allows readers to see a list of files on the web server if no index.html file is present in the specified directory. The Order and Allow lines allow all users to access the web pages on this server.

But wait a second! By default, there are no files in the /var/www/html directory. Based on the description, you should navigate to the system in question and see the screen shown in Figure 14-5. As there are no files in the /var/www/html directory, no files are shown in the output.

However, when you navigate to the default web site associated with the Apache server, the page shown in Figure 14-6 appears. For more information on how that worked, see Exercise 14-2.

### FIGURE 14-5

Browse to an index of files

![](img/9139201cfcaf4292284a0eed074928e5_779_0.png)
