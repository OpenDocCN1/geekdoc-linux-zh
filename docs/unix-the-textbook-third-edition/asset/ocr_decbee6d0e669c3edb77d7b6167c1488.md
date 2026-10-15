memory mapped, the X server puts the information it receives from the various clients into one contiguous display buffer in the main memory. Depending on its location on the screen, each client window occupies a particular region of the buffer. The single-process server then uses the select() system call to handle asynchronous input from the client-side sockets and paint the screen accordingly.

You may also like to write the client for a particular service that simultaneously connects with multiple servers for a given service. Such concurrent clients are written using the master–slave model, where a slave process is created to handle a particular server. The domain names and/or IP addresses of the servers are passed to the client as command line arguments. One reason for writing such concurrent clients is to measure the response time for different servers.

# EXERCISE 20.29

Write the names of five well-known Internet services that use concurrent clients. Explain why these services use concurrent clients.

# 20.12 WEB RESOURCES

Table 20.26 lists useful Web sites for UNIX IPC and related topics.

| TABLE 20.26 Web Resources for the UNIX IPC and Related Topics | |
|---|---|
| http://www.iana.org/ | Webpage for Internet Assigned Numbers Authority (IANA): responsible for the global coordination of the DNS Root, IP addressing, transport protocol port numbers, and other Internet protocol resources |
| http://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml
http://tools.ietf.org/html/rfc6335 | Service Name and Transport Protocol Port Number Registry
RFC6335: Internet Assigned Numbers Authority (IANA) Procedures for the Management of the Service Name and Transport Protocol Port Number Registry; forums, user groups, etc. |
| http://www.iana.org/assignments/protocol-numbers
https://www.freebsd.org/ | Official names and numbers of the protocols
Home page for FreeBSD. Contains a lot of useful material, including FreeBSD source, manual pages, support, SVN repository; forums, user groups, etc. |
| http://www.tlshopper.com/tools/port-number/N/
http://www.adminsub.net/tcp-udp-port-finder/N
http://www.tutorialspoint.com/ | Reports IANA assigned service on port 'N' (e.g., for N=22 the page reports the service that is assigned port 22)
Excellent site for tutorials on all kinds of programming languages, including UNIX system programming in C |
| http://stackoverflow.com/ | Free question and answer site for rookie and professional programmers |