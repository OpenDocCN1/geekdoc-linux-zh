# Listing 14-3: fontsize.fcgi

```
#!/usr/bin/perl

# Load the FCGI module
use FCGI;

# Global variables
my $MAX = 10;
my $i;

# FastCGI Loop
while (FCGI::accept() >= 0) {

    # Content Header
    print "Content-type: text/html\n\n";

    # Main Loop
    for ($i=0; $i < $MAX; $i++){
        print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";
    }
}

exit 0;
```

# ## Setting Up FastCGI for Apache

To install `mod_fastcgi` with Apache, follow these steps:

+   1. Download the latest `mod_fastcgi` module for Apache from www.fastcgi.com for Apache.
+   2. Extract the source in the `/usr/local/src` directory. A new directory called `mod_fastcgi_version` is created. Read the INSTALL file in this new directory for details on how to install the module, as the installation changes from time to time.
+   3. Copy the new directory to a subdirectory called fastcgi under the modules directory within your Apache source tree.
+   4. From the Apache source distribution directory, run the following `configure --enable-module=fastcgi` and any other options that you want to specify with the `configure script.` (See Chapter 3 for details on other options available for the `configure script.)` If you have already compiled Apache you can replace `configure` with `config.status` in the preceding command to ensure that all of the options you specified when you ran configure last time are applied again.
+   5. Run `make` and `make install` to compile and install Apache with `mod_fastcgi` support.