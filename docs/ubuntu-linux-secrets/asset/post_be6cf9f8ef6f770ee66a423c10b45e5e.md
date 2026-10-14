
# Using named as a Local Cache Server

The easiest way to use the named program on your server is to cache DNS responses on the Ubuntu server for future DNS requests. This configuration points all DNS requests received by the Ubuntu server (either from the server itself or from other network devices pointing to the Ubuntu server) to the named program running on the local server. The named program configuration redirects all requests to a common remote DNS server, usually provided by an ISP.

The benefit to this method is that the named program will cache all the DNS requests it handles. Thus, it can immediately answer any future requests for the same hostname without having to contact the remote DNS server. This capability can significantly speed up interactions on the Internet for your local network.

There are two things you’ll need to do to get this method set up on your Ubuntu server:

- ◆ Set the nameserver entry in the resolv.conf file to point to the localhost.
- ◆ Set the named configuration to point to a common remote DNS server.

Here are the steps required to change the nameserver entry in the resolv.conf file:

- 1. Open the /etc/resolv.conf file in a text editor. If you’re working on the Ubuntu server, you’ll need to use a command-line editor such as the vim editor. To edit this file you must have administrative privileges (see Chapter 17, "Users and Groups"). Enter the command:
- sudo vim /etc/resolv.conf
- 2. Copy the current value set in the nameserver line. The default Ubuntu configuration should have detected the network nameserver via DHCP unless you manually entered that value to set a static IP address for your server at installation time. The nameserver line should look like this:
- nameserver 10.0.1.1
- Copy that IP address. You’ll need it for a later step.
- 3. Change the IP address on the line to 127.0.0.1. This redirects all DNS requests to the named program running on the server.
- 4. Save the file and exit the editor. The vim command to save the file and exit the editor is ZZ.

```
continued
2419200 ; Expire
604800 ) ; Negative Cache TTL
; @ IN NS localhost.
1.0.0 IN PTR localhost.
```

This information defines a single PTR record for the 127.0.0.1 address (remember, the IP octets are listed in reverse order in the PTR record). This defines the reverse lookup for the special localhost IP address.

Next you'll need to configure the named program to forward all DNS requests to the remote DNS server that was originally listed in the resolv.conf file. Follow these steps:

- 1. Open the /etc/bind/named.conf.options file in a text editor. Again, if you're working on the Ubuntu server, you'll need to use a command-line editor such as vim to edit the file. To edit this file you must have administrative privileges (see Chapter 17, "Users and Groups"). To edit the file, enter this command:

```
sudo vim /etc/bind/named.conf.options
```

- 2. Look for the forwarders section in the named.conf.options file, and change it to look like this:

```
forwarders {
  10.0.1.1;
};
```

You'll have to remove the comments (double forward slashes) in front of these lines to make them active. The IP address you use should be the one you copied from the original resolv.conf file.

- 3. Save the file, and edit the editor. The vim command to save the file and exit the editor is ZZ.

The named program is now ready to go. You'll need to restart the named program, either by rebooting the Ubuntu server or entering the command:

```
sudo /etc/init.d/bind9 restart
```

This command restarts the named program, which will read the new configuration and run as a local cache server.

# Using named as a Master DNS Server

If you want your Ubuntu server to be the main DNS server for your network, you'll need to do a bit more work. The DNS server responsible for a network is called a master DNS server. A master DNS server contains records that define all of the hosts on the network, both for internal communications and for communications outside of your network. If any server on the Internet needs to know the IP address for a hostname of your network, your Ubuntu server must be available to answer the request.

This configuration uses the same named configuration files as in the local cache server example, but it adds the network zone information to the configuration files. The configuration files need both the hostname and IP address information for the hosts you want to make available to the Internet.

- /etc/bind/named.conf.local: This file stores the zone names and file locations.
- /etc/bind/db.smallorg.org: A zone configuration file based on your domain name, it stores the zone hostname information for your hosts.
- /etc/bind/db.10: A reverse lookup configuration file based on the first octet of your IP network address, it stores the reverse IP address information for your hosts.
