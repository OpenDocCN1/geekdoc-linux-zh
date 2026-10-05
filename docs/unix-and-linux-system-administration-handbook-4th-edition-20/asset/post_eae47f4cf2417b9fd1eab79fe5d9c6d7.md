
# Exim-specific exercises

**E20.16** Take the ACL example for the SMTP RCPT command shown on page 815 and reverse its default behavior to deny, while leaving the same addresses through.

- **E20.17** Version 4.70 and later removed the DomainKeys code in favor of DKIM. Simplify the example DKIM setup on page 851 to support only a single domain and single signing key. Add some policy rules, such as logging unsigned mail from Gmail or Yahoo! or rejecting failed verifications from PayPal or your bank.

- **E20.18** Explain how you would configure an Exim server to accept mail for both your domain and a virtual domain. Allow the virtual domain to relay mail to an off-site mailbox.

- **E20.19** Look through the configuration snippets in the spec.txt document in the Exim distribution and experiment with some of them in your configuration. Turn on verbose logging for each thing you try and examine the logs to see if it has the desired behavior.

# Postfix-specific exercises

**E20.20** Try to set up a "null client”—that is, a mail system that only sends mail and cannot receive it. Make sure that port 25 is closed.

**E20.21** Configure Postfix to authenticate your site to your provider or companion server (even Gmail!); use the following parameters:

```
smtp_sender_dependent_authentication
sender_dependent_relayhost_maps
smtp_sasl_auth_enable
smtp_sasl_password_maps
```

**E20.22** Why do you think Postfix supports so many map types?

**E20.23** What would you use pcre maps for? useful mail systems? Do you need to use the postmap command to compile pcre maps?

**E20.24** Look up the meaning of the recipient_delimiter parameter in the documentation (postconf man page). What could it be used for?

- **E20.25** Explain how you would configure Postfix to accept email for both your domain and a virtual domain. Allow the virtual domain to relay mail to an off-site mailbox.

# 21 Network Management and Debugging

Network management is the art and science of keeping a network healthy. It generally includes the following tasks:

- Fault detection for networks, gateways, and critical servers
- Schemes for notifying an administrator of problems
- General network monitoring, to balance load and plan expansion
- Documentation and visualization of the network
- Administration of network devices from a central site

On a single network segment, it is generally not worthwhile to establish formal procedures for network management. Just test the network thoroughly after installation and check occasionally to ensure its load is not excessive. When it breaks, fix it.

As your network grows, management procedures should become more automated. On a network consisting of several different subnets joined with switches or routers, you may want to start automating management tasks with shell scripts and simple programs. If you have a WAN or a complex local network, consider installing a dedicated network management station.

Your organization reliability needs will dictate the sophistication of your network management system. A problem with the network can bring all work to a standstill. If your site cannot tolerate downtime, it may well be worth to obtain and install a high-end enterprise network management system.

Unfortunately, even the best network management system cannot prevent all failures. It is critical to have a well-documented network and a high-quality staff available to handle the inevitable collapses.

## 21.1 NETWORK TROUBLESHOOTING

Several good tools are available for debugging a network at the TCP/IP layer. Most give low-level information, so you must understand the main ideas of TCP/IP and routing in order to use the debugging tools.

On the other hand, network issues can also stem from problems with higher-level protocols such as DNS, NSF, and HTTP. You might want to read Chapter 14, TCP/IP Networking, and Chapter 15, Routing, before tackling this chapter.

In this section, we start with general troubleshooting strategy. We then cover several tools, including `ping`, `traceroute`, `netstat`, `tcpdump` and Wireshark. We don't discuss the `arp` command in this chapter, though, too, is sometimes a useful debugging tool—see page 468 for more information.

Before you attack your network, consider these principles:

- Make one change at a time. Test each change to make sure that it had the effect you intended. Back any changes that have an undesired effect.
- Document the situation as it was before you got involved, and document every change you make along the way.
- Problems may be transient, by capturing relevant information with tools like `sar` and `nmon`. This information may come in handy as you are unraveling the problem.
- Start at one end of a system or network and work through the system's critical components until you reach the problem. For example, you might start looking at the network configuration on a client, your way up to the physical connections, investigate the network hardware—and finally, check the server's physical connections and software configuration.
- Communicate regularly. Most network problems affect lots of different people: users, system administrators, telecom engineers, network administrators, ISPs, Clear, consistent communication prevents you from hindering another's efforts to solve the problem.
- Work as a team. Years of experience show that people make stupid mistakes if they have a peer helping out. If the problem has any visibility, management will also want to be involved. Take advantage of managers' interest to get technical people from other groups on board and to cut through red tape where necessary.
- Use the layers of the network to negotiate the problem. Start at the "top" or "bottom" and work your way through the protocol stack.

This last point deserves a bit more discussion. As described on page 450, the architecture of TCP/IP defines several layers of abstraction at which components of the network can connect. For example, HTTP depends on TCP, TCP depends on IP, IP depends on the Ethernet protocol, and the Ethernet protocol depends on the integrity of the network cable. Can dramatically reduce the amount of time spent debugging a problem if you first figure out which layer is misbehaving.

Ask yourself questions like as you work down the stack:

- Do you have physical connectivity and a link light?
- Is your interface configured properly?
- Do your ARP tables show other hosts?
- Is there a firewall on your local machine?
- Is there a firewall anywhere between you and the destination?
- If firewalls are involved, do they pass ICMP packets and responses?
- Can you ping the localhost address (127.0.0.1)?
- Can you ping other hosts by IP address?
- Is DNS working properly?
- Can you ping other hosts by hostname?
- Can you ping hosts on another network?
- Do high-level services such as web and SSH servers work?
- Did you really check the firewalls?

Once you've identified the problem lies and have a fix in mind, take a step back to consider the effect that your subsequent tests and fixes will have on other services and hosts.

## 21.2 PING: CHECK TO SEE IF A HOST IS ALIVE

The ping command is embarrassingly simple, but in many situations it is the only command you need for network debugging. It sends an ICMP ECHO REQUEST packet to a target host and waits to see if the host answers.

1. If a machine hangs at boot, boots slowly, or hangs on inbound connections, DNS should be a prime suspect. Solaris and Linux use a sophisticated approach to name resolution that is configurable in /etc/nss.conf. On these systems, the name caching daemon (ncd) is of particular interest. With the transition to IPv6, we find that many DNS queries provide DNS forwarding services that simply drop requests for IPv6 (AAAA) DNS records. This "optimization" causes long timeouts on all resolution requests. Use the getent command to check whether your resolver and name servers are working properly (e.g., getent google.com).
