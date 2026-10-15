
is assigned the expression to test. The test is able to compare two strings using standard comparison operators such as <=, !=, or =. Variables used in the test are evaluated with the

```
<!--#set myvar="Goodbye" -->
<!--#if expr="$myvar = Hello" -->
```

Other helpful SSI elements are exec, which executes CGI programs, or shell commands, which read the contents of a file into the Web page and also execute CGI files. The echo element displays values such as the date, the document's name, and the page's URL. With the config element, you can configure certain values, such as the date or file size.

## PHP

PHP (PHP Hypertext Preprocessor) is a scripting language designed for use in Web pages. PHP-enabled pages allow you to create dynamic Web pages that can perform tasks instead of just displaying data. PHP is an official project of the Apache Software Foundation. You can find out more about PHP at www.php.net.

Unlike CGI programs, which are executed separately from a Web page, PHP commands are embedded as tags within the page itself, much as SSI commands are. PHP support to interpret and execute these commands is provided directly by the Web server. This embedded support is enabled in Apache with the mod_php module (/etc/httpd/conf.d/php.conf configuration file). Instead of having to separately construct programs to be invoked and run outside the Web server, with PHP, such commands are embedded within a Web page and run by the Web server. The Web server maintains complete control at all times whenever tasks are being performed. It is possible, however, to implement PHP in a CGI mode, where PHP pages are constructed as separate programs, invoked by a Web page much as a Perl-based CGI program is.

PHP has flexible and powerful programming capabilities on the same level as C and Perl. As in those languages, you can create control structures such as if statements and loops. In addition, PHP has capabilities specifically suited to Web page tasks. PHP can interact directly with databases such as Oracle, MySQL, and IBM DB2. It can easily interact with all the standard protocols, such as IMAP, LDAP, HTTP, and POP3. It even has text processing abilities such as interpreting regular expressions and displaying XML documents. There are also extensions for searches, compression tools like gzip, and language translations. PHP supports a massive collection of possible operations. Check its Web site for a complete listing, as well as online manuals and tutorials.

## Apache GUI Configuration Tools

Red Hat provides a GUI configuration tool called the Apache Configuration Tool, accessible from the GNOME and KDE desktops. Also available is Comanche, a popular Apache configuration tool that you download from the Internet. The Apache GUI Project (gui.apache.org) provides a set of GUI tools for configuring and managing your Apache Web server. Its currently active projects are Comanche and TkApache. In the Linuxconf utility, you can also configure your Apache Web server. Webmin provides a very complete Apache Web server module.

The Apache Configuration Tool opens with a window displaying panels for Main, Virtual Hosts, Server, and Performance Tuning. In each of these you will see buttons to open dialog boxes where you can enter default settings. You will also be able to enter settings for particular items such as virtual hosts and particular directories. For example, in the Virtual Hosts panel you can enter default settings for all virtual hosts, as well as add and edit particular virtual hosts. Click the Help button to display a Web page-based reference manual that details how to use each panel. On the Main panel, you enter your Web server address, the Web master’s e-mail address, and the ports the Web server will be listening on (see Figure 22-1).

On the Virtual Hosts panel, be sure to click the Edit Default Settings button to set the default settings for pages searches, error codes, log files, and directories. To add a virtual host, click Add to open a window where you can enter host information such as the virtual hostname and IP address. On the sidebar, you can select different configuration panels for the virtual host, such as log files and directory controls.

On the server panel, you set administrative settings such as the Apache server’s user ID and the process ID file. The Performance Tuning panel lets you set different usage limits such as the maximum number of requests and the number of requests per connection.

When the Apache Configuration Tool saves its settings, it will overwrite a Apache configuration file, /etc/httpd/conf/httpd.conf. It is advisable that you first make a backup copy of your httpd.conf file in case you want to restore the original settings created by your distribution for Apache. If you have already manually edited this file, you will receive a warning, and the Apache Configuration Tool will make a backup copy in /etc/httpd/conf/httpd.conf.bak.

![](img/6c226e8ba1efd427dec3bf582418d33f_465_0.png)
