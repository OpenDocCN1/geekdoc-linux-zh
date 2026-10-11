
# Part 3
Application Security

## Chapter 6
**Electronic Mail**

- Sendmail
- Secure Mail Relaying via SMTP Authentication
- SMTP over TLS
- Using STARTTLS
- Qmail
- Postfix
- The Post Office Protocol (POP) V.3
- APOP
- Installing the Qpopper Software
- Configuring the Qpopper Software
- Using the Qpopper Software
- IMAP
- Installing the IMAP Server Software
- Configuring the Secure IMAP Server
- Using the Secure IMAP Server
- PGP and GnuPG
- Installing GnuPG
- Configuring GnuPG
- Using GnuPG
- In Sum

## Chapter 7
**HTTP Services**

- The Apache HTTP Server
- Configuring Apache Security
- Hardening the Apache Server
- Application Logs
- mod\_ssl
- Installing mod\_ssl
- Configuring mod\_ssl
- Apache-SSL
- In Sum

## Chapter 8
**Samba Security**

- The Samba Server
- Installing Samba
- Samba Administration with SWAT
- Securing Samba
- Using Samba as a Windows NT Primary Domain Controller
- In Sum

# Part 4
Perimeter Security

## Chapter 9
**Network Layer Firewalls**

- Firewalls: An Overview
- Linux as a Firewall Platform
- Packet Filtering
- The Legacy: `ipfwadm` and `ipchains`
- Using `ipchains`
- `ipchains` Examples
- The Present: Netfilter
- Configuring Netfilter
- `iptables`
- Sample Firewall Scenarios
- Single-Homed Dial-up Server
- Dual-Homed Firewall: Public and Private Addresses
- Triple-Homed Firewall with a Demilitarized Zone
- Protecting against Well-Known Attacks
- Network Address Translation
- Configuring NAT Using `iptables`
- In Sum

## Chapter 10
**Transport Layer Firewalls**

- Proxy Servers
- The SOCKS Protocol
- SOCKS4 vs. SOCKS5
- Do You Need SOCKS?
- The NEC SOCKS5 Proxy Server
- Installing SOCKS5 with RPM
- Compiling the Latest SOCKS5 Release
- Configuring the SOCKS5 Server
- The SOCKS5 Password File
- Starting and Stopping the SOCKS5 Server
- The runsocks Script
- SOCKS5 Shared Library Configuration
- Configuring Windows SOCKS5 Clients
- The SOCKS5 IPv4-to-IPv6 Translator
- In Sum

## Chapter 11
**Application Layer Firewalls**

- FWTK: The TIS Firewall Toolkit
- Installing the FWTk Firewall Toolkit
- FWTK Architectures
- Configuring the FWTk Firewall Toolkit
- NetACL Rules
- Gateway Rules
- Using Strong Authentication with FWTk
- _authsrv_
- In Sum

# Part 5
Remote Access and Authentication

## Chapter 12
**Virtual Private Networking**

- A VPN Primer
- The IP Security Protocol (IPsec)
- IP Authentication Header
- IP Encapsulating Security Payload (ESP)
- FreeS/WAN
- Obtaining FreeS/WAN
- Installing FreeS/WAN
- Configuring FreeS/WAN
- Editing the ipsec.secrets File
- Editing the ipsec.conf File
- Testing the Configuration
- Point-to-Point Tunneling Protocol (PPTP)
- PopTop
    - Downloading PopTop
    - Configuring PopTop
    - Running PopTop
- Secure Shell (SSH)
    - How SSH Works
    - OpenSSH
- In Sum

## Chapter 13
**Strong User Authentication**

- Kerberos
    - Configuring the Kerberos Domain Controller (KDC)
    - Managing Kerberos Credentials
    - Using Kerberos-Enabled Applications
- S/Key and OPIE
    - Installing OPIE
    - Configuring OPIE
    - Using OPIE
- Pluggable Authentication Modules (PAMs)
    - Installing PAM
    - Configuring PAM
    - PAM Examples
- In Sum

# Appendices

- Appendix A
    - Other Sources of Information
    - Security Trade Associations
    - Linux Information Sites
    - Linux Vendor Sites
    - Security Advisories
    - Security Magazines
    - Security Mailing Lists
- Appendix B
    - **PAM Module Reference**
    - Overview
    - The *pam_access* Module
    - The *pam_cracklib* Module
    - The *pam_deny* Module
    - The *pam_group* Module
    - The *pam_limits* Module
    - The *pam_pwdb* Module
    - The *pam_rootok* Module
    - The *pam_securetty* Module
    - The *pam_unix* Module
- Index

# Introduction

With the advent of the Internet revolution came the ability of hundreds of geographically dispersed software developers to collaborate on projects that would have been inconceivable just years before. It was the fall of 1991, and while the Internet hadn’t yet become the household name that it is today, a global team of talented software junkies was hard at work crafting what would become the most successful public-domain software offering of all time: the Linux operating system. Ten short years after the first 0.x release, the “Volkswagen of operating systems” enjoys an increasingly strong foothold in the work-station marketplace and stands above all other server platforms as one of the most robust, and certainly the most cost-effective, operating systems.

Ironically, the same Internet explosion that helped usher in the development of the Linux operating system is also to blame for the climate of lawlessness that has forced network administrators to re-examine their network security postures. As corporations large and small look to the Internet as a necessary way to conduct business, network managers become instant security experts, and what once was the distant threat of malicious intrusion is now the order of the day.

While there is no such thing as a *secure* network server, the Linux operating system was designed with a strong focus on security, and its open-source nature allows administrators, developers, and end users to constantly audit it for vulnerabilities. It’s precisely this ability to look “under the hood” that makes Linux the platform of choice in environments where security is just as important as high availability and ironclad stability.

This book concentrates on what it takes to make your Linux servers as secure as possible, and how to ensure that your servers continue to be secure, even in the face of the ever-mutating array of malicious threats that plague the Internet today. It contains practical, step-by-step advice on how to harden a Linux installation, starting with a “stock” distribution using freely available software tools. The tips and techniques described in this book are equally relevant to installations of one or one thousand Linux servers. The advice that you’ll find here is the result of over ten years of experience that includes Linux systems, large-scale TCP/IP network administration, security consultation, and security product development for a leading Internet service provider.

## Who Should Buy This Book

This book goes well beyond a simple introduction to Linux security. Instead, it offers a comprehensive reference that is tailored for network administrators and experienced Linux users. While it does describe in detail all the security concepts that are introduced,
