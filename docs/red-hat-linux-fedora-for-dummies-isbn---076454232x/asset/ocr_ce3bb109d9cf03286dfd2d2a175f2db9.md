The second filter rule controls the packets coming back from outgoing connections. When you connect to a Web site, for example, your browser sends out packets and the web server responds to them. You may click a button on the Web site, and a new display pops up. Clicking a button sends a packet out, and the web server sends packets back. You have previously blocked packets from the Internet. This rule creates an exception that allows packets which belong to an existing connection — such as the connection that represents you clicking a button — to return to your computer through the firewall. Note that we don’t allow new incoming connections (--state NEW) to be established because that would defeat the purpose of this firewall.

6. **(Optional) Use the following rule to allow SSH connections to your Linux computer:**

```
```bash
iptables -A INPUT -p tcp -m state --state NEW,ESTABLISHED
        -j ACCEPT -dport 22
```
```

This rule permits SSH connections on Port 22 to enter into your computer. You can install an OpenSSH server by logging in as root, mounting your companion DVD, and running this command:

```
```bash
rpm -ivh /mnt/cdrom/RedHat/RPMS/openssh-server*
```
```

Start the OpenSSH server by running this command:

```
```bash
/etc/init.d/sshd start
```
```

You can modify this rule to allow other types of incoming connections to your computer. For example, add a new rule using -dport 80, and the firewall allows incoming HTTP packets. All you need to do is install the Apache web server (included on this book’s companion DVD-ROM and described in Chapter 16), and your workstation morphs into a web server.

You have just created a simple, effective firewall that protects your computer from the werewolves of Netdom. (“They’ll rip your heart out, Jim!”) Your firewall remains active until you turn the rules off or reboot your computer. The following section shows how to display your new firewall rules.

# ## Displaying Your Firewall Rules

After you configure your firewall, you naturally want to verify that the filtering rules are set up correctly. To display the firewall rules, follow these steps:

+   1. Open a GNOME Terminal emulator window, by right-clicking any empty portion of the desktop and selecting the **New Terminal** menu.