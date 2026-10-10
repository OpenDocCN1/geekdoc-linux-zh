# ## THE GUTS OF DNS

In this section we’ll explore some background material necessary to your understanding of the installation and configuration of a DNS server and client.

# ## Domains and Hosts

Up until now, you’ve most likely referenced sites by their Fully Qualified Domain Name (FQDN), like this one: www.hyperreal.org. Each string between the periods in this FQDN has a significance. Starting from the right end and moving to the left, you have first the top-level domain (`.org`, `.com`, `.net`, `.mil`, `.gov`, `.edu`, `.int`, and the two-letter country codes such as `.us` for the United States).

> **NOTE:** Getting a new top-level domain approved is a difficult process. At this writing, serious debate continues over the issue of creating new top-level domains. Whether they will actually be deployed anytime soon is still unknown.

From these top-level domains come actual organizational boundaries. Companies, ISPs, educational communities, and nonprofit groups typically acquire unique names under one or more of the domains. Here are a few examples: redhat.com, caldera.com, planetoid.org, hyperreal.org, and theory.com. Assignment of these names is done by special groups under the authority of the IANA (Internet Assigned Numbering Authority). Visually, you can imagine the DNS format as an upside-down tree, as shown in Figure 12-1. The root of the tree is a single period; this is the period that is supposed to occur after every FQDN. Thus the proper FQDN for www.planetoid.org is really www.planetoid.org. (with the root period at the end). Most applications have come to assume that the user will not place the suffixing period.

![](bbox=[0.12, 0.6, 0.88, 0.83])

Figure 12-1. The DNS tree, two layers deep