
# Attacking and Defending Unix • Chapter 14

attacker would want information about services, network configuration, and network defends before attempting to attack a host. However, the intelligence used by an Operator would typically have been gathered, analyzed, and compiled into a report by a third party, whereas an attacker making a direct attack against a host would likely have to gather their own intelligence, using any available means to be as inconspicuous as possible.

Information gathering tools are freely and readily available. The most common is portscanning utility—in this area there are nmap, then there are all others. Nmap, is a port scanner utility that is versatile in functions and freely available. Figure 14.1 shows nmap SYN scan and fingerprinting a Linux system. Nmap supports many types of scanning, including stealth scans using half-open connections, and makes full use of idiosyncrasies in the TCP/IP protocol to gather information on the target host. It is the best for determining services on the target host.

### ### Figure 14.1 Nmap Scan Against an Example System

![](img/729efc56f204a2ebffb8295c3a2dfdfb_755_0.png)

Once information has been gathered about the services on a target host, the attacker may attempt to further identify the specific vendor that authored the service, as well as the version number. This often requires communicating with the service directly. This type of information gathering can be carried out by a utility designed for the particular protocol. This is illustrated in Figure 14.2, where a ncinfo command is executed against a Linux host. From this, we gain valuable information about potentially vulnerable services running on the host.

Sometimes, you will not have a tail to do that work for you. In this case, Telnet will often suffice, although netcat is the best and most common choice. Using interactive utilities requires knowledge of the protocol spoken by the host. This information can be gathered from many places, although the best resource is the Request for Comments (RFC) repository. In Figure 14.3, you can see an example of information gathering using knowledge of the Hypertext Transfer Protocol (HTTP), of which the 1.1 version is specified in RFC 2616.

# Chapter 14 • Attacking and Defending Unix

## 14.2 Execution of an rpcinfo Command Against an Example Unix Host

![](img/729efc56f204a2ebffb8295c3a2dfdfb_756_0.png)

## 14.3 Using netcat to Identify Web Server Services

![](img/729efc56f204a2ebffb8295c3a2dfdfb_756_1.png)

Information gathering attacks are free, and may occur with the probe of only one particular service for a vulnerability. This is the case with worms such as the modap worm, which was designed to compromise Linux systems with a vulnerable version of the Apache Web Server (you can see the alert for the modap worm at http://analyzer.securityfocus.com/alerts/020913-Alert-Apache-mod_ssl-Exploit.pdf). This also occurs with mass-root utilities designed to attack large numbers of systems. It is not unusual for these utilities to be launched at all by these services, just an exploit attempt made inside.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_756_2.png)

# Attacking and Defending Unix • Chapter 14

For our own attack we do not need to be quiet, the same methods apply. Scanning the target system, identifying and gathering information about services, and creating a plan of attack are all necessary for our attack. And if the whim strikes us, we can be quiet to see how easily network defenses can be evaded.

When an attacker making a directed attack at a host has finally gathered enough information to proceed, a plan for attack will have been formulated. This involves finding a service that is known to be vulnerable to an issue, or attempting to find a vulnerability in a service on the target. Once the plan has been made, the attack begins.

# Gaining Remote Access

Gaining remote access is the objective of most attacks against a Unix system. Remote access to a host allows an attacker to access the resources of the compromised host, and turn in the system being used as a platform for the launch of other attacks. Remote access attempts are launched through exploitation of services executing on a Unix host.

In the case of a service executing with minimal privileges, remote access can result in unprivileged access. In the case of a service executing with elevated privileges, gaining remote access through the service results in a catastrophic compromise of administrative privileges. In the case of unprivileged remote access, it is merely a matter of time before the attacker finds a way to gain elevated privileges.

Remote access is often gained through one of a few methods. One such method is the exploitation of a programming error such as a buffer overrun or format string vulnerability. Another is the use of an input validation bug, such as that of a PHP vulnerability. A brute force attack may also be used. The following sections examine each type of attack in detail.

# Exploiting Programming Errors

Programming errors are one of the more commonly exploited types of vulnerabilities in software. Programming errors are broad, and often obscure bugs that exist in software. Their occurrence is common, and their exploitation usually catastrophic.

Two of the most commonly exploited programming errors are buffer overflows and format string vulnerabilities. In the case of an exploitable instance of either these types of vulnerabilities, it is possible for an attacker to execute arbitrary code. The code executed by the attacker is run on the vulnerable host in

![](img/729efc56f204a2ebffb8295c3a2dfdfb_757_0.png)

# 734 Chapter 14 + Attacking and Defending Unix

the context of the vulnerable process; that is, any code executed through the service is executed with the privileges of the service. The code executed can perform any action the attacker requests, but typically the code is used to execute a command shell, giving the attacker an interactive means of accessing the host.

By design, services require elevated privileges to function on ports below 1024. Because of the design of systems, all the frequency of severe vulnerabilities in services that execute with elevated privileges, many services include functionality that allows them to drop privileges after execution. In practice, this is good, although it may be possible to reclaim elevated privileges when the service is exploited. The easiest method of attacking services vulnerable to programming errors is with an exploit.

# Input Validation Errors

Input validation errors occur when a program trusts input from parties it does not trust. These types of vulnerabilities generally involve assumptions on the part of the program that the source of input will never send anything unexpected. As a result, unexpected input sent to the service allows the attacker to carry out actions that should not be permitted.

A PHP include, a function in PHP which imports another file into the PHP script, is one such problem. This function is used to allow the use of multiple pieces of information spread across different files. A PHP include can use a variable as the source of file. However, if an attacker can define this variable, they may play commands in the include file. When the PHP script loads it, the attacker could potentially execute commands through the include file.

Exploiting PHP requires placing files in a directory of a Web server that can be reached from the target Web server. A malicious string defines the variable for the include is sent to the server, and the file is downloaded and executed on the vulnerable host. Commands executed on the host through a PHP include vulnerability are performed with the privileges of the Web server process. This vulnerability could be used to download and execute malicious programs. Systems with PHP should be audited. Web applications written in PHP that run on the host should be audited, and checked for include() vulnerabilities. Pre-written Web applications can be downloaded from their respective vendor, and a cursory search performed using a utility such as grep. Include definitions and variables used with them can be followed through the source code using
