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
EOF
for (keys %ENV) {
    print "$_ = ${ENV{\$_}}\\n";n}
print <<EOF;
</BODY>
</HTML>
EOF
```

If you're going to write CGI programs in Perl, take some time to study the CGI modules that come bundled with Perl. An extensive Perl module library, which contains many modules that are designed to be used when writing CGIs, is accessible at http://www.cpan.org.

If you're using many CGIs written in Perl, examine the mod_perl module. It embeds a Perl interpreter within the Apache server. Using this module will result in faster execution times for your CGIs because there is no need to start a new Perl interpreter for each request. You'll find information about using mod_perl under /usr/share/doc/mod_perl-1.99_05/docs/ directory if you install it from this book's CD-ROMs.

> Always check for security updates and bug fixes if you use CGIs developed by other users or outside developers. Poorly audited and improperly written CGIs can pose significant security threats in your system.

# SSI

Server-side includes are directives written directly into an HTML page, which the server parses when the page is served to the Web client. SSIs can be used to include other files, the output from programs, or environment variables.