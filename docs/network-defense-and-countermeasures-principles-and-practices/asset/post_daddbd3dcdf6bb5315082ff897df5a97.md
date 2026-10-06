
## In Practice

## Extra Firewall Features

You have noted that many of the firewall solutions come with a variety of extra features not directly related to packet filtering/blocking. You have probably noticed that many of these features can be obtained from other sources for free. So, the question arises: Why not just use the built-in Windows firewall or some other firewall, and then get the other features on your own?

The answer is reality of use. In addition to functionality, any technology product has to be evaluated based on usability. For example, you can use traceroute commands, scan your machine for vulnerabilities, and monitor various websites to keep current with attacks, but given that most administrators are quite busy, isn't it more convenient to have all these features in one place?

Home users certainly do not have access to a dedicated network administrator and certainly do not have a dedicated network security professional. Many small- to medium-sized organizations are in the same boat. They may not have a basic general support person on site. In this case the person handling security has limited skills and will benefit from tools that do much of the work for them.

From a practical point of view, some of these features might be superfluous to a security-savvy network administrator or a dedicated network security professional. However, for the small or office user, they can be absolutely critical. You will be asked to recommend security solutions on the job as well as in your private life. You must keep in mind not only the technical strengths of each product, but how easy the product will be for the person who uses it.

There are other personal firewall solutions. Most Linux distributions have one or more built-in firewalls. A Google or Yahoo search for "free firewall" will provide several options. In most cases, personal firewalls will simply be packet filtering firewalls. Most free solutions have limited features, whereas many commercial products will add in additional features.

## Using Small Office/Home Office Firewalls

The small/home office system (often referred to as SOHO) will frequently have needs similar to the individual PC firewall. The personnel handling the firewall will have limited network administration and security training. Both Norton and McAfee offer solutions to be perimeter firewalls for a small network. These products are quite similar to their individual PC firewalls, but with added features and a slightly higher cost. However, there are other solutions for the SOHO which we will examine here. Keep in mind that critical consideration with any firewall for this environment is ease of installation and use.

## SonicWALL

SonicWALL is a vendor of several firewall solutions. Their TZ series is made specifically for small networks with 10 to 25 users. It costs between $350 and $700, depending on the version and retailer. TZ200 is a router-based firewall, as shown in Figure 4-6. You can purchase their products from their vendor SonicGuard, http://www.sonicguard.com. That one is now discontinued and the current products are TZ300 or TZ400, or you can use TZSOH (Small Office Home Office).

![](img/b9022ea8d49ef539d37d0ec09f73f71c_132_0.png)

FIGURE 4-6 The SonicWall TZ 200 01-SSC-8741 Security Appliance Firewall

Most importantly, this product uses stateful packet inspection, which is significantly more secure than basic packet filtering.

One additional feature that SonicWALL products offer is built-in encryption so that all transmissions are encrypted. Currently their products offer AES and 3DES encryption. While not strictly a firewall feature, this is an important part of network security. When packets are sent around a network and outside the network, it is not difficult to intercept these packets with a packet sniffer and get the data if the packets are not encrypted.

Management of the SonicWALL firewall should be easy to master for those familiar with Windows 2000 and later versions of Windows because the management is based on objects, such as users, groups, and even IP address ranges. Once a group is defined, you can apply filtering/blocking properties to that group.

> FYI: AES and 3DES Encryption

> Chapter 6, "Encryption Fundamentals," describes encryption in detail, including how various encryption methods work. At this point it is important to understand that both AES and 3DES are considered highly secure encryption methods and should be appropriate for any network security situation. However, AES is preferred by the NIST (National Institute of Standards) and is generally recommended above 3DES.

SonicWALL, as well as many other modern firewalls, offer built-in NAT. This technology is designed to replace proxy servers. It accomplishes the same goal of hiding internal network IP addresses from the external world.

SonicWall offers more advanced firewall solutions with their next-generation security appliances. NSA 2650 is one of those appliances. These include features such as the ability to decrypt SSL/TLS and examine it. This prevents internal users (or malware) from using SSL/TLS to exfiltrate data from your network. These systems also have integrated intrusion prevention systems (IPS). We will be discussing IPS in detail in Chapter 5, “Intrusion-Detection Systems.”

The advantages and disadvantages of SonicWALL are briefly listed here.

### Advantages

- SonicWALL firewalls provide stable packet inspection.
- SonicWALL firewalls provide built-in encryption.
- SonicWALL firewalls provide management and configuration that is easy for Windows administrators.
- SonicWALL firewalls provide built-in NAT.

### Disadvantages

- The price of SonicWALL firewalls may be prohibitive for small offices on a tight budget.
- SonicWALL firewalls require some skill to configure and are not intended for the complete novice.

## D-Link DFL-2560 Office Firewall

D-Link makes a number of products for home users and for small offices. Its NetDefend firewall is a router-based firewall that uses stateful packet inspection to filter network traffic, D-Link has products for small and large businesses, and you can see all of their products at http://us.dlink.com/home-solutions/cloud/product-family/. The NetDefend Network UTM Firewall DFL-2560 is shown in Figure 4-7.

![](img/b9022ea8d49ef539d37d0ec09f73f71c_133_0.png)

FIGURE 4-7 The DFL-2560

This firewall is fairly easy to configure and has a web-based interface, similar to the type used by many home wireless router manufacturers. By using any computer connected directly to the router, you can enter the router's IP address and you will be presented with a web page that enables you to configure the router. Of course, one of the first things you should do is change the password to prevent other parties from reconfiguring your router-based firewall. This firewall solution can be a bit more expensive than the others we have discussed, costing several thousand dollars. However, it is not a single firewall solution, but rather a solution for your gateway, protecting your entire network. Unlike many firewall solutions, the vendor does not require any licenses for additional users, so if your company goes from 20 to 50 users, it need not purchase additional licenses.

Here are the advantages and disadvantages of the DFL-2560.

### Advantages

- The DFL-2560 includes built-in reliable encryption.
- The DFL-2560 supports whitelisting and blacklisting.
- The DFL-2560 has built-in intrusion detection systems.
- The DFL-2560 has built-in antivirus.
- The DFL-2560 uses stateful packet inspection.
- The DFL-2560 combines multiple firewall types.
- The DFL-2560 includes built-in NAT.
- The DFL-2560 includes built-in VPN.

### Disadvantages

- The DFL-2560 lacks some security features that more advanced systems might offer.

## Using Medium-Sized Network Firewalls

Medium-sized networks can be defined as having as few as 25 users up to several hundred users all on a single LAN at a location. Administrators of medium-sized networks face configuration and security issues beyond what an administrator in a home or small offices might encounter. To begin, medium-sized networks are likely to have a more diverse group of users and applications running. Each of these presents different access needs and security requirements. On the other hand, medium-sized networks typically benefit from the support of dedicated network administration personnel. This means there is someone on site who has at least a basic understanding of computer security.

## Check Point Firewall

Check Point is a well-known manufacturer of security equipment, and it offers a range of firewall products designed explicitly for medium- to large-sized networks. The 1400 and 3000 security appliance