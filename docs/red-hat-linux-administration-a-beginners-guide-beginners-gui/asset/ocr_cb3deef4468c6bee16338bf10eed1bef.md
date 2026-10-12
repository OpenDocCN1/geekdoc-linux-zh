If you're using the **neat** tool, the entries in the DNS tab correspond to the information in /etc/resolv.conf.

![](bbox=[0.28, 0.17, 0.72, 0.57])

> > **TIP**
> > If you use DHCP to get your IP address, be sure you understand the effect that it will have on files like `/etc/resolv.conf` before you spend a lot of time customizing those files. Otherwise, you may find that all your hard work has disappeared the next time you boot. For more information, see Module 20.

# ## The /etc/nsswitch.conf File

The /etc/nsswitch.conf file tells the system where it should look up certain kinds of configuration information (services). When multiple locations are identified, the /etc/nsswitch.conf file also specifies the order in which the information can best be found. Typical configuration files that are set up to use /etc/nsswitch.conf include the password file, group file, and hosts file.

The format of the /etc/nsswitch.conf file is simple: The service name comes first on a line (note that /etc/nsswitch.conf applies to more than just host name lookups), followed by a colon. Then come the locations that contain the information. If multiple locations are identified, the entries are listed in the order in which the system should perform the search. Valid entries