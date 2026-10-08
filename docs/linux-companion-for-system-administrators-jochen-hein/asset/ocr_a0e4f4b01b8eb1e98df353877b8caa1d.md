# PROTOCOLS 399

Depending on the protocol, the application data are equipped with the appropriate header. These headers are defined in the corresponding RFCs: Each additional protocol layer adds its own management data as the overhead increases and an increasingly larger amount of data must be transmitted. Only in the last step are the packets converted into a format that suits the transmission medium; that is, they are equipped with an Ethernet or Token Ring header and then output to the transmission medium.

On the basis of TCP and UDP further (application) protocols or services are defined (in the file /etc/services, Listing 14.2), which are used by the individual applications, such as telnet or ftp. It is these applications that make a network useful. The file /etc/services assigns protocol names to the TCP and UDP ports, through which communication takes place.

In the first column, the file /etc/services (Listing 14.2) contains the official name of the protocol. In the second column (separated by tabs or spaces) you will find the number of the port and the protocol used. A port can simultaneously be used for services on UDP and TCP; on the basis of the protocol numbers defined in /etc/protocols and used in the packet headers, the correct drivers are selected in the kernel and the data is forwarded to the correct program. Additional columns can be used to define aliases for the ports. Comments begin with a hash sign and end with the end of line.

| tcmux | 1/tcp | # TCP port service multiplexer |
| echo | 7/tcp | |
| echo | 7/udp | |
| discard | 9/tcp | sink null |
| discard | 9/udp | sink null |

Listing 14.2 Excerpt from the file /etc/services.

Many protocols, including their port numbers, are standardized Internet. The officially reserved ports are administered by the Internet Assigned Numbers Authority (IANA) (see http://www.iana.org). For general information, the numbers are published periodically, most recently in [rfc2600]. The port numbers, if possible, be unique. programmers should register the ports they are using with the IANA.

Port numbers can lie in the range from 1 to 65 535, where the ports from 1 to 1024 are reserved for the user root. This ensures that at the other end of a connection an service is waiting, for example in a telnet or ftp connection through which a password is transmitted (without encryption).

Programs use port numbers internally, the port names can be converted into the corresponding numbers by means of the function getservbyname(3). In a large network keeping the services files