
```
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
...
</VirtualHost>
```

To implement IP-based dynamic virtual hosting instead, set the UseCanonicalName to DNS instead of Off.

```
UseCanonicalName DNS
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

## Interpolated Strings

The mod_vhosts_alias module supports various interpolated strings, each beginning with a % symbol and followed by a number. As you have seen, %0 references the entire Web address. %1 references only the first segment, %2 references the second, %-1 references the last part, and %2+ references from the second part on. For example, if you want to use only the second part of a Web address for the directory name, you would use the following directives:

```
VirtualDocumentRoot /var/www/hosts/%2/html
VirtualScriptAlias /var/www/hosts/%2/cgi-bin
```

In this case, a request made for www.mygolf.com/html/mypage would use only the second part of the Web address. This would be "mygolf" in www.mygolf.com, and would evaluate to

```
/var/www/hosts/mygolf/html/mypage
```

If you used %2+ instead, as in /var/www/hosts/%2/html, the request for www.mygolf.com/html/mypage would evaluate to

```
/var/www/hosts/mygolf.com/html/mypage
```

The same method works for IP addresses, where %1 references the first IP address segment, %2 references the second, and so on.

## Logs for Virtual Hosts

One drawback of dynamic virtual hosting is that you can set up only one log for all your hosts. However, you can create your own shell program to simply cut out the entries for the different hosts in that log.

```
LogFormat "%V %h %l %u %t \"%r\" %>s %b" vcommon
CustomLog logs/access_log vcommon
```

## IP Addressing

Implementing dynamic virtual hosting in the standard way as shown previously will slow down the process, as your server will have to perform a DNS lookup to discover the name of your server using its IP address. You can avoid this step by simply using the IP address for your virtual host's directory. So, for IP virtual host 192.198.1.6, you would create a directory /var/www/hosts/192.198.1.6, with an html subdirectory for that host's document root. You would use the VirtualDocumentRootIP and VirtualScriptAliasIP directives to use IP addresses as directory names. Now the IP address can be mapped directly to the document root directory name, no longer requiring a DNS lookup. Also be sure to include the IP address in your log, %A.

```
UseCanonicalName DNS
LogFormat "%A %h %l %u %t \"%r\" %>s %b" vcommon
CustomLog logs/access_log vcommon
VirtualDocumentRootIP /var/www/hosts/%0/html
VirtualScriptAliasIP /var/www/hosts/%0/cgi-bin
```

You can mix these commands in with other virtual host entries as you need them. For example, to specify the document root directory for a nondynamic name-based virtual host, you could simply use the **VirtualDocumentRoot** directive. In other words, you can simply use the same directories for both dynamic and nondynamic virtual hosts. You could still specify other directories for different nondynamic virtual hosts as you wish. In the following example, the **www.mypics.com** name-based virtual host uses the dynamic virtual host directive **VirtualDocumentRoot** to set its document root directory. It now uses **/var/www/www.mypics.com/html** as its document root directory. The CGI directory, however, is set as a nondynamic directory, **/var/www/mypics/cgi-bin**.

```
UseCanonicalName Off

NameVirtualHost 192.168.1.5

<VirtualHost 192.168.1.5>
ServerName www.mypics.com
ServerAdmin webmaster@mail.mypics.com
VirtualDocumentRoot /var/www/%0/html
ScriptAlias /var/www/mypics/cgi-bin
...
</VirtualHost>
```

## Server-Side Includes

Server-side includes (SSIs) are designed to provide a much more refined control of your Web site content, namely the Web pages themselves. Server-side includes are Apache directives placed within particular Web pages as part of the page's HTML code. You can configure your Apache Web server to look for SSI directives in particular Web pages and execute them. First, you have to use the Options directive with the include option to allow SSI directives.

### Options Includes

You need to instruct the server to parse particular Web pages. The easiest way to enable parsing is to instruct Apache to parse HTML files with specified extensions: Usually, the extension .shtml is used for Web pages that have SSI directives. In fact, in the default Apache configuration files, you can find the following entry to enable parsing for SSI directives in HTML files. The AddType directive here adds the .shtml type as an HTML type of file, and the AddHandler directive specifies that .shtml files are to be parsed (server-parsed).

```
# To use server-parsed HTML files
AddType text/html .shtml
AddHandler server-parsed .shtml
```

Instead of creating a separate type of file, you can use the XBitHack directive to have Apache parse any executable file for SSI directives. In other words, any file with execute permission (see Chapter 28) will be parsed for SSI directives.

SSI directives operate much like statements in a programming language. You can define variables, create loops, and use tests to select alternate directives. An SSI directive consists of an element followed by attributes that can be assigned values. The syntax for a SSI directive is shown here:

```
<!--#element attribute=value ... -->
```

You can think of an element as operating much like a command in a programming language and attributes as its arguments. For example, to assign a value to a variable, you use the set element with the variable assignment as its attribute. The if directive displays any following text on the given Web page. The if directive takes as its attribute expr, which is assigned the expression to test. The test is able to compare two strings using standard comparison operators such as <=, !=, or =. Variables used in the test are evaluated with the $ operator.

```
<!--#set myvar="Goodbye" -->
<!--#if expr="$myvar = Hello" -->
```

Other helpful SSI elements are exec, which executes CGI programs, or shell commands, which read the contents of a file into the Web page and also execute CGI files. The echo element displays values such as the date, the document's name, and the page's URL. With the config element, you can configure certain values, such as the date or file size.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_533_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abcchm.html

## PHP

PHP (PHP Hypertext Preprocessor) is a scripting language designed for use in Web pages. PHP-enabled pages allow you to create dynamic Web pages that can perform tasks instead of just displaying data. PHP is an official project of the Apache Software Foundation. You can find out more about PHP at www.php.net.

Unlike CGI programs, which are executed separately from a Web page, PHP commands are embedded as tags within the page itself, much as SSI commands are. PHP support to interpret and execute these commands is provided directly by the Web server. This embedded support is enabled in Apache with the mod_php module (`/etc/httpd/conf.d/php.conf` configuration file). Instead of having to separately construct programs to be invoked and run outside the Web server, with PHP, such commands are embedded within a Web page and run by the Web server. The Web server maintains complete control at all times whenever tasks are being performed. It is possible, however, to implement PHP in a CGI mode, where PHP pages are constructed as separate programs, invoked by a Web page much as a Perl-based CGI program is.

PHP has flexible and powerful programming capabilities on the same level as C and Perl. As in those languages, you can create control structures such as if statements and loops. In addition, PHP has capabilities specifically suited to Web page tasks. PHP can interact directly with databases such as Oracle, MySQL, and IBM DB2. It can easily interact with all the standard protocols, such as IMAP, LDAP, HTTP, and POP3. It even has text processing abilities such as interpreting regular expressions and displaying XML documents. There are also extensions for searches, compression tools like gzip, and language translations. PHP supports a massive collection of possible operations. Check its Web site for a complete listing, as well as online manuals and tutorials.
