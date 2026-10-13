Below these second-level domains you will find two types of names:

+   - Individual hostnames, such as `metallab.unc.edu` or `www.cnn.com`.
+   - Further sub-divided domains such as `ca.bahai.org`, which can be divided into hostnames such as `www.ca.bahai.org` and further sub-domains.

DNS was designed with decentralized administration in mind. Domains are delegated to organizations. The organization so delegated becomes responsible for maintaining host and subdomain data for their domain. The organization can change their domain data without worrying about the parent domain. The parent domain only keeps pointers to the subdomain’s name servers, to which it can direct queries. The domain bahai.org, for example, is delegated to the Bah’ World Centre. The Bah’ World Centre can delegate a sub-domain such as u.bahai.org. The subdomain can maintain its own data, without bothering the domain administrators of bahai.org. All bahai.org must do is keep a pointer to the name servers of us.bahai.org. This is the power and convenience of decentralized DNS administration.

# DNS Name Resolution

DNS provides the mechanism to translate hostnames to IP addresses and reverse translations of IP addresses to hostnames.

A name lookup is done starting at the root of the tree at `.` and traversing the various branches until the process arrives at a leaf node (which contains a hostname). Each `.` in the name is a branching point. Branching points will become clear as we consider examples using the `nslookup` utility.

The process of translating names to IP addresses is called *name resolution*. DNS stores all names and IP Addresses of hosts in a domain in a set of maps, which are called *zone files*.

You can also look up names for IP addresses. This process is called *reverse name resolution*. DNS uses a special domain called `in-addr.arpa` for this purpose. We will discuss reverse lookups in detail later in this chapter.

DNS zones are made up of a set of resource records that define hostnames, administrative information, and other information which can be stored in a DNS database. Some of the most commonly used record types are outlined in Table 22.2.

**Table 22.2 Common DNS Record Types**

| Record Identifier | Record Name | Description |
|---|---|---|
| SOA | Start of Authority | Marks the start of a zone of authority. Each zone must contain one, and only one, SOA record. |
| A | Address | Defines an IP address for a hostname in the domain. |