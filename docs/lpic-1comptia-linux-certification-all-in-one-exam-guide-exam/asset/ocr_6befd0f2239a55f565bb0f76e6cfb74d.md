+   - Router address
+   - DNS server address(es)

What hostname will be assigned to the system? Every Linux system needs to have a hostname assigned. This hostname should be unique on your network, meaning no other system on the network should have the same hostname assigned. During the installation process, you will be prompted to provide a hostname.

What is the name of the DNS domain the system will reside in? More than likely, your organization has its own DNS domain, such as mycorp.com. You will be asked to provide your organization's domain name during the installation process.

Will the system need a host firewall configured? Most Linux distributions include a host firewall that gets enabled by default during the installation process. A host firewall can be an invaluable asset to your organization's security. Essentially, the host-based firewall prevents other systems on the network from establishing connections to the system.

For workstation systems, you should enable this firewall and block all of your IP ports and services. You should also enable the host firewall on server systems. However, most server systems run applications that provide network-based services to other hosts on the network. Therefore, you will need to open up the necessary IP ports in the firewall to allow network hosts to connect to the associated services.

If you're installing a server system, you should list the network services it will provide in your deployment plan along with their associated port numbers. This list will provide you with the information you need to make the necessary exceptions in your firewall configuration. For example, if you're installing a Linux system that will function as a web server, you will need to open ports 80 and 443 in the host firewall to allow clients to connect to the httpd service running on the system.

With your network configuration information specified, you're ready to move on to the last part of your deployment plan: selecting an installation source. Let's discuss how this is done next.

# ## Selecting an Installation Source

Most Linux distributions provide you with many different options for installing the system. These options include the following:

+   - Installing locally from an optical disc
+   - Installing remotely from a network server
+   - Completing a remote installation using VNC

Let's first discuss how to complete an installation from a local optical disc.