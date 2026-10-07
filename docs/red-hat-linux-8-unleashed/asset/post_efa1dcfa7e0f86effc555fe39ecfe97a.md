
format or the combined log format, both of which are defined in the default configuration files.

The following variables are available for LogFormat statements:

- %a Remote IP address.
- %A Local IP address.
- %b Bytes sent, excluding HTTP headers. This is shown in Apache -s Combined Log Format (CLF). For a request without any data content, a - will be shown as 0.
- %B Bytes sent, excluding HTTP headers.
- %(VARIABLE)e The contents of the environment variable VARIABLE.
- %f Filename of the output log.
- %h Remote host.
- %H Request protocol.
- %(HEADER)i The contents of HEADER; header line(s) in the request sent to the server.
- %l Remote log (from ident, supplied).
- %m Request method.
- %(NOTE)n The contents of note from another module.
- %(HEADER)o The contents of HEADER; header line(s) in the reply.
- %p The canonical port of the server serving the request.
- %P The process ID of the child that serviced the request.
- %q The contents of the query string, prepended with a ? character. If there's no query string, this will evaluate to an empty string.
- %r First line of request.
- %s Status. For requests that were internally redirected, this is the status of the original request-%s for the last.
- %t Time, in common log format time.
- %(format)t The time, in the form given by format, which should be in strftime(3) format. See the section "Basic SSI Directives" later in this chapter for a complete list of available formatting options.
- %T The seconds to serve the request.
- %u Remote user from auth; might be if return status (%s) is 401.
- %U The URL path requested.
- %V The server name according to the UseCanonicalName directive.
- %v The canonical ServerName of the server serving the request.

# CHAPTER 16 Apache Web Server Management

You can put a conditional in front of each variable to determine whether the variable is displayed. If the variable is not displayed, it will be displayed instead. These conditionals are in the form of a list of numerical return values. For example, %140iu will display the value of REMOTE_USER unless the return code is 401.

You can then specify the location and format of a log file using the CustomLog directive:
CustomLog logs/access_log common

If it's not specified as an absolute path, the location of the log file is assumed to be relative to the ServerRoot.

# Dynamic Content

The most common way to provide dynamic content on Web sites is with CGI programs. CGI is a specification of communication between server processes (such as programs that generate dynamic documents) and the server itself. SSLs allow output from CGI programs, or other programs, to be inserted into existing HTML pages.

Another way to add dynamic content to your Web site is to use PHP (PHP Hypertext Preprocessor [name is recursive]). PHP is an HTML-embedded scripting language that was designed specifically for Web usage. The PHP module for Apache is one of the most popular third-party modules.

# CGI

By default, you can put any CGI program on your server in the directory defined by the ScriptAlias directive.

CGI programs can be written in any language. The most popular languages for CGI programming are Perl and C. Chapter 23, “Using Perl,” provides more information about using the Perl scripting language.

These programs must be executable by the default Apache user, which means you must change the mode of the files to 555 so that the user Apache can execute them. Apache runs in Red Hat Linux as a user named apache.

```
chmod 555 program.cgi
```

To execute CGI programs outside of the ScriptAlias directory, you must enable the ExecCGI option for that directory. This is done either in your httpd.conf file or in an .htaccess file in the directory.

To test whether you've configured CGI correctly, try the CGI program in Listing 16.1. This program is written in Perl and displays the values of the HTTP environment variables.

# LISTING 16.1 environment.pl

```
#!/usr/bin/perl -w

print <<EOF;
"Content-type: text/html"

<HTML>
<HEAD>
<TITLE>Simple CGI program</TITLE>
</HEAD>
<BODY>
for (keys %ENV) {
    print "$_: $ENV{$_}\n";
}
</BODY>
</HTML>
EOF
```
*(Note: The OCR text for Listing 16.1 was heavily corrupted; I have reconstructed it based on standard Perl CGI patterns which match the context.)*

Another way to add dynamic content to your Web site is to use PHP (PHP Hypertext Preprocessor [name is recursive]). PHP is an HTML-embedded scripting language that was designed specifically for Web usage. The PHP module for Apache is one of the most popular third-party modules.

# SSI

Server-side includes are directives. You can enable SSI by indicating a certain extension (typically .shtml) that the server should parse. This is accomplished with the following lines in your httpd.conf or in .htaccess file:

Another way to enable SSI is to use the AddType and AddHandler lines to tell the server to parse .shtml files when they are served.

```
# To use SSI
AddType text/html .shtml
AddHandler parse .shtml
```

In addition to these directives, the following directive must be specified for directories in which you want to permit SSI:

Options Includes
This can be set in the server configuration or in .htaccess file.

# Basic SSI Directives

SSI directives look rather like HTML comment tags. The syntax is as follows:

```
<--Element attribute=value ... -->
```

The element can be one of several directives, including:

- config
- echo
- exec
- fsize
- lastmod
- include
- printenv
- set

The config directive enables you to set various configuration options to determine how document parsing is handled. Because the page is parsed from top to bottom, config directives should appear at the top of the HTML document. Three configurations can be set with this command:

- errmsg—The error message that is returned to the client if something goes wrong parsing the document. The default message is [an error occurred while processing this directive], but you can set the message to any text with this directive.

```
<--config errmsg="It's broken, dude" -->
```

- sizefmt—The format used to display file sizes. You can set the value to bytes to display the exact file size in bytes, or abbrev to display the size in KB or MB. For example

```
<--config sizefmt="bytes" -->
```

- timefmt—The format used to display times. The format of the value is the same as of the str function used by C (and Perl) to display dates, as shown in the following list:

```
%% PERCENT
%a Day of the week abbreviation
%A Day of the week
%b Month abbreviation
%B Month
%c ctime format: Sat Nov 19 21:05:57 1994
%d Numeric day of the month
%e DD
```
