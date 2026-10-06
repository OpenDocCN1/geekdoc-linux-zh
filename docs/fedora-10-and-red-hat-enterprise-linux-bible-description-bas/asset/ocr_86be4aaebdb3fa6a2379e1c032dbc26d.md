# Securing Linux Servers

Opening your Fedora or RHEL system as a server on a public network creates a whole new set of challenges when it comes to security. Instead of just turning nearly all incoming requests, your computer will be expected to respond to requests for supported services (such as Web, FTP, or mail service) by supplying information or possibly running scripts that create in data.

Entire books have been filled with information on how to go about securing your servers.
Many businesses that rely on Internet servers assign full-time administrators to watch over the security of their servers. So, think of this section as an overview of some of the kinds of attacks to look out for and some tools to secure your Fedora or RHEL server.

# Understanding attack techniques

Attacks on computing systems take different forms, depending on the goal and resources of the attacker. Some attackers want to be disruptive, while others want to infiltrate your machines and utilize the resources for their nefarious purposes. Others are targeting your data for financial gain or blackmail. There are three major categories of attacks:

+   - Denial of service (DOS) — The easiest attacks to perpetrate are denial-of service attacks. The primary purpose of these attacks is to disrupt the activities of a remote site by overloading it with irrelevant data. DOS attacks can be as simple as sending thousands of page requests per second at a web site. These types of attacks are easy to operate and protect against. When you have a one where the attack is coming, from a simple phone call to the perpetrator's ISP will get the problem solved.

+   - Distributed denial of service (DDOS) — More advanced DOS attacks are called distributed denial-of service attacks. DDoS attacks are much harder to perpetrate and nearly impossible to stop. In this form of attack, an attacker takes control of hundreds or even thousands of weakly connected Internet computers. The attacker connects them in union to send a stream of irrelevant data to a single Internet host. The result is that the power of one attacker is magnified thousands of times. Instead of an attack coming from one direction, as is the case in a normal DOS, it comes from thousands of directions at once. The best defense against a DDoS attack is to contact your ISP to see if it can filter traffic at their border routers.

Many people use the excuse, "I have nothing on my machine anyone would want" to avoid having consider security. The problem with this argument is that attackers have a lot of reasons to use your machine. The attacker can turn your machine into an agent for later use in a DDoS attack. More than once, authorities have shown up at the door of a dumbfounded computer user asking questions about threats originating from their computer. By ignoring security, the owners have opened themselves up to a great deal of liability.