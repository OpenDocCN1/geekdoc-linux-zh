# Setting Up an NIS Server

A single NIS server can serve information for multiple NIS domains. We cover setting up a server for a single domain; the extension to multiple NIS domains is straightforward.

# Note:

> Although an NIS server can serve multiple domains, it cannot support multiple password files, at least according to the documentation in /usr/doc/nis-server-2.0/README.server. Thus, for all practical purposes, it is useless to have a server serving more than one NIS domain.

To set up an NIS server, you must decide on an NIS domain name. For historical reasons, many people choose yp followed by their DNS domain name, as in yp.roaringpenguin.com. However, there’s no real reason to do this; you could as easily choose yp.foo if you wish. At any rate, pick an NIS domain name. Also, decide on a machine to use as an NIS server.

On the NIS server, create a directory called /etc/nis/domainname. If you picked yp.foo as the domain name, the directory would be /etc/nis/yp.foo.

# Setting Up Map Sources

In the directory /etc/nis/yp.foo, you must set up the source files for all the NIS maps. For example, if you are going to publish the passwd and group maps, you should place the text files for those maps under /etc/nis/yp.foo. If the NIS maps are to contain the same information as the system configuration files on the NIS server (a fairly common setup), just make symbolic links from /etc/passwd and /etc/group into /etc/nis/yp.foo. If you are using shadow passwords, you need to link /etc/shadow as well.

# Warning

> Using NIS with shadow passwords defeats the whole point of shadow passwords. With NIS, anyone can read the password database with a simple ypcat command. If you want to use shadow passwords, do not distribute the password files with NIS.

![](bbox=[0.86, 0.64, 0.97, 0.92])