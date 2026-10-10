
- `/usr/bin` — Some of the utilities from the Apache package are placed here—for example, the `htpasswd` program, which is used for generating authentication password files.
- `/var/log/httpd` — The server log files are placed in this directory. By default, there are two important log files (among several others): `access_log` and `error_log`. However, you can define any number of custom logs containing a variety of information. See the “Logging” section, later in this chapter, for more detail.
- `/usr/src/redhat/SOURCES/` — This directory might contain a tar archive containing the source code for Apache and, in some cases, patches for the source. You must have installed the Apache SRPM for these files to be created.

When Apache is running, it also creates the file `httpd.pid`, containing the process ID of Apache's parent process in the `/var/run/` directory.

> **NOTE**  
> If you are upgrading to a newer version of Apache, RPM doesn't write over your current configuration files. RPM moves your current files and appends the extension `.rpmnew` to them. For example, `srm.conf` becomes `srm.conf.rpmnew`.

## Building the Source Yourself

There are several ways to obtain the source code for Apache. Fedora provides SRPMs containing the source of Apache, which include patches to make it work better with the Fedora distribution. The most up-to-date, stable binary version for Fedora can be installed through `Pirut`, or by installing a source RPM from Fedora's source repository. When you install one of these SRPMs, a tar archive containing the Apache source is created in `/usr/src/redhat/SOURCES/`.

After you have the `tar` file, you must unroll it in a temporary directory, such as `/tmp`. Unrolling this tar file creates a directory called `apache_version_number`, where `version_number` is the version you've downloaded (for example, `apache_1.3.21`).

You can also download the source directly from `http://www.apache.org/`. The latest version at the time of this writing, `2.2.6`, is a 6MB compressed tape archive, and the latest pre-`2.0` version of Apache is `1.3.31`. Although many sites continue to use the older version (for script and other compatibility reasons), many new sites are migrating to or starting out with the latest stable version.

> **TIP**  
> As with many software packages distributed in source code form for Linux and other Unix-like operating systems, extracting the source code results in a directory that contains a `README` and an `INSTALL` file. Be sure to peruse the `INSTALL` file before attempting to build and install the software.

To build Apache the easy way, run the `./configure` script in the directory just created. You can provide it with a `--prefix` argument to install it in a directory other than the default, which is `/usr/local/apache/`. Use this command:

```bash
# ./configure --prefix=/preferred/directory/
```

This generates the makefile that’s used to compile the server code.

Next, type `make` to compile the server code. After the compilation is complete, type `make install` as root to install the server. You can now configure the server via the configuration files. See the “Runtime Server Configuration Settings” section, later in this chapter, for more information.

> **TIP**  
> A safer way to install a new version of Apache from source is to use the `ln` command to create symbolic links of the existing file locations (listed in the “Installing from the RPM” section earlier in this chapter) to the new locations of the files. This method is safer because the default install locations are different from those used when the RPM installs the files. Failure to use this installation method could result in your web server process not being started automatically at system startup.
>
> Another safe way to install a new version of Apache is to first back up any important configuration directories and files (such as `/etc/httpd`) and then use the `rpm` command to remove the server. You can then install and test your new version and, if needed, easily restore your original server and settings.
>
> It is strongly recommended that you use Fedora’s RPM version of Apache until you really know what happens at system startup. No “uninstall” option is available when installing Apache from source!

## Apache File Locations After a Build and Install

Files are placed in various subdirectories of `/usr/local/apache` (or whatever directory you specified with the `--prefix` parameter) if you build the server from source.

The following is a list of the directories used by Apache, as well as brief comments on their usage:

- `/usr/local/apache/conf/` — This contains several subdirectories and the Apache configuration file, `httpd.conf`. See the “Editing httpd.conf” section, later in this chapter, to learn more about configuration files.
- `/usr/local/apache/` — The `cgi-bin`, `icons`, and `htdocs` subdirectories contain the CGI programs, standard icons, and default HTML documents, respectively.
- `/usr/local/apache/bin/` — The executable programs are placed in this directory.
- `/usr/local/apache/logs/` — The server log files are placed in this directory. By default, there are two log files—`access_log` and `error_log`—but you can define any number of custom logs containing a variety of information (see the “Logging” section later in this chapter). The default location for Apache’s logs as installed by Fedora is `/var/log/httpd`.

## A Quick Guide to Getting Started with Apache

Setting up, testing a web page, and starting Apache with Fedora can be accomplished in just a few steps. First, make sure that Apache is installed on your system. Either select it during installation or install the server and related RPM files.

Next, set up a home page for your system by editing (as root) the file named `index.html` under the `/var/www/html` directory on your system. Make a backup copy of the original page or www directory before you begin so that you can restore your web server to its default state if necessary.

Start Apache (again, as root) by using the service command with the keywords `httpd` and `start`, like this:

```bash
# service httpd start
```

You can also use the `httpd` script under the `/etc/rc.d/init.d/` directory, like this:

```bash
# /etc/rc.d/init.d/httpd start
```

You can then check your home page by running a favorite browser and using `localhost`, your system’s hostname, or its Internet Protocol (IP) address in the URL. For example, with the `links` text browser, use a command line like this:

```bash
# links http://localhost/
```

For security reasons, you shouldn’t start and run Apache as root if your host is connected to the Internet or a company intranet. Fortunately, Apache is set to run as the user and group `apache` no matter how it’s started (by the `user` and `group` settings in `/etc/httpd/httpd.conf`). Despite this safe default, Apache should be started and managed by the user named `apache`, defined in `/etc/passwd` as:

```
apache:x:48:48:Apache:/var/www:/sbin/nologin
```

After you are satisfied with your website, use the `setup` (select Services) or `ntsysv` (select httpd) command to ensure that Apache is started properly.

It is time to start Apache up for the first time. The following sections show how to start and stop Apache, or configure Fedora to start or not start Apache when booting.

### Starting the Apache Server Manually

You can start Apache from the command line of a text-based console or X terminal window, and you must have root permission to do so. The server daemon, httpd, recognizes several command-line options you can use to set some defaults, such as specifying where httpd reads its configuration directives. The Apache httpd executable also understands other options that enable you to selectively use parts of its configuration file, specify a different location of the actual server and supporting files, use a different configuration file (perhaps for testing), and save startup errors to a specific log. The -v option causes Apache to print its development version and quit. The -V option shows all the settings that were in effect when the server was compiled.

The -h option prints the following usage information for the server (assuming that you're running the command as root):

```bash
# httpd -h

Usage: httpd [-D name] [-d directory] [-f file]
  [-C "directive" | -c "directive"]
  [-k start|restart|graceful|stop]
  [-v] [-V] [-h] [-l] [-L] [-t]

Options:
 -D name        : define a name for use in <IfDefine name> directives
 -d directory   : specify an alternate initial ServerRoot
 -f file         : specify an alternate ServerConfigFile
 -C "directive" : process directive before reading config files
 -c "directive" : process directive after reading config files
 -e level        : show startup errors of level (see LogLevel)
 -E file         : log startup errors to file
 -v              : show version number
 -V              : show compile settings
 -h              : list available command-line options (this page)
 -l              : list compiled in modules
 -L              : list available configuration directives
 -t -D DUMP_VHOSTS : show parsed settings (currently only vhost settings)
 -t              : run syntax check for config files
```

Other options include listing Apache's *static modules*, or special, built-in independent parts of the server, along with options that can be used with the modules. These options are called *configuration directives* and are commands that control how a static module works. Note that Apache also includes nearly 50 *dynamic modules*, or software portions of the server that can be optionally loaded and used while the server is running.

The -t option is used to check your configuration files. It's a good idea to run this check before restarting your server, especially if you've made changes to your configuration files.
