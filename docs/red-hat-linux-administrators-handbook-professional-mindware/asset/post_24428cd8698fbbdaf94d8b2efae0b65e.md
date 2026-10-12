
For the curious, the **restart** argument makes **apachectl** send a SIGHUP signal to Apache, and the **graceful** argument makes it send a SIGUSR1 signal instead. Because the latter is user-defined (by the Apache developers), it is much more agreeable to the running server.

To get the full status of the running server, run the script as follows:

```
/path/to/bin/apachectl fullstatus
```

You get a page of information showing various server status data. Redirecting the status information to a file is recommended, because it most likely will be more than a full screen of details. Here is how to redirect the data to a file called `/tmp/status`:

```
/path/to/apache/sbin/apachectl fullstatus > /tmp/status 2>&1
```

To test the server configuration files for syntax errors, run the **apachectl** script as follows:

```
/path/to/apache/sbin/apachectl configtest
```

## **ab**

This utility allows you to run benchmarks on your Web server. Run the program without any options to find out about the command-line options it takes.

## **apxs**

This utility helps in compiling modules for dynamic loading. It is not useful unless you have Dynamic Shared Object (DSO) support enabled on your Apache server, and your version of Linux supports DSO.

## **logresolve.pl**

This Perl script is not installed automatically, but you can manually copy it to an appropriate place from the *src/support* directory of your Apache source distribution. This script resolves IP addresses found in an Apache log file to their host names. This script spawns child processes and uses the parent process to provide caching support to speed up DNS lookups, which are often very slow.

This utility works practically the same way as the logresolve.pl script, except that this executable program gets installed by default. To learn about the command-line syntax, run it with the -h option.

## **logresolve**

## **htpasswd**

This utility allows you to create username/password pairs for per-directory authentication schemes. To see the usage syntax, run the program without any arguments. Unlike the previously mentioned support tools, this utility gets installed in the bin directory of your Apache server installation directory.

## **dbmmanage**

This utility allows you to manage DBM-based username/password pairs for DBM-based authentication schemes. To see the usage syntax, run the program without any arguments. This utility is also installed in the bin directory of your Apache server installation directory.

## **htdigest**

This utility allows you to create username/password pairs for MD5 digest-based authentication schemes. To see the usage syntax, run the program without any arguments. This utility is also installed in the bin directory of your Apache server installation directory.

# **Customizing Apache with optional or third-party modules**

Try out the standard Apache first before you add any third-party modules, to make sure that everything is working before you introduce any third-party code to the picture. After the standard Apache is running on your system, you can customize it as you please. In such a case, you no longer need to run the configure script in the same manner you did the first time. A script called `config.status` is automatically created when you run the configure script. The `config.status` script maintains a history of the options you supplied to the configure script. For example, if you run the configure script as follows,

the `config.status` script will look like this:

```sh
#!/bin/sh
##
## config.status -- APACI auto-generated
## configuration restore script
##
## Use this shell script to rerun the APACI
## configure script for restoring your configuration.
## Additional parameters can be supplied.
##

./configure \
"--prefix=/usr/local/apache" \
"--disable-module=cgi" \
"$@"
```

Suppose you want to enable the usertrack module. Run `configure` again as follows:

```sh
./configure --prefix=/usr/local/apache \
--disable-module=cgi --enable-module=usertrack
```

Or, run the following:

```sh
./config.status --enable-module=usertrack
```

The `config.status` script makes it easier to work with `configure`, so use it for all future compilations. If you decide to start fresh, you can simply delete `config.status` and run `configure` to create a new `config.status` script.

## Adding FastCGI support

Before you can add FastCGI support in your Apache, you have to download the latest FastCGI module (`mod_fastcgi.c`) from the FastCGI Web site, http://www.fastcgi.com/, and follow the steps below:

- 1. Extract the FastCGI module distribution. Next, copy or move the distribution to the `src/modules/fastcgi` directory of your Apache source distribution.

Then, change directories to your top-level Apache source distribution directory and run the configuration script as follows:

```sh
./configure \
--activate-module=src/modules/fastcgi/libfastcgi.a
```

- 2. If you previously compiled Apache using APACI and want to keep the existing configuration along with the new mod_fastcgi.c module update, run the following command instead:

```sh
./config.status \
--activate-module=src/modules/fastcgi/libfastcgi.a
```

- 3. Now, rebuild the Apache server executable (httpd) by running the make command. If you get no error messages, run the make command again with the install option to reinstall the Apache executable.

- 4. After you build the new Apache executable, check to verify that the mod_fastcgi.c module is included in the executable. The easiest way to verify this is to run the following command:

```sh
/path/to/your/apache/httpd -l
```

- 5. Use the appropriate path instead of /path/to/your/apache, as shown earlier. You should see mod_fastcgi.c listed in the output produced by the -l option. If you don’t see it, you have missed one or more steps in compiling Apache, so go back and verify your steps.

## Adding an embedded Perl interpreter

Make sure you have the latest Perl version installed on your system. Check the version number of your installed Perl by using the `perl -v` command and verify what the latest version available is at http://perl.com/. If you don’t have the latest version, download and install it.

After you install the latest Perl version on your target system, download the latest version of mod_perl from http://perl.apache.org/.

Also, many of the tests used for verifying a mod_perl installation use the LWP Perl modules, so install LWP modules along with LWP’s prerequisite modules. If you have installed Perl properly, you can install the LWP modules quite easily using the CPAN module. Run CPAN as follows:

```sh
perl -MCPAN -install LWP
```

After you complete these prerequisite tasks, install the mod_perl module as follows:

- 1. Installing mod_perl support into your Apache server involves two parts: updating your Perl distribution with mod_perl, and then updating your Apache distribution with mod_perl. To make things simpler, this discussion assumes that you have downloaded and decompressed the mod_perl source distribution from http://perl.apache.org/ into a directory so that both Apache server and mod_perl source share the same top-level directory as their parent directory; in other words, both Apache source and mod_perl source distributions are subdirectories of a single parent directory. For this example installation, assume that the Apache server is in `/usr/local/build/apache-1.3.12`, and the mod_perl source distribution is in `/usr/local/build/mod_perl-1.16`. (Your version numbers for both Apache and mod_perl may vary.)

- 2. Change directories to the source distribution (`/usr/local/build/mod_perl-1.16`) and run the following command:

```sh
perl Makefile.PL APACHE_SRC=../apache-1.3.12/src \
DO_HTTPD=1 \
USE_APACI=1 \
PREP_HTTPD=1 \
EVERYTHING=1
```

- 3. This builds the Perl side of mod_perl and prepares the Apache side of mod_perl. Next, run the following commands, as long as any error messages do not stop you:

```sh
make
make test
make install
```

- 4. If you are compiling Apache for the first time, run the following command from the Apache source distribution directory to complete the Apache side of the mod_perl installation:

```sh
./configure --prefix=/path/to/where/you/want/to/install/apache \
--activate-module=src/modules/perl/libperl.a
```
