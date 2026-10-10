
# HTTPd web server

For a while after the NCSA HTTPd project was discontinued, a number of people wrote a variety of patches for the code, to either fix bugs or add features they wanted. A lot of this code was floating around and people were freely sharing it, but it was completely unmanaged.

After a while, Brian Behlendorf and Cliff Skolnick set up a centralized repository of these patches, and the Apache project was born. The project is still composed of a small core group of programmers, but anyone is welcome to submit patches to the group for possible inclusion in the code.

There’s been a surge of interest in the Apache project over the past several years, partially buoyed by a new interest in open source on the part of enterprise-level information services. It’s also due in part to crippling security flaws found in Microsoft’s Internet Information Services (IIS); the existence of malicious web task exploits; and operating system and networking vulnerabilities to the now-infamous Code Red, Blaster, and Nima worms. IBM made an early commitment to support and use Apache as the basis for its web offerings and has dedicated substantial resources to the project because it makes more sense to use an established, proven web server.

In mid-1999, The Apache Software Foundation was incorporated as a nonprofit company. A board of directors, elected on an annual basis by the ASF members, oversees the company. This company provides a foundation for several open-source software development projects, including the Apache Web Server project.

The best places to find out about Apache are the Apache Software Foundation’s website, http://www.apache.org/, and the Apache Week website, http://www.apacheweek.com/, where you can subscribe to receive Apache News by email to keep up on the latest developments in the project, keep abreast of security advisories, and research bug fixes.

> **TIP**
> 
> You’ll find an overview of Apache in the Apache Software Foundation’s frequently asked questions (FAQs) at http://httpd.apache.org/docs-2.2/faq/ . In addition to extensive online documentation, you can also find the complete documentation for Apache in the HTML directory of your Apache server. You can access this documentation by looking at http://localhost/manual/index.html on your new Fedora system with one of the web browsers included on your system. You’ll need to have Apache running on your system!

Fedora ships with Apache 2.2, and the server (named httpd) is included on this book’s CD-ROMs and DVD. You can obtain the latest version of Apache as an RPM installation file for a Fedora FTP server; upgrade using *update*, *yum*, or *apt-get*; or get the source code from the Apache website and, in true Linux tradition, build it for yourself.

To determine the version of Apache included with your system, use the web server’s -V command-line option like this:

```bash
$ /usr/sbin/httpd -V
Server version: Apache/2.2.4 (Unix)
Server built: April 10 2007 12:47:09
```

The output continues on the next page:

```bash
Server's Module Magic Number: 20051115:4
Architecture: 32-bit
Server MPM: Prefork
threaded: no
forked: yes (variable process count)
Server compiled with... 
```

The output displays the version number, build date and time, platform, and various options used during the build. You can use the -v option to see terser version information.

## Installing the Apache Server

You can install Apache through Pirut, from your own RPMs, or build it yourself from source code. The Apache source builds on just about any Unix-like operating system and on Win32. If you elect to install the Web Server group of files when first installing Fedora, Apache and related software and documentation in 17 packages are installed automatically.

If you're about to install a new version of Apache, you should shut down the old server. Even if it's unlikely that the old server will interfere with the installation procedure, shutting it down ensures that there will be no problems. If you don't know how to stop Apache, see the “Starting and Stopping Apache” section later in this chapter.

### Installing Through Pirut

Although the “Web Server” category was available during install, it's often best to install Fedora clean of any services so that you minimize your attack vectors out of the box. As soon as Fedora is installed, you can use Pirut to add Apache by choosing Web Server from the Servers category.

However, you might find it useful to use the List tab rather than the Browse tab, because all the Apache modules start with “mod” to help you find them easily. Fedora ships with many Apache modules, some of which are discussed in the following sections. However, only a handful are enabled by default—you need to use Pirut to install and activate them.

### Installing from the RPM

You can find the Apache RPM on the Fedora installation media, on the Fedora FTP server, or at one of its many mirror sites. Check the Fedora site as often as possible to download updates as they become available. Updated RPM files usually contain important bug and security fixes. When an updated version is released, install it as quickly as possible to keep your system secure.

> **NOTE**
> 
> Check the Apache site for security reports. Browse to http://httpd.apache.org/security_report.html for links to security vulnerabilities for Apache 1.3, 2.0, and 2.2. Subscribe to a support list or browse through up-to-date archives of all Apache mailing lists at http://httpd.apache.org/mail/ (for various articles) or http://httpd.apache.org/lists.html (for comprehensive and organized archives).

If you want the most recent, experimental version of Apache for testing, check Red Hat's Rawhide distribution, which is also available on the Fedora FTP server (http://download.fedorahat.com/pub/fedora/linux/core/development/). This distribution is experimental and always contains the latest versions of all RPMs. However, note that the Apache package might depend on new functionality available in other RPMs. Therefore, you might need to install many new RPMs to be able to use packages from Rawhide. If you still want to use an Apache version from the Rawhide distribution for testing, a better option might be to download the source code RPM (SRPM) and compile it yourself. That way, you avoid dependencies on other new packages.

> **CAUTION**
> 
> You should be wary of installing experimental packages, and never install them on production servers (that is, servers used in “real life”). Very carefully test the packages beforehand on a host that isn’t connected to a network!

After you have obtained an Apache RPM, you can install it with the command-line rpm tool by typing the following:

```bash
rpm -Uvh latest_apache.rpm
```

where `latest_apache.rpm` is the name of the latest Apache RPM.

The Apache RPM installs files in the following directories:

- `/etc/httpd/conf/` — This directory contains the Apache configuration file, httpd.conf. See the section “Configuring Apache for Peak Performance” later in this chapter for more information.
- `/etc/rc.d/` — The tree under this directory contains the system startup scripts. The Apache RPM installs a startup script named `httpd` for the web server under the `/etc/rc.d/init.d` directory. This script, which you can use to start and stop the server from the command line, also automatically starts and stops the server when the computer is halted, started, or rebooted.
- `/var/www/` — The RPM installs the default server icons, Common Gateway Interface (CGI) programs, and HTML files in this location. If you want to keep web content elsewhere, you can do so by making the appropriate changes in the server configuration files.
- `/var/www/manual/` — If you’ve installed the `apache-manual` RPM, you’ll find a copy of the Apache documentation in HTML format here. You can access it with a web browser by going to http://localhost/manual/.
- `/usr/share/man/` — Fedora’s Apache RPM also contains man pages, which are placed underneath this directory. For example, the `httpd` man page is in section 8 of the man directory.
