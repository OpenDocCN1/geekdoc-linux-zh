
# Attacking and Defending Unix • Chapter 14

text editor. As with programming errors, information on known issues can be gathered from vulnerability databases, exploit archives, and security mailing lists.

Input validation errors also occur in CGI programs. An attacker is able to supply the definition of a variable to the script, or is able to execute commands using escape characters such as the backtick (`) ) and vertical bar (|) in an input field. When the string is rejected, similar to the PHP include issue, commands are executed with the privileges of the Web server.

Input validation bugs may also result in the disclosure of information that can allow an attacker to gain access to a host, or elevated privileges. Through an input validation error, an attacker could gain information such as the contents of a password file, core file, or other sensitive information. This is particularly true of directory traversal problems that exist in some Web servers, where an attacker could supply the path to the file to be viewed. An attacker could also potentially use this problem to disclose the contents of the master password file on the system, unveiling the list of user names that would be useful in a brute force attack, which we will discuss next.

# Brute Force Attacks

A brute force attack involves using time and chance to gain access to a host. Brute force attacks can be performed manually against a host, or using an automated-program. The easiest method is the latter.

A brute force attack can be used to gain remote access by trying username and password combinations through an interactive service such as Secure Shell (SSH), Telnet, or the File Transfer Protocol (FTP). Most Unix systems direct login of an administrator remotely, therefore unprivileged access is gained from this type of attack.

Once a valid username and password combination is discovered, the attacker gains access to the host with the privileges of the cracked user. The attacker can use the user's account to launch attacks from the host, or the attacker can attempt to gain elevated privileges on the host. Gaining elevated privileges and compromising the administrative account on the system is priority, as it allows the attacker to put software in place to hide their penetration of the system.

A brute force attack is a matter of probability. The odds are stacked in favor of the house, as the probability of an attacker guessing a username and password are somewhat slim. However, if an attacker can use another bug such as an input validation issue to gain access to a list of valid accounts on the host, the probability of success increases dramatically, especially with the use of an automated brute force tool.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_759_0.png)

75

# Local Privilege Elevation

If the attack did not result in elevated privileges after a system has been compromised, additional steps are required. To gain elevated privileges locally, an attacker must find a means of exploiting a vulnerable program or process. Accordingly, we would take the same path as gaining elevated privileges.

Once access to the local system has been gained, you must evaluate your situation to determine your next move. First, you must determine if you have gained full access to the host, or if you are confined to a particular section of the host, such as a chroot directory. You must also determine the privileges you have locally on the compromised system.

Once you have gathered information, you must determine the method you are going to use to gain elevated privileges. Gaining elevated privileges may be performed through one of the types of vulnerabilities mentioned in the previous section on gaining remote access. It may also be performed through a few other methods, which we discuss in this section.

# Restricted Environments

Once you have compromised the service to gain access to the system, you must determine if the process you have exploited has been confined to a directory using the chroot() or jail() system calls. Services that have been compromised and restricted to a directory using these system calls will require breaking the restricted environment to launch privilege escalation attacks on the local host.

The steps required to break a restricted environment depend entirely on the restricted environment. First, if the process is run as root, you can use known problems with the implementation of some chroot environments to escape. If you do not have root access through the compromised service, but have the ability to exploit something in the chroot environment to gain root access, you can follow the previously mentioned procedure with the additional step of gaining root access.

Other restricted environments, such as restricted shells, can be escaped using other known problems with implementations. One such example is the capability of most Unix editors to spawn a shell, which is often restricted. If you have compromised a host and gained access to a restricted shell, you will have to circumvent the shell before you can launch further attacks on the host.

# Attacking and Defending Unix • Chapter 14

# Vulnerability Exposure

Previously I discussed a few different types of attacks used to remotely gain access to a host. These attacks included exploiting programming errors, exploiting input validation errors, and brute force attacks.

These types of attacks however do not only apply to the system in a remote environment. You may also use these types of attacks in gaining privileges on the local host. This involves knowing what to look for, and where to start these types of attacks.

To exploit programming errors and input validation bugs, you need only find a program on the system that executes with elevated privileges. This can be a program that is setuid, or one that is executed by a privileged user, such as cron or other methods. The best way to find problems that grant elevated privileges when exploited is to search out a vulnerability database or exploit archive, and reference system details against available information.

It is also possible to take advantage of other classes of vulnerabilities with local system access. Problems such as configuration errors are more devastating at the local system level. Other issues, such as environment errors and race conditions, also become more feasible to exploit. Once local access has been gained to the system, it is merely a matter of time, patience, and research before gaining elevated privileges.

# Engineering a Secure Unix System

A secure, reliable system does not just happen. Secure systems are created through the gathering of information, planning, and secure implementation of the system; in other words, they are engineered. Adequately planning a system and implementing it securely from the beginning limits the exposure of systems to common vulnerabilities. In turn reduces the number of staff responsible for systems time, which ultimately equates to saving money.

In this section, we look at the resources and steps necessary to engineer a secure system. We examine the aspects of gathering information for the planning of the system and the organizing of a system design, followed by some general strategies for implementing a system design securely.

# System Information Gathering

Before building a system or even creating a design for a system, the distinct set of gathering information must be performed. While this may seem obvious, it is

![](img/729efc56f204a2ebffb8295c3a2dfdfb_761_0.png)

# Chapter 14 • Attacking and Defending Unix

often the case that there is an information breakdown that ultimately results in the poor design of a system. In this scenario, two distinct situations emerge:

- Insufficient information
- Irrelevant information

# Gathering Sufficient Information

One breakdown in information gathering is the gathering of an insufficient quantity of information. This error is common because information gathering can be extremely complex. Gathering information to create a secure system must go beyond only taking into account the purpose of the system. A system that will act as an-mail server or SQL database server is affected by a number of variables in the network environment.

Considerations such as management and network design must also be taken into account when planning a system. For example, a host that is destined to sit on a public network is subject to stricter access control requirements than that one will act as a file server on a private network. This is further complicated by such factors as the method of management, software used to monitor hosts, and what kind of access users will need to the host.

Before information gathering can occur, you must decide how much information is needed, and what information is needed. Figure 14.4 shows a short checklist of basic information required. This list can be expanded or contracted to fit your needs. A list of information need not be a formal document, though it should be as legible as possible. This document should be retained in the maintenance logbook kept for the system, and should be legible and detailed enough to give future administrators an idea as to why design decisions were made, and what influences were taken into account when the initial model was developed. As you will see, information is a double-edged sword that can add unneeded complexity.

# Figure 14.4 Checklist of Information to Gather when Planning a Secure Server

| Purpose Of Server | Mail Server |
|---|---|
| Operating System | Solaris |
| Neighbor Servers | Gateway01, www |
| Required Software | Postfix, Apache, Imp |
| | Continued |
