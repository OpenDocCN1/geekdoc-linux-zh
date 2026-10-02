
Because it’s impossible to protect computer systems from all attacks, solutions identified through the risk management process must support three integral concepts of a holistic security program:

- **Protection:** Provide countermeasures such as policies, procedures, and technical solutions to defend against attacks on the assets being protected.
- **Detection:** Monitor for potential breakdowns in the protective measures that could result in security breaches.
- **Reaction (response):** Respond to detected breaches to thwart attacks before damage occurs; often requires human involvement.

Because absolute protection from attacks is impossible to achieve, a security program that doesn’t incorporate detection and reaction is incomplete.

## Managing security

In addition to implementing security solutions, you also need to implement security management measures to continually monitor, detect, and respond to any security incidents.

The combination of the risk analysis, security policy, security solutions, and security management provides the overall security framework. Such a framework helps establish a common level of understanding of security concerns and a common basis for the design and implementation of security solutions.

## Securing Linux

After you define a security policy, you can proceed to secure the system according to the policy. The exact steps depend on what you want to do with the system, whether the system is a server or workstation, and how many users must access the system.

To secure the Linux system, you have to handle two broad categories of security issues:

- **Host-security issues:** These issues relate to securing the operating system and the files and directories on the system.
- **Network-security issues:** These issues refer to the threat of attacks over the network connection.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_389_0.png)

If your host is connecting to a large network, Directory Services can become a significant issue. Directory Services security is outside the scope of this book, but you can find information about it by searching online.

## Understanding the host-security issues

Here are some high-level guidelines to address host security (some of which I cover in detail in Book 6, Chapter 2):

- When installing Linux, select only the package groups that you need for your system. Don't install unnecessary software. If your system is used as a workstation, for example, you don't have to install most of the servers (web server, news server, and so on).
- Create initial user accounts, and make sure that all passwords are strong enough that password-cracking programs can't guess them. Linux includes tools that enforce strong passwords.
- Set file ownerships and permissions to protect important files and directories.
- If mandatory access-control capabilities are available, enable them. Support for this feature has been incorporated, through Security Enhanced Linux (SELinux) since kernel 2.6. The best way to think of SELinux is as a wrapper that can be placed around standard Linux to provide more security measures. AppArmor is favored over SELinux in some distributions but it serves the same purpose and offers similar features to SELinux.
- Use the GNU Privacy Guard (GnuPG) to encrypt or decrypt files with sensitive information and to authenticate files that you download from the Internet. GnuPG comes with Linux, and you can use the gpg command to perform tasks such as encrypting or decrypting a file and digitally signing a file. (See Book 6, Chapter 2 for an explanation of digital signatures.)
- Use file-integrity checking tools, such as Tripwire, to monitor any changes to crucial system files and directories. Visit www.tripwire.com for the commercial version.
- Periodically check various log files for signs of any break-ins or attempted break-ins. These log files are in the /var/log directory of your system.
- Install security updates as soon as they're available and tested. These security updates fix known vulnerabilities in Linux. Be sure to test an update on nonproduction machines before rolling it out to your production servers.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_390_0.png)

You can spend a great deal of time *hardening* your server — locking down the services on it to make it as secure across the network as possible. But don’t overlook the fact that someone could pick up the server and walk right out the door with it. When locking down a system, be sure that you also physically secure it with locked doors and cables where necessary.

## Understanding network-security issues

The issue of security comes up as soon as you connect your organization’s internal network to the Internet. You need to think of security even if you connect a single computer to the Internet, but security concerns are more pressing when an entire internal network is opened to the world.

If you’re an experienced system administrator, you already know that the cost of managing an Internet presence doesn’t worry corporate management; management’s main concern is security. To get management’s backing for the website, you have to lay out a plan to keep the corporate network secure from intruders.

You may think that you can avoid jeopardizing the internal network by connecting only external servers, such as web and FTP servers, to the Internet, but employing this simplistic approach isn’t wise. This approach is like deciding not to drive because you might have an accident. Not having a network connection between your web server and your internal network also has the following drawbacks:

- You can’t use network file transfers, such as FTP, to copy documents and data from your internal network to the web server.
- Users on the internal network can’t access the corporate web server.
- Users on the internal network don’t have access to web servers on the Internet. Such a restriction makes a valuable resource — the web — inaccessible to the users in your organization.

A practical solution to this problem is to set up an Internet firewall and to put the web server on a highly secured host outside the firewall.

In addition to using a firewall, here are some steps you can take to address network security (explained further in Book 6, Chapter 2):

- Enable only those Internet services you need on a system. In particular, don’t enable services that aren’t properly configured.
- Use Secure Shell (`ssh`) for remote logins. Don’t use the r commands, such as `rlogin` and `rsh`.
- Secure any Internet services, such as FTP or Telnet, that you want to run on your system. You can use the TCP wrapper access-control files — `/etc/hosts.allow` and `/etc/hosts.deny` — to secure some of these services. (See Book 6, Chapter 3 for more on the TCP wrapper.)
- Promptly fix any known vulnerabilities of Internet services that you choose to run. Typically, you can download and install the latest security updates from your Linux distribution's online update sites.

## Delving Into Computer Security Terminology and Tools

Computer books, magazine articles, and experts on computer security use some terms that you need to know to understand discussions of computer security (and to communicate effectively with security vendors).

![](img/322157d1fa7d965f05bcd68ed0ffc36b_391_0.png)

Table 1-1 describes some commonly used computer security terms. If you’re taking the LX0-104 exam, port scanning and setuid are important.

## TABLE 1-1 Common Computer Security Terminology

| Term | Description |
|---|---|
| Application gateway | A proxy service that acts as a gateway for application-level protocols, such as FTP, HTTP, NNTP, and SSH. |
| Authentication | The process of confirming that a user is indeed who he or she claims to be. The typical authentication method is a challenge-response method wherein the user enters a username and secret password to confirm his or her identity. |
| Backdoor | A security weakness that a cracker places on a host to bypass security features. |
| Bastion host | A highly secured computer that serves as an organization's main point of presence on the Internet. A bastion host typically resides on the perimeter network, but a dual-homed host (with one network interface connected to the Internet and the other to the internal network) is also a bastion host. |
| Buffer overflow | A security flaw in a program that enables a cracker to send an excessive amount of data to that program and to overwrite parts of the running program with code in the data being sent. The result is that the cracker can execute arbitrary code on the system and possibly gain access to the system as a privileged user. The new exec-shield feature of the Linux kernel protects against buffer overflows. |

(continued)
