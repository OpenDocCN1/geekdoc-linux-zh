# Tutorial

# Diagnosing issues

Finding the root problem can be tricky, but
there are a number of places you can look first

# What's not working – connecting to one website or all of them?

If it's just one then it may still be a problem at your end, but if it's everything, let's find out where the problem is.

First, your network connection – most desktop distros ship with NetworkManager to manage connections. From the command line, typing **nm-tool** will report what it knows of your network – look for 'State: connected'.

If you don't have nm-tool, use **ifconfig** to see which interfaces are recognised and **ethtool** for connection status information, or use **iwconfig** for wireless connections.

While ethtool will show you physically connected to the network (Link detected: yes) and iwconfig will show you connected to a wireless router, ifconfig will give you your IP address and netmask, telling you that this much of your networking is successfully configured.

Running **route** will show the routing table, which includes the default gateway to the rest of the Internet. If there's no default gateway shown for addresses outside the local subnet, you will need to fix this. Route can be used to add routes but you need to address the cause of the problem.

Your servers will have fixed IP addresses, which can be edited to correct gateway and other network details. Laptops tend to be configured automatically by a DHCP (Dynamic Host Configuration Protocol) daemon, often running on an ADSL router, where settings can be changed for the problem machine if necessary.

Having corrected settings, a network restart:

```
sudo service networking restart
```

![](bbox=[0.05, 0.75, 0.3, 0.88])

Above **www.downtimeforeveryoneofustm.com** is a very handy diagnostic tool, simple as it sounds

# Can't connect to Wi-Fi?

The wiist tool shows you everything your wireless network interface can see

![](bbox=[0.33, 0.35, 0.55, 0.58])

...will pick up the revised settings on Debian-based PCs – leave out the gerund (the –ing) for Red Hat boxes. Run route again to check for the appearance of the default gateway.

**Ping** uses another part of the TCP/IP protocol stack, ICMP, to send an ECHO_REQUEST datagram, and the ICMP ECHO_RESPONSE produced by the host or gateway pinged is used to calculate a time for the trip. Ping tells you if a machine is up, what latency there is in the network and how many packets are lost, all indicative of something unless the server has been set to drop ICMP requests by an overzealous sysadmin, something of negligible security use in most cases. Use ping to check that you have a route to hosts on the Internet. Start by pinging your gateway:

```
ping 192.168.0.1
```

…then ping a reliable host like 8.8.8.8, one of Google's public-facing DNS servers (the other is 8.8.4.4). We've been using IP addresses and

# Nslookup gives you the domain's IP address, and where it looked for it. Simple, but effective

![](bbox=[0.55, 0.36, 0.75, 0.5])

**n-s** switches to avoid DNS problems distracting us from other network faults, but now's the time to check DNS functionality. **Nslookup**, less sophisticated than **dig** (part of dig's output can be seen above), is fine for checking that a domain name resolves to an IP address. If you don't get an answer, have a look in /etc/resolv.conf.

![](bbox=[0.55, 0.58, 0.75, 0.7])

If you've ruled DNS out, try some of the tools overhead – traceoute to see if you can route all the way there, telnet and frdns to see if a particular port is open, dig for more DNS and Wireshark for investigating unresponsive or slow services.

If it is your webserver that's the problem, then **ssh** in and run:

```
netstat -lnp | grep -1 apache
```

(replacing apache with nginx, httpd or whatever is appropriate) to see if your web server is listening to all addresses on port 80. You could **grep 80** if that's the only port which you're concerned with, but check what else Apache is up and listening on.

# A text-based interface and a scriptable version are available for Wcd, but the GUI frontend is fine

![](bbox=[0.75, 0.37, 0.95, 0.6])