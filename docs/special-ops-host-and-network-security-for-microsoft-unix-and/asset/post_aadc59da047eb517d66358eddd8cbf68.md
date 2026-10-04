
# Attacking and Defending Windows XP Professional • Chapter 4

- IP Security (IPSec) IPSec is an Internet Protocol (IP)–layer encryption schema to encrypt data between systems. IPSec is an industry standard in tunnel encryption for internal and external connections. In terms of security impact, IPSec should be utilized for consistent system-to-system traffic, in the case of local network virtual networks (VPNs). This feature is not XP-specific.

- Kerberos Windows XP is bundled with the Kerberos authentication protocol as a standard for authenticating across numerous types of platforms and throughout the network. The standard encrypts all payload data during the authentication process. Kerberos can be utilized for multiple platforms and can be utilized for a single sign-on for Windows 2000 and .NET Server resources. In terms of security impact, all systems should utilize the latest version of Kerberos and an inherent trust between the Kerberos clients and servers. This feature is not XP-specific.

- Smart cards Embedded smart-card functionality is by default within Windows XP. It allows you to use a terminal services client to log into smart-card servers or terminal servers with additional third-party smart-card applications. Implementing a smart-card infrastructure provides an excellent method for ensuring that password and authentication schemes are secured. In terms of security impact, smart-card servers should be secured from a local, network, and physical perspective since it is a highly trusted system. This feature is not XP-specific.

- Remote Desktop The Remote Desktop application allows users to access their machines remotely. It is similar to other remote administrations in which only one session can be executing at a time; you cannot be logged on and working locally while another individual is working on a remote session. Remote Desktop currently utilizes Microsoft’s RDP 5.5 communication protocol. It allows users to work on their systems remotely and is excellent for developers who want to connect via a less-popular laptop and run enterprise-level applications. It is possible for a malicious user to connect to your computer and take control of it via successful authentication credentials. If this were to happen, the malicious user would have access of the authentication credentials provided. This feature is not XP-specific.

- Credential Manager Credential Manager serves as a secure location for authentication credentials, usernames, and passwords, so that they may be automatically reused in the future for repeatable logons or access to secured network-based resources. It saves time and repetitive energy from end users who must consistently re-enter usernames and passwords for resource access. Currently, there are no published vulnerabilities that exploit the credential manager allowing malicious users or processes the ability to retrieve credentials. This feature is XP-specific.

- Internet Connection Firewall (ICF) The ICF feature is a good utility considering that it is freely bundled with the OS for Windows XP. It protects against Transmission Control Protocol (TCP)-based attacks and requires only one click to implement. It is a good tool that adequately protects unsolicited network-based attacks. It is easy to use, and is free! In terms of security impact, ICF provides adequate protection for unsolicited attacks, network probes, and port scans. However, it should not be confused with BlackICE or Tiny because it does not have a detail-oriented intrusion detection technology nor not protect against session hijacking, some protocol or bandwidth attacks, and all application-layer attacks. This feature is XP-specific.

- Set of Policy (RSoP) The RSoP administration tool allows administrators to verify the effects of a Group Policy configuration on a system before it is implemented on such system. The feature provides an excellent interface for troubleshooting. Administrators can view potentially unexpected or undesired policy effects before being pushed to production status. There is no security impact from this feature. It is not XP-specific.

## Attacking XP Professional

Attacking Windows XP Professional is similar to attacking other operating systems—and yes, some of the same attacks work. However, a few arise when you are attacking a system that has implemented some of the key security features within the XP Professional environment. In the following section, you will learn to identify the OS in an organizational environment in addition to learning to identify a system with the XP Internet Connection Firewall implemented. You will also learn the details for the most critical attacks that currently exist specifically for the XP Professional platform.

## Attacking and Defending Windows XP Professional - Chapter 4

Of course, numerous tools and techniques are available to profile and exploit Windows-based operating systems and applications. Throughout this portion of the chapter I have utilized a subset of these security tools in combination with public and author-developed exploits. The tools and techniques we have chosen to present represent a good method for testing and exploiting the given targets.

## Profiling Windows XP Professional

The attacker modus operandi differs from person to person; however, most attackers will agree that they need a substantial amount of information about a target before attempting any attacks. In the initial chapters of the book, you learned a good methodology for profiling or footprinting a target system. It is not uncommon for attackers to profile a target system and its applications for a significant amount of time (this could be 80–90 percent of the overall assessment time). Our profile of Windows XP will encompass all of the techniques tactics utilized during an above-average vulnerability assessment. It will not encompass utilizing packet replay attacks or additional machines for packet capturing or man-in-the-middle attacks. It is important to note that the profile was created and the tools were executed in a non-evisive manner. Some of the results may be different if you want to bypass intrusion detection systems or filtering systems.

## The Windows XP Professional Target

The XP Professional profile that we'll develop in this chapter is meant to accurately detail what services, protocols, and responses can be ascertained from footprinting a default installation of XP without any installed patches or hotfixes. We'll use the profile as an identifier for potential target injection points and methods for determining which attacks and nudge strings return what types of information without actually executing the attacks.

Profiling the XP Professional target in this case will consist of determining what ports are open on the system and corresponding services, identifying system users and shares, gathering implemented protocols, and analyzing protocol responses. Analysis of this information will enable you to potentially glean exploitable holes and security injection points within XP Professional.

## Port Scanning

An excellent method in determining active services and open ports on a system is to run a complete port scan of the target system. When conducting a profile of a system when you are not concerned with evading intrusion detection systems, whether it is local or remote systems, it is always recommended to go with a full TCP Connect scan. The following scan output displays how NMAP 3.0 would show if you run it for a full port scan SYN or TCP Connect methods:

```
Starting nmap V. 3.00 ( www.issource.org/nmap )
Interesting ports on 10.0.100.100:
(The 65535 ports scanned but not shown below are in state: closed)
Port        State       Service
135/tcp      open        loc-srv
139/tcp      open        netbios-ssn
445/tcp      open        microsoft-ds
1025/tcp     open        NFS-or-IIS
5000/tcp    open        UPnP
Remote operating system guess: Windows Millennium Edition (Me),
Win 2000, or WinXP

map run completed -- 1 IP address (1 host) scanned in 37 seconds
```

The following is a full-blown UDP scan of the XP Professional target system:

```
Starting nmap V. 3.00 ( www.issource.org/nmap )
Interesting ports on 10.0.100.100:
(The 65523 ports scanned but not shown below are in state: closed)
Port        State       Service
123/udp      open        ntp
135/udp      open        epmap
137/udp      open        netbios-ns
138/udp      open        netbios-dgm
445/udp      open        microsoft-ds
500/udp      open        isakmp
1026/udp     open        unknown
1029/udp     open        unknown
1033/udp     open        unknown
1900/udp     open        unknown
```
