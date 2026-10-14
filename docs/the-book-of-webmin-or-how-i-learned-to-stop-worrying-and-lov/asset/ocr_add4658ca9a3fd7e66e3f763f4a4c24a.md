![](bbox=[0.22, 0.12, 0.44, 0.27])

Figure 2-1: Session authentication

**NOTE** Many systems are configured with Webmin running in SSL encrypted mode. On these systems, you will log in using a URL beginning with https:// rather than http://. Also, at least one Linux distribution that includes Webmin, specifically Caldera, installs it on port 1000 rather than 10000. This is theoretically a more secure arrangement, however, be aware that some firewalls will prevent you from accessing your Webmin-enabled server from outside of the local network if Webmin runs on a port below 1024.

# Logging In with Lynx

Sometimes, it may be desirable or necessary to administer your system from the command line without the benefit of a GUI. Luckily, one does not have to give up Webmin entirely in these circumstances. Using Lynx, or a similarly capable text-mode web browser, one can log in and use most of the Webmin modules much the same as using a graphical browser. Logging in when Webmin is using session authentication is identical to logging in with a graphical browser, but logging in when Webmin is configured to use traditional HTTP authentication is slightly different. Lynx requires that authentication information be included on the command line when starting up:

```
[joe@delilah joe]$ lynx -auth root:passwd http://delilah:10000
```

**CAUTION** If you plan to administer your system via a text-mode browser, you will want to choose an alternate theme rather than the new default MSC.Linux theme. The old default theme, or the Swell Technology theme has a simpler icon and table layout, allowing Lynx and other text-mode browsers to display them more effectively. The MSC.Linux theme, while attractive in a GUI browser, uses a complex layout that leads many areas of Webmin to be difficult to read and impossible to use in a text-mode browser.

Another limitation of using a command line client is that SSL is not well supported by all versions of Lynx and other text-mode browsers. This means you may need to run your Webmin server without encryption; therefore, more extreme measures should be taken to ensure the security of your server. Securing a Webmin installation will be discussed in detail in later chapters.

# A First Look

Webmin is divided into a number of modules that each allow you to administer a single aspect of your system. Modules exist for most common, and many uncommon, system administration tasks. The standard modules provide a graphical interface for: Apache, Squid, Bind, NFS, man pages, Sendmail, Postfix,