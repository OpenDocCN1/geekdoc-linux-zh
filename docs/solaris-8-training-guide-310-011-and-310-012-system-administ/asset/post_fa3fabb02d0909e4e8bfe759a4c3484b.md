
## APPLY YOUR KNOWLEDGE

stream of packets to hostB:

```
spray hostB
```

5. Watch the information that is displayed in the first window that is running snoop.

## Review Questions

1. Name and provide a brief description of each layer of the seven-layer OSI model.

2. Name and provide a brief description of each layer of the five-layer TCP/IP model.

3. In TCP/IP, a packet that contains a header from the Physical layer, followed by a header from the Network layer (IP), followed by a header from the Transport layer (TCP), followed by the application protocol data would be referred to as what?
A. De-Encapsulation
B. Encapsulation
C. Encryption
D. Decryption

4. By what other name is a host's unique Ethernet address referred to?
A. IP address
B. MAC address
C. Internet address
D. Hostname

5. Which of the following network configuration files does the Solaris installation program always set up? Choose all that apply.
A. /etc/hostname.interface
+   B. /etc/nodename
C. /etc/inet/hosts
D. /etc/defaultdomain

6. Which daemon starts the appropriate server process when a request for that service is received?
A. inetd
B. init
C. mountd
D. nfsd

7. What is TCP/IP?
A. A general name for a set of protocols that allow computers to share resources across the network
B. A network security specification used widely on the Internet
C. One of the services provided by the domain name service
D. Transfer control protocol/information protocol

8. Which of the following statements about IP addresses are true? Choose all that apply.
A. IP addresses are written as four sets of numbers separated by periods.
B. IP addresses provide a means of identifying and locating network resources.
C. IP addresses are divided into three unique numbers: network, class, and host.
D. The IP address identifies the machine to its peers on the network.

9. Which of the following statements is true about the /etc/hostname.xxy file?
A. It is a system script file.
B. It is a SPARC executable file.
C. It contains the hostname of the local host.
D. It identifies the network interface on the local host.

10. Which of the following is a network component that forwards Ethernet packets from one network to another?
A. Hub
B. Switch
C. Network interface
D. Router

11. Which of the following contains the IP addresses and hostnames of machines on your network?
A. /etc/inet/hosts
B. /etc/hostname.xxy
C. /etc/defaultdomain
D. /etc/nodename

12. Which of the following network classes is for medium-sized networks such as campuses and large businesses with many hosts on their network?
A. Class A
B. Class B
C. Class C
D. Class D

13. Which of the following commands are used to transfer one or more files between two systems on the network? Choose all that apply.
A. rexec
B. telnet
C. ftp
D. rcp
E. rsh

14. Which of the following commands executes a shell on a remote system?
A. rlogin
B. rexec
C. telnet
D. rcp
E. rsh

15. Which of the following commands displays information on users logged on the local or other systems?
A. who
B. logins
C. finger
D. rexec

16. Which of the following commands can tell you whether packets are being delayed or dropped on your network?
A. spray
B. ping
C. netstat
D. iostat

17. Which of the following commands is used to monitor the system's TCP/IP network activity?
+   A. iostat
B. vmstat
C. netstat
D. ping

18. Which command is used to determine the information that is flowing across the network between systems?
+   A. netstat
B. snoop
C. iostat
D. ping

## Answers to Review Questions

1. Physical. Layer 1 describes the network hardware, including electrical and mechanical connections to the network.

Data Link. Layer 2 splits data into frames for sending on the Physical layer and receives acknowledgement frames. It performs error checking and retransmits frames not received correctly.

Network. Layer 3 manages the delivery of data via the Data Link layer and is used by the Transport layer. IP is the most common Network layer protocol.

Transport. Layer 4 determines how to use the Network layer to provide a virtually error-free, point-to-point connection so that host A can send messages to host B and they will arrive uncorrupted and in the correct order.

Session. Layer 5 uses the Transport layer to establish a connection between processes on different hosts. It handles security and creation of the session.

Presentation. Layer 6 performs functions such as text compression, code, or format conversion to try to smooth out differences between hosts. Allows incompatible processes in the Application layer to communicate via the Session layer.

Application. Layer 7 is concerned with the user's view of the network (that is, formatting electronic mail messages). The Presentation layer provides the Application layer with a familiar local representation of data independent of the format used on the network.

2. The Hardware layer corresponds to the ISO/OSI Physical layer and describes the network hardware including electrical and mechanical connections to the network. This layer regulates the transmission of unstructured bit streams over a transmission medium.

The Network Interface layer corresponds to the ISO/OSI Data Link layer and manages the delivery of data across the physical network. This layer provides error detection and packet framing.

The Internet layer corresponds to the ISO/OSI Network layer and manages data addressing and delivery between networks, as well as fragmenting data for the Data Link layer.

The Transport layer corresponds to the ISO/OSI Transport layer and ensures that messages reach the correct application process using TCP and UDP.

The Application layer corresponds to the Session layer, Presentation layer, and Application layer of the ISO/OSI model. The Application layer manages user-accessed application programs and network services. This layer is responsible for defining the way in which cooperating networks represent data.

3. B. When systems communicate via a network, think of the data progressing through each layer down from the Application layer to the Hardware layer, across the network, and then flowing back up from the Hardware layer to the Application layer. A header is added to each segment received on the way down the layers. This is referred to as encapsulation.

4. B. A host's unique Ethernet address is also referred to as the MAC address.

5. A., B., C. The following network configuration files, /etc/hostname.interface, /etc/nodename, and /etc/inet/hosts, are initially set up by the Solaris installation program.

6. A. An inetd daemon starts the appropriate server process when a request for that service is received.

7. A. TCP/IP is a general name for a set of protocols that allow computers to share resources across the network.

8. A., B., D. The following are true of IP addresses: IP addresses are written as four sets of numbers separated by periods, IP addresses provide a means of identifying and locating network resources, IP addresses identify the machines to their peers on the network.

9. D. The /etc/hostname.xxy file identifies the network interface on the local host.

10. D. The router is a network component that forwards Ethernet packets from one network to another.

11. A. The /etc/inet/hosts file contains the IP addresses and hostnames of machines on your network.

12. B. Class B network classes are for medium-sized networks, such as campuses and large businesses with many hosts on their network. A class B network can accommodate a maximum of 65,534 hosts.

13. C., D. The commands ftp and rcp are used to transfer one or more files between two systems on the network.

14. E. The rsh command executes a shell on a remote system.

15. C. The finger command displays information on users logged on the local or other systems.

16. A. The spray command tests the reliability of your network. It can tell you whether packets are being delayed or dropped. spray sends a one-way stream of packets to a host using a Remote Procedure Call (RPC). It reports how many were received, as well as the transfer rate.

17. C. The netstat command is used to monitor the system's TCP/IP network activity. netstat can provide some basic data about how much and what kind of network activity is happening.

18. B. The snoop command is used to determine what information is flowing across the network between systems.
