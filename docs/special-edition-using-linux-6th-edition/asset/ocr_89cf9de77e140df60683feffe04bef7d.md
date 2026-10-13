```
**LISTING 26.5 CONTINUED**

calderasystems.com.       1H IN NS       gw.caldera.com.
ns.calderasystems.com.    1H IN A        207.179.18.7
gw.caldera.com.           3h26m31s IN A  207.179.18.252
```

Notice that the first query returns all information, including NS, MX, and all A entries that are applicable. The second query returns all the entries it found about the host gw, including the host ns. If you can’t see why, the host gw has an RR that corresponds to calderasystems.com. Likewise, calderasystems.com corresponds to both gw and ns. Also note that gw has two domain names, the old caldera.com and the newer calderasystems.com.

# HOST

If all you want to know is the IP address for a particular hostname, the host program provides it in a clean format that is easily redirected to a file or run through awk for direct inclusion into a file such as /etc/hosts. Sample output of host caldera.caldera.com returns the following:

```
caldera.calderasystems.com             A        207.179.18.1
```

To change this, simply do something like the following:

```
host caldera.calderasystems.com | awk "{print $3 \"\t\" $1 }" -
```

The awk print command reverses the order of the output and inserts a Tab character (\t) between them. This can be redirected and appended to /etc/hosts via >>.

> **Caution**
> 
> The preceding example is only to be used for hosts over which you have control, or which you know will not change. Putting Caldera’s hosts in your /etc/hosts file if you are not the domain administrator for Caldera is a bad idea.

# WHOIS

The last program you’ll look at in this chapter is whois. Although it is not one of the BIND utilities, this program provides DNS-related information. Specifically, it provides information from the internic.net database regarding domain registration information. It is advisable to direct your query to the appropriate whois server. As of this writing, whois servers include the following:

+   - **whois.internic.net**—International InterNet NIC
+   - **whois.nic.gov**—U.S. Government NIC
+   - **whois.nic.mil**—U.S. Military NIC
+   - **whois.ripe.net**—RIPE European Network Coordination Centre
+   - **whois.apnic.net**—Asia Pacific NIC
+   - **whois.arin.net**—American Registry for Internet Numbers
+   - **whois.funet.fi**—Finland NIC