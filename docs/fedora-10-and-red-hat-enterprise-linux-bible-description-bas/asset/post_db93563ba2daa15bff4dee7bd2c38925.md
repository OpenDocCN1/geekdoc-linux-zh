
# Part IV: Fedora RHEL Network and Server Setup

```
key /etc/openvpn/easy-rsa/2.0/keys/server.key  # This file should be kept secret
d dh /etc/openvpn/easy-rsa/2.0/keys/dh1024.pen
```

```
server 10.8.0.0 255.255.255.0

keepalive 10 120
comp-l

persist-key
persist-tun

status openvpn-status.log
```

In this configuration, the OpenVPN server listens on port 1194, UDP protocol, as a routing VPN server (dev tun). You can use a different port number, to make the service more obscure, but the clients must use that port as well. The private network that OpenVPN clients will be able to reach from this VPN connection is on the subnetwork 10.8.0.0 (identified by 10.8.0.0 255.255.255.0). With the configuration file completed, you can start the OpenVPN server on the server by typing the following:

- # service openvpn start

The last step you to make your OpenVPN server ready to accept connections is to open your firewall to accept connections on port 1194 and to allow your system to route packets to your private subnetwork. In this example, we use a private subnetwork with IP addresses of 10.8.0.1 through 10.8.0.254. See the “Firewall” section of Chapter 14 for details.

# Create OpenVPN client configuration

To configure an OpenVPN client to connect to the OpenVPN server you need to copy the key files to the clients, create a client configuration file, and start the service. Here is an example of how you might copy the keys from the server:

```
# cd /etc/openvpn
# mkdir dir
# sc root@server1:/etc/openvpn/easy-rsa/2.0/keys/ca.crt keys
# sc root@server1:/etc/openvpn/easy-rsa/2.0/keys/client01.crt keys
# sc root@server1:/etc/openvpn/easy-rsa/2.0/keys/client01.key keys
```

Copy a client configuration file to your /etc/openvpn directory and edit it as appropriate. For example, type the following:

```
# cd /usr/share/doc/openvpn-2.1/sample-config
# cp client.conf /etc/openvpn/
```

# Chapter 16: Connecting to the Internet

Here is an example of an edited client.conf:

```
client
dev tun
proto udp
cert-type server
remote example.com 1194
resolv-retry infinite

persist-key
persist-tun

ca /etc/openvpn/keys/ca.crt
cert /etc/openvpn/keys/client01.crt
key /etc/openvpn/keys/client01.key
comp-l 3
```

To test your VPN configuration is working, type the following:

```
# openvpn --config client.conf
```

The output you see from this command will help you debug any problems you have connecting to the OpenVPN server. If you use a GUI interface to start your OpenVPN client, be sure to identify the location of your client configuration files and keys.

# Setting Up Linux as a Proxy

You have a Linux set up, and your Linux computer has both connection to the LAN and a connection to the Internet. One way to provide Web-browsing services to the computers on the LAN without setting routing is to configure Linux as a proxy. The Squid server package comes with Fedora and RHEL. In a basic configuration, you can get the software working quickly. However, the package is full of features that let you adapt it to your needs. You can control which hosts have access to proxy, how memory is used to cache data, how logging is done, and variety other features. Here are the basic proxy services available with Squid:

- Allowing HTTP — the primary reason to use Squid. This is what lets computers access Web pages on the Internet from their browsers (through your Linux computer). In other words, HTTP proxy services will find and return the content to you.
- **FTP** — This represents File Transfer Protocol (FTP) proxy services. When you enable HTTP for a client, you enable FTP automatically.
- **Gopher** — Gopher protocol proxy service was one of the first mechanisms for organizing and searching documents on the Internet (predates the Web by more than a decade). Nobody uses gopher. However, gopher is automatically supported when you use HTTP for a client.

Besides proxy services, Squid can also be part of an Internet cache hierarchy. This occurs when content is taken from the original server and copied to a caching server. When you, or someone else in the caching hierarchy, requests that contain content are taken from the caching server instead of the original server. You don't have to cache content for other computers to participate in caching with Squid that will allow access and speed up your Web browsing. Caching services in Squid are provided through your system's IPC. Besides proxy services, you can also enable Simple Network Protocol (SNMP) services. SNMP lets provide statistics and status information about itself to agents on the network. SNMP is a feature for monitoring and maintaining computer resources.

> CAUTION: SNMP poses a potential security risk if is not configured properly. Use caution when configuring Squid.

The squid daemon can be started automatically at system boot. After it is set up, the configuration for Squid is done in the /etc/squid/squid.conf file. The Squid.conf file contains lots of information about how to configure Squid (the file contains more than 4300 lines of comments and examples, although there are only 35 lines of active settings). For further information about the Squid proxy server, refer to the Squid Proxy Cache page (www.squid-cache.org).

# Starting the squid daemon

When you install Fedora or RHEL, you have an opportunity to install the Squid package. If you are not sure whether not Squid is installed, type following:

```
rpm -q squid
```

If squid is not installed, you can install it from the DVD or by typing yum install to install it over the network. Next you can check whether not squid is configured to run. To do that, type the following:

```
chkconfig --list squid
squid 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

If the squid service is off for run levels 3, 4, and 5 (it's off at all run levels by default), you can set it to start automatically at boot time. To set up the squid daemon to start at boot time, type the following:

```
# chconfig squid on
```

At this point, the squid daemon should start automatically when your system boots. By default, the squid daemon will run with the -D option. The -D option enables Squid to start without having an active Internet connection. If you want to add other options to the squid daemon, you can edit the /etc/sysconfig/squid configuration file. Look for the line that looks similar to the following:

```
SQUID_OPTS="-D"
```

You can add any options, with the -D option between the quotes. Most of these options are useful for debugging Squid:

- a port — Substitute for port a number that will be used instead of the default port number (3128) for servicing proxy requests. This is useful for temporarily trying out an alternative port.
- f squidfile — Use this option to specify an alternative squid.conf file (other than /etc/sysconfig/squid.conf). Replace squidfile with the name of the alternative squid.conf. This is a good way to try out a new squid.conf file before you replace the old.
- d level — Change the debugging level to a number indicated by level. This also causes debugging messages to be sent to stderr.
- -X — Use this option to check that the values are set properly in your squid.conf file. It runs on full debugging while the squid.conf file is being interpreted.

You can restart the squid service by typing /etc/init.d/squid restart. While the squid daemon is running, there are several ways you can run the squid command to change how the daemon works, using these options:

- squid k reload — Causes Squid to read again its configuration file.
- squid k shutdown — Causes Squid to exit after waiting briefly for current connections to exit.
- squid k interrupt — Shuts down Squid immediately, without waiting for connections to close.
- squid k kill — Kills Squid immediately, without closing connections or log files. (Use this option only if other methods don't work.)
