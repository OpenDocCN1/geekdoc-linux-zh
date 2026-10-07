
%D MM/DD/YY

%h Month abbreviation

%H Hour, 24-hour clock, leading zeros

%I Hour, 12-hour clock, leading zeros

%j Day of the year

%k Hour

%l Hour, 12-hour clock

%m Month number, starting with 1

%M Minute, leading zeros

%n NEWLINE

%o Ordinal day of month—1st, 2nd, 25th, and so on

%p AM or PM

%r Time format: 09:05:57 PM

%R Time format: 21:05

%S Seconds, leading zeros

%t Tab

%T Time format: 21:05:57

%U Week number, Sunday as first day of week

%w Day of the week, numerically; Sunday = 0

%W Week number, Monday as first day of week

%x Date format: 11/19/94

%X Time format: 21:05:57

%y Year (two digits)

%Y Year (four digits)

%Z Time zone in ASCII, such as PST

```
echo
```

The echo directive displays any of the include variables in the following list. Times are displayed in the time format specified by timefmt. Use the var attribute to indicate the variable to be displayed.

- DATE_GMT—The current date in Greenwich mean time.
- DATE_LOCAL—The current date in the local time zone.
- DOCUMENT_NAME—The filename (excluding directories) of the document requested by the user.
- DOCUMENT_URI—The (%-decoded) URL path of the document requested by the user. Note in the case of nested include files, this isn't the URL for the current document.
- LAST_MODIFIED—The last modification date of the document requested by the user.

execnThe exec directive executes a shell command or a CGI program, depending on the parameters. Valid attributes are cgi and cdi.

- cgi—The URL of a CGI program to be executed. The URL must be a local cgi, not one located on another machine. The CGI program is passed the QUERY_STRING and PATH_INFO that were originally passed to the requested document, so the URL cannot contain this information. You should use include instead of this directive.
- cmd—A shell command to be executed. The results will be displayed on the HTML page.

fsizenThe fsize directive displays the size of a file by either the file or virtual attribute. Size is displayed as specified with the sizefmt directive.

- file—The path (file system path) to a file, either relative to the root if the value starts with / or relative to the current directory if it doesn’t.
- virtual—The relative URL path to a file.

lastmod Displays the last modified date of a file. The desired file is specified as with the fsize directive.

includenThe directive includes the contents of a file. The file is specified with the file and virtual attributes, as with fsize and lastmod.

If the file is a CGI program and IncludesNOEXEC isn't, the program will be executed and the results displayed. This is to be used in preference to the exec directive. You can pass a QUERY_STRING with this directive—something you can’t with the exec directive.

printenv
Displays all existing variables. There are no attributes. For example
<!--#printenv -->

set
Sets the value of a variable. Attributes are var and value. For example
<!-#set var="animal" value="cow" -->

> NOTE
All defined CGI environment variables are also allowed as include variables.

> NOTE
In your configuration files (or in .htaccess), you can specify Options IncludesNOEXEC disal-low the exec directive because this is the least secure of the SSI directives. Be especially cautious
When users are able to create content (such as a guest book or discussion board) and these
options are enabled!

These variables can be used elsewhere with some of the following directives.

# Flow Control

Using the variables set with the set directive and the various environment and include variables, a limited flow control syntax can be used to generate a certain amount of dynamic content on server-parsed pages.

The syntax of the if/else functions is as follows:

```
<#if expr="test_condition" -->
<!--elif expr="test_condition" -->
<--#else -->
<!--endif -->
```

exp can be a string, which is considered true if nonempty, or a variety of comparisons tween two strings. Available comparison operators are =, !=, <, >, and >=. The second string has the format /string/, the strings are compared with regular expressions. Multiple comparisons can be string together with && (AND) and || (OR). Any text appearing between the if/elif/else directives will be displayed on the page. An example of such a structure follows:

```
<##set var="agent" value="$HTTP_USER_AGENT" -->
<!--#if expr="$agent /Mozilla/" -->
Mozilla!
```

```
<!--#else -->
Something else!
<!--#endif -->
```

This code will display Mozilla! if you're using a browser that passes Mozilla as part of its USER_AGENT string, and Something else! otherwise.

# Graphic Interface Configuration of Apache

Some of Apache's basic behavior can be configured using Red Hat's redhat-config-http, a GUI tool for the X Window System. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's... This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's... This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's... This can provide an easy way...

Some of Apache's basic behavior can be configured using Red Hat's redhat-config-http, a GUI tool for the X Window System. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way... This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way... This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks.

 This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's...

 This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way...

> NOTE
All defined CGI environment variables are also allowed as include variables.

> NOTE
In your configuration files (or in .htaccess), you can specify Options IncludesNOEXEC disal-low the exec directive because this is the least secure of the SSI directives. Be especially cautious
When users are able to create content (such as a guest book or discussion board) and these
options are enabled!

These variables can be used elsewhere with some of the following directives.

# Flow Control

Using the variables set with the set directive and the various environment and include
variables, a limited flow control syntax can be used to generate a certain amount of
dynamic content on server-parsed pages.

The syntax of the if/else functions is as follows:

```
<#if expr="test_condition" -->
<!--elif expr="test_condition" -->
<--#else -->
<!--endif -->
```

exp can be a string, which is considered true if nonempty, or a variety of comparisons
tween two strings. Available comparison operators are =, !=, <, >, and >=.
The second string has the format /string/, the strings are compared with regular expressions.
Multiple comparisons can be string together with && (AND) and || (OR). Any text appearing
between the if/elif/else directives will be displayed on the page. An example
of such a structure follows:

```
<##set var="agent" value="$HTTP_USER_AGENT" -->
<!--#if expr="$agent /Mozilla/" -->
Mozilla!
```

```
<!--#else -->
Something else!
<!--#endif -->
```

This code will display Mozilla! if you're using a browser that passes Mozilla as part of its USER_AGENT string, and Something else! otherwise.

# Graphic Interface Configuration of Apache

Some of Apache's basic behavior can be configured using Red Hat's redhat-config-http, a GUI tool for the X Window System. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an...

Some of Apache's basic behavior can be configured using Red Hat's redhat-config-http, a GUI tool for the X Window System. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's user and group name, location of PID and process locks. This can provide an easy way to configure settings such as Apache's...

In the General Options, to set defaults as which files are loaded when no files are specified (the default is index.*)

# CHAPTER 16 Apache Server Management

![](img/446debe023486a07fde5752457a3ff_579_0)

FIGURE 16.2 The redhat-config-httpd main dialog provides access to basic configuration of the Apache server.

![](img/446debe023486a07fde5752457a3ff_579_1)

FIGURE 16.3 redhat-config-httpd's Virtual Host Properties gives access to numerous options for configuring the properties of Apache's virtual hosts.
