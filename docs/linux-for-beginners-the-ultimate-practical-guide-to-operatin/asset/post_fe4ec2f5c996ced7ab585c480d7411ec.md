
## 3) -sU scan (UDP scan)

This scanning is also in the penetration-testing checklist after the importance of -sS scan. There is no need to send SYN packets like in TCP scan because this will just find UDP ports that are open. When the hackers start using the scan, a UDP packet reaches the target host and waits for a positive response. If at all a response is received, an open port is found. If it sends an error message with an Echo command, then the port is closed.

Below is the command line for -sU scan hacking:

```
kali@kali:~$ nmap -sU 192.168.2.1
```

## 4) -sF scan (FIN scan)

This is a special type of scan that is used because some targets may have installed intrusion detection systems and firewalls that stop SYN packets that are sent using a TCP scan. For this sole reason, FIN scan is used if there is any extra detection scan happening on the other side. FIN scan does not save any log information to be detected, so there is a great chance of the FIN packet to find out few open ports by sneaking into the target systems. Here is the command for -sF scan:

```
kali@kali:~$ nmap -sF 192.168.2.1
```

## 5) -sP scan (Ping scan)

Ping is a famous network protocol method that checks whether a host is live or not by trying to connect to the target host. Ping scanning in Nmap also is used for the same purpose and is not used to check open ports. Ping scan asks for root access to start a scan. If you are not ready to provide the administrative privileges, you can just use the connect method to start a ping sweep from Nmap. Here is the command for -sP scan:

```
kali@kali:~$ nmap -sP 192.168.2.1
```

## 6) -sV scan (Version detection scan)

A version detection scan is one of the obsessive usages of Nmap for hackers. To attack a target system, you need to know about the technology and operating system the host is using so you create your exploits and backdoor strategies to break into the system. However, unlike TCP scans, version detection scan takes a lot of time because when we start a -sV scan in the background, TCP scan gets started and searches for the open ports. After the hunt for open ports gets finished, -sV scan automatically analyzes them and determines the information about the target host. Due to this complex procedure, it may take a lot of time. Here is the command for -sV scan:

```
kali@kali:~$ nmap -sV 192.168.2.1
```

## 7) -sI scan (Idle scan)

This is one of the craziest features of Nmap because it just acts like a proxy server while doing attacks. When using an idle scan, you can send packets using another host IP. This anonymity can help hackers to stay in the dark if something goes wrong or severe. Protecting himself from the investigation is what every hacker strives for, especially in these modern times. Here is the command for -sI scan:

```
kali@kali:~$ nmap -sI 192.168.2.6 192.168.2.1
```

## Things Nmap can detect:

Nmap can detect the Device type of the host that is (router, workgroup, etc.), running operating system, operating system details i.e. version and network distance (approximate distance between the target and the attacker). While using Nmap, always use a ping scan only when necessary because some firewalls in the target hosts can detect that an attack is going to happen and will block the attacker's addresses to make any connection. By using the below command, you are saying to the software that it doesn't ping the remote host:

```
kali@kali:~$ nmap -O -PN 192.168.5.6/12
```

Using the -PN parameter can bypass the Ping Command, but it does not affect the discovery of the host system. NMAP operating system detection is based on open and closed ports. If OS scan cannot detect at least one open or closed port, it will return the following error. The error code is below:

Warning: we cannot find any open or closed ports to get information on the target system

It is difficult to accurately detect the remote operating system with NMAP, so we need to use NMAP's guess function. osscan-guess operation guesses which operating system type is closest to the target.

```
# nmap -O --osscan-guess 192.168.2.1
```

By using the following commands and strategies, you can research a lot of information about the target point and can use that information to create backdoors and exploit the system. The exploitation of the system using Metasploit will be explained in further chapters but only after a description of Nessus, an automatic vulnerability assessment tool that finds vulnerabilities automatically, otherwise which you need to find manually by boring procedures. Before going to talk about Nessus, let us have a simple exercise. Please try to do this exercise for a better understanding of the Information Gathering.

## Exercise

Start Kali Linux terminal and enter into Nmap using the commands. Find the subnet masks for www.nmap.org and find the operating system and version that it uses. Complete different scans and create a detailed report on all the available ports.

## Automatic Vulnerability Scanning

First of all, let us learn in detail about what vulnerability means along with examples of a few vulnerabilities.

## What is vulnerability?

Vulnerability is a defect in the host system that lets hackers create backdoors to enter into the system by creating an exploit for the vulnerability. For example, Ransomware has used a vulnerability in Windows to exploit hundreds of systems worldwide. Web applications also are prone to vulnerabilities. XSS vulnerability, CSRF detection and others are declared high-risk vulnerabilities by OWASP, which determines the severity of vulnerabilities.

## What is Automatic Vulnerability Scanning?

Vulnerabilities can be easily found out with manual testing after the coding. However, it is so boring and time-consuming that many avoid it. For this purpose, certain automated scanners are made to scan the system and detect any if coincided from the database that they have. Software's like Nessus and Burp Suite make this automatic scanning effective and are prone to get good results if done well.

## Nessus

Nessus is said to be an automatic scanning tool that has a wide database with well-known vulnerabilities, which the tool will use to scan the target and give results for the attacker. For Penetration Tester, Nessus is one of the essential tools. A summary of Nessus typically includes thousands of up-to-date vulnerabilities, a variety of scanning options, and an easy-to-use graphical interface and effective reporting. Nessus is loved because it has several characteristics.

Here’s how it works:

- To provide a complete computer vulnerability scanning service and update its vulnerability database at any time.
- Different from the traditional vulnerability scanning software, Nessus can analyze and scan the vulnerability of the system at the same time, and its efficiency can be adjusted according to the resources of the system.
- If the host is configured with more resources (such as faster CPU speed or increased memory size), its performance can be improved because of the abundance of resources.
- It can define its own plug-in; NASL (Nessus Attack Scripting Language) is a Language issued by Tenable, security Test Options for Writing Nessus.
- Full support for SSL (Secure Socket Layer).

Nessus is preinstalled in the Kali Linux and can be opened from the menu or by using a search box. It has a GUI and can be easily understood. On Linux, the Nessus tool is installed by default in the /opt/Nessus directory.

1. Nessus is enabled and accessed using the browser. For example, if your IP is 192.168.2.1, the browser enters the https protocol under `https://192.168.2.1:8834`.
2. First, we need to register a login and password to use Nessus. You can do that by going to the Nessus official website.

### Creating a Basic Scan in Nessus

Step 1: Usually when we want to Scan a host or website, click My Scans in the Nessus menu and then click on New Scan, which creates a New Scan. We can select Web Application Tests if we are scanning a website; if we are scanning a host, we need to select Advanced Scan.
