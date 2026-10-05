# Chapter 14 TCP/IP Networking

If the local host obtains the addresses of its DNS servers through DHCP, the DHCP client software stuffs these addresses into the resolv.conf file for when it obtains the leaves. Since DHCP configuration is the default for most systems, you generally do not need to configure the resolv.conf file manually if your DHCP server has been set up.

Many sites use Microsoft’s Active Directory DNS server implementation. That works fine with the standard UNIX and Linux resolv.conf; there's no need to do anything different.

# 14.11 SYSTEM-SPECIFIC NETWORK CONFIGURATION

On early UNIX systems, you configured the network by editing the system startup scripts and directly changing the commands they contained. Modern systems have read-only scripts; they cover a variety of configuration scenarios and choose among them by reusing information from other system files or configuring their own.

Although this separation of configuration and implementation is a good idea, every system does it a bit differently. The format and use of the /etc/hosts and /etc/resolv.conf files are relatively consistent among UNIX and Linux systems, but that’s all about you can count on sure.

Most systems provide some sort of GUI interface for basic configuration tasks, but the mapping between the visual interface and the configuration begins the scenes is often unclear. In addition, the GUIs tend to ignore advanced configurations, and they are relatively inconvenient for remote and automated administration. In the next sections, we pick apart some of the variations among our example systems, describe what’s going under the hood, and cover the details of network configuration for each of our supported operating systems. In particular, we cover

+   * Basic configuration
* DHCP client configuration
* Dynamic reconfiguration and tuning
* Security, firewalls, filtering, and NAT configuration
* Quirks

Now, not all of our operating systems need discussion for each topic.

Keep in mind that most network configuration happens at boot time, so there’s some overlap between the information here and the information presented in Chapter 3, Booting and Shutting Down.

# 14.12 LINUX NETWORKING

Linux is always one of the first networking stacks to include new features. Linux folks are sometimes so quick that the rest of the networking infrastructure

![](bbox=[0.196, 0.898, 0.237, 0.943])