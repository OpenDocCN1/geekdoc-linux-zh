
-   - Application control
-   - Mouse control
-   - System shutdown/restart
-   - Audio control
-   - Complete system information

During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
   \RunServices - nssx
```

Port: 1349, 31337-31338, 54320-54321

Service: Back Orifice

Hacker's Strategy: This is the infamous and extremely dangerous Back Orifice daemon whose worldwide distribution inspired the development of many Windows Trojans. What's unique with this software is its communication process with encrypted UDP packets as an alternative to TCP—this makes it much more difficult to detect. What's more, the daemon also supports plug-ins to include many more features. During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
   \RunServices - bo
```

Port: 31785-31792

Service: Hack'a'Tack

Hacker's Strategy: This is yet another disreputable remote control daemon with wide distribution. As illustrated in Figure 4.40, Hack'a'Tack contains all the typical features. During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
   \RunServices - Explorer32
```

Port: 33911

Service: Spirit

Hacker's Strategy: This well-known remote backdoor daemon includes a very unique destructive feature, monitor burn. It constantly resets the screen's resolution and rumors indicate an update that changes the refresh rates as well. During configuration, the following registry entry is utilized:

![](img/ba85bb40c695c02adae8cbd6666f2e0c_131_0.png)

**Figure 4.40** Hack'a'Tack features.

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
\RunServices - SystemTray = "c:\windows\window.exe"

**Port:** 40412

**Service:** The Spy

**Hacker's Strategy:** This daemon was designed as a limited key logger. The Spy only captures keystrokes in real time and as such, does not save logged keys while offline. During configuration, the following registry entry is utilized:

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
\RunServices - systay

**Port:** 47262

**Service:** Delta Source

**Hacker's Strategy:** This daemon was designed in Visual Basic and was inspired by *Back Orifice*. As a result, Delta Source retains the same features as BO. During configuration, the following registry entry is utilized:

HK EY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices - Ds admin tool

**Port: 65000**

**Service: Devil**

**Hacker's Strategy:** Devil is an older French Visual Basic remote control daemon that does not remain active after a target station restart. The limited feature base, as shown in Figure 4.41, consists of messaging, system reboot, CD-ROM control, and an application killer.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_132_0.png)

**Figure 4.41** The limited features of the Devil Trojan.

Armed and familiar with the liabilities pertaining to common and concealed system ports and services, let's move right into unraveling the secrets of security and hacking. The knowledge gained from the next chapter and those to follow will become pertinent in building a solid security hacking foundation, to aid in developing a supervative security intuition. Before we begin, it is important to express the serious legal issues regarding techniques in this book. *Without written consent from the target company, most of these procedures are illegal in the United States and many other countries also. Neither the author nor the publisher will be held accountable for the use or misuse of the information contained in this book.*

# What's Next

The intention of this chapter was to establish a fundamental understanding of input/output computer ports and their associated services. It is important to identify with the potential vulnerabilities of these ports as we venture forth into the next chapter. At that juncture, we will learn how to scan computers for any vulnerable ports and ascertain pre-hack attack information of a target network.

# CHAPTER 5

# Discovery and Scanning Techniques

Today, a gateway is open to technological information and corporate espionage, causing growing apprehension among enterprises worldwide. Hackers target network information using techniques referred to collectively as *discovery*. That is the subject of the first part of this chapter. Discovery techniques are closely related to scanning techniques, which is the topic of the second part of this chapter. Scanning for exploitable security holes has been used for many years. The idea is to probe as many ports as possible, and keep track of those receptive and at risk to a particular hack attack. A scanner program reports these receptive listeners, analyzes weaknesses, then cross-references those frailties with a database of known hack methods for further explication. The scanning section of this chapter begins by defining scanning, then examines the scanning process, and lists several scanners available for security analysis. Finally, the section illustrates scanning functionality using a real-world scenario.

# Discovery

Online users, private and corporate alike, may desire anonymity as they surf the Web and connect to wide area networks but having an anonymous existence online, though not impossible, is technologically difficult to achieve. However, you can visit www.anonymizer.com for free anonymous Web browsing (shown in Figure 5.1).

![](img/ba85bb40c695c02adae8cbd6666f2e0c_134_0.png)

Figure 5.1 Anonymous Web browsing.

This section delves into the query processes used to discover and survey a target network, in preparation for the section on vulnerability scanning and penetration attacking, using real world illustrations.

Discovery is the first step in planning an attack on a local or remote network. A premeditated, serious hack attempt will require some knowledge of the target network. A remote attack is defined as an attack using a communication protocol over a communication medium, from outside the target network. The following techniques will demonstrate the discovery preparation for a remote attack over the Internet.

The techniques described in this section can be performed in any order, usually depending on current knowledge of the target network. The examples that follow are based on a target company—euphemistically called XYZ, Inc. (the company’s actual name, domain, and addresses have been changed for its protection).

# Whois Domain Search Query

Finding a specific network on the Internet can be like finding the proverbial needle in a haystack; it’s possible, but difficult. Whois is an Internet service that enables a user to find information, such as a universal resource locator (URL), for a given company or user who has an account at that domain.

Conducting a Whois domain search query entails locating the target company’s network domain name on the Internet. The domain name is the address of a device connected to the Internet or any other TCP/IP network, in a system that uses words to identify servers, organizations, and types of organizations, such as www.companyname.com. The primary domain providing a Whois search is the Internet Network Information Center (InterNIC). InterNIC is responsible for registering domain names and IP addresses, as well as for distributing information about the Internet. InterNIC, located in Herndon, Virginia, was formed in 1993 as a consortium comprising the U.S. National Science Foundation, AT&T, General Atomics, and Network Solutions Inc.

The following list contains specific URLs for domains that provide the Whois service:

-   **www.networksolutions.com/cgi-bin/whois/whois**. InterNIC domain-related information for North America
-   **www.ripe.net**. European-related information
-   **www.apnic.net**. Asia-Pacific-related information

Figures 5.2 and 5.3 represent a Whois service example, from Network Solutions (InterNIC), for our target company XYZ, Inc. As you can see, Whois discovered some valuable information for target company XYZ, Inc., namely, the company’s URL: www.xyzinc.com.

Now that the target company has been located and verified as a valid Internet domain, the next step is to click on the domain link within the Whois search result (see Figure 5.4). Subsequently, address verification will substantiate the correct target company URL. The detailed Whois search indicates the following pertinent information:

-   XYZ, Inc. domain URL www.xyzinc.com
-   **Administrative contact**. Bill Thompson (obviously an employee of XYZ, Inc.)
-   **Technical contact**. Hostmaster (apparently XYZ’s Internet service provider [ISP])
-   **Domain servers**. 207.237.2.2 and 207.237.2.3 (discussed later in the book)
