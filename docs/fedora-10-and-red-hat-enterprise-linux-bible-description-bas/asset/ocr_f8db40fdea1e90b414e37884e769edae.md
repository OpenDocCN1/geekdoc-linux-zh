# Appendix B: Running Network Services

well, to which you will be alerted when you try to install the package.) Then use the rpm command to install the software from the installation DVD or CD.

+   2. Is the start-up script set to launch the service automatically? Most network services are launched from start-up scripts that cause daemon processes to listen to the network continuously for requests for the service. See the "Networking Service Daemons" section for information on how to find start-up scripts and have them launch automatically.

+   3. Does SELinux permit access to the service? When SELinux is enabled, it puts an additional layer of security over selected network services. If you get permission denied messages when you are told that the firewall and file/directory permissions are appropriately, run system-config-selinux. On the SELinux tab, check that the appropriate service (Web, FTP, Samba, and so) is enabled.

+   4. Is the configuration file created for the service? Even if the daemon process is listening for requests for a network service, or more configuration files associated with the service might be set up before requests are accepted. Table B-1 lists important configuration files for each type of service.

+   5. Does the configuration file permit access to the service? Within the configuration file for a service, there might be several levels of permissions that a user must go through to permission to the service. For example, a configuration file might allow access to a particular host computer, but deny access to a particular user. If the service has TCP wrappers enabled, host computers can be allowed or denied access to the service based on settings in the /etc/hosts.allow and /etc/hosts.deny files.

+   6. Does the firewall permit access to the service? The first time you boot Fedora after installation, the first bootstrap enables you to configure a firewall. If you choose the default firewall, most services will not be available outside your local computer. Refer to Chapter 14 for information on how to change your firewall configuration to open ports that provide the different services.

+   7. Are there other restrictions to the service being shared? Some standard Linux security measures might block access to a service that is otherwise being shared. For example, you can share a Linux directory using NFS or FTP services, but local file permissions might block access to the directory or files within the shared directory.

To determine whether a service failure occurs, look to the log files contained in the /var/log directory. The messages and dmesg files contain general messages about processing that occurs when services and hardware are initialized. Many services, such as Sendmail and Apache, have their own log files. Setting debug levels on service daemons is a way to get more details about how a service is working (see the Debugging Services sidebar).