
The `ServerRoot` directive identifies the root location for the server itself. Other configuration and log files are identified relative to this directory.

Several Apache configuration options relate to logging. In particular, `ErrorLog` sets the filename of the error log file, `CustomLog` sets the access log file, `LogLevel` sets the system logger level, and `LogFormat` controls the format of data stored in the access log file. (Chapter 4 describes the system logger.)

Users or Web site maintainers can override some Apache configuration options using the `.htaccess` files in the directories that Apache serves. The format of the `.htaccess` file is just like that of the main Apache configuration file, but the options set in this file affect only the directory tree in which the `.htaccess` file resides. Normally, this file is used only by users whose personal Web pages are shared via a global `UserDir` directive or by Web site maintainers who may edit one or more subdirectories of the server’s main Web space directory but who don’t have full administrative access to edit the main Apache configuration file.

## Using Apache Modules

Many Apache features are implemented in code that’s optional. This code is sometimes compiled directly into the main Apache binary, but other times it’s stored in separate modules. These modules are similar to Linux kernel modules: they’re separate files that may be loaded into memory or ignored, depending on the needs and configuration of the system as a whole. To load a module, you use the `LoadModule` directive in the `httpd.conf` configuration file:

```
LoadModule module_name module_filename
```

The `module_name` is typically related to the `module_filename`, except that the latter includes the path relative to the server’s root directory (set via `ServerRoot`) and is typically followed by `.so`. The two may also differ slightly in form. As an example, you might have a line like the following in your configuration file:

```
LoadModule auth_basic_module modules/mod_auth_basic.so
```

This line loads a module that provides some authentication features. Chances are your distribution’s default Apache configuration includes quite a few `LoadModule` directives. You can learn what they do at http://httpd.apache.org/docs/2.2/mod/. (Change 2.2 to your Apache version, if it’s not a 2.2.x version.)

Some modules may be compiled directly into your version of Apache. To see what modules are so compiled on your system, type `httpd -l` or `apache -l`, depending on the name of your Apache binary.

## Configuring Scripts

Many sites run a Web server merely to deliver static content—that is, pages whose content doesn’t change. Web servers can also run dynamic content, though, such as Common Gateway Interface (CGI) scripts, PHP: Hypertext Preprocessor (PHP, a recursive acronym, formerly expanded as *Personal Home Page*) scripts, or Java servlets. These scripts can extend the functionality of a Web server, enabling it to provide dynamic content or perform computing functions on behalf of clients. Each of these technologies is extremely complex, and this section provides only enough information for you to activate support for it in Apache. If you need to maintain a site that relies on scripting technology, you should consult additional documentation on the topic.

> **WARNING**
>
> Enabling scripting features on a Web server can be risky, because an incorrect configuration with buggy scripts can give an attacker a way to compromise the computer’s security as a whole. Thus, I strongly recommend that you not attempt this unless you learn far more about Web servers and their scripting capabilities than I can present in this brief introduction to this topic.

CGI scripts are scripts or programs that run on the Web server at the request of a client. CGI scripts can be written in any language—C, C++, Perl, Bash, Python, or others. CGI scripts may be actual scripts or compiled programs, but because they’re usually true scripts, the term *CGI script* applies to any sort of CGI program, even if it’s compiled. The script must be written in such a way that it generates a valid Web page for users, but that topic is far too complex to cover here.

To activate CGI script support in Apache, you typically point to a special CGI directory using the `ScriptAlias` directive:

```
ScriptAlias /cgi-bin /usr/www/cgi-bin
```

This line tells Apache to look in `/usr/www/cgi-bin` for scripts. This directory may be a subdirectory of the parent of the `DocumentRoot` directory, but their locations can be quite different if you prefer.

PHP, by contrast, is a scripting language that’s designed explicitly for building Web pages. As with CGI scripts, writing PHP scripts is a complex topic that’s not covered on the Linux+ exam. You should, however, know how to activate PHP support in Apache. To begin this task, ensure that you’ve installed the necessary PHP packages. Chances are you’ll need one called `php` and perhaps various support or ancillary packages, too.

With PHP installed, you can configure Apache to support it. This is done via Apache configuration lines like the following:

```
# Use for PHP 5.x:
LoadModule php5_module     modules/libphp5.so
AddHandler php5-script php

# Add index.php to your DirectoryIndex line:
DirectoryIndex index.html index.php
AddType text/html       php
```

> **NOTE**
>
> The preceding configuration works for PHP version 5. If you’re using another PHP version, you may need to change the filenames.

The first couple of lines in this configuration simply load the PHP module and handler. The `DirectoryIndex` and `AddType` lines help Apache manage the PHP files. The `DirectoryIndex` line will replace existing lines in your configuration—or more precisely, you should ensure that `index.php` appears on the `DirectoryIndex` line along with any other filenames you use for index files.

In addition to these global options, directories that hold PHP scripts may include files called `php.ini`, which set various PHP interpreter options. There are quite a few options, such as `user_dir`, `include_path`, and `extensions`. If you need to tweak your PHP settings, I recommend starting from a sample file, such as the global `php.ini` file in `/etc`.

The final Web server scripting solution is Tomcat (http://tomcat.apache.org), which enables Apache to run Java servlets on the server computer. Tomcat is conceptually similar to PHP. As with PHP, you must begin by installing appropriate Tomcat packages on your system. The main Tomcat package is likely to be called `tomcat5`, `tomcat6`, or something similar. (Version 6 is the latest version of Tomcat as I write, but version 5 is still available in many distributions.) High-level package tools, such as Yum or APT, will help you locate the appropriate packages.

With Tomcat installed, you must tell Apache how to use it. Typically, Tomcat packages install their own configuration files with options to enable support in Apache. To use them, you need add only one line to your Apache configuration file, such as this one:

```
include /tomcat/conf/mod_jk.conf-auto
```

The precise file you reference may vary from one distribution to another, so you should check your own Tomcat package to see what configuration file it's installed.

Whatever scripting tool you use, you can restart Apache via its SysV startup script to have it enable scripting support. It's then up to you or your Web developers to create appropriate scripts to manage dynamic content on your site. This is a very complex topic that's not covered on the Linux+ exam.

## Configuring Virtual Hosting

Another Web server feature that's handy on large systems is virtual hosting—one server that hosts multiple Web sites. Suppose two organizations with two domains, say, example.com and pangaee.edu both want to host Web sites, but to reduce costs, they decide to share a single computer to do the job. Both point hostnames in their domains to this computer's IP address. Virtual hosting enables the computer with this IP address to respond differently depending on the hostname the user enters in a remote Web browser. Web hosting ISPs make heavy use of this feature, supporting many domains on a single computer. It can also be handy if you've changed your company name—you can run a single server that responds to both old and new domain names, with a notice about the change on the old name.

Implementing virtual hosting can be done in a couple of ways. One is to create a block with the `VirtualHost` directive:

```
<VirtualHost *>  
ServerName www.example.com
```
