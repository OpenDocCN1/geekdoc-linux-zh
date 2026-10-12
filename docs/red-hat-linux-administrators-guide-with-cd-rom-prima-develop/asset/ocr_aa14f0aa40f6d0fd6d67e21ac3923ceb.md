also comes in an RPM format, tcp\_wrappers automatically makes the needed changes to the inetc.conf file, so editing the file manually is unnecessary.

# Finding Port Numbers in the /etc/services File

Every service that runs under Linux requires a port number, a specific number to which a client connects to obtain the service. This can be either an external or local service. If the port number of a certain service is not known, you can usually find it in the /etc/services file. This specific file lists all available services such as SMTP, FTP, Telnet, HTTP, and a host of others. Generally, the port numbers for basic Linux services are kept under 1024. These are reserved ports and should only be used for specific services as defined by the Internet Assigned Numbers Authority (IANA). A daemon must be run by root to use these port numbers. For security reasons, it is best to monitor what services are run on ports numbered lower than 1024. Any number higher than 1024 is either open for use or reserved for other network applications.

Listing 2.4 shows a sample excerpt of an /etc/services file. It lists ports 21 through 25 and the services they offer. Generally, all services will be available with any default Red Hat Linux setup. Additional ports such as 110 for the Post Office Protocol (POP) service rarely require tweaking. Editing the /etc/services file does not change the security on your system. The daemon itself must be disabled in either the /etc/inetd.conf file or by editing the startup scripts if you wish to increase the security or use tcp\_wrappers. You may have to add an additional field to /etc/services if implementing a new service such as Secure Shell (ssh) or when redefining an existing protocol such as POP3 when establishing an additional alias.

Listing 2.4 is a small excerpt from the /etc/services file and shows how each field is configured.

# Listing 2.4 An Excerpt Taken from a Default /etc/services File

```
ftp			21/tcp
fspd		21/udp		fspd
ssh		22/tcp			# SSH Remote Login Protocol
ssh		22/udp			# SSH Remote Login Protocol
telnet	23/tcp
# 24 - private
smtp	25/tcp		mail
```