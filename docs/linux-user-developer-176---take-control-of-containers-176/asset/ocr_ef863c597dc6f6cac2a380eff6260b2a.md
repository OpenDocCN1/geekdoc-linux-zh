# Server administration in Ubuntu

Take a deeper look at server admin under Ubuntu

![](bbox=[0.06, 0.25, 0.18, 0.39])

Swayan Prakash

has a master's degree in computer engineering. He has been working in information technology for several years, concentrating on areas such as operating systems, networking, network security, e-commerce, internet services, LDAP and web servers. Swayan has authored a number of articles for trade publications, and he presents his own papers at industry conferences. He can be reached at swayan.prakash@ gmail.com.

# Resources

+   - System admin topics
+       bit.ly/2kt6yXx
+   - A step-by-step approach to understanding the Ubuntu Linux system
+       bit.ly/2kCi642
+   - Basic Ubuntu server administration
+       bit.ly/2kQxIeJr
+   - Ubuntu server guide (PDF)
+       bit.ly/18NkPkK

**Right** The widely used sar utility for server administration

**When we set up a Linux system to act as a server, we need to focus on several tasks.** As the name implies, servers exist to serve. The data that they serve can include webpages, files, database information and so on. From a server administration perspective, there are some typical challenges to your system administration skills.

The first is remote access. In the majority of cases, administration will be carried out using remote access tools. Since graphical interfaces may not be available, you need to depend solely on command-line tools to carry out various tasks such as remote login, remote copying and remote execution. The most common of these tools are built on the SSH facility.

The second is security. As expected, a server will accept requests from remote users and systems. As a result, a server administrator will open the ports to the services that are needed and lock down the ports that are not required. Various tools are available that can be used to secure the services.

The third is constant monitoring. Servers are expected to stay up 24/7, 365 days a year. There is a significant need to configure the tools that can be used to monitor each of your servers. With such monitoring, you will be able to collect the required log messages and also trigger an email whenever suspicious activity occurs. It is always good to collect data around CPU usage, memory usage, network activities and so on.

It is important to note here that whether you are starting a file server or a web server, many of the steps that are required to get the server up and running will remain the same. When it comes to configuration and tuning, we see a bunch of differences. Once we have successfully installed the server, the next step is to have a look at its default configuration. It needs to be noted here that most of the server packages are installed with a default configuration setting that leans towards providing more security.

As we know, most Linux servers can be configured using plain text in the /etc directory. In most cases, there is a primary configuration file and sometimes, a related configuration directory from which files with an extension of .conf can be pulled into the main configuration file. Apache web server is an example where we have a primary configuration file and a directory where other configuration files can be dropped in and included with the service. The main configuration file is /etc/httpd/conf/httpd.conf and the configuration directory is /etc/httpd/conf.d/.

As mentioned earlier, most server software packages are installed with very minimal configuration and this has its own limitations if we need to fully use those servers. Mail servers and DNS servers are typical examples of servers with limited functionality. Please note that both of these servers are installed with their default configurations and they start on reboot. But the thing here is both of them only listen for the requests on your localhost. Therefore, until we configure these servers, people who are not logged into your local server will not be able to send email to that server or use your computer as a public DNS server.

Once we have installed and configured the server, the next step is to start it. Generally, most servers that we install on Linux are configured to start up when the system boots up. After that, the services run continuously and keep listening for requests. This will continue until the system is shut down. You can manage the services using two major facilities: systemd and System V init scripts. Regardless of which facility is used on the Linux system, it is up to you to determine whether you want the services to come up when the system boots and to start, stop and reload the services as needed. Another thing to note here is that the majority of the services are implemented as daemon processes. The table here gives a brief description of the parameters.

| Parameter | Description |
| :-- | :-- |
| User and group permissions | Daemon processes normally run as users and groups other than the root. The reason behind this is that if someone hacks these daemons, they will not have permission to access files beyond those the service can access. |
| Daemon configuration files | Generally, a service has a configuration file for the daemon, stored in /etc/sysconfig: Refer to the man page details of the specific daemon for more. |
| Port numbers | Most standard services have specific port numbers that daemons listen to and clients can connect to. Typically we do not need to change the ports that a daemon process listens on. |

![](bbox=[0.2, 0.72, 0.62, 0.95])