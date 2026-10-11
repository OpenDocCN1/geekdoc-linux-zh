# ## DNS AND DHCP
## CONFIGURATION GUIDE

# ### 46.1 Features and Benefits

There are few subjects in the UNIX world that might raise as much contention as Domain Name System (DNS) and Dynamic Host Configuration Protocol (DHCP). Not all opinions held for or against particular implementations of DNS and DHCP are valid.

We live in a modern age where many information technology users demand mobility and freedom. Microsoft Windows users in particular expect to be able to plug their notebook computer into a network port and have things “just work.”

UNIX administrators have a point. Many of the normative practices in the Microsoft Windows world at best border on bad practice from a security perspective. Microsoft Windows networking protocols allow workstations to arbitrarily register themselves on a network. Windows 2000 Active Directory registers entries in the DNS namespace that are equally perplexing to UNIX administrators. Welcome to the new world!

The purpose of this chapter is to demonstrate the configuration of the Internet Software Consortium (ISC) DNS and DHCP servers to provide dynamic services that are compatible with their equivalents in the Microsoft Windows 2000 Server products.

This chapter provides no more than a working example of configuration files for both DNS and DHCP servers. The examples used match configuration examples used elsewhere in this document.

This chapter explicitly does not provide a tutorial, nor does it pretend to be a reference guide on DNS and DHCP, as this is well beyond the scope and intent of this document as a whole. Anyone who wants more detailed reference materials on DNS or DHCP should visit the ISC Web site at <http://www.isc.org>¹. Those wanting a written text might also be interested in the O’Reilly publications on DNS, see the O’Reilly² web site, and the BIND9.NET³ web site for details. The books are:

1. <http://www.isc.org>
2. <http://www.oreilly.com/catalog/dns/index.htm>
3. <http://www.bind9.net/books-dhcp>