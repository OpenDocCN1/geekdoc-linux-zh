
## Preloading Perl Modules to Save Memory

CGI qw(-compile :standard), or CGI qw(-compile :standard :html3), and so on, to reduce memory usage by CGI.pm itself. Remember that keeping a lot of unused code in memory wastes your system resources.

Also notice that the CGI object, `$query`, is created within the `handler()` method. This is necessary because if you create a CGI object outside the `handler()` method in the global section of the module, such as the `$callCounter`, the object will be created once for the first request and it will only have that request's information. For example, if you move the `my $query = new CGI;` line outside of the `handler()` method and place it right after the `my $callCounter = 0;` line, the script will treat each subsequent request after the initial request as the same request. Thus, if you need to access the query string information using the `$query->param()` method, you will only get the data for the first request because the `$query` object is not created for each request. This is why it is very important that you create the request-specific `$query` object within the `handler()` method as shown in Listing 16-2.

The `SimpleAPIUsingCGI.pm` module provides the same functionality as the `SimpleAPI.pm` and can be run via the `http://your_server_name/cgim_example` URL after you add the following lines to `httpd.conf` and restart the server:

```
# Configuration for running mod_perl modules
PerlModule Development::SimpleAPIUsingCGI

<Location /cgim_example>
  SetHandler perl-script
  PerlHandler Development::SimpleAPIUsingCGI
</Location>
```

If you use a lot of CPAN modules such as CGI or DBI, or have a lot of custom-developed modules for your Apache server, you might want to use the `PerlModule` directive to preload them during server startup. Doing so saves time during the first request for such modules and also increases the chances of sharing the code pages (memory) among the Apache child processes. For example, if you use the standard CGI, DBI, and `Digest::MD5` modules in one or more of your `mod_perl` modules, you can simply preload these modules by placing the following directives in `httpd.conf`:

```
PerlModule CGI
PerlModule DBI
PerlModule Digest::MD5
```

Another approach is to use the `PerlRequire` directive. This directive can be set to an external Perl script that loads all the modules that you want to preload and possibly share among the Apache child processes. For example:

```
PerlRequire /usr/local/apache/apps/startup.pl
```

This tells Apache require the `/usr/local/apache/apps/startup.pl` script during startup. This script is loaded into memory, which, in turn, should load the necessary modules. For example, this script can be as follows:

```perl
#!/usr/bin/perl

use CGI ();
use DBI ();
use Digest::MD5 ();
1;
```

Each of the `use module_name ()` lines loads a specific module. The empty parentheses ensure that default importing of symbols from these modules is not performed, which saves some memory.

> **Note**
>
> If you use all the features of the `CGI.pm` module you can add `CGI->compile('all')` to the `startup.pl` script to compile them, which saves time during request processing.

Also, make sure that the `startup.pl` script is accessible and executable by the Apache user (set using `User` directive in `httpd.conf` file).

## Keeping Track of mod_perl Modules in Memory

Being able to keep track of which `mod_perl` modules your Web server is using is a great help in system administration. By using the `Apache::Status` module that comes with `mod_perl`, you can keep track of loaded modules and get lots of information about them. To do so, follow these steps:

1. As root, you must install the `perl::Syndump` module from a CPAN mirror site by using this command:
   ```
   perl -MCPAN -e 'install perl::Syndump'
   ```
2. Add the following configuration segment to the `httpd.conf` before any other `PerlModule` directive.
   ```
   PerlModule Apache::Status

   <Location /perl-status>
     SetHandler perl-script
     PerlHandler Apache::Status
   </Location>
   ```
   This code ensures that the `Apache::Status` module is loaded before any other modules. If you use the `PerlRequire` directive to load modules via an external startup script, you do not need the `PerlModule Apache::Status` line. Instead, load the `Apache::Status` module in the startup script before any other module.
3. Restart the Apache server and access information on loaded `mod_perl` modules by using `http://your_server_name/perl-status`. This page displays a list of options (links), as shown here:

   - Perl Configuration
   - Loaded Modules
   - Inheritance Tree
   - Enabled `mod_perl` Hooks
   - Environment
   - PerlRequired Files
   - Signal Handlers
   - Symbol Table Dump
   - ISA Tree
   - Compiled Registry Scripts

4. Click on the `Loaded Modules` link to view all the loaded `mod_perl` modules. The other links also provide valuable status information on the `mod_perl` specifics.

## Implementing ASP by Using the Apache::ASP Module

Active Server Page (ASP) is a common scripting platform in the Windows world. However, it is no longer a Windows-only scripting platform. By using `mod_perl` with the `Apache::ASP` CPAN module you can create ASP pages that have embedded Perl-based ASP scripts. Here is how:

1. As `root`, run the following command:
   ```
   perl -MCPAN -e 'install Apache::ASP'
   ```
   The CPAN module installs the `Apache::ASP` module from a local CPAN mirror site. If it fails for some reason, investigate why and resolve the issues. Usually installation is successful unless you are missing a prerequisite module. In such event, install the missing prerequisite module in the same manner, and then install `Apache::ASP`.

2. After the `Apache::ASP` module is installed, create a subdirectory called `asp` in your document root directory. I assume that your `DocumentRoot` directive is set to `/www/mysite/htdocs` and that you created the `/www/mysite/htdocs/asp` directory.

3. Create a test script called `test.asp` as shown below and store it in `/www/mysite/htdocs/asp` directory.
   ```html
   <html>
   <head><title>ASP Example</title></head>
   <body>

   <%          
   $Application->Lock();
   $Application->{Count}++;
   $Application->Unlock();
   %>
   <h1> ASP Page </h1>
   <hr>
   <p>
   This page has been called <%- $Application->{Count} %> times.
   </p>
   </body>
   </html>
   ```
   This simple `test.asp` ASP page simply increments the ASP Application object by one each time this page is called.

4. Add the following lines to the `httpd.conf` file:
   ```
   Alias /asp/ "/www/mysite/htdocs/asp"

   <Location /asp/>
     SetHandler perl-script
     PerlHandler Apache::ASP
     PerlSetVar Global /tmp
   </Location>
   ```
   Here's what's going on in the preceding lines:
   - The `/asp/` alias points to the `/www/mysite/htdocs/asp` directory. Make sure you change this so that it points to appropriate directory in your system.
   - The `<Location>` container tells Apache to use the `Apache::ASP` module to handle all the files in this directory; it also sets the `Global` variable to the `/tmp` directory.
   - The `Apache::ASP` module creates a directory called `/tmp/.state` in which it stores state information so that even if you shutdown and restart the server, the state information is not lost.

5. Change the file permissions for the `asp` directory and its contents to enable Apache user (i.e. allowing you set the `User` directive to in `httpd.conf`) to access the files. For example, use the `chown -R httpd:httpd /www/mysite/htdocs/asp` and `chmod -R 750 /www/mysite/htdocs/asp` commands to ensure that Apache user (httpd) and Apache group (httpd) can access the directory and files stored in it.

6. Restart the Apache server by using the `/usr/local/apache/bin/apachectl` restart command and access the `test.asp` page by using `http://your_server_name/asp/test.asp`.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_497_0.png)

To learn more about how to write ASP scripts in Perl visit the ASP Web site at www.apache-asp.org.
