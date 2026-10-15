Internet Explorer proxy settings are in Tools/Internet Options. From the Connections tab, click the LAN Settings button and enable the Use a Proxy Server for Your LAN option. Enter the address as the IP of your Squid machine, and then specify 3128 as the port.

# Access Control Lists

The main Squid configuration file is /etc/squid/squid.conf, and the default Ubuntu configuration file is full of comments to help guide you. The default configuration file allows full access to the local machine but denies the rest of your network. This is a secure place to start; we recommend you try all the rules on yourself (localhost) before rolling them out to other machines.

Before you start, open two terminal windows. In the first, change to the directory /var/log/squid and run this command:

```
sudo tail -f access.log cache.log
```

That reads the last few lines from both files and (thanks to the -f flag) follows them so that any changes appear in there. This allows you to watch what Squid is doing as people access it. We refer to this window as the “log window,” so keep it open. In the other window (again, with sudo), bring up the file /etc/squid/squid.conf in your favorite editor. This window is referred to as the “config editor,” and you should keep it open, too.

To get started, search for the string acl all—this brings you to the access control section, which is where most of the work needs to be done. You can configure a lot elsewhere, but unless you have unusual requirements, you can leave the defaults in place.

> NOTE
> The default port for Squid is 3128, but you can change that by editing the http_port line. Alternatively, you can have Squid listen on multiple ports by having multiple http_port lines: 80, 8000, and 8080 are all popular ports for proxy servers.

The acl lines make up your access control lists (ACLs). The first 16 or so define the minimum recommended configuration that set up ports to listen to, and so on. You can safely ignore these. If you scroll down further (past another short block of comments), you come to the http_access lines, which are combined with the acl lines to dictate who can do what. You can (and should) mix and match acl and http_access lines to keep your configuration file easy to read.

Just below the first block of http_access lines is a comment like # INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS. This is just what we are going to do. First, though, scroll just a few lines further; you should see these two lines:

```
http_access allow localhost
http_access deny all
```