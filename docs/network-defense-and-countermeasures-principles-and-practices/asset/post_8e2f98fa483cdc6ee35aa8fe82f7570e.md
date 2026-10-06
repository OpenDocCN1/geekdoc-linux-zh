
## CHAPTER 2 Types of Attacks

The danger from IP spoofing is that some firewalls do not examine packets that appear to come from an internal IP address. Routing packets through filtering routers is possible if they are not configured to filter incoming packets whose source address is in the local domain.

Examples of router configurations that are potentially vulnerable

- Routers to external networks that support multiple internal interfaces
- Proxy firewalls where the proxy applications use the source IP address for authentication
- Routers with two interfaces that support subnetting on the internal network
- Routers that do not filter packets whose source address is in the local domain

The best method of preventing IP spoofing is to install a filtering router. Filtering routers filter incoming packets by not allowing a packet through if it has a source from your internal network, you should filter outgoing packets that have a source address different from your internal network to prevent a source IP spoofing attack originating from your site. Many commercial firewall vendors, such as Cisco, FortGate, D-Link, and Juniper, use this option.

If your router does not support filtering on the inbound side of the interface and you feel the need to immediately filter the spoofed IP packets by using a second router between your external interface and your outside connection. Configure this router to block, the outgoing interface connected to your original router, all packets that have a source address in your internal network. For this purpose, you can use a filtering router or a Unix system with two interfaces that supports packet filtering.

## Defending Against Session Hijacking

Another form of attack is session hacking or hijacking. TCP session hijacking is a process whereby a hacker takes over a TCP session between two machines. Because authentication is frequently done only at the start of a TCP session, this allows the hacker to break into the communication stream and take control of the session. For example, a person might log on to a machine remotely. After she has established a connection with the host, the hacker might use session hacking to take over that session and thereby gain access to the target machine.

One popular method for session hacking is using source-routed IP packets. This allows a hacker at point A on the network to participate in a conversation between B and C by encouraging the IP packets to pass through the hacker's machine.

The most common sort of session hacking is the “man-in-the-middle attack.” In this scenario hacker uses some sort of packet-sniffing program to simply listen in on the transmissions between two computers, taking whatever information he or wants but not actually disrupting the conversation.

A common component of such an attack is to execute a DoS attack against one end point to stop it from responding. Because that end point is no longer responding, the hacker can now intercept his own machine to stand in that end point.

The point of hijacking a connection is to exploit trust and gain access to a system to which one would not otherwise have access.

The only way to truly defend against session hacking is to use encrypted transmissions. Chapter 6, "Encryption Fundamentals," discusses various encryption methods. If the packets are not encrypted, then the communication is vulnerable to session hacking. Many network administrators use encrypted transmissions when communicating outside their network, but fewer encrypt internal communications. For a truly high level of security, consider encrypting all transmissions.

Packet sniffers are discussed in more detail in Chapter 15, "Techniques Used by Attack." Right now what you need to be aware of that a packet sniffer is software that intercepts packets across a network or the Internet and copies them. This gives the attacker a copy of every packet you send. These tools have legitimate uses in network traffic monitoring, but are also used by hackers to intercept communications and, in some cases, for session hacking.

## Blocking Virus and Trojan Horse Attacks

The preceding sections of this chapter examined the denial of service attack, buffer overflow attack, and session hacking. However, virus attacks are the most prevalent threats to any network. Therefore, protecting against virus attacks is essential for any security-conscious network administrator.

## Viruses

By definition, a computer virus is a program that self-replicates. Generally, a virus also has some other unpleasant function, but the self-replication and rapid spread are its hallmarks. This growth, in and of itself, can be a problem for an infected network. Worms are viruses that can replicate without human interaction.

Consider the infamous Slammer virus and the effects of its impact, high-volume scanning. Any rapidly spreading virus can reduce the functionality and responsiveness of a network. It can lead to too much traffic and prevent the network from functioning properly. By simply exceeding the traffic load a network was designed to carry, the network can be rendered temporarily nonfunctional.

## How Does a Virus Spread?

You have seen how viruses can impact infected systems and have looked at a few actual cases. Clearly the key to stopping a computer virus is to prevent it from spreading to others. To do this you must have a good understanding of how viruses typically spreads. A virus usually spreads in one of two ways.

The first is scanning a computer for connections and then copying it to other machines on the network to which machine has access. This is the most efficient way for a virus to spread and is a typical spread of worms. However, this method requires more programming skill than other methods. The second and more popular method is reading the e-mail address book and sending itself to everyone in it. Programming this type of virus is a trivial task, which explains why it is so prevalent.

The latter method is, by far, the most usual method for virus propagation, and Microsoft Outlook might be the one e-mail program most often hit with such virus attacks. The reason is not so much a security flaw in Outlook as it is the ease of working with Outlook. All Microsoft Office products are made so that a legitimate programmer can access many of the application's internal objects and easily create integrate applications within the Microsoft Office suite. For example, a programmer could write an application that would access a Word document, import an Excel spreadsheet, and then use Outlook to automatically e-mail the resulting document to interested parties. Microsoft has done a good job of making this process very easy. Accomplishing these tasks takes a minimal amount of programming. In case of Outlook, referencing Outlook and sending out a e mail takes less than five lines of code to do. This means a program can literally change Outlook itself to send e mails, unknown to the rest. Numerous code examples on the Internet show exactly how to do this, for free to the charge.

However a virus arrives, it is on a system it attempts to spread. In many cases the virus attempts to cause harm to the system. If a virus is on a system it can do anything a legitimate program can do. That means it could potentially delete files, change system settings, or cause other harm. The threat from virus attacks cannot be overstated. Let's take a moment to look at a few virus outbreaks, see how they operated, and the damage they caused. Some of these are older, some recent.

## The Sobig Virus

The Sobig virus is an older virus but it is a good example of how viruses spread. One interesting thing about this virus was the multi-modal approach by which it spread. In other words, it used more than one mechanism to spread and infect new machines. Sobig copied itself to any shared drives on the network and e-mailed itself out to the address book. Because of this approach, Sobig can be classified as a worm rather than simply a virus. This multi-modal ability to spread meant that the Sobig was particularly virulent—a term signifying that the virus spread rapidly and infected new targets.

Like most other distributed attacks, this one had telltale signs in the e-mail subject or title that could be used to identify the e-mail as infected by a virus. The e-mail would have a title such as “here is the sample” or “the document” and encourage you to open the attached file. The virus then