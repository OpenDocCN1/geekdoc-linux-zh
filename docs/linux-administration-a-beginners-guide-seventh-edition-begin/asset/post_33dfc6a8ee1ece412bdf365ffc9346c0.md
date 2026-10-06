
# CHAPTER 18 Apache Web Server

## 493

## User

This specifies the user ID with which the web server will answer requests. The server process will initially start as the root user but will later downgrade its privileges to those of the user specified here. The user should have only enough privileges to access files and directories that are intended to be visible to the world outside the web server. Also, the user should not be able to execute code that is not HTTP- or web-related.

On a Fedora system, the value for this directive is automatically set to the user named apache. In openSUSE Linux, the value is set to the user wwwrun. In Debian-like system as Ubuntu, the value is set to the user www-data (set via the $APACHE-RUN variable).

Syntax: User unix_userid

## Group

This specifies the group name of the Apache HTTP server process. It is the group with which the server will respond to requests. The default value under the Fedora and RHEL flavors of Linux is apache. In openSUSE Linux, the value is set to the group www. In Ubuntu, the default value is www-data (set via the $APACHE_RUN_GROUP variable).

Syntax: Group unix_group

## Include

This directive allows Apache to specify and include other configuration files at runtime. It is mostly useful for organization purposes; you can, for example, to store all the configuration directives for virtual domains in appropriately named files, and Apache will automatically know to include them at runtime.

Syntax: Include file_name_to_include_OR_path_to_directory_to_include

Many of the mainline Linux distros rely heavily on the Include directive to organize site-specific configuration files and directives for the web server. Often, this file and directory organization is the sole distinguishing factor between Apache installation/setup among the different distros.

## UserDir

This directive defines the subdirectory within each user's home directory, where users can place personal content that they want to make accessible via the web server. This directory is usually named public_html and is often stored under each user's home directory. This option is, of course, depending on the availability of the mod_userdir module in the web server setup.

Here's a sample usage of this option in the httpd.conf file:

```
UserDir public_html
```

## 494 Linux Administration: A Beginner's Guide

### Quick How-To: Serving HTTP Content from User Directories

After enabling the UserDir option, and assuming the user yangang want to make some web content available from within her home directory via the web server, these steps will make this happen:

1. While logged into the system as the user yangang, create the public_html folder:
2. Set the proper permissions for the parent folder:
3. Set the proper permissions for the public_html folder:
4. Create a sample page index.html under the public_html folder:

```
yangang@server:~$ mkdir ~/public_html
```

```
yangang@server:~$ chmod a+x
```

```
yangang@server:~$ chmod a+x public_html
```

```
yangang@server:~$ echo "Ying Yang's Home Page" >> \
~/public_html/index.html
```

As a result of these commands, files placed in the public_html directory for a particular user and set to world-readable will be on the web server. To access the contents of that folder via HTTP, you would need to point a web browser to this URL:

```
http://YOUR_HOST_NAME>/-<USERNAME>
```

WHERE YOUR_HOST_NAME is the server's FQDN or IP address. And if you are sitting directly on the web server itself, you can simply replace that variable with localhost.

For the example shown here for the user yangang, the exact URL will be http://localhost/-yangang. And the IPv6 equivalent is http://[::]/-yangang.
Note on older versions of Red Hat-like distros with SELinux subsystem enabled, you may have to do a little more to get the UserDir directive working. This is because of the default security contexts of the files stored under each user's home directory. By default, the context is user_home_t For this functionality to work properly, you will have to change the context of all files under ~/username/public_html to http_sys_content_t. This allows Apache to read the files from the public_html directory.

```
[yangang@fedora-server ~$] chcon -Rt http_sys_content_t public_html/
```

## CHAPTER 18 Apache Web Server

## 495

## ErrorLog

This defines the location where errors from the web server will be logged.

Syntax: ErrorLog file_path| syslog[:facility]:

Example: ErrorLog /var/log/httpd/error_log

## LogLevel

This option sets the level of verbosity for the messages sent to the error logs. Acceptable log levels are emerg, alert, crit, error, warn, notice, info, and debug. The default log level is warn.

Syntax: LogLevel level

## Alias

The Alias directive allows documents (web content) to be stored in any other location on the file system that is different from the location specified by the DocumentRoot directive. It also allows you to create abbreviations (or aliases) for path names that might be quite long.

Syntax: Alias URL_path actual_file_or_directory_path

## ScriptAlias

The ScriptAlias option specifies a target directory or file containing CGI scripts that are to be processed by the CGI module (mod-cgi).

Syntax: ScriptAlias URL-path actual_file_path_OR_directory-path

Example: ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"

## VirtualHost

One of the most features of Apache is its ability to support virtual hosts. This makes it possible for a single web server to host multiple web sites if each site had its own dedicated domain. It works by allowing the web server to provide different, autonomous content, based on the hostname, port number, or IP address that is being requested by the client. This is accomplished by the HTTP protocol, which specifies the desired site in the HTTP header rather than relying on the server to fetch from its IP address.

This directive is actually made of two tags: an <VirtualHost> tag and a closing </VirtualHost> tag. It is used to specify the options that pertain to a particular virtual host. Most of the directives that we discussed are valid here, too.

Syntax: <VirtualHost ip_address_OR_hostname[:port]>

Options
< /VirtualHost >

## 496 Linux Administration: A Beginner's Guide

Suppose, for example, that we wanted to set up a virtual host configuration for a host named www-example.org. To do this, we can create a VirtualHost entry in the httpd.conf file (or use the Include directive to specify a separate file), like this:

```
<VirtualHost www.example.org>
ServerAdmin webmaster@example.org
DocumentRoot /www/docs/example.org
ServerName www.example.org
ErrorLog logs/error_log
</VirtualHost>
```

On Debian-like distros, we can use another set of utilities (a2ensite and a2dissite) to enable virtual hosts and sites quickly. For example, assuming we created the configuration file named www-example.org and stored it under the /etc/apache2/sites-available/ directory, we can enable the virtual site using the following command:

```
master@ubuntu-server:~ sudo a2ensite www-example.org
```

Similarly, to the virtual site, we can run this:

```
master@ubuntu-server:~ sudo a2dissite www-example.org
```

After running any of the previous commands (a2ensite and a2dissite), we should make Apache reload its configuration files by running the following:

```
master@ubuntu-server:~ sudo /etc/init.d/apache2 reload
```

Finally, don't forget that it is not enough to configure a virtual host using Apache's VirtualHost directive—the value of the ServerName in the VirtualHost container must be a value that is resolvable via DNS (or any other means) to the web server machine.

![](img/9f6657924397c33f088db5321b751a83_512_0.png)

> NOTE Apache's options/directives are too numerous to be covered in this section. But the software comes with its own extensive online manual, which is written in HTML so that you can access it in a browser. If you installed the software via RPM, you might find documentation for Apache has been packaged into a separate RPM binary, and as a result, you will need to install the proper package have access to it. If you downloaded and built the software from source code, you will find the documentation in the manual directory of your installation prefix (for example, /usr/local/httpd/manual). Depending on the Apache version, the documentation is available online at the project's web site at http://apache.org/docs/.
