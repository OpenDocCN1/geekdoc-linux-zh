Chapter 4 • Networking Basics

Sometimes, additional subdomains are used, each separated by a dot. Several top-level domains have been established, including the following:

+   - **com** Networks operated by businesses
- **edu** Networks operated by schools
- **gov** Networks operated by U.S. government agencies
- **mil** Networks operated by the U.S. military
- **net** Networks operated by Internet service providers (ISPs)

In addition, most countries around the world have a designated top-level domain. For example, the UK has the domain uk.

An organization registers its domain name (or names) with the Internet authority, it assigns host names that include the domain name. As a simple example, the host name `www.redhat.com` consists of

+   - a host name, `www`
- a domain name, `redhat.com`, which consists of:
  - a subdomain, `redhat`
  - a top-level domain, `com`

It's common for hosts within a network to refer to one another by host name, without reference to their implied domain name. The combination of a host name and domain name is called a *fully qualified domain name* (FQDN).

# TCP/IP Model

The previous section described how TCP/IP hosts are named and numbered. This section describes how TCP/IP networks function and the types of services they provide.
It's common to explain a protocol suite by referring to the Open Systems Interconnection (OSI) reference model, which groups network functions into seven layers. However, the TCP/IP family of protocols does not closely conform to the OSI model. It's more convenient to think of TCP/IP as consisting of four protocol layers, as shown in Figure 4.1. The following subsections explain each of these layers in detail.

Copyright©2000 SYBEX, Inc., Alameda, CA      www.syex.com