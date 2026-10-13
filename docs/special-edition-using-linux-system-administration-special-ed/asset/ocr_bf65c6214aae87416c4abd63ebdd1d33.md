# ## Network Security

Every system connected to your LAN should be secured against attacks from the network to the highest degree possible. There are several key strategies that you can use to help secure systems:

+   - Turn off as many services as possible. A default Linux distribution usually has numerous unnecessary services running. If you are not offering content to the network through FTP, turn off `ftpd`. If you don’t require Telnet for remote access and management, turn off `telnetd`.
+   - Remove unnecessary daemons from starting up through `inetd`. For others use TCP wrappers if possible to launch the services from within `inetd`. This provides finer control and greater security.
+   - Use `/etc/hosts.allow` and `/etc/hosts.deny` to control access to the services that are running on your system as outlined in Chapter 13, “Linux Network Configuration and TCP/IP.”
+   - Try to prevent unencrypted passwords from traveling across the network. For instance, Telnet sends plain text passwords across the network when you log in remotely. You can prevent this by using `ssh` instead of Telnet for remote login. `ssh` is a secure replacement for Telnet and `rsh`, and can be downloaded from http://www.ssh.org/.

# ## Internet Security

If your network will be connected to the Internet, it is essential that you implement sufficient security at the gateway connecting you to the Internet. If not, you expose all systems on your network to potential attack by any user on the Internet and eventually a security hole or misconfiguration will be found and capitalized on by an attacker.

Two key steps must be taken in securing your network against attack from the Internet:

+   - Create a firewall to prevent unwanted packets from reaching your internal network from the Internet.
+   - Move services which must be accessed from the Internet to a demilitarized zone and allow limited access to these from the Internet while preventing all access to other systems from the Internet. Services that are candidates for this include email, Web, FTP, and DNS.

The creation of a firewall and a DMZ are discussed in Chapter 19, “Linux and Firewalls.”

# ## Security Tools

A wide range of tools exists that are useful in implementing and monitoring your security policies. Most of these tools are focused on Internet and network security. These tools include the following: