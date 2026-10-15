# directory Option

A critically important option found in most configuration files is the directory option, which holds the location of the name server’s zone and cache files on your system. The following example is taken from the Red Hat /etc/named.conf file. This example specifies the zone files are located in the /var/named directory. In this directory, you can find your zone files, including those used for your local system.

```
options {
    directory "/var/named";
    forwarders { 192.168.0.34;
                192.168.0.47;
    };
};
```

# forwarders Option

Another commonly used global option is the forwarders option. With the forwarders option, you can list several DNS servers to which queries can be forwarded if they cannot be resolved by the local DNS server. This is helpful for local networks that may need to use a DNS server connected to the Internet. The forwarders option can also be placed in forward zone entries.

# notify Option

With the notify option turned on, the master zone DNS servers send messages to any slave DNS servers whenever their configuration has changed. The slave servers can then perform zone transfers in which they download the changed configuration files. Slave servers always use the DNS configuration files copied from their master DNS servers. notify takes one argument, yes or no, where yes is the default. With the no argument, you can have the master server not send out any messages to the slave servers, in effect preventing any zone transfers.

# named.conf Example

The following example is a simple named.conf file based on the example provided in the BIND documentation. This example shows samples of several of the configuration statements. The file begins with comments using C++ syntax, //. The options statement has a directory entry that sets the directory for the zone and cache files to /var/named. Here, you find your zone files, such as named.local and reverse mapping files, along with the cache file, named.ca. The first zone statement ( ) defines a hint zone specifying the root name servers. The cache file listing these servers is named.ca. The second zone statement defines a zone for the mytrek.com domain. Its type is master, and its zone file is named "mytrek.com." The next zone is used for reverse IP mapping of the previous zone. Its name is made up of a reverse listing of the mytrek.com domain’s IP address with the term IN-ADDR.ARPA appended. The domain address for mytrek.com is 192.168.0, so the reverse is 1.168.192. The IN-ADDR.ARPA domain is a special domain that supports gateway location and Internet address-to-host mapping. The last zone statement defines a reverse mapping zone for the loopback interface, the method used by the system to address itself and enable communication between local users on the system. The zone file used for this local zone is named.local.