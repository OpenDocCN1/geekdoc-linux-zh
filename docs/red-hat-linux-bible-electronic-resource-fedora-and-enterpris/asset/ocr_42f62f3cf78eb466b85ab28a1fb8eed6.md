After you set up your network interfaces and related information for your server, test the Internet connection by using the `ping` command, as I describe in Chapter 16. Next, if DNS is already configured for your domain, try to `ping` your server by name to see whether those in the outside world can reach you by name. Make sure that the static IP address that appears in response matches the static IP address that you were assigned.

# Configuring servers

Some services are more appropriate for public exposure than others. You probably don’t want to offer your print server, for example, to anyone on the Internet. Similarly, file sharing with Samba or NFS isn’t appropriate to share publicly across the Internet.

If you’re creating your first public server, you may want to consider setting up at least the following basic types of servers:

+   - **Web server** — This type of server, of course, provides the most common way to publish text, images, and a variety of other content to the Internet. Refer to Chapter 21 for information on configuring an Apache Web server.
+   - **FTP server** — This type of server provides the most common way of sharing directories of documents, images, application programs, and other content that users can download from your site. See Chapter 20 for information on setting up an FTP server.
+   - **Mail server** — Presumably, if you have a domain name that you like and a Linux server up and running, you may very well want to get a mail server running too. That way, you can create one or more e-mail addresses that look like `chris@linxutoys.net`. See Chapter 19 for information on configuring a mail server.

Of course, you can share any type of server that you choose. Web, FTP, and mail servers however, are designed for sharing publicly. The basic configuration for these types of servers isn’t that difficult. Securing and monitoring these — or any — public servers, however, requires special effort, as the following sections describe.

# Managing security

Before you set up your Red Hat Linux system as a server, you may use it simply to make outgoing connections to the Internet. You can use your firewall (ipchains or iptables) to close off the ports on your interface to the Internet (making your computer quite secure). Now, however, you need to open some of the ports on that interface to accept incoming requests. With more ports open, you must also become more consistent in monitoring those ports.

# Opening your firewall

Making your server public doesn’t mean leaving your computer wide open. By using firewall rules, you can set your computer to allow outsiders to open connections to certain ports and block requests on other ports. Assuming that you set up your firewall to block incoming