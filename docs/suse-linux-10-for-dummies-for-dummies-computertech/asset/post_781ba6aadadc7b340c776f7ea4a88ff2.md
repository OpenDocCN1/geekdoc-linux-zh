
## Table 19-1

| Term | Description |
|---|---|
| Bastion host | A highly secured computer that serves as an organization’s main point of presence on the Internet. A bastion host typically resides on the perimeter network, but a dual-homed host (with one network interface connected to the Internet and the other to the internal network) is also a bastion host. |
| Buffer overflow | A security flaw in a program that enables a cracker to send an excessive amount of data to that program and to overwrite parts of the running program with code in the data being sent. The result is that the cracker can execute arbitrary code on the system and possibly gain access to the system as a privileged user. |
| Certificate | An electronic document that identifies an entity (such as an individual, an organization, or a computer) and associates a public key with that identity. A certificate contains the certificate holder’s name, a serial number, expiration date, a copy of the certificate holder’s public key, and the digital signature of the Certificate Authority so a recipient can verify that the certificate is real. |
| Certificate Authority (CA) | An organization that validates identities and issues certificates. |
| Cracker | A person who breaks into (or attempts to break into) a host, often with malicious intent. |
| Confidentiality | Of data, a state of being accessible to no one but you (usually achieved by encryption). |
| Decryption | The process of transforming encrypted information into its original, intelligible form. |
| Denial of Service (DoS) | An attack that uses so many of the resources on your computer and network that legitimate users cannot access and use the system. From a single source, the attack overwhelms the target computer with messages and blocks legitimate traffic. It can prevent one system from being able to exchange data with other systems or prevent the system from using the Internet. |
| Distributed Denial of Service (DDoS) | A variant of the denial-of-service attack that uses a coordinated attack from a distributed system of computers rather than a single source. It often makes use of worms to spread to multiple computers that can then attack the target. |
| Digital signature | A one-way MD5 or SHA-1 hash of a message encrypted with the private key of the message originator, used to verify the integrity of a message and ensure nonrepudiation. |
| DMZ | Another name for the perimeter network. (DMZ originally stood for *demilitarized zone*, the buffer zone separating the warring North and South in Korea and Vietnam.) |
| Dual-homed host | A computer with two network interfaces (think of each network as a home). |
| Encryption | The process of transforming information so it’s unintelligible to anyone but the intended recipient. The transformation is done by a mathematical operation between a key and the information. |
| Exploit tools | Publicly available and sophisticated tools that intruders of various skill levels can use to determine vulnerabilities and gain entry into targeted systems. |
| Firewall | A controlled-access gateway between an organization’s internal network and the Internet. A dual-homed host can be configured as a firewall. |
| Hash | The result when a mathematical function converts a message into a fixed-size numeric value known as a *message digest* (or *hash*). The MD5 algorithm, for example, produces a 128-bit message digest; the Secure Hash Algorithm-1 (SHA-1) generates a 160-bit message digest. The hash of a message is encrypted with the private key of the sender to produce the digital signature. |
| Host | A computer on a network that is configured to offer services to other computers on the network. |
| Integrity | Of received data, a state of being the same as originally sent (that is, unaltered in transit). |
| IPSec (IP Security Protocol) | A security protocol for the Network layer of the OSI Networking Model, designed to provide cryptographic security services for IP packets. IPSec provides encryption-based authentication, integrity, access control, and confidentiality. |
| IP spoofing | An attack in which a cracker figures out the IP address of a trusted host and then sends packets that appear to come from the trusted host. The attacker can send packets but cannot see responses. However, the attacker can predict the sequence of packets and essentially send commands that set up a backdoor for future break-ins. |
| Logic bombs | A form of sabotage in which a programmer inserts code that causes the program to perform a destructive action when some triggering event occurs, such as terminating the programmer’s employment. |
| Nonrepudiation | A security feature that prevents the sender of data from being able to deny ever having sent the data. |
| Packet | A collection of bytes, assembled according to a specific protocol, that serves as the basic unit of communication on a network. On TCP/IP networks, for example, the packet may be referred to as an *IP packet* or a *TCP/IP packet*. |
| Packet filtering | Selective blocking of packets according to type of packet (as specified by the source and destination IP address or port). |
| Perimeter network | A network between the Internet and the protected internal network. The perimeter network (also known as DMZ) is where the bastion host resides. |
| Port scanning | A method of discovering which ports are open (in other words, which Internet services are enabled) on a system, performed by sending connection requests to the ports, one by one. This procedure is usually a precursor to further attacks. |
| Proxy server | A server on the bastion host that enables internal clients to access external servers (and enables external clients to access servers inside the protected network). There are proxy servers for various Internet services, such as FTP and HTTP. |
| Public-key cryptography | An encryption method that uses a pair of keys — a private key and a public key — to encrypt and decrypt the information. Anything encrypted with the public key is decrypted only with the corresponding private key, and vice versa. |
| Public-Key Infrastructure (PKI) | A set of standards and services that enables the use of public-key cryptography and certificates in a networked environment. PKI facilitates tasks, such as issuing, renewing, and revoking certificates, and generating and distributing public- and private-key pairs. |
| Screening router | An Internet router that filters packets. |
| Setuid program | A program that runs with the permissions of the owner regardless of who runs the program. For example, if `root` owns a setuid program, that program has `root` privileges regardless of who started the program. Crackers often exploit vulnerabilities in setuid programs to gain privileged access to a system. |
| Sniffer | Synonymous with packet sniffer — a program that intercepts routed data and examines each packet in search of specified information, such as passwords transmitted in clear text. |
| Symmetric-key encryption | An encryption method wherein the same key is used to encrypt and decrypt the information. |
| Spyware | Any software that covertly gathers user information through the user’s Internet connection and, usually, transmits that information in the background to someone else. Spyware can also gather information about e-mail addresses and even passwords and credit card numbers. Spyware is similar to a Trojan horse in that users are tricked into installing spyware when they install something else. |
| Threat | An event or activity, deliberate or unintentional, with the potential for causing harm to a system or network. |
| Trojan horse | A program that masquerades as a benign program, but, in fact, is a backdoor used for attacking a system. Attackers often install a collection of Trojan horse programs that enable the attacker to freely access the system with `root` privileges, yet hide that fact from the system administrator. Such collections of Trojan horse programs are called *rootkits*. |
| Virus | A self-replicating program that spreads from one computer to another by attaching itself to other programs. |
| Vulnerability | A flaw or weakness that may cause harm to a system or network. |
