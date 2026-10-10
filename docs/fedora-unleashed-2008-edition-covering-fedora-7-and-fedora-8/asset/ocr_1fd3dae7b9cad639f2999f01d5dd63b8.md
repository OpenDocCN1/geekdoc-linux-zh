commands or edit specific files under the /etc/sysconfig directory. To configure the hardware through a graphical interface, you can use Fedora's graphical tool called system-config-network. This section introduces command-line and graphical software tools you can use to configure a network interface and network settings on your Fedora system. You'll see how to control your NIC and manage how your system interacts with your network.

Using the command-line configuration tools can seem difficult if you are new to Linux. For anyone new to networking, the system-config-network graphical tool is the way to go. Both manual and graphical methods require root access to work. If you do not have root access, get it before trying any of these actions. You should not edit any scripts or settings files used by graphical network administration tools on your system. Your changes will be lost the next time the tool, such as system-config-network, is run! Either use a manual approach and write your own network setup script, or stick to using graphical configuration utilities.

> **NOTE**
> The network configuration process described in this section is for client hosts. You cannot perform server network configuration, such as Domain Name System (DNS) and DHCP during installation. (See Chapter 23, “Managing DNS,” for more information on configuring DNS; see the “DHCP” section later in this chapter for more information on that item.)

# Using Graphical Configuration Tools

If you are new to networking or still becoming proficient with the command line, the graphical configuration tool is your best method for configuring new hardware in Fedora. Like most graphical tools, system-config-network enables you to fill in the blanks; press the proper buttons, and the tool modifies the required files and issues the proper commands. Remember, you must be root to run system-config-network.

You can access system-config-network by going to the System, Administration menu and selecting Network. You will be asked for the root password because you are able to make systemwide changes using this tool.

After it is started, system-config-network will display the screen shown in Figure 14.1. Click the DNS tab to configure your system's DNS settings, hostname, or DNS search path. Click the Hosts tab, and then click either the New or Edit button (after selecting a host) to create or edit an entry in your system's /etc/hosts file—for example, to add the IP addresses, hostnames, and aliases of hosts on your network. See Figure 14.2 for an example of editing a host entry.