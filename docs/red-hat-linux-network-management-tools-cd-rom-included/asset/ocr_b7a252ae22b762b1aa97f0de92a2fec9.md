![](bbox=[0.18, 0.1, 0.82, 0.45])

Figure 3.2 TCP/IP protocol suite.

# End-User Tools

The end-user tools, which are common to many UNIX system implementations of TCP/IP, are applications that are generally available to normal system users. As a result, these tools do not require system root privileges for operation. For example, general users without any special consideration from an administration standpoint can invoke the Telnet and FTP commands. Some services within the TCP/IP suite refer to both end-user applications and protocols. Telnet is a good example of this because it represents both a user tool and a communication protocol. In practice, however, this isn’t a big problem, because end-user applications on UNIX are lower case (such as telnet) and protocols are generally written in upper case.

It is interesting to note that certain organizations disable some TCP/IP services as a way of tightening security. One organization in particular did not want its users to have the ability to send or receive Email on core development systems and removed the SMTP servers from those systems. Another way that organizations