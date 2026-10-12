
## Summary

- For security in depth, you need to augment your firewall with other security systems.
- Intrusion detection systems detect penetration attempts by recognizing a “signature” or pattern of events on the host or network.
- Penetration testing lets you scan your network for vulnerabilities accessible from the Internet.
- Special proxy servers can provide extra security, control, and logging over services such as e-mail, Web, and FTP. They can:
  - Scan content for viruses and remove them or discard the message.
  - Scan downloaded or e-mailed content for confidential or offensive material.
  - Check a requested URL against a database that classifies Web pages for certain criteria and block undesirable pages. Because the check is on the URL string itself, the page doesn’t have to be downloaded before it is blocked.
- E-mail servers can use lists of known spammers and open relays to block junk e-mail.

## What's next?

In the next chapter, we look at dial-up networking for connecting to the Internet just for surfing, or for accessing your office LAN from outside. In the chapter after that, we return to security and see how VPN can help you secure your dial-up links, and links to branch offices.

## Notes and further reading

Security is now such a big issue that every IETF RFC issued has to include a “Security Considerations” section.

A security-related benefit of **syslog** (Module 17.12) is that it lets you store logs of sensitive machines on a different machine. That way, even if the machine is compromised, the hacker can’t modify or delete the logs, so you still have the information to trace the intruder and, if necessary, to use it as legal evidence. You can even send logs to more than one logging machine for extra security.

### Intrusion detection systems

- [http://www.snort.org/](http://www.snort.org/)
  *Snort – The Open Source Network Intrusion Detection System*
- [http://www.snort.org/docs/lisapaper.txt](http://www.snort.org/docs/lisapaper.txt)
  *A very readable overview of Snort, what it does, and how it works*
- [http://www.snort.org/docs/idspaper/](http://www.snort.org/docs/idspaper/)
  *Insertion, Evasion, and Denial of Service: Eluding Network Intrusion Detection*, some of the problems faced by IDSs

### Penetration testing and vulnerability scanning

There are many commercial scanning systems, but here are some free ones. (Note that this type of tool may be developed by security folks or by hackers.)

- [http://www.porcupine.org/satan/](http://www.porcupine.org/satan/)
  SATAN (Security Administrator Tool for Analyzing Networks) – one of the oldest and best-known security scanners
- [http://www.hoobie.net/brutus/](http://www.hoobie.net/brutus/)
  Brutus A remote online password cracker
- [http://www.nessus.org/](http://www.nessus.org/)
  Nessus – a free, powerful, up-to-date, and easy-to-use remote security scanner
- [http://www.insecure.org/nmap/](http://www.insecure.org/nmap/)
  Nmap – Free Stealth Port Scanner For Network Exploration & Security Audits network mapper. The main part of this site has lots of other security information of interest
- [http://www.cert.org/incident_notes/IN-99-01.html](http://www.cert.org/incident_notes/IN-99-01.html)
  CERT® Incident Note IN-99-01 – “scan” Scanning Tool, which can be configured to automatically exploit vulnerabilities that it detects
- [http://packetstormsecurity.nl/Crackers/NT/10/phcrack/](http://packetstormsecurity.nl/Crackers/NT/10/phcrack/)
  L0phcrack is a password cracker for Windows. (Recent versions are full commercial products with significant license fees.)

### Poor man's URL blocking

Let’s say you want to block the Web site ads.example.com because it is a banner-ad site and you don’t want to waste time and bandwidth downloading silly ads. Add the line:

```
127.0.0.1 ads.example.com
```

to your **hosts** file (in spite of what we said about **hosts** in Chapter 19). When your Web browser retrieves a Web page containing a link to ads.example.com, it will try to retrieve the ad image from 127.0.0.1, which is your own machine, which of course doesn’t have the ad, so it will display it as a big red X or an “Action canceled” legend or similar. Ugly but fast. You can insert as many of these lines as you like in your **hosts** file.

### E-mail filters

- [http://www.mailabuse.org](http://www.mailabuse.org)
  Follow the links for RBL – Realtime Blackhole List, DUL – Dialup Users List, and RSS – Relay Spam Stopper

### TCP wrappers

The “TCP wrappers” security tool is available for Linux and often comes as part of a standard distribution. This lets you log who uses what service on this machine. This is ideal if the service itself doesn’t use **syslog** or keep a log file. You can also protect services by restricting who (i.e., which IP addresses) may access them. For example, you could have a rule specifying “only allow sub-net 10.5.5.5/25 to access the FTP server on this machine.” You enter a list of “permit” rules in `/etc/hosts.allow` and “prohibit” rules in `/etc/hosts.deny`.

TCP wrappers is implemented as the **tcpd** daemon, which usually works in conjunction with the **inetd** super-server (Appendix 20).

> **Warning:** if TCP wrappers is installed and wrongly configured, it will block access to services that you think ought to be available to you.

To download the software and for more information:

- `ftp://ftp.porcupine.org/pub/security/`
- `ftp://ftp.porcupine.org/pub/security/tcp_wrapper.ps.Z` or `ftp://ftp.porcupine.org/pub/security/tcp_wrapper.txt.Z`
- See the `tcpd(8)`, `hosts_access(5)` manpages in your Linux distribution, which may well include TCP wrappers.

### Appendices

Appendix 20: controlling network services

![](img/a2132b646d336d5f9a21102d6320e537_690_0.png)

## Dial-up networking and PPP

- 26.1 Dial-up networking – overview
- 26.2 Overview of Windows dial-up networking
- 26.3 Connect a modem to your Windows-NT PC
- 26.4 Install dial-up software on your PC
- 26.5 Configure PC with details of your ISP account
- 26.6 Configure PC with ISP TCP/IP addressing details
- 26.7 Dialing up
- 26.8 Monitoring the connection status
- 26.9 Troubleshooting
- 26.10 Configure the PC's dial-up default gateway and other routing
- 26.11 Dial-up PC connecting to HQ's network
- 26.12 Miscellaneous
- Summary

### Introduction

In this chapter, we cover dial-up networking, connecting a single machine (as opposed to a whole LAN) to the Internet. Usually the purpose of the connection is to give Internet facilities to a person who's traveling or working from home, or to integrate a remote PC into the infrastructure on the HQ's LAN, and give the user access to resources on the LAN, such as printers, file servers, the corporate e-mail system, etc. We explain how to configure a PC to dial up to the Internet via an ISP, how to configure the necessary settings on your dial-up PC, and the significant differences between dial-up and normal (Ethernet, LAN) connections.

### 26.1 Dial-up networking – overview

Up to now we’ve dealt with permanent, always-on connections. Most of these have been LAN-Ethernet connections, but others were permanent leased lines, ADSL links, etc. to the Internet. (We also mentioned ISDN links for connecting a site to the Internet, but as these are usually set up to dial on demand, they look much the same as an always-on connection to a user on the LAN.) In this chapter, we look at connections via dial-up links, usually to the Internet, and primarily for single machines rather than networks of several machines.

Typical scenarios where you need dial-up connections are:

1. Occasional access to the Internet with a single PC from home or a hotel room or other remote location, using a dial-up ISP (Figure 26.1). For added security, this configuration is often used with virtual private networking (VPN; Chapter 27). You may also want to connect to your office network via the dial-up link.
2. Dial-in from home or hotel room directly to your own office, not using an ISP at all (Figure 26.2). In this configuration, if you access the Internet, it is via your own LAN and then out again via your organization’s Internet router.

![](img/a2132b646d336d5f9a21102d6320e537_691_0.png)

**Figure 26.1 Using a dial-up ISP to access the public Internet**

We won’t cover the second scenario in much detail because:

a. The first one is much more common.
b. Scenario 1 combined with VPN can give you the same connectivity and more than scenario 2 with a lot less hassle. Table 26.1 compares the two approaches. In our experience, using an ISP is *much* easier, if only because managing dial-up connections and modems is always troublesome.

Later on, in Module 26.12, we outline some other scenarios that are useful although relatively rarely needed.

A dial-in connection from a single PC using an ISDN line and an ISDN modem (as opposed to an ISDN router) is almost identical to dial-up using a normal, voice (analog) phone line: the ISDN modem or terminal adapter behaves just like a modem as far as the PC is concerned (and even implements the usual modem “AT commands” to control the dial-up session). Accordingly, we’ll say no more about ISDN, and in the rest of this chapter we will concentrate on scenario 1 above, and how it differs from the always-on connections we’ve used so far.
