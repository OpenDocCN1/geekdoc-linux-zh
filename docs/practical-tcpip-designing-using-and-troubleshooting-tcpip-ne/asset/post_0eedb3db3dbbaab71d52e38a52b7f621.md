
## 24.8 Implementing a firewall

This module outlines how to implement a firewall on your network. Because firewalls vary so much, this is of necessity very general. First, some general points to note are:

-   If you're using a general-purpose PC with firewall software (as opposed to a purpose-built appliance) *don't* run anything else on it:
    -   Many security holes arise from software bugs. All software has bugs. The more software you are running, the more bugs there are, and potentially the more security holes you have.
    -   If you're running your firewall on a Windows PC, adding an operating system Service Pack to fix a problem, e.g. with a Web server, could break your firewall.
-   Firewalls are usually for TCP/IP protocols only. If you use IPX or NetBEUI, you may open up an unprotected backdoor from "outside" to "inside" because NetBEUI traffic bypassed the firewall code. Even NetBT (NetBIOS over TCP/IP) can be dangerous because it's a whole networking system in itself, making it easy to permit wider access than you intended. If you don't need Windows Networking on your firewall, disable and remove it.
-   Don't allow any modems on your firewall. If a modem connects to the Internet, it provides a backdoor that bypasses all your firewall's security.

### Implementation outline

1.  Read all the documentation before you start! (Nobody ever does, but it really helps to view the big picture before diving in.)
2.  Draw up a security policy – a document that says who needs to be able to do what, from where, and why (e.g. "internal e-mail server must be accessible from 192.0.2.64/224, our Edinburgh branch office, so they can pick up e-mail for their users"). Write down all your needs and decisions, and keep the document up to date as you change your security configs. This is a great help for new staff, and auditors love it too.
3.  Draw a map of your network, and keep this with your security policy. (See Appendix 9 for an example diagram.)
4.  If you're not using a ready-built appliance:
    -   Prepare your firewall PC by removing all unnecessary software. (Even better, start with a new PC or a re-formatted disk, and install only what you need. Then you *know* there's nothing else lying around from previous installations.)
    -   Install the firewall software.
5.  Configure the firewall's network settings: IP and netmask for internal and external interfaces, and DMZ if you have one. It is at this point that you enable and configure NAT if you're using it. You also have to configure the firewall's default gateway, which will almost certainly be the address of the internal interface of your Internet router.
6.  Configure the firewall's basic rules and logging:
    -   Enable detailed logging. (When the firewall is up and running OK you may want to decrease the verbosity of the logs.)
    -   Set the firewall to block everything, in and out.
7.  Insert the firewall into your network.
8.  Modify any settings on LAN machines that have to take account of the firewall. For example, if you've just enabled NAT, you'll have to renumber your LAN PCs. The default gateway for the LAN PCs depends on your configuration and firewall type, so you'll have to check your documentation. If you're using NAT, the default gateway is usually the firewall's internal interface address. (This without NAT, it could be either the firewall's internal interface, or the firewall's own default gateway. (See under “Proxy ARP” in the Notes for why there are two different possibilities.)
9.  Refine your firewall rules:
    -   On paper, translate your security policy into a set of firewall rules.
    -   Apply these rules to the firewall.

We've usually found it's best to apply rules in stages. First allow outgoing **ping** traffic, and check that that part works correctly. Then allow other outgoing traffic, and check it, before allowing traffic initiated from outside. (This implicitly assumes that you're using an SPI firewall.) Finally, if you have a DMZ, configure it and apply any necessary rules.

We use a checklist to remind us of what tests we need to do, and to record the results (Appendix 25).

You will probably need to check that certain TCP services (e.g. HTTP, SMTP) are accessible from outside, but it's unlikely you have the necessary servers on your test “inside” PC. You can either enable the **daytime** service and modify your rules accordingly for testing, or alternatively run `netcat` on the inside machine – acting as a “manual” server listening on the appropriate port, as we described in Modules 17.5 and 17.4.

10. When the firewall is behaving as you want it:
    -   Save its configuration settings to file, and store them on a safe machine on your LAN, *not on the firewall*. In the same location, save the firewall software (or firmware if it's an appliance). See Web Appendix 3X for the convention we use to make sure we have everything we need to restore our firewall configs.
    -   Continue with your network implementation as described in Chapter 23.

### Adding a firewall to an existing live network

If you're adding the firewall into an existing live network, it's often easiest if you build a small test network first, so you can familiarize yourself with the firewall without disrupting anyone else. Add one machine “outside” the firewall and one machine “inside,” to simulate the WAN and LAN respectively. The outside machine will be the firewall's default gateway and vice versa. Otherwise, configuration is almost exactly as described earlier.

When the firewall is working as you require, insert it into your live network, and continue as with step 8 above.

## 24.9 Troubleshooting with a firewall in place

As with the previous module, this module can give only a general approach rather than a detailed formula, because all firewalls are different.

Troubleshooting with a firewall is harder than normal networking because the firewall “interferes with” the traffic (which is its job after all). We say “troubleshooting with a firewall in place” rather than “troubleshooting your firewall” because often you don’t know whether it’s the firewall that’s the problem, or whether something else is misbehaving. (The whole of this book grew out of troubleshooting firewall installations. It’s ironic that this chapter is one of the shortest in the book, but we’ve often found that on a three-day project to install a firewall, only half a day is devoted to firewall setup/configuration/debug. The rest of the time is spent sorting out the customer’s network and routing and DNS and Windows Networking.) If you understand your network thoroughly, you’ll be able to diagnose whether a problem is really being caused by the firewall or whether it’s a normal networking issue.

The key idea to keep in mind is that traffic can go onto two ways through the firewall from outside (Figure 24.12): either the firewall passes it to the LAN, or the firewall drops it and shows the reason why. (We’ve assumed that we’re sorting out a problem with incoming traffic; this is where most problems arise since many sites permit all outgoing traffic.) Then work through the steps below:

![](img/a2132b646d336d5f9a21102d6320e537_671_0.png)

**Figure 24.12 Possible paths through the firewall from outside**

1.  Look at the firewall’s logs to see whether it tells you straight away why the traffic was blocked. If not ...
2.  a. Configure the firewall to give its most detailed logging, at least on the type of traffic or source/destination that you’re having the problem with.
    b. As well as logging, the firewall may have debugging options. But be careful – they can reduce performance significantly, e.g. enabling debug on one of our firewalls increases the time for a **ping** from about 5 milliseconds to 600 milliseconds. If you’re troubleshooting a live firewall you may have to choose a very slack time or work out of hours.
3.  a. Run **tcpdump** between the firewall and router (A1, Figure 24.13) and ...
    b. ... Run **tcpdump** inside the firewall also (A2, Figure 24.13). If you’re paranoid, use two separate sniffer PCs; otherwise, you can use a single PC with two NICs. The danger is that your **tcpdump** PC could get hacked, because A1 is outside the firewall.
