# ## CHAPTER 10
# Setting Up Networking Services

![](bbox=[0.15, 0.1, 0.38, 0.29])

Increasingly, embedded systems are called upon to include networking capabilities. An embedded system may, for example, provide a web server to enable web-based configuration. It may also enable remote login for maintenance and upgrading purposes. Because the Linux kernel and the networking software that runs on it are often the preferred software for running networking services that require high reliability and high availability, you will find Linux particularly well suited for networking applications.

In this chapter, we will discuss the setup and configuration of the networking services most commonly found in embedded Linux systems. This discussion includes instructions on how to cross-compile each networking package and how to modify the target’s root filesystem to run the services each package provides. In particular, we will cover:

+   * Use of the Internet super-server (inetd)
+   * Remote administration with SNMP
+   * Network login through Telnet
+   * Secure communications with SSH
+   * Serving web content through HTTP
+   * Dynamic configuration through dynamic host configuration protocol (DHCP)

There are, of course, many other networking services that can run on top of Linux. Though we couldn’t realistically cover all of them in a single chapter, the explanations included here should provide you with some hints as to how to install and use other networking packages. Also, we won’t cover the setup, configuration, and use of actual networking hardware, nor many of the Linux advanced networking options—such as IPv6, source-based routing, firewalling and network address translation support—as most are not specific to embedded systems. If you need information regarding these issues, have a look at *Running Linux* by Matthias Dalheimer and Matt Welsh and *Linux Network Administrator’s Guide* by Tony Bausits et al. (both from O’Reilly). We also will not provide in-depth coverage of the configuration and use of the various networking packages, since many already have entire books dedicated to them. For more informa-