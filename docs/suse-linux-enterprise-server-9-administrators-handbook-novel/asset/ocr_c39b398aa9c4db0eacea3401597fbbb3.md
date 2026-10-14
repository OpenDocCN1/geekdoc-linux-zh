those addresses. Further granularity can be achieved by placing the `only_from` line in the application-specific configuration file in the `/etc/xinetd.d` directory. Using this approach, you can allow ssh traffic to a list of hosts while allowing VNC traffic from a different list.

The xinetd restriction on IP further reduces the exposure of version harvesting for other utilities such as sftp, echo, and telnet. Because some versions of applications are known to have vulnerabilities, restricting connections—and hence the display of any banner information—reduces the chance of an unwanted machine mining services for information.

In the case of VNC, you could reopen port 5801 on the firewall. With xinetd, you can then grant access to unique static IP addresses for selected machines. You would then be able to offer VNC over HTTP to these specific clients.

# A Secure System Management Environment

In the previous sections, you saw several different methods for accessing a server to perform system management tasks. Because of the sensitivity of the information typically used in system management, encrypted channels are mandatory.

The ssh command was used to create a secure channel through which normally insecure VNC could be used. This allows the system administrator to exploit the benefits of the GUI interface without compromising the security of the session. We also examined how to restrict access to the xinetd family of services to specific IP addresses. In a properly switched environment, such restrictions could be used to allow VNC and XDMCP access to specific workstations.

The secure access methods discussed here can be used to facilitate system management and reduce the number of people requiring physical access to the servers themselves.

# Network Name Services

A Network Name Service is a mechanism by which a requesting client machine can inquire information about a network-available machine or service. In the following sections, we examine services available under SLES.

# Samba

Usually, the Samba software is perceived to be a file and printer sharing application. For it to perform this task, however, a number of factors must be in