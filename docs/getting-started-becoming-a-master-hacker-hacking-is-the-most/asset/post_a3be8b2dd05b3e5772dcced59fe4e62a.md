
10. iloveyou

11. princess

12. admin

13. welcome

14. 666666

15. abc123

16. football

17. 123123

18. monkey

19. 654321

20. !@#$%^&*

21. charlie

22. aa123456

23. donald

24. password1

25. qwerty123

If someone on the network is using one of these common passwords, or the 5,000 other most-common passwords, the attacker can crack it in seconds!

There are at least two types of password cracking, online and offline. Offline cracking is much simpler once the password hash (most passwords are stored in one-way encryption known as a hash. See Appendix A, “Cryptography Basics for Hackers”) has been obtained and the hacker can employ whatever resources are at their disposal to crack it. Online cracking is far more difficult, as many systems have lockouts that can limit our attempts.

## Exploitation

If we have failed with password-cracking, the next step is to attempt exploitation. Based on the information garnered in the reconnaissance phase, we can develop a strategy for exploitation. Exploitation is usually accomplished because of a flaw in the operating system or application. The most notorious of these flaws is the buffer overflow. The buffer overflow occurs when a variable area is overflowed with too much, or with a specific type, of data and then enables the attacker to place their remote code (usually a rootkit, payload, or listener) in its place. This replacement code is then executed by the target system, and the attacker then connects to and controls the target system (for more on buffer overflows see Exploit Development, Part 1 at https://www.hackers-arise.com/single-post/2017/05/26/Exploit-Development-Part-1-Anatomy-of-Buffer-Overflows ).

Although there are many tools and scripts available for exploitation, Metasploit is the tool of choice for the beginner-to-intermediate hacker. Metasploit is a framework for the exploitation (and other tools) against known vulnerabilities in computer systems. The key words here are "known vulnerabilities."

Metasploit does not help you hack with new, zero-day (never seen before) exploits, but instead catalogs and deploys tools and exploits against known vulnerabilities in operating systems, services, and applications.

It’s important to note that systems are NOT always patched and up-to-date. As we saw in the History of Hacking section in Chapter 1, even after the patch for the EternalBlue exploit was released, the attackers were able to exploit hundreds of thousands of systems around the world and garner billions of dollars in ransom.

In this book, we will focus on the use of Metasploit and some Python scripts for exploitation.

## Post-Exploitation

Post-exploitation is what happens after the hack, or exploitation. The hack gets the attacker inside the system, but access is generally just the beginning. Post-exploitation can include grabbing passwords, accessing the database, turning on and accessing the microphone or webcam, etc. It may also include pivoting to compromise other parts of the network. For instance, if the hacker can compromise a single user on the network, that user’s systems will not likely have the valuable assets the hacker is seeking, such as the database that contains personally identifiable information, credit card numbers, or confidential information. The hacker needs to learn to pivot from the compromised system to other systems on the network to be successful.

## Covering Tracks

Once the exploitation is complete, and the post-exploitation havoc has been done (taking or reading documents, turning on the microphone, pivoting to other systems, etc.), the final task for the hacker is to cover their tracks. This phase makes it more difficult for a forensic investigator to be able to track the hacker’s activity and actions. This can mean deleting or altering log files, deleting bash commands, changing timestamps on files, and others.

## Summary

Now that we have an idea of the process of hacking or exploitation, let's get started!

In the next chapter, we will set up the safe lab environment where we can practice without any chance of legal ramifications.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_94_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_94_1.png)

# Building Your Hacking Virtual Lab

The desire for safety stands against every great and noble enterprise.

*Tacitus*

Now that we completed all the preliminaries, let’s get started hacking!

Before we launch our journey to becoming a master hacker, we must first build a safe lab where we can practice our tools and techniques.

The best way to do that is to use a virtual environment. Virtualization enables you to run many operating systems all within the same physical machine, and thereby practice your skills in secure environment.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_95_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_96_0.png)

There are numerous virtual machine environments available to you. These include VMware Workstation, VirtualBox, Parallels, Virtual PC, Xen, ESXi, Hyper-V, and any others. You can use any of these, but in the following section, I will walk you through setting up your hacking lab in Oracle’s free VirtualBox.

VirtualBox is a solid choice for virtualization, and most importantly, it’s free!

Virtualization means we can set up our attacking system, such as Kali, on the same physical computer as our victim system, such as Windows 7 or Metasploitable 2 (this is a purposely vulnerable Linux system).

There are at least two primary ways to virtualize operating systems, type-1 or full-virtualization and type-2 or hardware-assisted virtualization.

Type-1 virtualization runs on “bare-metal” or in other words, there is nothing between the virtualization system (hypervisor) and the hardware. In type-2 virtualization, we are able to run a guest operating system (OS) inside a host operating system. This is not the most efficient, but it is excellent as a lab environment. That’s what we will do here with VirtualBox.

## Kali Linux

Let’s begin by downloading our attack system, Kali Linux. It was developed by Offensive Security as a hacking/pentesting operating system built on a distribution of Linux called Debian. There are many distributions of Linux, and Debian is one of the best. You are probably most familiar with Ubuntu as a popular desktop distribution of Linux. Ubuntu is also built on Debian. Other distributions include Red Hat, CentOS, Mint, Arch, SUSE and several others. Although they all share the same Linux kernel (the heart of the operating system that controls the CPU, RAM, and so on), each has its own utilities, applications, and choice of graphical interface (GNOME, KDE, and others) for different purposes. As a result, each of these distributions of Linux looks and feels slightly different. Kali was designed for penetration testers and hackers and comes with a significant complement of hacking tools.

## Kali Linux Downloads

### Download Kali Linux Images

We generate fresh Kali Linux image files every few months, which we make available for download. This page provides the links to download Kali Linux in its latest official release. For a release history, check our Kali Linux Releases page. Please note: You can find unofficial, untested weekly releases at http://cidimage.kali.org/kali-weekly/. Downloads are rate limited to 5 concurrent connections.

| Image Name | Download | Size | Version | SHA256Sum |
| :--- | :--- | :--- | :--- | :--- |
| Kali Linux 64-Bit | HTTP \| Torrent | 3.2G | 2019.2 | 67574ee0039eaf4043a237e7c40e0b432cc07feb93c7b20d6667e83bc3900b2cf |
| Kali Linux 32-Bit | HTTP \| Torrent | 3.2G | 2019.2 | 1e9a023b0db81fdec9c69712210c2c48f62da3f9900d0f1dbe73f150ee6f246282 |
| Kali Linux LXDE 64-Bit | HTTP \| Torrent | 3.0G | 2019.2 | cdd07fc955275d49b40208838f8ca2984d5cebc942f54556d351d009edc8dc |
| Kali Linux HATE 64-Bit | HTTP \| Torrent | 3.1G | 2019.2 | f81caca35bc61678f1a84dc8949023b11c743d080f35be2ac8d6f008fdf93bad |
| Kali Linux Light armhf | HTTP \| Torrent | 741M | 2019.2 | 0f3ad59fc2fed888cb36daab3c6798da190e54e65c50b9562f847ad71a73963 |
| Kali Linux KDE 64-Bit | HTTP \| Torrent | 3.5G | 2019.2 | b794d2609231cf2c73f00783b8506cbfe304746c20e009ad21aa37b473c32749f |

I strongly recommend that you use Kali for this book. Although you can use other Linux distributions, you will likely spend significant amount of time downloading, installing and configuring the various tools we will be using (as many tools as Kali has, we will still need to download and install a few more).

You can download Kali Linux at www.kali.org.
