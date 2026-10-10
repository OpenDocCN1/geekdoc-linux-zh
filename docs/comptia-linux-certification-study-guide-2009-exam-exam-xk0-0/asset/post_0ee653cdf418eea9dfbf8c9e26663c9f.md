
rm -r /tmp/test and rm -r /tmp/test. The difference of a single errant space, in this case, will tell the system to try and delete every file on your machine. To protect your system as well as to use the idea of "least privilege" discussed in the previous section, it's advisable to use your system with normal user privileges whenever possible. When extra authority is called for, you can use the power of Privilege Escalation.

## sudo

The standard way of getting extra administrative power from a terminal window is to use sudo (think "do as super user"). It gets put in front of whatever command you want to run, and after you press the enter key, it will ask for your regular user password and run the command as administrator. The syntax is

```
sudo [OPTIONS] command
```

Some of the more interesting options include

- `-u` will let you run a command as a user other than the system administrator. This is handy for troubleshooting problems that involve user privileges.
- `-e` lets you enter a file to be edited instead of a command.

As a convenience, once you authenticate with sudo, it will remember the password for a few minutes, so additional uses of sudo don't ask for a password.

## su

Even with the several minute password grace period it can become tiresome to keep typing sudo, so if you need to do a bunch of stuff, it is often easier to start an entire new command shell with administrative privileges with the su command. Unlike the sudo command, su uses the administrator password. The syntax is

```
su [OPTIONS] [username]
```

As with sudo, su can be used to open a shell as any other user, too.

> **Note**
> Note that su opens a whole new shell, as a different user. Because of this there is a completely separate history file, so you can't use the "up" arrow to get to the command that you just got denied from running because you weren't root. Typing exit or <ctrl>d will put you back to your normal user shell.

## /etc/sudoers

You wouldn't want to give just anyone the awesome power of `super` user. Only users who are listed in the /etc/sudoers file can use privilege escalation. It also provides a number of options.

Although the /etc/sudoers file is just another text file, it is recommended that you use `visudo` as root to make any changes. This opens the sudoers file in `vi` and protects it from simultaneous edits, similar to `vi`pw. It also does a sanity check on the file before saving to ensure syntax is correct.

The options are typically described in commented sections within the file (see Figure 10.6) and include limits to what files each user can run, as well as the very bad option of allowing users to assume administrator privileges without a password.

![](img/95b3ebd6248b36778ccf73988aaab2f2_327_0.png)

**FIGURE 10.6**

A typical example of /etc/sudoers.

## EXERCISE 10.4: Assuming Administrator Rights

In this exercise, we’ll escalate your user privileges to administrator level using `su`. In a terminal window running under a normal user account, type the following:

1. `cat /etc/shadow` – as a normal user, this is a restricted file.
2. `su`.
3. enter the administrator (root) password.
4. `cat /etc/shadow` – now with your administrative privileges you should be able to see the file. Tread carefully, it is important to know when you are ready to return to your normal user level.

## SECURITY APPLICATIONS AND UTILITIES

In addition to the start management utilities for keeping a Linux system secure, there are a number of additional software packages that can be used to keep a close eye on your system and network. Each of the following tools are open source and available online (except Nessus, see below) through a standard package manager. They are all very complex and feature rich, and each is the topic of multiple books. For the exam, it is important to know what each tool is used for, although additional reading about each will be greatly beneficial to any professional system or network administrator.

> **Exam Warning**
> These tools are very useful for protecting your systems, but like any power tool, they can be misused easily. Be sure you have full authorization – preferably in writing – before using them outside of your own test environment. The tools that send out test packets are capable of sending information that can cripple or reboot some systems, which is a great way to test whether a system is vulnerable but could lead to a lot of problems. Please use these tools with care.

## nmap

Nmap is an open-source network scanning tool. It is invaluable for seeing what is attached to your network and can test any attached system for services or open network ports and works great for finding unauthorized network devices and services and testing firewalls. It can use known differences in replies to different packet types to guess what operating system is running on each device and can scan both User Datagram Protocol (UDP) and Transmission Control Protocol (TCP) network ports. It can be installed using your distributions package management system, or downloaded directly from http://nmap.org.

The advanced features and options available with nmap are well beyond the scope of the exam, but the basics are as follows:

```
nmap [Scan Type] [OPTIONS] target
```

A typical use of nmap is

```
nmap -sP 192.168.1.0/24
```

This will quickly use the ping ICMP utility to check for active hosts on the entire 192.168.1.1 – 192.168.1.254 subnet.

Use man nmap or check the extensive documentation on the nmap Web site for additional details.

## EXERCISE 10.5: Using nmap

In this exercise, we’ll do a quick network scan using nmap. If your system doesn’t have nmap installed already, you should be able to easily add it using the standard package manager. If not, you can download it from http://nmap.org. In a terminal window, type the following:

1. `nmap 127.0.0.1` is an easy place to start; it will scan the machine you are on.
2. `netstat -l` will also show ports on your local machine that are in a “listening” state, for comparison.
3. `netstat -r` will show the subnet you are attached to; use that address for the network in the next step. If you are using a typical home wireless route, there is a good chance your network will be 192.168.1.0. I’ll use that as an example.
4. `nmap 192.168.1.0/24` to scan the local network or enter a specific host address without the “/24” subnet mask bits to scan a single machine.

## Wireshark

Wireshark is a graphical network traffic analyzer built on the text-based `tcpdump` utility. Both are open sourced and available through standard package managers.

Wireshark can be used to monitor all network traffic coming in and out of an interface on your computer. Note, however, that to optimize performance, most modern network equipment limits the traffic that your individual workstation has to see. Most managed switches have an option to allow all traffic to be copied to a given port for monitoring and troubleshooting; enable this option on your switch to see the full power of *Wireshark*.

The main *Wireshark* window is split into three panes. The top section shows one line for each packet; the middle section shows a textual description of each portion of a specific selected packet, and the bottom section shows the raw hex information for the same packet.

Watching all the traffic can be fascinating, but overwhelming. *Wireshark* provides a complex way of filtering out traffic so you don't want to see based on specific hosts or protocols.

Although *Wireshark* is clearly a fantastic network troubleshooting tool, it is also very useful for fixing network applications, such as client-server database problems, remote access authentication issues, and printing errors. Frequently, the client software hides error details from the user, and a lower level view is needed to isolate the real issue.

As with the other tools, use *Wireshark* with care, as it is possible to view other user's passwords or private information; keep in mind that many applications, including e-mail, don't use encryption.

More information about *Wireshark* can be found at www.wireshark.org.

> **Note**
> Although the command-line-based `tcpdump` isn't as user friendly as *Wireshark*, it has a distinct advantage if you need to check traffic on a remote system using ssh. It offers identical filtering and capturing features and can be just the thing to quickly confirm whether your network packets are in fact reaching a remote system.

## Nessus

*Nessus* is a tool for testing networked systems for security vulnerabilities, which are defined as "any programming error or misconfiguration that could allow an intruder to gain unauthorized access." Previous versions were released under the GNU Public License (GPL) open source licence; any changes since release 3 Nessus have been kept the proprietary property of Tenable Network Security, although they continue to make the *Nessus* tool available for no charge.

*Nessus* can be installed and used by mere mortals, but it has the capability to scale by splitting up the part that does the scanning from the part that analyses the results, so you can install dedicated machines at remote sites and then centrally review the results.
