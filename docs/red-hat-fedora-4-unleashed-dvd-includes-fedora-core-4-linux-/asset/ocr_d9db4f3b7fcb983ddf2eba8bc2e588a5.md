In this situation, you should consider a virus scanner for your machine. You have several to choose from, both free and commercial. The most popular free suite is Clam AV (www.clamav.net), but Central Command, BitDefender, F-Secure, Kaspersky, McAfee, and others all compete to provide commercial solutions—look around for the best deal before you commit.

# Configuring Your Firewall

Always use a hardware-based or software-based firewall on computers connected to the Internet. Fedora includes a graphical firewall configuration client named `system-config-securitylevel`, along with a console-based firewall client named `lokkit`. Use these tools to implement selective or restrictive policies regarding access to your computer or LAN.

Start the `lokkit` command from a console or terminal window. You must run this command as root; otherwise, you will see an error message like this:

```
$ /usr/sbin/lokkit
ERROR - You must be root to run lokkit.
```

Use the `su` command to run `lokkit` like this:

```
$ su -c "/usr/sbin/lokkit"
```

After you press Enter, you see a dialog as shown in Figure 33.1. Press the Tab key to navigate to enable or disable firewalling. You can also customize your firewall settings to allow specific protocols access through a port and to designate an Ethernet interface for fire-walling if multiple NICs are installed. Note that you can also use a graphical interface version of `lokkit` by running the `gnome-lokkit` client during an X session.

![](bbox=[0.26, 0.59, 0.72, 0.8])

**FIGURE 33.1** Fedora's `lokkit` command quickly generates firewall rules in memory for Linux.

Using `system-config-securitylevel` is a fast and easy way to implement a simple packet-filtering ruleset with filtering rules used to accept or reject TCP and UDP packets flowing through your host's Ethernet or designated device, such as `eth0` or `ppp0`. The rules are created on-the-fly and implemented immediately in memory using `iptables`.