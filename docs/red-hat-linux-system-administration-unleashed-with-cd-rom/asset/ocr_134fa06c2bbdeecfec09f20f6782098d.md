# Security and Legal Issues

Because the File Transfer Protocol allows remote users to retrieve and possibly store information on your network-connected servers, it brings with it several important security and legal issues. It is necessary for all of these issues to be carefully examined before any FTP-enabled host is allowed on your network.

One extremely important issue to be aware of when setting up a File Transfer Protocol server is the legal standpoints concerning site content. United States Federal law decrees that sites are indeed responsible for their content. This means that any illegal files or data contained on an FTP server could result in possible legal ramifications for that particular site’s owner. Since this can result in possible serious legal trouble for site operators depending on the type of illegal content, much planning and thought should be undertaken before setting up any FTP server. Assistance with this matter is given in the “Dealing With Warez D00dz” section of this chapter.

Administrators should also be aware of the security issues associated with operating an FTP site. File Transfer Protocol servers often run with root privileges, resulting in the possibility of a total system compromise if attackers are able to compromise a vulnerable or misconfigured server.

Security flaws are often found in many popular FTP server packages, which open sites to such vulnerabilities. Care should be taken to properly secure your FTP servers and monitor the output of the security community for vulnerabilities affecting any software packages in use.

# Protecting Your FTP Servers

There are many options available that can be of assistance when securing an FTP server. This section concentrates on the options available for Red Hat 6 systems running WU-FTPD. However, it should be noted that other FTP server packages may support the same configuration methods listed here.

This is because other products may be derivatives of the WU-FTPD system or may simply share similar options and capabilities.

It may be desirable when securing an FTP server to restrict access based on remote clients’ IP addresses. This can be a valuable, but not foolproof, tool for protecting a server. Address-based access control can be easily fooled using network spoofing techniques. Therefore, this method of access control should only be considered a supplemental, not primary, security measure. FTP server access may be restricted for particular user accounts