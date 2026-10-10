+   Add DNS Server Information — Although the server IP addresses that you enter for DNS servers are probably ones that your ISP configured, you may want to add your own DNS servers. If so, make sure that your server points to your master and slave DNS servers for IP address resolution. You can also have the other computers on your LAN point to your DNS servers to resolve domain names to IP addresses. (The /etc/resolv.conf file is where you identify your DNS servers.) After you add your own DNS server, all your clients should change their /etc/resolv.conf files to include the new domain name and DNS server information.

+   Add Hostname — As soon as you have a real domain name, you can name your computer within the structure of that domain name. If you haven’t installed CentOS, you can enter this hostname during installation.

> NOTE Changing your hostname after you install can sometimes cause problems. Services such as printing and the X server (for your graphical desktop) sometimes fail after you change your hostname. Check to make sure that printing and other network services are still working after you change your hostname. Sometimes restarting the network interface can solve the problem.

After you set up your network interfaces and related information for your server, test the Internet connection by using commands such as host, nslookup, and dig. Next, if DNS is already configured for your domain, try to query your server by name to see whether those in the outside world can reach you by name. Make sure that the static IP addresses that appear in response match the static IP addresses that you were assigned.

# Configuring Servers

Some services are more appropriate for public exposure than others. You probably don’t want to offer your print server, for example, to anyone on the Internet. Similarly, file sharing with Samba or NFS isn’t appropriate to share those services natively across the public Internet. (To access those services over an Internet connection, however, you could run them up a virtual private network.)

If you’re creating your first public server, you may want to consider setting up at least the following basic types of servers:

+   Web Server — This type of server, of course, provides the most common way to publish text, images, and a variety of other content to the Internet. Refer to Chapter 20 for information on configuring an Apache Web server.

+   FTP Server — This type of server provides the most common way of sharing directories of documents, images, application programs, and other content that users can download from your site. See Chapter 19 for information on setting up an FTP server.

+   Mail Server — Presumably, if you have a domain name that you like and a Linux server up and running, you may very well want to get a mail server running too. That way, you can create one or more e-mail addresses that are specific to your domain. Because mail servers are high-risk targets for spammers, if you are inexperienced at system