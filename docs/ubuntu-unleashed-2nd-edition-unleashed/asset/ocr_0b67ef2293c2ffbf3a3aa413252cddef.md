In this example, the host checks the `/etc/hosts` file first and then performs a DNS lookup. A couple more options control how the name service is used. The only reason to modify this file is if you use NIS for your name service or you want one of the optional services. The nsswitch option can be a good option for system security. It compares a standard DNS lookup to a reverse lookup (host-to-IP then IP-to-host) and fails if the two don't match. The drawback is that often when proxy services are used, the lookup fails, so you want to use this with caution.

# Using Graphical Configuration Tools

As mentioned earlier, if you are new to networking or still becoming proficient with the command line, the graphical configuration tool is your best method for configuring new hardware in Ubuntu. Like most graphical tools, network-admin allows you to fill in the blanks; press the proper buttons, and the tool modifies the required files and issues the proper commands. Remember, you must be root to run network-admin.

There are two ways to start network-admin: from the command line of an X11 terminal window with the command `network-admin`, using the panel's Run Application menu item, or by clicking the Networking option under the System, Administration menu (In either case, you are prompted to enter the root password.)

After it is started, you will see the screen shown in Figure 18.1.

![](bbox=[0.054, 0.499, 0.526, 0.811])

FIGURE 18.1   Use network-admin to configure your network devices.

Click the DNS tab to configure your system's DNS settings, hostname, or DNS search path. Click the Hosts tab, and then either click the Add or Properties button (after selecting a host) to create or edit an entry in your system's `/etc/hosts` file, for example, to add the IP addresses, hostnames, and aliases of hosts on your network. See Figure 18.2 for an example of editing a host entry.