global level (Internet environment). To address this scaling issue, FNS can be used to *federate* or link NIS or NIS+ with a global-level naming service, such as X.500 via the Lightweight Directory Access Protocol (LDAP) or DNS. By linking these naming services, the information managed by the enterprise-level name service is accessible globally.

Sun Microsystems does not fully embrace X.500/LDAP as a naming service or provide an LDAP server as part of the Solaris 8 distribution. However, it does provide an LDAP client and an LDAP data caching mechanism.

![](bbox=[0.148, 0.286, 0.261, 0.355])

Of these naming services, NIS and NIS+ are covered in the most detail on the exam. The /etc files and DNS are covered briefly. FNS will probably not be mentioned. However, be sure to understand the significance of enterprise-level (NIS and NIS+) versus global-level (DNS and LDAP) naming services.

# Domain Name System (DNS)

DNS, part of the TCP/IP protocol suite, is the name service the Internet uses. It provides hostname-to-IP address resolution as well as IP address-to-hostname resolution. The DNS namespace is divided into domains that in turn are divided into subdomains (or zones). One or more DNS servers can be responsible (authoritative) for a zone. All the DNS servers work together to provide name resolution services across the entire namespace. The DNS server provided with Solaris 8 is version 8.1.2 of the Berkeley Internet Name Domain (BIND) program, referred to as the *Internet name daemon* (in.named).

Information on the namespace is stored in text files using a predefined syntax known as *records*. The named program uses the following data files:

+   - **/etc/named.conf**—The BIND configuration file that identifies zones over which the DNS server is authoritative and the associated data files
+   - **/etc/resolv.conf**—When configured as a DNS client, a file that identifies the DNS server that should be used for name resolution
+   - **named.ca**—The names and IP addresses of the Internet root DNS servers
+   - **hosts**—The DNS address (A type) records used for resolving hostnames to IP addresses (not to be confused with the /etc/hosts file)
+   - **hosts.rev**—The DNS pointer (PTR type) records used for resolving IP addresses to hostnames
+   - **named.local**—The DNS records for the localhost or the loopback interface