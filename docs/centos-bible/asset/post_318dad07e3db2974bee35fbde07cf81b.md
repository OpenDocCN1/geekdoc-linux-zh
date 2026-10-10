
administration, you might decide not to maintain your own public mail server. See Chapter 18 for information on configuring a mail server.

Of course, you can share any type of server that you choose. Web, FTP, and mail servers, however, are designed for sharing publicly. The basic configuration for these types of servers isn't that difficult. Securing and monitoring these -- or any -- public servers, however, requires special effort, as the following sections describe.

## Managing Security

Before you set up your CentOS system as a server, you can use it simply to make outgoing connections to the Internet. You can use your firewall (iptables) to close off the ports on your interface to the Internet (making your computer quite secure). Now, however, you need to open some of the ports on that interface to accept incoming requests. With more ports open, you must also become more consistent in monitoring those ports. You can use SELinux to set boundaries around your Internet services.

## Opening Your Firewall

Making your server public doesn't mean leaving your computer wide open. By using firewall rules, you can set your computer to allow outsiders to open connections to certain ports and block requests on other ports. Assuming that you set up your firewall to block incoming connections, here's a list of services (and the associated port numbers) that you may want to consider accepting through your firewall from your external interface to the Internet:

- **Web Server** — Port 80
- **Mail Server** — Port 25 (and possibly port 587)
- **FTP Server** — Ports 20 and 21
- **DNS Server** — Port 53 (if you're supporting your own DNS)
- **SSH Server** — Port 22 (allows secure login service to administer the computer remotely or remote users to add Web content or other server content to the server)

To see which ports are assigned to which services by default, refer to the /etc/services file. See www.lana.org/assignments/port-numbers for a full list of service ports. In most cases, a configuration file for a service indicates the default port number the service listens on. One way of making a service more private is to change the port number that a service listens on. Then the user must know to ask for the service at that particular port. To see which ports are currently exposed on your system, you can use the nmap command.

Chapter 13 describes how to change your firewall to accept requests for these services. I start with the iptables example in that chapter when I create the DNS example later in this chapter. You can use that description as a model for setting up a firewall to go with DNS. In the DNS example, you have separate computers for mail, FTP, and Web servers. For a low-volume server, however, you can have them all on the same computer.

## Enabling SELinux

Security Enhanced Linux (SELinux) is now enabled by default in CentOS. As it is implemented with targeted policies, most popular server types (including Web, FTP, and DNS) have policies set that restrict what intruders can do if they manage to break into the service. You should look over how policies are set on the SELinux Administration window (system-config-selinux command) for services you are offering. Refer to Chapter 9 for more information on SELinux.

## Checking Logs and System Files

By making your servers public, you also make them more open to attacks. Although firewalls are a good first line of defense, you still need to watch the activity on those ports that you leave open. A consistent program of monitoring traffic and checking changes to your server, therefore, becomes more critical. The following are a few techniques that you can use to help secure your servers:

- **General Security** — Make sure that you protect all your user accounts by using good passwords and the correct file permissions settings.
- **Aide** — Use aide to take a snapshot of your critical system files so that you can check later whether anyone's altered those files. The aide package is available in the CentOS repository.
- **File System Saint** — As with aide, File System Saint maintains a database of every file on your system. You can find out more information from the project's SourceForge.net site (http://sourceforge.net/projects/fss/).
- **Logwatch** — Use Logwatch, which is on by default in CentOS, to screen log files and suspicious e-mail messages to you. At the very least, you should change the MailTo value in the /etc/logwatch/conf/logwatch.conf file to an e-mail address you keep up with (this is where Logwatch will send its screened log messages).

I describe these and other security techniques in Chapter 13.

## Keeping Up with Updates

You can expect to find and correct security issues continuously. You must keep up with software updates that are published to plug security holes. Although some of these updates address theoretical security problems, others are created in response to real break-ins or denial-of-service attacks that are known to exploit weaknesses in the components that come with your operating system.

For CentOS, you can use pirut or yum to download and install updates from CentOS mirror sites that carry those updates (see Chapter 5 for information on using yum). You should also check CERT and other organizations (which I describe in Chapter 13) for security alerts.

After your server is secure and correctly configured, your last step is to start the server on the Internet with a domain name that points to it. Either ask your service provider to configure DNS for you or set up your own DNS server, as I describe in the following section.

## Setting Up a Domain Name System Server

The *Domain Name System* (DNS) is essentially a distributed database that translates hostnames into IP addresses (and IP addresses back to hostnames). That database also contains information related to each domain, such as how the domain is organized into zones, where to route mail for that domain, and whom to contact with questions associated with the domain.

By setting up a DNS server, you become part of a hierarchy of DNS servers that make up the Internet. At the top of this hierarchy is the root server, represented by a dot (.). Below the root server are the top-level domains, or TLDs (such as *com*, *org*, etc.). Domains that individual organizations own and maintain lie below the TLDs, branching in a way that looks like an upside-down tree structure. That’s where you come in.

As someone who’s setting up a DNS server, you’re responsible for managing the hostnames and IP addresses for the computers in the domain (or domains) for which you’re responsible. Keeping your DNS information correct means that people can access the services that you want to share, and the Internet as a whole works that much better as a result.

Besides using your DNS server to help people from the Internet find the public servers in your domain, you can also use DNS to provide name and IP address mapping for computers on your private network. The example in the “DNS Name Server Example” section later in this chapter describes how to configure both private and public name and IP address records for a domain.

> **WARNING** Setting up a DNS server can be a complex and (these days) potentially dangerous undertaking. A compromised DNS server can cause requests for host addresses to be directed to a cracker’s server. The sample DNS server in this section is one created as an example of a DNS server for a home or small office environment. For information on the many different ways to set up a DNS server, go to the *BIND 9 Administrator Reference Manual* at /usr/share/doc/bind-9\*/arm/Bv9ARM.html.

## Understanding DNS

The basic function of a name server is to answer queries by providing the information that those queries request. A DNS name server primarily translates domain and hostnames into IP addresses. Each domain is typically represented by at least two DNS servers.

- **Primary (Master) Name Server** — This name server contains the master copy of authoritative information about the domains that it serves. In response to queries for information about its domains, this server proclaims that information **marked as being authoritative**. The primary is the ultimate source for data about the domain.
- **Secondary (Slave) Name Server** — This name server gets all information for the domain from the primary name server. As is the case for the primary server, DNS considers the *secondary’s* information about the domain that it serves authoritative, although the domain records can be overwritten from the primary.
