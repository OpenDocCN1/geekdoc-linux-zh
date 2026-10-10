
![](img/0c79e6db97822eb68322dfe40d8564fe_107_0.png)

## MP3 Players

MP3 players made by other hardware manufacturers such as Microsoft, HP, and Creative are gaining in popularity. There is very little risk inherent in the MP3 and MP4 formats, and the threat to MP3 players is that they can be hacked and used as data drives. Therefore, some of the same vulnerabilities that affect iPods affect other MP3 players.

## Flash Drives

Flash drives are also called Memory Sticks, thumb drives, or USB drives. They can be very small with a large capacity because of the nature of flash memory. Because they are portable external drives, they are susceptible to some of the same vulnerabilities and threats as iPods and MP3 players.

## Common Operating Systems in Handheld Devices

### Mobile Phone Operating Systems

Advanced mobile phones usually work on any of the following operating systems:

- Palm OS
- Windows Mobile OS
- Symbian OS
- Linux

### OS Structures in Mobile Phones

Three of the OS structures in mobile phones are shown in Figure 4-3.

### Palm (Garnet) OS

Palm OS has been used on handheld devices since 1996. It was first developed by U.S. Robotics for personal digital assistants (PDAs). Palm was the first to develop desktop syncing technologies, such as HotSync.

### Windows Mobile Operating System

Windows Mobile operating system, developed by Microsoft Corporation, is a noncomponent-based operating system used in mobile devices and smartphones. It acts like a standard platform for PDAs and cell phones to provide common user interfaces. Windows Mobile applications include mobile versions of Microsoft Office, Internet Explorer, Windows Media Player, and the Microsoft API.

![](img/0c79e6db97822eb68322dfe40d8564fe_108_0.png)

Figure 4-3 This shows three operating system structures in mobile phones.

### Symbian Operating System

The Symbian operating system is an open mobile operating system developed in 1998. This OS supports a wide range of devices that are categorized with different user interfaces. It supports CDMA, GSM, and GPRS. *CDMA* is a cellular technology originally known as IS-95. It is a competing network technology to GSM. *GSM (Global System for Mobile communications)* is an open, digital cellular technology used for transmitting mobile voice and data services. *GPRS* is a nonvoice service available with most GSM networks.

### Linux Operating System

This is an open source operating system that provides Internet access, VoIP, and Wi-Fi.

## Vulnerabilities in Handheld Devices

### Evolution of the Mobile Threat

Mobile malware is a fast-growing threat that is difficult to detect. Compared to other malware, mobile malware can spread more quickly. Most organizations and individuals now rely on mobile communication. A pandemic-level attack can harm millions of mobile users.

Smartphones' operating systems consist of many open APIs that are vulnerable to attack. Mobile devices have a number of connectivity methods by which the malware can be spread. Mobile malware has increased at an alarming rate in recent years.

Malware can spread over the following:

- Mobile networks
- The Internet
- SMS
- Bluetooth technology
- Wireless
- Symbian installation files (SIS)
- MMS
- USB devices
- Infrared

### Examples of Vulnerabilities in Mobile Phones

The following are examples of vulnerabilities in mobile phones:

- Research in Motion Ltd.'s BlackBerry 7270 SIP (a protocol used to create, modify, and terminate sessions such as VoIP or video over an IP network) stack has a format string vulnerability that disables the calling feature in the mobile device. A hacker can use certain header tokens to copy or write data in an IP stack or in working memory. This allows the hacker to overwrite valid data with malicious code.
- Samsung's SCH-i730 phone running SJPhone SIP Client has a buffer overflow vulnerability. By exploiting this, a hacker can disable the mobile phone and slow the operating system.
- HTC HyTn using AGEPhone is vulnerable to malformed SIP messages sent over wireless LAN connections; it disconnects active calls.
- Dell Axim running SJPhone SIP soft phones are vulnerable to denial-of-service attacks, which can disable the mobile phone and drain the battery.
- The SDP parsing module of D-Link DPH-540 and DPH-541 Wi-Fi phones has a vulnerability that disables the phone's calling feature.

### Hacking Handheld Devices

When a password-protected handheld device is stolen or is intentionally made inoperable, a hacker can retrieve data from the bricked device using a number of tools to unlock it and restore software. **A brick** is a device that cannot function in any capacity. With mobile devices, this refers to devices that are locked, damaged, or destroyed. The hacker can restore access to network connections and other devices trusted by the original user.

Hackers can also attack mobile phones using spyware and other mobile malware. They can download addresses and other personal information from a mobile device without the user's knowledge. Some hackers not only extract information but may change or delete information stored on the mobile device. Hackers can access personal voice mails from a mobile device if the password is disabled. They can also access address books, read messages and e-mails using various mobile spyware, and listen to conversations. On some devices, hackers can even gain access to bank accounts and transfer cash electronically. Hackers can insert viruses and spyware in mobile devices using Bluetooth or GPRS. A virus can remove all personal information such as contacts, messages, and e-mails.

This section will explore various malware and attacks hackers may use on mobile devices.

### Mobile Malware Propagation

Mobile malware spreads via the Internet. It first infects PCs; the infected PCs can then infect smartphones via infrared and Bluetooth. Infected smartphones can continue to infect other smartphones over the wireless LAN. The mobile malware can infect many mobiles through MMS, and then the infected device can spread the malware to another mobile device by using General Packet Radio Service (GPRS).

Malware allows hackers access to critical and often confidential information stored on the device as well as any connected networks or devices. Malware programs can steal information, address lists, logs of calls and messages, or other sensitive data. Malware can also be used to issue commands from the device so a hacker can have control of a smartphone or mobile phone to make calls or send text messages. Malware spreads more quickly across mobile networks than on desktop systems. It is difficult to detect because mobile viruses and Trojan variations are still too diverse to trace using classification-based virus detection techniques.

#### Spyware

Mobile spyware manipulates SMS messages and enables them to be read by others. **SMS** is a communication service standardized in the GSM mobile communication system that allows interchange of short text messages between mobile telephone devices. Mobile spyware is invisible to the user, loads on startup, and forwards SMS messages from the mobile device to the hacker. First, the attacker sends an SMS to the target mobile device. The victim then opens the message and unwittingly installs the spyware onto the device. The spyware takes the SMS messages and forwards them back to the hacker without alerting the user.

#### Botnets

Bots are software applications that run automated tasks over the Internet. A collection of bots present in a channel is a *botnet*. Botnets consist of a set of compromised systems that are monitored for a specific command infrastructure. These can compromise large numbers of machines without the intervention of machine owners. These botnets can pose denial-of-services attacks, or compromised machines can run and spread Trojans and worms.

### DDoS Floods

A botnet owner needs to send an instruction to the botnet present on the mobile device after infecting it. After receiving instruction to launch DDoS floods, the mobile owner's core infrastructure is filled with a high volume of seemingly legitimate requests. This results in a denial of service for the connected systems.

### Malware: SymbOS/Htool-SMSSender.A.intd

- Affects: Symbian OS

SymbOS/Htool-SMSSender.A.intd is a prototype spyware program that attempts to return copies of received SMS messages to the spyware author. The source code is distributed in an archive file named HackSMS.rar. The archive includes a SIS file named XaSMS.SIS. The spyware is installed under the name XaSMS.

SymbOS/Htool-SMSSender.A.intd provides an example for intercepting and forwarding SMS in the manner of SymbOS/Mobispy.A or SymbOS/ACallno.A. This entails copying the text of the last SMS message received, placing it into a new SMS, and then forwarding the message to the spyware author. The spyware copies the text of the last received SMS into a new message in the drafts folder. It never sends the drafted SMS messages. It also starts automatically on reboot.

The source code for SymbOS/Htool-SMSSender.A.intd does not include functions for sending SMS messages to the malware author. It does include unimplemented functions, unused arguments, and functions that are commented out. These unimplemented functions cause no harm to the affected system, but may someday prove useful to other potential authors of SMS spyware.

### Malware: SymbOS/MultiDropper.CG

- Affects: Symbian OS

SymbOS/MultiDropper.CG is a spyware application that targets the Symbian operating system for mobile phones. It comes bundled with different multidropper mobile phone Trojans. It tracks text messages from the target phone and copies the log files of incoming and outgoing mobile numbers.

### BlackBerry Attacks: Blackjacking

*Blackjacking* is a method of hijacking BlackBerry connections. Attackers make use of the BlackBerry environment to penetrate the security perimeter and directly attack the host network.

The BlackBerry Attack Toolkit contains the BBProxy, BBScan, and relevant MetaSploit patches to exploit the trust relationship between the existing BlackBerry devices and the server to hijack sessions and gain access to confidential data. BBProxy is a security assessment tool that allows an attacker to use BlackBerry devices as a proxy between the Internet and the internal network. The attacker either installs BBProxy on a user's BlackBerry or sends it in an e-mail attachment to the target device. When this tool is activated, it creates a covert channel between the attacker and the hosts of an unsecured enterprise network. This channel is encrypted between the BlackBerry server and mobile device, and it cannot be identified by security products.

### iPhone Attacks

- Affects: iPhones and iPods, including iPod Touch

Although Apple's iPhone operating system is closed, iPhone hacking is not difficult. In order to hack an i-Phone, all that an attacker needs is the iPhone Hacking Kit and an Intel-based Mac that is on the same network as the target iPhone.

Jailbreaking is a process that unlocks iPhone and iPod Touch devices to permit the installation of third-party applications. It can also add ringtones or change wallpaper on an iPhone. It opens up the file system of an iPhone so that it can be accessed from the computer. Many nonmalicious users use jailbreaking in order to hack into and customize their own phones. Malicious hackers, of course, can use the software to install malicious code or software to help access, conceal, or destroy information stored on the iPhone or iPod.

The tools used for jailbreaking include the following:

- iDemocracy
- iActivator
