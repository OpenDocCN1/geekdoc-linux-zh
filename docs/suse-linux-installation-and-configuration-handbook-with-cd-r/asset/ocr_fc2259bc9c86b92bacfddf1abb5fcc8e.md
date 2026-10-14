+   - Lines 3—The serial number, also known as the version number, is used when secondary servers check for zone changes. If you make any changes to the zone that this file controls, you have to increase this number to reflect an update in the zone information.
+   - Lines 4–7—These lines define the behavior of BIND against the cached addresses.
+   - Line 8—Using the NS resource record, which defines the domain name of the origin, this line defines the name as local host.
+   - Line 9—The digit 1 at the start of the line will be appended to the IP address of the origin. The whole new IP address will be set to the name local host.

NOTE The most important three resource records (RR) that a zone file can contain are SOA, NS, and PTR. The first is the Start Of Authority resource record (SOA). This record defines the origin from which the hosts or domains branch. The second resource record is the Name Service (NS). The NS tells the DNS the domain name of the origin. The third is the pointer resource record (PTR), which defines subnets and hosts from the origin.

# Setting Up a Caching Only Name Server

Now that you have built a knowledge base, it's time to make use of it. Setting up a caching only name server is a good way to lessen the name lookup time. If your machine is on a LAN, it will lessen the load on the existing name servers if you tell the other people on the LAN to use it as a domain name server, too.

# Setting Up the Server

You should start by setting up the main configuration file /etc/named.conf. Open the file in your favorite editor and enter the following configuration:

```
```
1 options {
2   directory "/var/named";
3   check-names master warn;
4   pid-file "/var/run/named.pid";
5   datasize default;
6   stacksize default;
7   coresize default;
8   files unlimited;
9   recursion yes;
10  multiple-cnames no;
11  // forwarders {    //This section would enhance the performance
12  //   xxx.xxx.xxx.xxx; //uncomment those and add your primary DNS
13  //   xxx.xxx.xxx.xxx; //and secondary DNS
14  // };
15 }
```
```