# Chapter 4. Advanced Concepts

These internal servers will have complete sets of information for site1.example.com, site2.example.com, site1.internal and site2.internal.

To protect the site1.internal and site2.internal domains, the internal nameservers must be configured to disallow all queries to these domains from any external hosts, including the bastion hosts.

The external servers, which are on the bastion hosts, will be configured to serve the "public" version of the site1 and site2.example.com zones. This could include things such as the records for public servers (www.example.com and ftp.example.com), and mail exchange (MX) records (a.mx.example.com and b.mx.example.com).

In addition, the public site1 and site2.example.com zones should have special MX records that contain wildcard (*) pointing to the bastion hosts. This is needed because external mail servers do not have any other way on how deliver mail to internal hosts. With the wildcard records, the mail will be delivered to the bastion host, which can then forward it to internal hosts.

Here's an example of a wildcard record:

+   * IN MX 10 external.example.com.

Now that they can mail on behalf of anything in the internal network, the bastion hosts will need to know how to deliver mail to internal hosts. In order for this to work properly, the resolvers on the bastion hosts will need to be configured to point to the internal nameservers for DNS resolution.

Queries for internal hosts will be answered by the internal servers, and queries for external hostnames will be forwarded back out to the DNS servers on the bastion hosts.

In order for all this to work properly, internal clients will need to be configured to query only the internal nameservers for DNS queries. This could also be enforced via selective filtering on the network.

If everything has been set properly, Example, Inc.'s internal clients will now be able to:

+   * Look up any hostnames in the site1 and site2.example.com zones.
* Look up any hostnames in the site1.internal and site2.internal domains.
* Look up any hostnames on the Internet.
* Exchange mail with internal AND external people.

Hosts on the internal will be able to:
* Look up any hostnames in the site1 and site2.example.com zones.
* Exchange mail with anyone in the site1 and site2.example.com zones.

Here is an example configuration for the setup we just described above. configuration information; for information on how to configure your zone files, see Section 3.1