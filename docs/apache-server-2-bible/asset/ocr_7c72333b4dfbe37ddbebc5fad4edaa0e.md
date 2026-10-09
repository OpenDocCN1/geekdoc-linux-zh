CGI qw(-compile :standard), or CGI qw(-compile :standard :html3), and so on, to reduce memory usage by CGI.pm itself. Remember that keeping a lot of unused code in memory wastes your system resources.

Also notice that the CGI object, $query, is created within the handler() method. This is necessary because if you create a CGI object outside the handler() method in the global section of the module, such as the $callCounter, the object will be created once for the first request and it will only have that request's information. For example, if you move the my $query = new CGI; line outside of the handler() method and place it right after the my $callCounter = 0; line, the script will treat each subsequent request after the initial request as the same request. Thus, if you need to access the query string information using the $query->param() method, you will only get the data for the first request because the $query object is not created for each request. This is why it is very important that you create the request-specific $query object within the handler() method as shown in Listing 16-2.

The SimpleAPIUsingCGI.pm module provides the same functionality as the SimpleAPI.pm and can be run via the http://your_server_name/cgipm_example URL after you add the following lines to httpd.conf and restart the server:

```
# Configuration for running mod_perl modules
PerlModule Development::SimpleAPIUsingCGI

<Location /cgim_example>
  SetHandler perl-script
  PerlHandler Development::SimpleAPIUsingCGI
</Location>
```

# ## Preloading Perl Modules to Save Memory

If you use a lot of CPAN modules such as CGI or DBI, or have a lot of custom-developed modules for your Apache server, you might want to use the PerlModule directive to preload them during server startup. Doing so saves time during the first request for such modules and also increases the chances of sharing the code pages (memory) among the Apache child processes. For example, if you use the standard CGI, DBI, and Digest::MD5 modules in one or more of your mod_perl modules, you can simply preload these modules by placing the following directives in httpd.conf:

```
PerlModule CGI
PerlModule DBI
PerlModule Digest::MD5
```

Another approach is to use the PerlRequire directive. This directive can be set to an external Perl script that loads all the modules that you want to preload and possibly share among the Apache child processes. For example:

```
PerlRequire /usr/local/apache/apps/startup.pl
```