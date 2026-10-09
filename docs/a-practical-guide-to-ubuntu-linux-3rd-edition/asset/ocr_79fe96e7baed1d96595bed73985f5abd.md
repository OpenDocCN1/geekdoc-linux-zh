```
$ apt-cache search libapache2-mod
libapache2-mod-auth-kerb - apache2 module for Kerberos authentication
libapache2-mod-auth-mysql - Apache 2 module for MySQL authentication
libapache2-mod-auth-pam - Module for Apache2 which authenticate using PAM
libapache2-mod-auth-pgsql - Module for Apache2 which provides pgsql authentication
libapache2-mod-authnz - Module for Apache2 which provides plaintext authentication
libapache2-mod-auth-sys-group - Module for Apache2 which checks user against system group
libapache2-mod-macro - Create macros inside apache2 config files
libapache2-mod-perl2 - Integration of perl with the Apache2 web server
libapache2-mod-perl2-dev - Integration of perl with the Apache2 web server - development files
libapache2-mod-perl2-doc - Integration of perl with the Apache2 web server - documentation
libapache2-mod-php5 - server-side, HTML-embedded scripting language (apache 2 module)
libapache2-mod-php5filter - server-side, HTML-embedded scripting language (apache 2...)
libapache2-mod-python - Apache 2 module that embeds Python within the server
...
```

```
$ apt-cache search libapache2-mod | grep ruby
libapache2-mod-ruby - Embedding Ruby in the Apache2 web server
```

# mod_cgi AND CGI SCRIPTS

The CGI (Common Gateway Interface) allows external application programs to interface with Web servers. Any program can be a CGI program if it runs in real time (at the time of the request) and relays its output to the requesting client. Various kinds of scripts, including shell, Perl, Python, and PHP, are the most commonly encountered CGI programs because a script can call a program and reformat its output in HTML for a client.

Apache can handle requests for CGI programs in several different ways. The most common method is to put a CGI program in the cgi-bin directory and then enable its execution from that directory only. The location of the cgi-bin directory, as specified by the ScriptAlias directive (page 929), is /usr/lib/cgi-bin. Alternatively, an AddHandler directive (page 923) can identify the filename extensions of scripts, such as .cgi or .pl, within the regular content (for example, AddHandler cgi-script .cgi). If you use AddHandler, you must also specify the ExecCGI option in an Options directive within the appropriate <Directory> container. The mod_cgi module must be loaded to access and execute CGI scripts.

The following Perl CGI script displays the Apache environment. This script should be used for debugging only because it presents a security risk if remote clients can access it:

```
#!/usr/bin/perl
##
## printenv -- demo CGI program that prints its environment
##

print "Content-type: text/plain\n\n";
foreach $var (sort(keys(%ENV))) {
    $val = $ENV{$var};
    $val =~ s/\n/\\n/g;
    $val =~ s/"/"/g;
    print "$var=$val";";
}
```