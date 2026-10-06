# Chapter 16 Setting Up a Web Site with the Apache Server 457

ScriptAlias /cgi-bin/ /srv/www/cgi-bin/

For the given example, the directive marks the target directory, /srv/www/cgi-bin, containing CGI scripts that will be processed by the Apache mod_cgi module 'cgi-script handler. Moreover, the mapping by this directive would result in any request for resources at http://ourservicever/cgi-bin/ causing the server to run a script in /srv/www/cgi-bin/.

However, CGI programs can be invoked from arbitrary directories. For CGI programs to reside anywhere in the directory of a site, two configuration steps need to be completed. First, the cgi-script handler must be activated using the AddHandler directive. Second, ExecCGI must be specified in the Options directive for any directory or subdirectories that may contain a CGI program.

...

```
<Directory /srv/www/htdocs/dir
Options +ExecCGI
</Directory>
```

The AddHandler directive serves to treat all files with the .cgi file extension as CGI programs. In addition the <Directory> container with the Options +ExecCGI directive tells Apache to permit execution of CGI programs that reside in the /srv/www/htdocs/dir or any subdirectories therein.

Listing 16-2 is a Perl script and an example CGI program that prints a welcome message to a client with the date.

# Listing 16-2: A Perl CGI script

```
#!/usr/bin/perl
# example.cgi
# An example script written to print a welcome message and the current
date
$month = =
('jan','feb','mar','apr','may','jun','jul','aug','sep','oct','nov','dec') [lo
caltime[4]];
$year = (localtime) [5];
$day = (localtime) [3];

print "Content-type: text/html\n\n"
print "<html><title>This is a test, is is only a test</title><body>\n"
print "Hello, World.<br>\br>/>"
print "Today is, $day;"
if ($day < 10) {
print "$month, "0",$day;
```

Continued