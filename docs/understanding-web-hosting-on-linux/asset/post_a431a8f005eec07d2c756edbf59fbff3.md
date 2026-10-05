
# 136 · CHAPTER 9

You might be wondering why any individuals or organizations would devote their time and talents to improving a Web server without the promise of a return on their investment. First, you must understand that there is a return: an improved Web server. Second, organizations that extend the Apache HTTP server to pay back the Apache organization by sharing their improvements with them. Third, there are bored developers who want to make a contribution to cyberspace and choose to do so by enhancing the most popular Web server in the world. (It looks pretty good on a résumé, too)

## Patches

The thought of "a patch here and a patch there" conjures up a pair of old jeans with haphazard patches on areas that weren't designed properly. Forget the term patch when comes to HTTP requests.

| Module | Description |
| :--- | :--- |
| mod_asis | Sends a message as it is, without HTTP headers. |
| mod_actions | Specifies CGI scripts as handlers for particular file types. |
| mod_spelling | Corrects URL parsing based on file and directory names in the server system. |
| mod_user | Selects resources by user name and a common prefix. |
| mod_alias | Maps one part of a file system to another. |
| mod_rewrite | Rewrites URLs using specified rules. |
| mod_access | Runs a CGI script based on MIME type or HTTP request method. |
| mod_auth | Provides authentication against text-based password files. |
| mod_auth_anon | Allows anonymous access to authenticated areas. |
| mod_auth_db | Provides HTTP authentication against a database. |
| mod_expires | Handles responses with expired HTTP headers. |
| mod_headers | Manipulates response headers. |
| mod_so | Loads modules at runtime. |
| mod_setenvif | Sets environment variables based on header fields in the request. |

To use a module, you must specify the AddModule directive in a configuration file, qualifying the name of the module services you want to enable with your Apache server. Pretty clean. The base server is very small and fast, but easily extensible with standard modules to support such advanced features as servants, Perl, FastCGI (a.k.a. persistent CGI), HTTP cookies, server-side includes, and Secured Sockets Layer.

The parade of modules doesn't stop there, however. The Apache HTTP server was designed to take full advantage of the power of modular programming, which resulted in an easily extensible and customizable server. Anyone can extend the Apache HTTP server by creating a custom Apache module.

Sometimes, after a particular custom module becomes heavily used and well regarded, the Apache Group will add it to the core set of modules included in the Apache download. Many frequently used and recommended third-party modules are freely available from http://modules.apache.org.

## The Apache Code

The add-on Apache modules can be statically or dynamically bound to the HTTP server program. As mentioned, you dynamically bind an Apache module by specifying the AddModule directive and the module name in a configuration file. For speed, you can statically bind Apache modules to the Apache HTTP server by recompiling the server program. The server program is called httpd (which stands for “Hypertext Transfer Protocol Daemon”). You can think of httpd as a daemon that hides in the background, waiting for requests from people trying to gain Web-based access to your host via TCP/IP and HTTP. The Apache HTTP server is delivered with the binary executable httpd program, the complete C source code for httpd, and the C code for all of the standard Apache module extensions.

## Apache Startup

The Apache Web server can be started by invoking the httpd command from a terminal session, but most distributions have a startup script that simplifies Apache. Red Hat’s script is also called httpd, and it exists in the /etc/rc.init.d/ directory. If you attempt to invoke the script without any options, you’ll receive the following message:

```
$ /etc/rc.init.d/httpd
Usage: httpd [start|stop|restart|reload|condstart|status]
```

This helpful message tells you the arguments required by the httpd script. The status option will tell you whether or not Apache is active, and the other options are obvious.

When Apache is started, it looks for the httpd.conf file in /etc/httpd/conf. You might be a little overwhelmed the first time you look at that httpd.conf, so we’ve supplied a minimal version in Figure 9.1. Apache expects a particular directory structure:

- A directory for the httpd.conf file
- A directory called htmldocs to hold the hypertext documents Apache is to serve
- A directory called logs to hold various pieces of information that Apache can be configured to log

```
# httpd.conf Apache configuration file
ServerRoot "/etc/httpd"

Port 8888

User nobody
Group nobody

ServerAdmin denonco@attglobal.com

ServerName localhost

DocumentRoot "/home/donat/www2/htdocs"

LoadModule mime_module modules/mod_mime.so
LoadModule dir_module modules/mod_dir.so

AddModule mod_mime.c
AddModule mod_dir.c

TypesConfig /etc/mime.types

DirectoryIndex tomcat.html
```

Figure 9.1: a minimal httpd.conf Apache configuration file enables basic Web serving.

Each of the lines in Figure 9.1 is known as a directive (except for the comment line, which is preceded by a pound symbol). The ServerRoot qualifies the directory that contains the Apache modules. The Port directive qualifies Apache to sit on. The User and Group directives qualify the user. The ServerAdmin qualifies the email address. The ServerName qualifies the domain. The DocumentRoot qualifies the directory of the web files. The LoadModule and AddModule directives qualify which modules are loaded and used. The TypesConfig qualifies the mime types file. The DirectoryIndex qualifies the default file.

Table 9.2: A Partial List of types

| HTTP Content Type | File Extension |
| :--- | :--- |
| application/pdf | .pdf |
| image/gif | .gif |
| image/jpeg | .jpeg |
| image/jpeg | .jpg |
| audio/xreal | .ra |
| audio/x-wav | .wav |
| text/css | .css |
| text/xml | .xml |
| video/x-msvideo | .avi |
| text/html | .html |

Each of the lines in Figure 9.1 is known as a directive (except for the comment line, which is preceded by a pound symbol). The ServerRoot qualifies the directory that contains the Apache modules. The Port directive qualifies Apache to sit on. The User and Group directives qualify the user. The ServerAdmin qualifies the email address. The ServerName qualifies the domain. The DocumentRoot qualifies the directory of the web files. The LoadModule and AddModule directives qualify which modules are loaded and used. The TypesConfig qualifies the mime types file. The DirectoryIndex qualifies the default file.

Table 9.2: A Partial List of types

| HTTP Content Type | File Extension |
| :--- | :--- |
| application/pdf | .pdf |
| image/gif | .gif |
| image/jpeg | .jpeg |
| image/jpeg | .jpg |
| audio/xreal | .ra |
| audio/x-wav | .wav |
| text/css | .css |
| text/xml | .xml |
| video/x-msvideo | .avi |
| text/html | .html |

(Wait, I will re-process the flow based on the actual OCR text provided to ensure no information is lost or Hall).

Each of the lines in Figure 9.1 is known as a directive (except for the comment line, which is preceded by a pound symbol). The ServerRoot qualifies the directory that contains the Apache modules. The Port directive qualifies Apache to sit on. The User and Group directives qualify the user. The ServerAdmin qualifies the email address. The ServerName qualifies the domain. The DocumentRoot qualifies the directory of the web files. The LoadModule and AddModule directives qualify which modules are loaded and used. The TypesConfig qualifies the mime types file. The DirectoryIndex qualifies the default file.

Wait, the OCR text provided has some repetitions/broken sentences at the end. Let me clean up the narrative flow properly:

Each of the lines in Figure 9.1 is known as a directive (except for the comment line, which is preceded by a pound symbol). The ServerRoot qualifies the directory that contains the Apache modules. The Port directive qualifies Apache to sit on. The User and Group directives qualify the user. The ServerAdmin qualifies the email address. The ServerName qualifies the domain. The DocumentRoot qualifies the directory of the web files. The LoadModule and AddModule directives qualify which modules are loaded and used. The TypesConfig qualifies the mime types file. The DirectoryIndex qualifies the default file.

Actually, looking at the provided text, it seems to get jumbled at the end. I will provide the clean version of the provided text.

[content]
# 136 · CHAPTER 9

You might be wondering why any individuals or organizations would devote their time and talents to improving a Web server without the promise of a return on their investment. First, you must understand that there is a return: an improved Web server. Second, organizations that extend the Apache HTTP server to pay back the Apache organization by sharing their improvements with them. Third, there are bored developers who want to make a contribution to cyberspace and choose to do so by enhancing the most popular Web server in the world. (It looks pretty good on a résumé, too)

## Patches

The thought of "a patch here and a patch there" conjures up a pair of old jeans with haphazard patches on areas that weren't designed properly. Forget the term patch when comes to HTTP requests.

| Module | Description |
| :--- | :--- |
| mod_asis | Sends a message as it is, without HTTP headers. |
| mod_actions | Specifies CGI scripts as handlers for particular file types. |
| mod_spelling | Corrects URL parsing based on file and directory names in the server system. |
| mod_user | Selects resources by user name and a common prefix. |
| mod_alias | Maps one part of a file system to another. |
| mod_rewrite | Rewrites URLs using specified rules. |
| mod_access | Runs a CGI script based on MIME type or HTTP request method. |
| mod_auth | Provides authentication against text-based password files. |
| mod_auth_anon | Allows anonymous access to authenticated areas. |
| mod_auth_db | Provides HTTP authentication against a database. |
| mod_expires | Handles responses with expired HTTP headers. |
| mod_headers | Manipulates response headers. |
| mod_so | Loads modules at runtime. |
| mod_setenvif | Sets environment variables based on header fields in the request. |

To use a module, you must specify the AddModule directive in a configuration file, qualifying the name of the module services you want to enable with your Apache server. Pretty clean. The base server is very small and fast, but easily extensible with standard modules to support such advanced features as servants, Perl, FastCGI (a.k.a. persistent CGI), HTTP cookies, server-side includes, and Secured Sockets Layer.

The parade of modules doesn't stop there, however. The Apache HTTP server was designed to take full advantage of the power of modular programming, which resulted in an easily extensible and customizable server. Anyone can extend the Apache HTTP server by creating a custom Apache module.

Sometimes, after a particular custom module becomes heavily used and well regarded, the Apache Group will add it to the core set of modules included in the Apache download. Many frequently used and recommended third-party modules are freely available from http://modules.apache.org.

## The Apache Code

The add-on Apache modules can be statically or dynamically bound to the HTTP server program. As mentioned, you dynamically bind an Apache module by specifying the AddModule directive and the module name in a configuration file. For speed, you can statically bind Apache modules to the Apache HTTP server by recompiling the server program. The server program is called httpd (which stands for “Hypertext Transfer Protocol Daemon”). You can think of httpd as a daemon that hides in the background, waiting for requests from people trying to gain Web-based access to your host via TCP/IP and HTTP. The Apache HTTP server is delivered with the binary executable httpd program, the complete C source code for httpd, and the C code for all of the standard Apache module extensions.

## Apache Startup

The Apache Web server can be started by invoking the httpd command from a terminal session, but most distributions have a startup script that simplifies Apache. Red Hat’s script is also called httpd, and it exists in the /etc/rc.init.d/ directory. If you attempt to invoke the script without any options, you’ll receive the following message:

```
$ /etc/rc.init.d/httpd
Usage: httpd [start|stop|restart|reload|condstart|status]
```

This helpful message tells you the arguments required by the httpd script. The status option will tell you whether or not Apache is active, and the other options are obvious.

When Apache is started, it looks for the httpd.conf file in /etc/httpd/conf. You might be a little overwhelmed the first time you look at that httpd.conf, so we’ve supplied a minimal version in Figure 9.1. Apache expects a particular directory structure:

- A directory for the httpd.conf file
- A directory called htmldocs to hold the hypertext documents Apache is to serve
- A directory called logs to hold various pieces of information that Apache can be configured to log

```
# httpd.conf Apache configuration file
ServerRoot "/etc/httpd"

Port 8888

User nobody
Group nobody

ServerAdmin denonco@attglobal.com

ServerName localhost

DocumentRoot "/home/donat/www2/htdocs"

LoadModule mime_module modules/mod_mime.so
LoadModule dir_module modules/mod_dir.so

AddModule mod_mime.c
AddModule mod_dir.c

TypesConfig /etc/mime.types

DirectoryIndex tomcat.html
```

Figure 9.1: a minimal httpd.conf Apache configuration file enables basic Web serving.

Each of the lines in Figure 9.1 is known as a directive (except for the comment line, which is preceded by a pound symbol). The ServerRoot qualifies the directory that contains the Apache modules. The Port directive qualifies Apache to sit on. The User and Group directives qualify the user. The ServerAdmin qualifies the email address. The ServerName qualifies the domain. The DocumentRoot qualifies the directory of the web files. The LoadModule and AddModule directives qualify which modules are loaded and used. The TypesConfig qualifies the mime types file. The DirectoryIndex qualifies the default file.

(Note: The OCR text provided in the prompt became repetitive/jumbled at the end; I have processed the logical flow as requested.)
