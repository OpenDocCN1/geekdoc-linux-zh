The two NS records define the primary and secondary DNS servers that will be used to resolve your hostnames (again, belonging to the ISP), and the two MX records define the primary (mail1.isp.net) and secondary (mail2.isp.net) mail servers that will receive and spool mail for your domain.

This configuration contains two CNAME records, which define nicknames for services in your domain. The hostname www.smallorg.org is a nickname that points to the ISP server that hosts your web pages. The address ftp.smallorg.org is also a nickname, and it points to the same ISP server that hosts your FTP site.

This is a service that most ISPs provide to customers who cannot afford to have a dedicated connection to the Internet but want to provide web and FTP services to their customers. The last two lines provide the Internet IP address information so that remote clients can connect to this server.

Once a DNS server has a valid database installed, it must be able to communicate with other DNS servers to resolve hostname requests from clients and respond to other DNS servers’ queries about hosts in its zone. The DNS protocol was invented to accomplish that.

# DNS Protocol

The DNS protocol serves two functions. It allows client computers to query a DNS server for an IP address or a hostname, and it allows DNS servers to communicate with each other and pass DNS database information back and forth.

It uses a standard request/response format, where the client submits a request packet, and the server returns a response packet with either the information from the database or an error message stating the reason the query could not be processed.

The DNS protocol uses either TCP or UDP well-known ports 53 to communicate. UDP has become the preferred method of transportation across the Internet because of its low packet overhead (UDP doesn't need to establish the connection to verify packets like TCP does).

The DNS packet contains five main sections:

+   - **Header:** Contains information identifying the packet and its purpose.
+   - **Question:** Contains the DNS queries the client wants answers for.
+   - **Answer:** Contains the DNS server response to the client questions.
+   - **Authority:** Contains information about which local DNS server is the authority for the zone of the requested questions.
+   - **Additional Information:** Contains information about the caching length and other features of the returned information.

Both the DNS client and server use the same DNS protocol packets, just with different information in them.

# Ubuntu as a DNS Client

If you do not have a dedicated connection to the Internet, you should not use your Ubuntu server as a DNS server for your domain. If someone tried sending email to you at 3 a.m., and your Ubuntu server was not up and connected to the Internet, they might not be able to resolve your domain name and send your message. Most ISPs provide a DNS server for their clients. You can use the DNS server that your ISP provides to resolve hostnames using your Ubuntu server as a client.