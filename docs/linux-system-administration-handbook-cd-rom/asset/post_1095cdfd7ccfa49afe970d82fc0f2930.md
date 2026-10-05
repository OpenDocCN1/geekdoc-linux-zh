
## 15.1 Web Server Software

rather silly idea that no one outside the United States could make stronger encryption). With these restrictions gradually loosening and strong (128-bit) encryption now available on Web servers sold inside and outside the United States, browsers are appearing which support stronger encryption. Within the United States, it is possible to get enhanced versions of Netscape's browser use 128-bit encryption. For more information on encryption and security, see the chapter on security.

Below is a sampling of secure and insecure httpd servers.

## Non-SSL Servers

- Apache (http://www.apache.org/)—currently the most popular Web server, has down. Loaded with features, it is also fast, free, and extensible.

- Boa (http://www.boa.org/)—a very new, fast Web server available with source code. Unlike Apache, it does not fork off child processes to handle additional clients; it multiplexes all connections internally.

- W3C http (formerly known as CERN httpd) (http://www.w3.org/pub/WWW/Daemon/)—the first Web server, ever. No longer in production, it is included for the sake of completeness;;

- NCSA (http://hohoo.ncsa.uiuc.edu/)—the successor to CERN and later the base for Apache, which has largely supplanted it.

- Ren (http://www.roxen.com/)—a commercial Web and FTP server. It also uses an extension to HTML called RXML (developed by Roxen) that allows pages to be modified at download time. It is available for free, or you can purchase it, along with commercial support. Source code is available, as well. Additionally, an SSL version is in progress and beta versions of it are freely available.

- WN (http://hof.math.nwu.edu/)—another freeware Web server. Not as extensible as Apache, but it has some nice features for modifying pages as they are served. (Also paired with a Gopher server under the name GN. See http://hof.math.nwu.edu/70/ for more information.)

- Zeus (http://www.zeus.co.uk/)—another non-forking server (like Boa). It is commercial and somewhat pricey, but then you get some commercial support. Source code is unavailable.

## SSL Servers

- Stronghold (http://www.c2.net)—As its alternate name suggests, this is Apache with SSL built in. It is unlike most commercial software that it comes with source code, and thus, none of Apache's extensibility is lost. Unlike Apache, Stronghold is not the most popular commercial Web server in its class; it is the second-most popular secure server.

- Apache-SSL (http://www.algar.co.uk/apache-SSL/)—It is free-Apache with SSL support. Since the SSL libraries that it uses were illegally exported from the United States, its use within the United States is illegal. It is essentially the same as Stronghold as far as the actual code is concerned. Both it and Stronghold support 128-bit encryption and have done so for some time.

- Roxen (http://www.roxen.com/)—Rox also comes in an SSL flavor.

- Zeus (http://www.zeus.co.uk)—Similar to Roxen, Zeus also comes in a secure version.

## 15.2 Hardware Issues

One of the primary considerations, if you are using a forking server or lots of interpreted CGI, is memory. Each server obviously takes up at least as much memory as the size of the executable. Each CGI script requires the loading of its respective interpreter. Dynamic linking of the executables can alleviate the problem to some extent. There are four subsystems you need to consider beyond the choice of a good personal computer-connect (PCI) motherboard, memory, CPU, hard disk, and network. The PCI bus has a throughput of 133 Mb/s, several times faster than even an ultra SCSI 3 adapter and is thus well equipped to handle fast peripherals.

However, there is simply no substitute for RAM—Not space (your hard disk is pitiful slow compared to on-board memory.), not CPU (if you are swapping to disk, your disk is what's slowing you down), nor a faster network card. RAM is cheap; buy a lot of it.

After RAM, the next most important subsystem is either disk or CPU depending on the peculiarities of your site. If you make extensive use of CGI, SSI, or database transactions, you will probably want to put a little more CPU in your system. Don't bother with MMX CPUs. There's really no gain to be had in this situation; just get a faster CPU for the same price or put the money into RAM or hard disk.

## 15.3 Apache and SSL/Stronghold

In a situation where you are simply serving large numbers of static pages, a good disk is probably a good investment. Spend some money to go from a fast or ultra SCSI 2 to ultra SCSI 3. We're assuming here you have the good sense not to use IDE (or even EIDE) drives in a server.

If you need higher throughput and you are saturating your Ti (i.e., you have no LAN connection issues), then you may want to look into having your server hosted at an ISP which has T3 access to the Internet backbone and consider moving from 10 Mb/s ethernet to 100 Mb/s (fast) ethernet. A properly configured Linux Web (and/or FTP) server can saturate a fast ethernet card and multiple Txs.

Because of its popularity, rich feature set, extensibility, and power, we will concentrate on Apache, although much of the information here will apply to any Web server.

As mentioned above, Apache is freely available with source code. Apache also provides an API. These two features allow for a great deal of customization and extensibility. Additionally, Apache is HTTP 1.1 compliant. This latest revision of HTTP introduces performance enhancements to the protocol. Unfortunately, to date, very few browsers support HTTP 1.1 and, thus, cannot take advantage of it.

## Getting Started

Since Apache is freely available, a number of Linux distributions are shipped with it, RedHat and Linux Pro included. Depending on how your vendor configured your machine, you need have only a few configuration details on-hand before you begin writing HTML pages and are on your way to a Web site.

- 1. Where is the document root for the server? In other words, where is the directory that contains the root of the directory tree that is served when someone hits your server? It is the directory from which files are served if no path information, aside from a filename, is given, (for example, http://www.ratatosk.org/davinci.html versus http://www.ratatosk.org/surreal/dali.html). This is typically something like /home/httpd/html or /home/httpd/docs (so the second URL above would retrieve /home/httpd/html/artists/sur-real/dali.html).

- 2. Where are the configuration files? Typically /etc/httpd/conf, /home/httpd/conf/, /usr/local/etc/httpd/conf, or something similar is used for this.

- 3. Is the server running? Depending on how the server was configured when Linux was installed, the http daemon may start automatically at boot time. You can use the ps command to check if httpd is running: ps -waux | grep httpd. If it is not, you need to invoke it as root and tell it where to find the directory containing the configuration files. For example, if your configuration directory is /etc/httpd/conf, you would type something like httpd -d /etc/httpd. If the directory containing your httpd binary is not in your path, you will need to use the absolute path to invoke it. Typically httpd lives in one of the sbin directories:/usr/local/sbin, /usr/sbin, or on rare occasions/sbin.

Aside from the various modules that can be used to extend Apache at compile time, there are many items that can be specified at run time in the config files: httpd.conf and srm.conf. These two control parameters, such as aliases for directories, aliases for icons, CGI scripts/virtual host directories, the document root, the file to be served from a directory if no other file is specified in the URL, and various access control and authentication directives.

## <Directory> and .htacces

These tools are used to modify access of all types for directory trees. <Directory> directives typically reside in the srm.conf or httpd.conf files. It can also occur in the <Virtualhost> directive (more on this later). The .htacces file resides somewhere in a directory tree of HTML documents. In both instances, instances placed in the directories are recursively effective for all the files and subdirectories in that directory. For example, to enforce basic authorization for a directory and all its contents, you could put the following in a .htacces file in that directory (say /home/web):

```
AuthType Basic
AuthFile /home/cary/etc/passwd
AuthGroupFile /dev/null
AuthName Realm of the Kazoos
```
