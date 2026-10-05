# Networking and Internet Services
PART II

In order to execute CGI programs outside of the ScriptAlias directory, you will need to enable the ExecCGI option for that directory. This is done either in your httpd.conf file (access.conf prior to version 1.3.4) or in an .htaccess file in the directory.

CGI programs can be written in any language. The most popular languages for CGI programming are Perl, Python and C. You may want to pick up a good book on CGI programming, such as CGI Programming With Perl, Second Edition, since this is not intended to be a CGI book. You can also go to http://www.perl.org to help locate Perl resources on the net.

For Python, a good book is Internet Programming With Python or you can visit http://www.python.org.

To test whether you have CGI configured correctly, try the following CGI program, written in Perl, which displays the values of the HTTP environment variables:

```
#!/usr/bin/perl
print "Content-type: text/html\n";nprint "<html><head>Simple CGI program</title></head><body>\n";
for (keys %ENV) {
    print "\$_ = \ENV{\$_}<br>\n";
}
print "</body></html>\n";
```

If you are going to be writing CGI programs in Perl, you may want to look at the module that bundled with Perl.

# SSI

Server Side Includes are directives written directly into an HTML page, which the server parses when the page is served to the Web client. They can be used to include other files, the output from programs, or environment variables.

The most common way to enable SSI is to indicate that files with a certain filename extension (typically .shtml) are parsed by the server when they are served. This is accomplished with the following lines in your httpd.conf file (srm.conf prior to version 1.3.4).

```
# To use server-parsed HTML files
#n#AddType text/html .shtml
#AddHandler server-parsed .shtml
```

By uncommenting the AddType and AddHandler lines, you could tell the server to parse all .shtml files for SSI directives.