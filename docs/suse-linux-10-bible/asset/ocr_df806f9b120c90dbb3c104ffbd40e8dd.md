# Chapter 21 ◆ Configuring a DNS Server 577

The SOA can be further analyzed to break down the record's uses.

# The SOA Server

After the definition of the domain you are managing, you need to define the server that is authoritative for the domain. It may seem bizarre, but you are referring to a name, not an IP address in this case, because BIND is aware that it needs to find the IP address for the server from its zone (it may sound like a vicious cycle, but it does work). In Listing 21-2, for example, the SOA for palcoder.net is zen.palcoder.net.

# The Hostmaster

With most things on the Internet, it is common practice to provide a technical contact for the service. In this case, it is the email address justin.palcoder.net. You will notice that there is no @ in the email address, but a full stop (period). The hostmaster for the palcoder.net zone is justin.palcoder.net (justin@palm-coder.net).

![](bbox=[0.125, 0.423, 0.16, 0.458])

> If the email address of the hostmaster contains a full stop, you need to "escape" it. For example, if your email address is justin.davies@palcoder.net, the host-entry is justin\.davies.palcoder.net.

# The SOA Record

The brackets around the rest of the data dictate that everything else up to the closing-bracket is part of the SOA record. All time settings are in seconds.

# The Serial Number

The first entry is the serial number for the zone. This is one of the most important parts of the SOA because it must be changed any time you edit the zone file. The serial number tells other DNS servers that are querying your DNS server has changed. If you do not change the serial number, your changes will not get propagated through the system.

The general form of the serial number is, followed by an arbitrary number. For the 24th of July, you use 2005072401 (July 24, 2005). Notice that the date is in reverse, with the year (2005), month (07), and day (24), with an additional two digits able to repeat multiple changes in one day.

# The Refresh Rate

If you have a slave DNS server in your system (as a backup to your master), the refresh rate tells the slave server how often to check for updates to the zone. If you look back at Listing 21-2, you will see the refresh rate set to 10,800 seconds (3 hours).