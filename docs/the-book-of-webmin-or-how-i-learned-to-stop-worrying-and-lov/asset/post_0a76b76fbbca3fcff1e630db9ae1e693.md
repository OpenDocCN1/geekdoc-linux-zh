
![](img/d84604054810a13cacfdac212ebee2f7_37_0.png)

Figure 2-1: Session authentication

**NOTE** Many systems are configured with Webmin running in SSL encrypted mode. On these systems, you will log in using a URL beginning with https:// rather than http://. Also, at least one Linux distribution that includes Webmin, specifically Caldera, installs it on port 1000 rather than 10000. This is theoretically a more secure arrangement, however, be aware that some firewalls will prevent you from accessing your Webmin-enabled server from outside of the local network if Webmin runs on a port below 1024.

## Logging In with Lynx

Sometimes, it may be desirable or necessary to administer your system from the command line without the benefit of a GUI. Luckily, one does not have to give up Webmin entirely in these circumstances. Using Lynx, or a similarly capable text-mode web browser, one can log in and use most of the Webmin modules much the same as using a graphical browser. Logging in when Webmin is using session authentication is identical to logging in with a graphical browser, but logging in when Webmin is configured to use traditional HTTP authentication is slightly different. Lynx requires that authentication information be included on the command line when starting up:

```
[joe@delilah joe]$ lynx -auth root:passwd http://delilah:10000
```

**CAUTION** If you plan to administer your system via a text-mode browser, you will want to choose an alternate theme rather than the new default MSC.Linux theme. The old default theme, or the Swell Technology theme has a simpler icon and table layout, allowing Lynx and other text-mode browsers to display them more effectively. The MSC.Linux theme, while attractive in a GUI browser, uses a complex layout that leads many areas of Webmin to be difficult to read and impossible to use in a text-mode browser.

Another limitation of using a command line client is that SSL is not well supported by all versions of Lynx and other text-mode browsers. This means you may need to run your Webmin server without encryption; therefore, more extreme measures should be taken to ensure the security of your server. Securing a Webmin installation will be discussed in detail in later chapters.

## A First Look

Webmin is divided into a number of modules that each allow you to administer a single aspect of your system. Modules exist for most common, and many uncommon, system administration tasks. The standard modules provide a graphical interface for: Apache, Squid, Bind, NFS, man pages, Sendmail, Postfix,

Samba, and much more. There also exists a wide array of third-party modules that provide even more extensive functionality. This book focuses on the standard modules, but may expand to encompass other modules in time.

Upon first logging in, you'll see a row of tabs and a number of icons (Figure 2-2). The tabs are labeled Webmin, System, Servers, Hardware, Cluster, and Others. You may also have, depending on your OS and version, one or two additional tabs. The selected tab when first logging in is always Webmin. This category is where all of the Webmin-related configuration details are located.

![](img/d84604054810a13cacfdac212ebee2f7_38_0.png)

Figure 2-2: A first look

The view from Lynx is actually pretty similar if using one of the traditional themes (Figure 2-3). The MSC.Linux theme makes many links inaccessible when using Lynx; overall usage is quite difficult when you're working in a text-mode browser, so be sure to switch to a more conventional theme if you'll be administering your system from the command line. On my server using the Swell Technology theme, Webmin is quite usable entirely from a text console, making Webmin useful even when no browser is available. The MSC.Linux theme can also be rather heavyweight when administering a server across a WAN link with a graphical browser. This is because the number and size of images makes browsing the pages rather slow even via a fast connection.

![](img/d84604054810a13cacfdac212ebee2f7_39_0.png)

Figure 2-3: A first look from Lynx

Because Webmin is web-based, interacting with the GUI will probably be immediately comfortable, though for beginners it may take a few minutes to locate specific modules or features. In the following chapters, the discussion will focus on specific Webmin modules and the services that the modules configure. It proceeds through the category tabs from left to right, beginning with Webmin and ending with Others.

## WEBMIN CONFIGURATION

![](img/d84604054810a13cacfdac212ebee2f7_40_0.png)

Webmin provides a number of configurable options and access control features, as well as flexible action logging that provides you with the maximum flexibility and security of the Webmin server and the various Webmin system administration modules.

These features are accessed through the Webmin tab on the index page of Webmin. When you display the Webmin tab, you see icons for Usermin Configuration, Webmin Actions Log, Webmin Configuration, Webmin Servers Index, and Webmin Users. Keep in mind that the modules located under the Webmin tab are for configuring Webmin itself, not the underlying system.

So, for example, creating a user in the Webmin Users module will not create a system user, only a Webmin user. Likewise, the Webmin Actions Log module allows you to search and view the Webmin log, not any system or service log that might exist. We'll get to those kinds of options later. For the moment, we're going to skip over Usermin Configuration because Usermin receives full coverage in the next chapter.

## Webmin Actions Log

The Webmin Actions Log page provides access to the Webmin log. You can configure this log for each module and individual users. This module does not configure the logs, but provides you with a means to search the logs for actions performed by particular logged users or actions performed in given logged modules. Configuration of Webmin logging capabilities is covered in the Webmin Configuration section.

With this module it is possible to search for actions by specific users, within specific modules, for a given range of dates, or any combination of those qualifications. For example, if you manage a number of junior system administrators and you'd like to find out if one of them has edited an Apache virtual server configuration in the past week, this module makes those kinds of questions easy to answer (assuming logging to that degree is enabled, of course).

## Webmin Configuration

The Webmin Configuration module (Figure 3-1) allows you to configure most of the important aspects of Webmin itself, as well as install new modules, upgrade existing modules, and upgrade Webmin itself. It also provides a means to change the port and address where the Webmin miniserv.pl web server listens for connections, select different languages, enable or disable SSL encryption, and configure the Webmin built-in logging features.

![](img/d84604054810a13cacfdac212ebee2f7_41_0.png)

Figure 3-1: Webmin Configuration

## IP Access Control

Webmin has its own web server, called miniserv.pl, which provides a simple IP access control feature. This page allows you to configure this option. You may enter IP networks (such as 192.168.1.0), IP host addresses (such as 192.168.1.79), and host names (such as joesbox.penguinfeet.org). It is wise to limit access to the Webmin server to just those addresses that are trusted. While Webmin has no known exploits in versions greater than 0.970, if someone were to obtain your password, this would provide an additional level of protection from unauthorized access. This option configures the accept and deny directives in the miniserv.conf file. The default is to allow any address to access Webmin.

> **CAUTION** *Be aware that using IP access controls within Webmin is an application-level security feature. In other words, if ever an exploitable problem were discovered in the Webmin miniserv.pl web server, it would still be accessible from an IP not permitted to use Webmin. So it is still theoretically possible to attack the web server even if the user isn't offered a login page. However, this is a pretty unlikely scenario, requiring a bug in miniserv.pl that is exposed even when an authentication page is not provided.*

## Port and Address

The Webmin server will, by default, listen on every active IP address on the system. But if you have multiple addresses and would prefer Webmin to only listen on one of them, you may use this option. So, for example, if you have one network interface connected directly to your local network and a second network interface connected to the Internet, you could improve security by causing Webmin to only listen on the local network. In this case, any requests from the Internet at large would be ignored, but it would still be possible to connect from local computers. This can be a very effective first line of defense. After all, if the bad guys can't even talk to the Webmin server, they certainly can't try anything funny to break into it.

The Listen on Port option specifies the network port on which Webmin will listen. In a standard Webmin install this will be port 10000, although Caldera installs it on port 1000. Some firewalls may restrict access to ports below 1024, and some may restrict even ports above 1024. If your network has strict proxy restrictions that prevent connecting on port 10000, you may wish to try port 553 or 443 (assuming these ports are not already in use on your Webmin server for normal SSL service). These ports will nearly always be usable through a proxy, even when using an SSL enabled Webmin.

> **NOTE** *In a proxied environment, your client browser must use a CONNECT method to construct a tunnel through the proxy device. Because of the potential for abusing CONNECT requests most proxies prevent this method on all but a few ports. The standard port for SSL web connections is 443, and so it is the most likely port to be available for CONNECT requests. If your proxy is running Squid and you have administrator privileges, you may wish to add Webmins default port to the allowed SSL ports as documented in the Squid chapter of this book.*

As mentioned briefly in the installation chapter, it is possible to alter these configuration settings in the miniserv.conf configuration file in addition to graphical configuration with the Webmin Configuration module. This may be
