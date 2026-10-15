
script and other compatibility reasons), many new sites are migrating to or starting out using the latest stable version.

After you have the tar file, you must unroll it in a temporary directory, such as /tmp. Unrolling this tar file creates a directory called apache_version_number, where version_number is the version you have downloaded (for example, apache_1.3.34).

There are two ways to compile the source—the old, familiar way (at least, to those of us who have been using Apache for many years) by editing Makefile templates, and the new, easy way using a configure script. You will first see how to build Apache from source the easy way. The configure script offers a way to have the source software automatically configured according to your system. However, manually editing the configuration files before building and installing Apache provides more control over where the software is installed and which capabilities or features are built in to Apache.

## TIP

As with many software packages distributed in source code form for Linux and other UNIX-like operating systems, extracting the source code results in a directory that contains a README and an INSTALL file. Be sure to peruse the INSTALL file before attempting to build and install the software.

## Using ./configure to Build Apache

To build Apache the easy way, run the ./configure script in the directory just created. You can provide it with a --prefix argument to install it in a directory other than the default, which is /usr/local/apache/. Use this command:

```
# ./configure --prefix=/preferred/directory/
```

This generates the Makefile that is used to compile the server code.

Next, type make to compile the server code. After the compilation is complete, type make install as root to install the server. You can now configure the server via the configuration files. See the "Runtime Server Configuration Settings" section for more information.

## TIP

A safer way to install a new version of Apache from source is to use the ln command to create symbolic links of the existing file locations (listed in the "Installing with APT" section earlier in this chapter) to the new locations of the files. This method is safer because the default install locations are different from those used when the package installs the files. Failure to use this installation method could result in your web server process not being started automatically at system startup.

Another safe way to install a new version of Apache is to first back up any important configuration directories and files (such as /etc/apache2) and then use the apt-get command to remove the server. You can then install and test your new version and, if needed, easily restore your original server and settings.

It is strongly recommended that you use Ubuntu's version of Apache until you really know what happens at system startup. No "uninstall" option is available when installing Apache from source!

## Apache File Locations After a Build and Install

Files are placed in various subdirectories of /usr/local/apache (or whatever directory you specified with the --prefix parameter) if you build the server from source.

The following is a list of the directories used by Apache, as well as brief comments on their usage:

- /usr/local/apache/conf—This contains several subdirectories and the Apache configuration file, httpd.conf. Debian-based systems such as Ubuntu often rename this to apache2.conf, so your mileage may vary. See the section "Editing apache2.conf" later in this chapter to learn more about configuration files.
- /usr/local/apache—The cgi-bin, icons, and htdocs subdirectories contain the CGI programs, standard icons, and default HTML documents, respectively.
- /usr/local/apache/bin—The executable programs are placed in this directory.
- /usr/local/apache/logs—The server log files are placed in this directory. By default, there are two log files—access_log and error_log—but you can define any number of custom logs containing a variety of information (see the "Logging" section later in this chapter). The default location for Apache's logs as installed by Ubuntu is /var/log/apache2.

## A Quick Guide to Getting Started with Apache

Setting up, testing a web page, and starting Apache using Ubuntu can be accomplished in just a few steps. First, make sure that Apache is installed on your system. Either select it during installation or install the server and related package files (refer to Chapter 31 if you need to install the server software).

Next, set up a home page for your system by editing (as root) the file named Index.html under the /var/www directory on your system. Make a backup copy of the original page or ww directory before you begin so you can restore your web server to its default state if necessary.

Start Apache through the Services window (under System, Administration from the menu bar), making sure to enable "Web Server".

You can also use the apache2 script under the /etc/init.d/ directory, like this:

```
sudo /etc/init.d/apache2 start
```

You can then check your home page by running a favorite browser and using localhost, your system's hostname, or its Internet Protocol (IP) address in the URL. For example, with the links text browser, use a command line like this:

```
# links http://localhost/
```
