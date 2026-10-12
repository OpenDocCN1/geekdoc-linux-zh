
If the IP address is cached or if the named daemon has not recently queried the server hosting that domain name, the nslookup command will respond with a nonauthoritative answer. This means that the time to live (TTL) for the domain has expired and the result pulled from the cache is no longer authoritative. The domain's IP address may have changed in the meantime. However, the IP address the nslookup command returned is what was pulled from that box's cache.

To change to another server and verify that the IP address received is valid elsewhere, enter the following command: `server <server name>`. Here is how a sample nslookup session may look when querying:

```
[kjcox@ns1 kj]$ nslookup
Default Server:     ns1.gnuware.com
Address:  205.82.148.254

> 205.82.148.20
Server:     ns1.gnuware.com
Address:  205.82.148.254

Name:     gnuware.com
Address:  205.82.148.20

> server ns1.vii.com
Default Server:     ns1.vii.com
Address:  206.71.77.2

>
```

Any name server queries will now ask ns1.vii.com for IP addresses or additional information rather than the local networked name server, ns1.gnuware.com. This is a viable alternative if your local name server is not correctly caching host-names. You can use nslookup for troubleshooting your configuration.

To look up the MX or mail server records for a particular domain, enter the following at the nslookup prompt:

```
> set q=mx
> gnuware.com
```

The output of this command will be similar to the following:

```
Server:	 ns1.gnuware.com
Address:	 205.82.148.10
```

```
gnuware.com	 preference = 10, mail exchanger = mail.gnuware.com
gnuware.com	 nameserver = ns1.gnuware.com
gnuware.com	 nameserver = ns2.gnuware.com
ns1.gnuware.com	 internet address = 205.82.148.254
ns2.gnuware.com	 internet address = 205.82.148.253
```

To set the type to be even more verbose, enter the following to extract more information from the queried name server:

```
> set q=any
```

You will find nslookup to be a useful tool when resolving IP addresses to domain names. To quit nslookup, enter `exit`. Entering `quit` will only return a “nonexistent host/domain” response. The nslookup utility will attempt to resolve the variable `quit` to a host or domain. You can also press `Ctrl-D` to stop the utility.

## Serving Up Web Pages

One of the most frequently used tools under Linux is Apache. Apache is probably the most popular Web daemon currently available for Linux. In fact, this tool is perhaps the prime reason that many burgeoning administrators even install Linux on a network machine. Apache enables them to try their hand at creating their own unique Web site or to host other virtual Web sites—sites that have domain names other than that of the local machine’s hostname. Apache comes installed by default under Red Hat Linux, even when the most minimal options are selected. Adding content to the default Web page is both quick and simple with Apache.

This section examines the basics for loading Apache on a Red Hat server and configuring it to meet your most fundamental needs. The section will look at some of the configuration settings for optimizing your machine and also explain how to install a secure server for doing e-commerce across the Internet. Because the topic of Apache could easily fill up an entire chapter covering all the nuances of its system, this chapter will simply cover the most basic settings.

# Part IV

# THINKING OUTSIDE THE BOX

If you wish to run a basic Web site, the standard RPM installation is sufficient to accomplish nearly any task. However, if you want to incorporate additional modules or programs such as PHP or MySQL databases into the setup, installing Apache from source code is the best option. Because so many of the systems at my office require *PHP scripting*, one method of incorporating database files into dynamic Web content, I often opt to install Apache from source. Try both using the RPM install and installing from source at least once to see which method you prefer.

## Installing the Apache RPMs

If the default installation has not already installed or updated the RPM packages, you can do so by locating the latest binaries from the RPM Repository site (http://rufus.w3.org/Linux/RPM/ or as it is now known http://www.rpmfind.net/). The key files are apache, apache-devel, and apache-manual. The last two files are not necessary but provide some valuable functionality if you want to develop the program further or read about Apache’s technical aspects.

Installation requires entering the following command as root in the same directory as that of the RPM files:

```
# rpm -ivh apache*
```

Or, if you want to upgrade to the latest Apache release, enter the following:

```
# rpm -Uvh apache*
```

Apache installs the httpd.conf configuration file in the /etc/httpd/conf/ directory. Older Apache releases included two additional files that required editing; srm.conf and access.conf. The latest Apache distribution consolidates these three configuration files into one. Here you can edit Apache’s root directory, determine how it handles httpd requests, and tweak a host of other configurable variables. The default variables already installed require little or no tweaking to operate.

The standard RPM install also creates a /home/httpd/ directory containing its respective cgi-bin/ and html/ directories. In the former, you can place CGI scripts that process perl or CGI requests from the Web pages. The html/ directory holds all static HTML Web pages. You place all *.html or *.htm files in this directory.

## Installing the Apache Daemon from Source

If you are installing Apache from source, the method is similar. The following steps are required to set up and configure Apache to run on a standard Linux machine successfully:

1. Download and unzip the Apache source code into a standard directory such as `/usr/local` or `/usr/local/etc`. I prefer the latter directory because that is the one in which older Apache releases were customarily installed.
2. Create a symbolic link between the expanded directory, such as `apache-1.3.3x/`, and a directory named `apache/`. To do this, change to the directory holding the expanded Apache files, then enter `ln -s apache-1.3.12 apache`.
3. Change to the new Apache directory, then go to the directory titled `src/` if you want to do the long manual installation (which is recommended) and then customize the file named `Configuration`.
4. If you wish to try the latest method, which resembles other source code compilation processes, remain in the same Apache directory and enter the following sequence of commands: `./configure --prefix=<prefix>`; `make`; `make install`; `<prefix>/bin/apachectl start`, replacing `<prefix>` with the Linux file system path under which Apache should be installed. For example, use `/usr/local/apache` or `/usr/local/etc/apache`.
5. There may not be much to change in the `Configuration` file, but look carefully through the file's contents for any additional modules you may wish to enable.
6. In the same directory, enter `./Configure`.
7. Enter `make`.
8. After the `make` command executes, you will have an executable file called `httpd` in that same directory. Copy the file down one level into the Apache root directory by entering `cp httpd ../`.
9. Customize the `httpd.conf` file located in the `conf/` directory. You will want to tailor this file to your server's specifications and needs.
10. To start up the server, enter the following (your system might require a different command): `/usr/local/etc/apache/httpd -f /usr/local/etc/apache/conf/httpd.conf`.
11. Test to make sure that the system is running by opening your base URL on a browser. For a machine named quasi.gnuware.com, for example, you would type the following URL in any browser window: `http://quasi.gnuware.com/`
12. You can also verify that the httpd daemon is running via the command line, by entering the following command: `ps -ef | grep root | grep http`.

Remember that your home html directory will no longer be /home/httpd/html/. If you installed everything as described in the preceding steps, you will find that your root html directory is in /usr/local/etc/apache/htdocs.

You will also want to modify your /etc/rc.d/init.d/httpd run command file. If you are impatient, copy the apache/bin/apachectl file to /etc/rc.d/init.d/ and rename it httpd. You should back up the original file first in case you later decide to use the older RPM Web daemon.

In the same root Apache directory you will also find the new cgi-bin/, conf/, and logs/ directories. Consult the Apache man pages for any additional information regarding system configuration. By following the preceding steps, you will be able to configure a new Web server from scratch and compile in any other modules or variables as needed.

## Securing the Web Server for E-Commerce

If you want to do any sort of secure transactions via the Internet, such as gathering credit card numbers and protecting them from prying eyes, you will probably need to set up encrypted Web pages using Apache. Though you can purchase various programs that will make your pages *encrypted* or enable the padlock icon on your Netscape Web browser, there are free modules that you can compile into your Apache Web daemon just as easily.

The only cost you might incur for setting up a secure site is the price of a secure certificate from one of two trusted sources: VeriSign and Thawte. Since it recently acquired Thawte, VeriSign now controls over 95 percent of the market for secure certificates. Though the two companies have merged, Thawte still offers certificates of the same quality as that of VeriSign, but at nearly a third of VeriSign's price.
