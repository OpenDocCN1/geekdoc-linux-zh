# Hunting for High Severity Vulnerabilities (HSV) • Chapter 3

operating most of these tools is not as easy as clicking on an icon. That being said, the freeware and open source tools have their place, and most of them do the job as advertised. I profile the following tools in this section:

+   - Nessus (www.nessus.org)
- Fire & Water Security Toolkit (www.ntobjectives.com)
- LanGuard Network Security Scanner (www.gfi.com)
- whisker (www.wiretrip.net/rfp)
- LHF Tool Suite (www.SpecialOpsSecurity.com)
- NBTEnum (http://ntlsleuth.0catch.com)
- Quick Kill (www.sensepost.com)
- SPIKE and SPIKE Proxy (www.immunitysec.com)
- CANVAS (www.immunitysec.com)

# Nessus

Nessus (www.nessus.org) is a free-source VA scanner that uses a Unix-based scan server and can use Unix or Windows clients. Nessus uses its discovery and service enumeration and executes vulnerability checks in its own scripting language called the Ness Attack Scripting Language (NASL). NASL is a C-like scripting language designed to allow users to quickly create vulnerability checks.

Nessus is the most popular and probably the most free tool. Nessus is a vulnerability scanner much like the commercial tools discussed in the preceding section. For a free scanning tool, it is just as good or in cases even better than most of the commercial products. Typically, using more than one scanning tool helps you obtain the most accurate and thorough results, and no matter what tool you use, your second scanner should be Nessus.

Nessus consists of both a client piece and a server. The server portion of Nessus runs on a Unix environment; client pieces are available for both the Unix and Win32 environments. Figure 3.5 depicts the client portion of Nessus performing a scan. It includes the following features:

+   - Smart service recognition Nessus will use its own detection system to find servers running on nonstandard ports.

![](bbox=[0.707, 0.94, 0.927, 0.966])