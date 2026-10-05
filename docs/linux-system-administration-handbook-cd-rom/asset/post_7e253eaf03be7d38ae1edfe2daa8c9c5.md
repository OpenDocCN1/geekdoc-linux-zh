
## 15.3 Apache and ApacheSSL/Stronghold

Listen—If you want the server to listen at an additional port, use this. It takes two arguments: the alias and the path to the directory. The path can either be relative to the ServerRoot or an absolute path.

ScriptAlias—Often, for security reasons, you will want to have the directories from which CGI programs can be executed outside of the directory tree. Or you may simply want to provide a shortcut for referencing a directory containing CGI programs.

Alias—Similar to ScriptAlias, but only non-cgi files can be served from the directory.

VirtualHost—If you want requests that come in on a different IP, server name or port to be served from a different document root, a different server name or with aliases pointing to different directories, then this is the directive for you. Any of DocumentRoot, Directory, ScriptAlias, Alias, User, Group, UserDir, or ServerName can be used as arguments inside it. A couple of examples should help to demonstrate the power of the VirtualHost directive.

A server for http://www.dognails.com on port 80 with its own cgi-bin and document root:

```
<VirtualHost www.dognails.com>
ServerName www.dognails.com
DocumentRoot /web/dognails/www
ScriptAlias /cgi-bin/ /web/dognails/cgi-bin/
</VirtualHost>
```

> To serve all requests on port 1200 as a separate DocumentRoot:

```
Listen 1200
<VirtualHost *:1200>
DocumentRoot /usr/local/wwwww1
</VirtualHost>
```

## Extensions for Apache

One of the more complicated extensions with a difficult setup process, suEXEC is a wrapper which allows CGI programs to be executed under a different UID than under which the server is running. This is often used by ISPs that let their users manage their own CGI; this forces the script to execute as that user. This obviously encourages the user to write good, secure CGI. It is also useful to allow access control similar to that allowed by the password file.

## Chapter 15 • Web Serving

Because suEXEC can open some serious security holes, its security model imposes several additional restrictions. The target program must reside in the Apache /webspace/ and thus, the path to it cannot start with a/ or have back references (...). Obviously the target user and group must be above a minimum (typically 100 or 500), which will prohibit execution as the root user or group. The target program cannot be set uid or gid and the final, non-trivial restrictions are that the directory containing the program to be executed and the program itself only be writable by the target user and belonging to the target.

suEXEC comes in a separate C source file and accompanying header file. Before compiling suEXEC, the header file needs to be edited to reflect the particulars of your system. The following may need to be changed: HTTP_USER, typically nobody or maybe a "web" or "www" user; LOG_EXEC, the log file for suEXEC transactions; DOC_ROOT, the root of the Apache Web space; and SAFE_PATH environment variable for suEXEC. Then you need to compile suEXEC: gcc -o suexec suexec.c, then copy it to root, set the userID (chmod -o suexec), and copy it to its final destination.

Apache must be recompiled to use the suEXEC wrapper. In the src/httpd.h file you will need to add or edit a line like:

```
#define suEXEC_BIN "/usr/sbin/suex"
```

To reflect where you installed the suexec, your new httpd, you should see this message:

Configuring Apache for use with the suexec wrapper.

To disable suEXEC, you can remove the binary, change its ownership from root, or unset the UID bit.

User and Group directives in VirtualHost directives can be used to tell suEXEC the target user and group for executing CGI. Another way is for the target user to do in HTTP requests to user directories. For example, http://thppt.org/~dwezzle/somescript.cgi-somescript.cgi would be executed as the user dwezzle. If neither of these conditions exists, the script will be executed as the main user and Group.

## PHP/FI

One of the most useful extensions for Apache is the PHP/FI program. PHP/FI is actually usable as CGI, FastCGI, or compiled into Apache (linked either statically or dynamically). Which option to employ is a matter of taste and use. If you plan on using it lightly, employing it as CGI or FastCGI is fine, though for more extensive use, you will likely want to compile into Apache, though this will raise your memory usage noticeably.

PHP/FI is a scripting language with syntax similar to Perl or C. It is embedded within HTML, set off by a variation on the comment tag: <? .. The code within the tag is parsed (either by the server itself or the CGI script, depending on your setup), and the output, if any, replaces the tag. This is very similar to how server side includes function. Typically, a special extension (.shtml) is used for PHP files to tell Apache to parse the file before sending it to the client. If you plan to use PHP in most or all of your files, you may want to tell Apache to parse all HTML files.

PHP boasts many functions for connecting to and extracting information from various databases, including mSQL (1 and 2), Postgres95, MySQL (another free database server over mSQL), Solid, Sybase, and Oracle. Additionally, it has very powerful support for Netscape cookies, file upload, and the GD library. That is a last C library for GIF creation. PHP also has additional functionality for setting attribute HTTP headers (besides sets cookies).

## SSL (Secure Socket Layer)

As mentioned above, SSL is a protocol for sending encrypted data via a network socket. This allows for some peace of mind when transmitting sensitive data over the Web. There are two implementations of Apache with SSL: Stronghold and Apache-SSL. The legality of Apache-SSL is somewhat in question for commercial use in the United States, as RSA means the SSL it uses covered by patents owned by RSA. So for commercial uses within the United States, you will likely want to use Stronghold. In either case, full source code is available.

Since Stronghold is well documented and comes with commercial support, we will go through the setup of Apache-SSL.

To use SSL with Apache you will need to retrieve two things: the SSLeay and the SSL patch for Apache. These will have names like SSay-0.8.0.tar.gz and apache_ssl-1.8.0.tar.gz, respectively. Make sure the patch you get matches the major and minor version of Apache that you are using. You will also need at least version 2.1 of patch.

SSLeay can be obtained at http://ftp.psu.uq.oz.au/pub/Crypto/SSL/ and Apache-SSL can be found at http://ftp.ox.ac.uk/pub/crypto/
Unpack SSLeay, cd into the source directory, run ./Configure linuxelf (or linux-out if linux-out), Apache-SSL in the root of the Apache (not in src subdirectory). Apply the patch: patch < <.. you you you an an,,,,,,,,,,,,,,,,,,,,,,,,,,,

 the
.

## Chapter 15 • Web Serving

Unpack Apache-SSL in the root of the Apache (not in src subdirectory). Apply the patch: patch < SSL. If this step produces an error, it is probably because you have an older version of the patch. Get a new version from your distribution's Web site or GNU mirror. Edit src/Configuration, as you would normally, but you will need to add the SSL-related directives to reflect any peculiarities on your system. If you are using a fresh copy of Apache, remember to add any extras you might be using, such as PHP.

```
/Configure
make
```

You should now have a shiny new httpsd!
If you get symbol errors, you may need to fiddle with the order of libraries in the link stage of the make as well as verify you are using the

## The httpd.conf

This will likely seem a little bizarre to anyone used to Apache's normal config file, but httpd.conf is the only config file used. srm. and access.conf are both empty. An example httpd.conf is included with the SSLdistribution. There are a few notes on setting up your httpd.conf we want to give you. These guidelines should work for Stronghold as well, since it is so similar to Apache-SSL.

Edit httpd.conf to reflect your setup and execute httpsd. Try connecting to the SSL server: your.host.com/ (note the “s” after http). If you can't, check the error_log and ssl_log and your config file. Fix any problems and restart the server with kill -1 /pid/, assuming it started on the first try or just try to start again.

Unless you want to maintain two sets of config files, run both the uneasy and secure servers on the same binary and config file. The easiest way to do this is to set up httpd.conf just as you would normally, except that you will need to add the contents of your srm. and access.conf files as server and then use the Listen and VirtualHost directives to run the server on a separate port. The default port for HTTPS is 443, so you will probably want to use that. Then move the SSLflag on directive the VirtualHost directive.

Start Apache-SSL and make sure you can connect to both the non-secure server (http://your.host.com/), and the secure one (https://your.host.com/).
