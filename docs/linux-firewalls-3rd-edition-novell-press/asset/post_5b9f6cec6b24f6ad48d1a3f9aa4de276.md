
shared printer or shared file systems. Or you might want all of your computers to have access to the Internet. One of your machines might host your private financial records. You might want to have Internet access from this machine, but you don't want anyone getting in. At some point, you might want to offer your own services to the Internet. One of the machines might be hosting your own website for the Internet. Another might function as your mail server or gateway. Your setup and goals will determine your security policies.

The firewall's purpose is to enforce the security policies you define. These policies reflect the decisions you've made about which Internet services you want to be accessible to your computers, which services you want to offer the world from your computers, which services you want to offer to specific remote users or sites, and which services and programs you want to run locally for your own private use. Security policies are all about access control and authenticated use of private or protected services, programs, and files on your computers.

Home and small-business systems don't face all the security issues of a larger corporate site, but the basic ideas and steps are the same. There just aren't as many factors to consider, and security policies often are less stringent than those of a corporate site. The emphasis is on protecting your site from unwelcome access from the Internet. A packet-filtering firewall is one common approach to, and one piece of, network security and controlling access to and from the outside.

Of course, having a firewall doesn't mean you are fully protected. Security is a process, not a piece of hardware. For example, even with a firewall in place it's possible to download spyware or adware or click on a maliciously crafted email, thereby opening up the computer and thus the network to the attack. It's just as important to have measures in place to mitigate successful attacks as it is to spend resources on a firewall. Using best practices inside of your network will help to lessen the chance of a successful exploit and give your network resilience.

Something to keep in mind is that the Internet paradigm is based on the promise of end-to-end transparency. The networks between the two communicating machines are intended to be invisible. In fact, if a network device somewhere along the path fails, the idea is that traffic between the two endpoint machines will be silently rerouted.

Ideally, firewalls should be transparent. Nevertheless, they break the Internet paradigm by introducing a single point of failure within the networks between the two endpoint machines. Additionally, not all network applications use communication protocols that are easily passed through a simple packet-filtering firewall. It isn't possible to pass certain traffic through a firewall without additional application support or more sophisticated firewall technology.

Further complicating the issue has been the introduction of Network Address Translation (NAT, or "masquerading" in Linux parlance). NAT enables one computer to act on behalf of many other computers by translating their requests and forwarding them on to their destination. The use of NAT along with RFC 1918 private IP addresses has effectively prevented a looming shortage of IPv4 addresses. The combination of NAT and RFC 1918 address space makes the transmission of some types of network traffic difficult, impossible, complex, or expensive.

# NOTE

Many router devices, especially those for DSL, cable modems, and wireless, are being sold as firewalls but are nothing more than NAT-enabled routers. They don't perform many of the functions of a true firewall, but they do separate internal from external. Be aware when purchasing a router that claims to be a firewall but only provides NAT. Although some of these products have some good features, the more advanced configurations are sometimes not possible.

A final complication has been the proliferation of multimedia and peer-to-peer (P2P) protocols used in both real-time communication software and popular networked games. These protocols are antithetical to today's firewall technology. Today, specific software solutions must be built and deployed for each application protocol. The firewall architectures for easily and economically handling these protocols are in process in the standards committees' working groups.

It's important to keep in mind that the combination of firewalling, DHCP and NAT introduces complexities that cause sites to have to compromise system security to some extent in order to use the network services that the users want. Small businesses often have to deploy multiple LANs and more complex network configurations to meet the varying security needs of the individual local hosts.

Before going into the details of developing a firewall, this chapter introduces the basic underlying concepts and mechanisms on which a packet-filtering firewall is based. These concepts include a general frame of reference for what network communication is, how network-based services are identified, what a packet is, and the types of messages and information sent between computers on a network.

# CHAPTER 1: Preliminary Concepts Underlying Packet-Filtering Firewalls

## The OSI Networking Model

The OSI (Open System Interconnection) model represents a network framework based on layers. Each layer in the OSI model provides distinct functionality in relation to the other layers. The OSI model contains seven layers, as shown in Figure 1.1.

**FIGURE 1.1**
The seven layers of the OSI model.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_29_0.png)

The layers are sometimes referred to by number, with the lowest layer (Physical) being layer 1 and the highest layer (Application) being layer 7. If you hear someone refer to a "Layer 3 switch," he is referring to the third layer of the OSI model. As a person interested in security and intrusion detection, you must know the layers of the OSI model to fully understand the attack paths that could compromise your systems.

Each layer in the OSI model is important. The protocols you use every day, such as IP, TCP, ARP, NFS, and others, reside on the various layers of the model. Each layer has its own distinct function and role in the communication process.

The Physical layer of the OSI model is occupied by the media itself, such as the cabling and related signaling protocols, in other words, transferring the bits. For the most part, the Physical layer is of less concern to the network intrusion analyst beyond securing the devices and cabling themselves. Because this book doesn’t really talk much about physical security (how interesting are door locks?), I won’t be devoting more time to the Physical layer of the OSI model either. Naturally, the steps you take to secure physical wires are different from those you would take to attempt to secure wireless devices.

The next layer above Physical is the Datalink layer. The Datalink layer transfers the data over the given medium and is responsible for things such as detection and recovery from errors in transmission. The Datalink layer is also the layer where physical hardware addresses are defined, such as an Ethernet card’s Media Access Control (MAC) address.

Above the Datalink layer, the Network layer is the all-important third layer in IP networks. This layer is responsible for the logical addressing and routing of data. IP is a Network layer protocol, which means that the Network layer is the layer on which IP addresses and subnet masks are used. Routers and some switches operate at layer three, moving data between both logically and physically divided networks.

The fourth layer, the Transport layer, is the primary layer on which reliability can be built. Protocols that exist at the Transport layer include TCP and UDP. The fifth layer is the Session layer, within which sessions are built between endpoints. The sixth layer, Presentation, is primarily responsible for communication with the Application layer above it, and it also defines such things as encryption to be used. Finally, the Application layer is responsible for displaying data to the user or application.

Aside from the OSI model, there exists another model, the DARPA model, sometimes called the TCP/IP reference model, which is only four layers. The OSI model has become the traditional or de facto model on which most network discussions take place.

As data moves from an application down the layers of the OSI model, the protocol at the next lower layer may add its own information onto the data. This data usually consists of a header that is prepended onto the data from the next highest level, though sometimes a trailer is added as well. This process, called encapsulation, continues until the data is transmitted across the physical medium. In the case of Ethernet, the data is known as a frame when it is transmitted. When the Ethernet frame arrives at its destination, the frame then begins the process of moving up the layers of the OSI model, with each layer reading the header (and possibly trailer) information from the corresponding layer of the sender. This process is called demultiplexing.

## Connectionless Versus Connection-Oriented Protocols

At some layers of the OSI model, protocols can be defined in terms of one of their properties, connectionless or connection-oriented. This definition refers to the methods that the protocol contains for providing such things as error control, flow control, data segmentation, and data reassembly.

Think of connection-oriented protocols in terms of a telephone call. Generally there is an acceptable protocol for making a phone call and having a conversation. The person making the call, the initiator of the communication, opens the communication by dialing a telephone number. The person (or machine, as is the ever-increasing case) at the other end receives the request to begin a telephone conversation. The request to initiate a telephone conversation is frequently indicated by the ringing of the telephone on the receiver's end. The receiver picks up the telephone and says "Hello" or some other form of greeting. The initiator then acknowledges this greeting by responding in kind. At this point, it's safe to say that the conversation or
