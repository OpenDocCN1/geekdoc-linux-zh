
# Chapter 13 • IMPLEMENTING SYSTEM SECURITY 361

## Physical Security

Physical security starts at a building's perimeter; it controls access to the building and requires authentication of each individual who attempts to enter. Physical security is essential to the security of any system. The advanced security features of applications and operating systems have little impact if physical access to the machines where they run is not restricted.

Many office buildings have unrestricted access during business hours. If your organization is concerned about sensitive information or equipment in the office, you can implement very basic physical security for your building by requiring the use of keys or access cards to gain access to entrances or doors. You can implement the same basic physical security in your data center by allowing only entry to employees who need to work in the data center. If the data center is shared with other companies, you can control access to the machinery using locked cages or cabinets.

On a smaller scale, you can also secure individual pieces of hardware. Many hardware vendors install locks on the chassis of servers and disk arrays, in order to prohibit access by unauthorized personnel to power switches and other critical system components.

You can audit physical security several ways; the simplest of these is to require everyone who enters the data center to sign their name in a sign-in book. Onsite staff must verify the identity of anyone entering the data center and ensure they sign the book. Access card systems provide another common form of physical security; these systems log the name or ID of everyone who enters the facility and the time of their arrival.

Surveillance cameras and video recorders provide site auditing by creating visual records of the data center and all who enter and leave the premises. These systems provide an added benefit by recording the actions of anyone inside the facility. They can also provide proof that someone was not inside the facility.

## Post Surveillance Notification

![](img/894492738e879267320b8d6f9a044180_382_0.png)

Using camera surveillance for physical security doesn't require you to "spy" on staff or visitors. Post notices about any surveillance cameras used in your facility, to warn people that they are under surveillance. This notification can avoid insulting or disturbing staff and visitors, and it may even prevent an incident from occurring.

## Real-World Example: Redundant Data Center Security

![](img/894492738e879267320b8d6f9a044180_382_1.png)

Many data centers use redundant forms of perimeter security. One such data center uses sign-in books and requires identification before you leave the front desk. Only people whose names are on a predefined list of authorized personnel are allowed. Access cards are used for entry to other areas and locks are installed on the doors of all customer cabinets, so that only authorized staff who know the combination can gain access to the hardware inside. Cameras are deployed throughout the facility for visual records of the roaming halls and rooms of the data center. The combination of all these physical security measures ensures that only authorized personnel can access a customer's hardware, while it provides a visual record of all activities that take place in the area and on secured hardware.

![](img/894492738e879267320b8d6f9a044180_382_2.png)

# Network Security

Network security controls what data is allowed in and out of your facilities. Depending on your network layout, the first line of defense on your network is either a firewall or router. The primary purpose of a router is to route traffic to the optimal path through its interfaces. Most routers also support port filtering, in which you can specify the port, source address, and destination address of traffic that is allowed into your network.

Firewalls accomplish the same task, but their hardware is dedicated to the task of layer 4 filtering (often called port filtering). Firewalls also provide protection against common network attacks, such as malformed IP packets and SYN flooding. Many layer 4 filters also watch for application-specific attacks in protocols such as SMTP, HTTP, and FTP. Without layer 4 filters, all IP traffic would be able to reach any network service running on your systems, leaving them open to remote access and exploits from anywhere on the Internet.

## Layer 4 Filtering

Layer 4 filtering works at the fourth layer of the OSI (Open Systems Interconnection) network model—the transport layer. Layer 4 filtering blocks network traffic on the basis of the source or destination port; it is one of the most common uses for a firewall.

Another network security mechanism is intrusion detection. Intrusion detection systems are dedicated to monitoring network traffic for patterns (called signatures) attributable to attacks on network services. They can email or page administrators in the event of suspicious activity and some can even interact with firewalls to block the offending traffic.

## Host Security

Once traffic passes through network security barriers, it reaches the individual hosts on your network. The goal of host security is to prevent unauthorized people from gaining access to files or services on a system. Host security operates at either the local or remote level. Remote host security focuses on hardening network services to prevent unauthorized access from other machines. Local host security protects local resources from users who are already logged into a system.

Both remote and local host security protect data and to prevent exploits and denial-of-service attacks. Local host security is more difficult to manage, however, because users already have access to your systems. Adding to the complexity of host security are third-party applications; systems are not of much use unless there are applications running on them. Applications that run as privileged users or over the network need to be secured against common exploits and configuration errors that could open up your entire system to compromise.

# Chapter 13 • IMPLEMENTING SYSTEM SECURITY 363

## Understanding Least Privilege

One of the most fundamental concepts of security, especially on multiuser systems such as Unix, is the concept of least privilege. Least privilege dictates that users should have only the privileges they need to perform their daily tasks and nothing more. Users with more privileges than they really need are to abuse those privileges and end up doing more damage than good.

For example

## Separation of Services

Separation of services is another important concept for those responsible for securing Unix systems. The basis of this concept is that services with different purposes should reside on separate systems, to minimize the risk to your system when one is compromised.

If one server is hosting three different services—say DNS, email, and your company's Web server—all three services are at risk if that single server is compromised. A hacker could change DNS records, read company email, and bring down your Web server, all by breaking into one machine. Separating these services onto three separate machines minimizes the risk of a total system compromise because the compromise of a single server only puts the service running on that server at risk.

![](img/894492738e879267320b8d6f9a044180_384_0.png)

## Separation of Services Policy

Implementing an effective separation of services policy requires a tradeoff between cost and security. A large number of separated services requires a large number of servers to host them. Providing separate servers to host individual services may be prohibitive to many organizations. If cost constrain your use of policy, separate only your most business-critical services.

## Managing Root Accounts

root is the most powerful account on Unix operating systems, and system administrators should guard it carefully. A poorly managed root account can lead to all kinds of problems—from suddenly changed system configurations to the deletion of entire file systems.
