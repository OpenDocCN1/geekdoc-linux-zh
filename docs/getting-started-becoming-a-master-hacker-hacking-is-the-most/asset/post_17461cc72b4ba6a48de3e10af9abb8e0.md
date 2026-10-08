
It's important to note that most online databases are no longer vulnerable to this simple attack, but a few still are. For more advanced SQL injection techniques such as blind SQL injection, look for my next book "Getting Started Becoming a Master Hacker 2."

WordPress is the world's most popular CMS for developing websites. Our tool wpscan, is excellent at identifying vulnerabilities of these sites, enumerating users and brute-forcing passwords.

## Exercises

- 1. Use Google hacking to find potentially vulnerable websites to SQL injection.
- 2. Use OWASP-ZAP to determine if the sites you found in the previous step are vulnerable to SQL injection.
- 3. Use Google hacking to find WordPress sites.
- 4. Use Google hacking to find information leaks in WordPress backups.
- 5. Use wpscan to search for vulnerabilities in the WordPress sites you identified in the previous step.
- 6. When you find vulnerabilities in the site, get more information and possibly the exploit by searching wpvulnsdb.com or packetstormsecurity.com.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_459_0.png)
![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_459_1.png)

## Chapter 13

### Evading AV and Shellcode Fools

*Master OTW*

When exploiting the target as we did in Chapter 9 with Metasploit, you are likely to encounter an anti-virus program running on the target system. It is a rare target that’s not protected with an anti-virus application. As such, we need to examine how we might evade such protection.

Often, the best way to avoid AV detection is to use a memory corruption exploit and load the payload directly into memory without ever writing to the hard drive. This is what we did with the EternBlue exploit. Unfortunately, that's not always possible with every exploit.

In the past, the msfvenom module of Metasploit from Chapter 9, was capable of creating payloads that could evade AV detection, but the AV developers didn't sit idle. These software companies soon developed techniques for detecting nearly any payload developed by msfvenom, but not all (recently, some advanced persistent threat (APT) malware from a nation-state effectively evaded AV using the shikata-ga-nai encoder). This means that to have a reasonable chance of success at evading detection by anti-virus software, we will need to turn to other software to help us re-encode our payloads.

### Metasploit's New Evasion Module

Recognizing the limitations of msfvenom to evade AV detection, the developers of Metasploit began a new project to aid in the evasion of anti-virus. When Rapid7 released Metasploit 5 in October 2018, it contained two new evasion modules. These modules were a departure for Metasploit, as there had not been any new module types in quite a few years.

When the new modules were released, they were very effective at evading Windows Defender in Windows 10. Unfortunately, in the ongoing chess game between attackers and defenders, the folks at Microsoft added detection of these payloads developed by these new modules shortly thereafter. Despite this, we must give kudos to Rapid7 for putting time and effort toward this crucial issue (for more on the new Metasploit evasion modules, read [Metasploit Basics for Hackers Part 24: The New Evasion Modules in Metasploit 5](https://www.hackers-arise.com/post/2019/03/27/metasploit-basics-for-hackers-part-24-the-new-evasion-modules-in-metasploit-5)).

### How Antivirus Software Works

Before we begin to work toward an undetectable payload, we need to understand how anti-virus software works. Most AV software can detect malicious code by comparing signatures (code snippets and other artifacts) of known malware against software that is entering the system (for more on how antivirus software works, go to [Evading AV: Anatomy of a ClamAV](https://www.hackers-arise.com/single-post/2016/10/28/Evading-AV-Anatomy-of-a-ClamAV)). Although some software developers have begun to use heuristic techniques (detecting known malicious behavior) this is still not widespread among AV applications as it requires significant CPU cycles to incorporate this approach. The result of using heuristics is slower scanning and system lag.

It is also important to note that not all AV software is created equal. Not every AV application will catch all known malware. VirusBulletin is an independent AV software testing laboratory. According to their results, commercial AV software is capable of detecting between about 60-98 percent of known malware.

Most of the major AV software developer results are clustered in the 95 percent range. Even with these, 95-percent detection means 1 in 20 known malware will go undetected by these applications. Of course, a zero-day--by definition, unknown malware-- is likely to sail right past **all** of these applications.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_462_0.png)
![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_462_1.png)

This perspective is key because to compromise a target, you may not need to be undetectable by **ALL** AV applications. You only need to be undetected by the target’s AV software. If you know what AV software the target is using, you can focus on making your payload undetectable by that application (see my article [How to Use Recon-ng to Determine the Target's AV Software](https://www.hackers-arise.com/single-post/2016/05/23/How-to-Use-Reconng-to-Determine-the-Targets-AV-SoftWare-1/) on using recon-ng to determine the target’s AV software).

### Tools for Making Payloads Undetectable

Among the tools available to create payloads/shellcode capable of going undetected by (AV) software such as veilevasion ([https://www.hackers-arise.com/evading-av-with-veilevasion](https://www.hackers-arise.com/evading-av-with-veilevasion)) or shellter ([https://www.hackers-arise.com/evading-av-with-shellter](https://www.hackers-arise.com/evading-av-with-shellter)), OWASP-ZSC (**Z**ero-day **S**hell**C**ode) may be the most versatile. OWASP-ZSC is a project of OWASP (the venerable Open Web Application Security project of the OWASP Top 10 fame and OWASP-ZAP, among other things), continues under development, but has some useful features not found in some of the other applications in this category. In this chapter, I will attempt to demonstrate some of the most important features of OWASP-ZSC and how they can be used to create shellcode/payloads that will go undetected by AV software.

### What is Shellcode?

Shellcode is simply a set of instructions (code) that, when executed into a running application such as SMB (like EternBlue does) or other vulnerable services, gives the attacker control of the system. This code is written in assembler language (for more on assembler language, see [Reverse Engineering Malware Part 2: Assembler Language Basics](https://www.hackers-arise.com/single-post/2017/02/27/Reverse-Engineering-Malware-Part-2-Assembler-Language-Basics)).

When a stack or heap-based buffer overflow is executed, the shellcode is then injected and often gives the attacker a way to control the target system through such things as a command shell (hence its name).

Whenever new shellcode becomes available, it is incumbent upon the anti-virus software developers (if they want to remain relevant in this industry) to develop a signature or other method to detect the malicious content. As hackers/pentesters, we need to constantly change our shellcode to evade the antivirus software and remain stealthy and effective. OWASP-ZSC is one more tool we can use to create, encode, and obfuscate our shellcode to remain undetected by the anti-virus software on the target's machine.

```bash
root@kali-2019:~# git clone https://github.com/zscproject/OWASP-ZSC
Cloning into 'OWASP-ZSC'...
remote: Enumerating objects: 2395, done.
remote: Total 2395 (delta 0), reused 0 (delta 0), pack-reused 2395
Receiving objects: 100% (2395/2395), 3.29 MiB | 7.30 MiB/s, done.
Resolving deltas: 100% (1553/1553), done.

Building Commandline
Copying Files

Now you can remove this folder
files copied in /usr/share/owasp_zsc.
to run zcr shellcoder please use "zsc" command line

| Visit https://www.owasp.org/index.php/OWASP_ZSC_Tool_Project --- |
root@kali-2019:~/OWASP-ZSC#
```

Let's take a look at how we can use OWASP-ZSC to build, encode, and obfuscate our shellcode.

### Download and Install OWASP-ZSC
