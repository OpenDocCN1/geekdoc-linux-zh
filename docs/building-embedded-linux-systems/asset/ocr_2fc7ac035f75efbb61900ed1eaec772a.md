Like Boa, *httd* operates with a special user account, the **nobody** account, by default. Create this account using the procedures outlined earlier, or set *httd* to use an account of your choice. The configuration file copied earlier specifies the use of the *httd* user. It also identifies the target *s/html/httpd/html* directory as the location for source HTML files:

```
$ mkdir -p $(PRJROOT)/rootfs/home/httd/html
```

Finally, edit your target *s/etc/inittab* file. Here is the line we added for *httd* in our SYSM module *s* **inittab**:

```
:::respawn::/usr/sbin/httd -c /etc/httd.conf
```

For more information on how to install and run *httd*, see the manpage included in the package and the project *s* website.

# A Word on Apache

Apache is available from *http://www.apache.org/* and is distributed under the Apache license.\footnote{This license is similar to the BSD license. See the LICENSE file included with the package for the complete licensing details.} As we said earlier, Apache does not lend itself well to cross-compiling. If you are not deterred by this warning and are still interested in attempting to cross-compile Apache, have a look at the procedure outlined by David McCready in his posting to the Apache development mailing list: *http://hypermail.linklord.com/new/htpd/2000/May/0175.html*. If you succeed, you *ll probably want to take peek at *Apache: The Definitive Guide* by Ben Laurie and Peter Laurie (*O Reilly*) for more information regarding the configuration and use of Apache.

# Dynamically Generated Web Content

Since the most common use for an HTTP server on an embedded system is providing a graphical management interface, your embedded system would most likely make use of dynamically generated web pages.

With the exception of Apache, none of the web servers mentioned earlier provides any internal scripting engine or plugin interface that would allow creation of dynamic web content, at least by themselves. Not all is lost, however, because all of them definitely do support the standard CGI interface that is used to delegate this task to some external program.

The idea behind CGI is a very simple and a very powerful one: when the *client* web browser requests a certain URL from the web server, the server, according to some internal logic, will locate a program in the target filesystem and run it, providing some needed information (such as request headers) in environment variables. The CGI program will then compute whatever dynamic page content its programmer had in mind,