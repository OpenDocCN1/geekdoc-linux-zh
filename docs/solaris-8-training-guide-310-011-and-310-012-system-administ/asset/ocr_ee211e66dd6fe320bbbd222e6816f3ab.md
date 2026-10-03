Name-to-address mapping occurs if a program running on your local system needs to contact a remote computer. The program most likely knows the host name of the remote computer, but might not know how to locate it, particularly if the remote system is in another company, miles from your site. To obtain the remote system’s address, the program requests assistance from the DNS software running on your local system, which is considered a DNS client.

Your system sends a request to a DNS name server, which maintains the distributed DNS database. The files in the DNS database bear little resemblance to the NIS+ host table or even to the local /etc/hosts file, although they maintain similar information: the host names, IP addresses, and other information about a particular group of computers. The name server uses the host name your system sent as part of its request to find or “resolve” the IP address of the remote system. It then returns this IP address to your local system if the host name is in its DNS database.

If the host name is not in that name server’s DNS database, this indicates that the system is outside its authority, or, to use DNS terminology, outside the local administrative domain.

Because maintaining a central list of domain name/IP address correspondences would be impractical, the lists of domain names and IP addresses are distributed throughout the Internet in a hierarchy of authority. A DNS server that maps the domain names in your Internet requests or forwards them to other servers in the Internet. It is probably within close geographic proximity to your Internet access provider.

> NOTE
DNS is not covered in depth on the System Administrator Certification Exam, Part II. You need to know the definition of DNS, but a working knowledge of it is not required until you take the Sun Certified Network Administrator examination.

# LIGHTWEIGHT DIRECTORY ACCESS PROTOCOL (LDAP)

LDAP is the latest name lookup service to be added to Solaris. Specifically, LDAP is a directory service. A directory service is like a database, but contains more descriptive, attribute-based information. The information in a directory is generally read, not written.