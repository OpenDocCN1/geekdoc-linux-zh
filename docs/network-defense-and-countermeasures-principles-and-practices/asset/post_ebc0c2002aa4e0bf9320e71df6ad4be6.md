
# CHAPTER 1 Introduction to Network Security

often dependent on frequencies. (If you have a touchtone phone, you will notice that, as you press the keys, each has a different frequency.) Machines record and duplicate certain frequencies are often essential to phone hacking.

# Security Terminology

Security professionals have specific terminology as well. Readers with any training or experience in network administration are probably already familiar with most of these terms. Although hacking terminology describes either the activity or the person performing it (hacking, sneaker, etc.), much of the security terminology you will learn in this book deals with devices and policies. This is quite logical because hacking is an offensive activity centered on attackers and attack methodologies, and security is a defensive activity concerned with defensive barriers and procedures.

The first and most basic security device is the firewall. A firewall is a barrier between a network and the outside world. Sometimes a firewall is a stand-alone server, sometimes a router, and sometimes software running on a machine. Whatever its form, the purpose is the same: to filter traffic entering and exiting a network. Firewalls are related to, and often used in conjunction with, proxy server. A proxy server handles your internal network IP addresses and presents a single IP address (its own) to the outside world.

Firewalls and proxy servers are used to provide network perimeter security. They filter incoming and outgoing network traffic but do not affect traffic on the network. Sometimes these devices are augmented by an intrusion-detection system (IDS). An IDS monitors traffic looking for suspicious activity that might indicate an attempted intrusion.

Access control is another important computer security term that will be of particular interest to you in several of the later chapters. Access control is the aggregate of all measures taken to limit access to resources. It includes login procedures, encryption, and any method that is designed to prevent unauthorized personnel from accessing a resource. Authentication is a subset of access controls, perhaps the most basic security activity. Authentication is simply the process of determining whether the credentials given by a user or another system, such as a username and password, are authorized to access the network resource in question. When a user logs in with a username and password, the system attempts to authenticate that username and password. If they are authenticated, the user will be granted access.

Non-repudiation is another term you encounter frequently in computer security. It is any technique that is used to ensure that someone performing an action on a computer cannot falsely deny that they performed that action. Non-repudiation provides reliable records of what user did a particular action at a specific time. In short, it is methods to track what actions are taken by user. Various system logs provide one method for non-repudiation. One of the most important security activities is auditing. Auditing is the process of reviewing logs, records, and procedures to determine whether they meet standards. This activity is discussed throughout this book and is the focus of Chapter 12. Auditing is essential to do checking that systems have appropriate security in place is the only way to ensure system security.

# Choosing a Network Security Approach

Least privileges is a concept you should keep in mind when assigning privileges to any user or device. The concept is that you only assign the minimum privileges required for that person to do his job, no more. Keep this simple but critical concept in mind.

You should also keep in mind the CIA triangle, or Confidentiality, Integrity, and Availability. All security measures should affect one or more of these areas. For example, hard drive encryption and good passwords help protect confidentiality. Digital signatures help ensure integrity, and a good backup system, or server redundancy, can support availability.

An entire book could be written on computer security terminology. These few terms were introduced to be ubiquitous and being familiar with them is important. Some of the exercises at the end of this chapter will help you expand your knowledge of computer security terminology. You might also find these links helpful:

- https://niccs.us-cert.gov/glossary (National Initiative for Cybersecurity Careers and Studies Glossary)
- https://www.sans.org/security-resources/glossary-of-terms/ (SANS Institute of Security Terms)
- https://nlvpubs.nist.gov/nistpubs/ir/2013/NIST.IR.7298r.pdf (NIST Glossary of Key Information Security Terms)

> FYI: Auditing and Penetration Testing

The process of a penetration tester is really just special type of audit. You might wonder what the difference is between penetration testing and auditing. The distinction lies in the methodology. Audits usually involve checking compliance with regulations, whereas penetration tests attempt to breach the system.

# Choosing a Network Security Approach

Organizations can choose from several approaches. A particular approach, or paradigm, will influence all security decisions. Network security paradigms can be classified by either the scope of security taken (perimeter, layered) or how proactive it is.

# Perimeter Security Approach

In a perimeter security approach, the bulk of security efforts are focused on the perimeter of the network. This focus might include firewalls, proxy servers, password policies, and any technology that makes unauthorized access less likely. Little or no effort is made to secure systems within the network. This approach is clearly flawed. So why do some companies use it? A small organization might use the perimeter approach if they have budget constraints or inexperienced network administrators and if they do not store sensitive data.

# Layered Security Approach

A layered security approach is one in which not only the perimeter is secured, but individual systems within the network are also secured. All servers, workstations, routers, and hubs within the network are secure. One way to accomplish this is to divide the network into segments and secure each segment as if it were a separate network so that, if security is compromised, no internal systems are affected. Layered security is the preferred approach whenever possible.

You should also measure your security approach by how proactive andor reactive it is. You do this by gauging how much of the system security infrastructure and policies are dedicated to preventive measures as opposed to how much are devoted to responding to an attack after it has occurred.

A passive security approach takes few or no steps to prevent an attack. Conversely a dynamic security approach, or proactive defense, is one in which steps are taken to prevent attacks before they occur. One example of a proactive defense is the use of an IDS, which detects attempts to circumvent security measures. These systems can tell a system administrator that an attempt to breach security has been made, even if that is not successful. An IDS can also be used to detect various techniques intruders use to assess a target system, then alerting a network administrator to the potential for an attack before it is initiated.

# Hybrid Security Approach

In the real world, network security is rarely completely in one paradigm or another. Networks generally fall along a continuum with elements of more than one security paradigm. The two categories also combine to form a hybrid approach. One can have a network that is predominantly layered, or one that is primarily perimeter, but proactive. The most desirable hybrid approach is a layered paradigm that is dynamic.
