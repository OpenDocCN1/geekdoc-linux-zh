
## Table 13.15 The caching-related /etc/httpd.conf directives.

| Directive | Purpose | Value |
| :--- | :--- | :--- |
| **CacheDefaultExpire** | Sets the default amount of time an item remains in the Apache cache before expiring. | Number of hours |
| **CacheGcInterval** | Specifies how often to check the cache to ensure that its size is not over the specified limits. | Number of hours, including partial hours expressed in decimal format |
| **CacheLastModifiedFactor** | Implements a formula that calculates how often an item should remain cached as a factor of how long ago it was last changed. | The decimal factor to multiply the last changed time against |
| **CacheMaxExpire** | Specifies the maximum amount of time an item remains cached without checking the server it came from for a more recent version. | Number of hours |
| **CacheRoot** | Specifies where to store Apache's cache. | Path to cache |
| **CacheSize** | Specifies how large you are willing to let the cache get before it needs to be cleaned out. | Size in K |
| **NoCache** | Identifies specific items not to cache. | Space-separated list of hosts, domains, and terms in items that should not be included in the cache |

Finally, we reach virtual hosting. First there is:

```
#NameVirtualHost 12.34.56.78:80
#NameVirtualHost 12.34.56.78
```

The **NameVirtualHost** directive is typically used in the following format:

```
NameVirtualHost IPaddress:port
```

This directive is used to specify what interfaces and ports contain virtual Web servers. Once you have this set, you continue to:

```
#<VirtualHost ip.address.of.host.some-domain.com>
# ServerAdmin webmaster@host.some-domain.com
# DocumentRoot /www/docs/host.some_domain.com
# ServerName host.some_domain.com
# ErrorLog logs/host.some-domain.com-error_log
# CustomLog logs/host.some_domain.com-access_log common
#</VirtualHost>
```

A `<VirtualHost>` statement is used to define a host and its behavior more clearly. You can actually build a long set of directives within this statement if you need to. What you see here is instead a typical minimal setup. None of the elements used here are new. And, finally:

```
#<VirtualHost default:*
#</VirtualHost>
```

It is recommended to uncomment this section if you do virtual hosting. It ensures that any HTTP request coming in to an address that is not a virtual host gets sent to the main server.

# Other Linux Web Servers

Apache is certainly not the only Web server available under Linux. Several solutions are available. Some are open source, some are proprietary, and some have their own license that you should become familiar with before deciding on using it. Some of the alternatives are free, and some are commercial, or have commercial features to them. If you are not sure whether you want to use Apache, and want to investigate your options, or you need functionality that Apache cannot provide, then see Table 13.16 for a list of what is available and where you can get more information.

**Table 13.16 Web servers available for Linux.**

| Name | Home |
| :--- | :--- |
| AOLserver | www.aolserver.com |
| EmWeb | www.agnanat.com/emweb/solutions/ |
| GoAhead Web Server | www.goahead.com/webserver/webserver.htm |
| Hawkeye | http://hawkeye.net |
| iServer | www.servertec.com/products/iws/iws.html |
| Java Web Server | http://java.sun.com |
| RapIdControl For Web | www.rapidlogic.com/products/rc_web.html |
| RomPAGER | www.allegrosoft.com/rproduct.html |
| Roxen | www.roxen.com/products/ |
| SpyGlass MicroServer | www.spyglass.com/solutions/technologies/microserver/ |
| vqServer | www.vqsoft.com |
| Xitami | www.xitami.com |
| Zeus Web Server | www.zeustech.net/products/zeus3/ |

There are also Web server solutions available with a “small footprint,” meaning that they do not take up much RAM. These primarily are of interest to network device developers, but you may find that you have use for them for some purposes.

## Immediate Solutions

### Installing Apache

To install the Apache Web server under Red Hat Linux, do the following:

- 1. Log in as root on the machine you want to use for your Web server.
- 2. Put the Red Hat CD-ROM in the CD-ROM drive.
- 3. Type “mount /mnt/cdrom” to add the CD-ROM to your file system.
- 4. Type “cd /mnt/cdrom/RedHat/RPMS” to change to the packages directory.
- 5. Type “rpm -ivh apache-1\*” and press Tab to complete the file name, and then press Enter to install the package.

### Configuring Apache

To configure your Apache Web server, do the following:

- 1. Log in as root on the machine you want to use for your Web server.
- 2. Set up server access information as described in the following section, “Configuring Apache Access.”
- 3. Set up the server itself as described in the section “Configuring **httpd**,” later in this chapter.
- 4. Set up what users can see when they look through your Web directories, as described in the section “Configuring What Web Browsers See,” later in this chapter.
- 5. Type “/etc/rc.d/init.d/httpd restart” to restart Apache.

> **NOTE:** You may have to use a different restart method in non-Red Hat distributions.

## Configuring Apache Access

To do your initial access configuration, do the following:

- 1. Log in as root on the machine you want to use for your Web server.
- 2. Type "vi /etc/httpd/conf/httpd.conf".

> **NOTE:** If you are using the original Red Hat 6.1 release or earlier, you may find that this information is instead in the file access.conf.

- 3. Type "<Directory>" and press Enter. You first jump down to this line:

```
<Directory />
```

- 4. Type "/" and press Enter again to repeat the search. This takes you down to the following line:

```
<Directory /home/httpd/html>
```

- 5. If you do not intend to store your Web pages in /home/httpd/html, type “i” to enter Insert mode, and then edit the directory to point to what you intend to use for your Web server’s base directory.

- 6. Move the cursor down to the next line:

```
Options Indexes Includes FollowSymLinks
```

- 7. If you want to change these **Options** and are not currently in Insert mode, type “i”. Table 13.3 outlines what each of these features does, and the alternatives available to you.

- 8. Move the cursor down to the next line:

```
AllowOverride None
```

- 9. If you want to change the allowable overrides and are not currently in Insert mode, type “i”. Table 13.3 outlines the alternatives to the **None** feature. However, consider whether you really want to let these families of settings be overridden by anyone else for your entire Web hierarchy.

- 10. If you are setting up an intranet with this server, and your Internet Web server is on another machine, move the cursor down to the next line:

```
order allow,deny
```

Then, change it to **order deny,allow** or **order mutual-failure**.

- 11. If you are setting up an intranet with this server, and your Internet Web server is on another machine, move the cursor down to the next line:

```
allow from all
```

Then, change it to reflect who should have access. For example, for the entire class C network 192.168.22.0, you might use:

```
allow from 192.168.22.
```

- 12. Move your cursor down to the following line:

```
<Directory /home/httpd/cgi-bin>
```

- 13. If you plan to keep the CGIs used by this server in another location, type “i” to enter Insert mode, and then change /home/httpd/cgi-bin to the new location.

- 14. If you do not plan to allow anyone to use CGIs, comment out this entire section, which means changing it to look like the following:

```
#<Directory /home/httpd/cgi-bin>
#AllowOverride None
#Options ExecCGI
#</Directory>
```

I highly recommend leaving this **AllowOverride** statement alone. Do not give people freedom with your CGIs unless you have a particular reason to. Change the **Options** statement if you want to, but still be careful here. Table 13.3 lists the alternatives.

- 15. Move the cursor down to the following line:

```
#<Location /server-status>
```

- 16. If you want to allow people to see the status of your server at any given time, uncomment this section by removing the hash marks from in front of it so that it looks like this:

```
<Location /server-status>
SetHandler server-status
order deny,allow
deny from all
allow from .your_domain.com
</Location>
```

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_470_0.png)
