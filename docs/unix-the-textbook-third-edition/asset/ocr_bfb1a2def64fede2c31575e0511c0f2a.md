```
% grep "internal"$ /etc/inetd.conf
daytime stream tcp nowait root internal
daytime stream tcp6 nowait root internal
daytime dgram udp wait root internal
daytime dgram udp6 wait root internal
time stream tcp nowait root internal
time stream tcp6 nowait root internal
time dgram udp wait root internal
time dgram udp6 wait root internal
echo stream tcp nowait root internal
echo stream tcp6 nowait root internal
echo dgram udp wait root internal
echo dgram udp6 wait root internal
... [output truncated]
%
```

These services are quite trivial and are handled directly by inetd without running any external program (daemon). They are useful for testing purposes, but are prone to “denial of service” (DoS) attacks. Accordingly, you should disable them by commenting them out. You can list the services that are enabled by using the grep -v "#" /etc/inetd.conf command.

# 20.10.1.2 Locating inetd Services on PC-BSD and Solaris

The /etc/services file is the database that contains the name of a service, the port number for the service, and the transport-layer protocol it uses for communication (usually tcp or udp). Any service that inetd offers must have an entry in the /etc/services file. It has one line per service in the following format:

```
service-name port-number/protocol-name [aliases]
```

Here, service-name is the name of the service such as smtp, port-number is the IANA assigned port number, such as 25 for smtp, and protocol-name is the transport-layer protocol, such as tcp, udp, and so on. Here is an example line from the /etc/services file:

```
pop3 110/tcp    #Post Office Protocol - Version 3
```

This line shows that pop3 is a TCP (i.e., connection-oriented) service, offered at port 110. The following session shows that there are three entries for the SSH service in the /etc/services file on our PC-BSD system. This means that the SSH service is offered on port 22 under the tcp, udp, and sctp protocols. Stream Control Transmission Protocol (SCTP) has been designed to transmit multiple streams of data between two connected sockets. It is also known as the “next generation TCP” or “TCPng.” The SSHELL service on port 614 is for secure socket layer shell (SSLshell).