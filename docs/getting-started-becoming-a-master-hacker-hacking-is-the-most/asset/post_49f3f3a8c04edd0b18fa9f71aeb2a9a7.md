
zsc/shellcode/download OWASP-ZSC then prompts us for the shellcode ID. Simply enter the ID of the shellcode you want to use. In this case, let’s use ID **627**.

```
shellcode_id> 627
```

OWASP-ZSC now downloads this shell and displays it on the screen as you can see above.

```
zsc> obfuscate
zsc/obfuscate>                  php              python        ruby
zsc/obfuscate> javascript perl
zsc/obfuscate> windows7shell
  encode> base64                rot13           simple_base64_rev simple_hex_rev
  jsfuck      simple_ascii      simple_hex
  encode> simple_hex_rev
  [+] file "windows7shell" encoded successfully!
zsc>
```

The next step is to obfuscate the shellcode. Obfuscation means to make it difficult to understand. In this case, we are trying to make it difficult for a malware analyst—or forensic analyst—to understand the intent and function of the code.

zsc > obfuscate When we hit the TAB key, it lists all the obfuscation methods. Let’s assume we want this shellcode to work with a browser exploit, so select javascript.

zsc/obfuscate > javascript Next, OWASP-ZSC prompts us for the filename we want to use for our obfuscated file. I named it windows7shell, but you can name it anything you want.

zsc > windows7shell The next step then is to encode the shellcode. OWASP-ZSC prompts us with encode >. The idea here is to make it more difficult for the AV application to match anything in this shellcode with its database of known malicious code.

When we hit the TAB key, it lists all the methods available for this shellcode. These encoding methods will differ slightly with different shellcode and obfuscation techniques.

In this case, we will encode it with jsfuck.

```
encode>
base64 rot13 simple_base64_rev simple_hex_rev
jsfuck simple_ascii simple_hex
encode> jsfuck
[+] file "windows7shell" encoded successfully!
```

encode > jsfuck Yes, jsfuck is a real encoding scheme. It is a seldom used subset of Javascript that is written with just 6 characters ([,],(,),! and +. It can be particularly useful for bypassing web form input validation and obfuscation.

When we hit enter, OWASP-ZSC encodes our shellcode with jsfuck and announces it has completed its task!

### Testing Our Shellcode

The final step is to test your new shellcode against AV software. If you know what AV software the target is using, simply test it against that one (check out my article on recon-ng to determine the AV the target is using). If not, you can test your new shellcode at VirusTotal (www.virustotal.com). It’s important to note that VirusTotal shares your code with the AV developers.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_473_0.png)

Analyze suspicious files and URLs to detect types of malware, automatically share them with the security community

# FILE

# URL

# SEARCH

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_473_1.png)

# Choose file

By submitting your file to VirusTotal you are asking VirusTotal to share your submission with the security community and agree to our Terms of Service and Privacy Policy. Learn more.

scanii.com Dashboard Documentation Support occupy theWeb

Good afternoon occupy theWeb! 50 /50 available credits

This just in → Simple Intrusion detection with AWS GuardDuty

# Why is this page mostly empty?

Your dashboard is empty because you haven't started using our API yet. As you start sending us requests we will populate your dashboard with all kinds of useful metrics and charts.

To help you get started, here are some quick links:

- What's the easiest way to get started?
- How do I upgrade my plan?
- Where can I find my API keys?
- Where do I go to file a support issue/question?

If you don’t want your code shared with the AV developers, use www.scanii.com to see how well it evades most commercial AV software.

In this case, I uploaded my encoded and obfuscated window7shell to VirusTotal and got the following results.

| DETECTION | DETAILS | RELATIONS | BEHAVIOR | COMMUNITY |
| :--- | :---: | :---: | :---: | :---: |
| Ad-Aware | Undetected | | | |
| AhnLab-V3 | Undetected | | | |
| Arity-AVL | Undetected | | | |
| Arcabit | Undetected | | | |
| Avast-Mobile | Undetected | | | |
| Avisa (no cloud) | Undetected | | | |
| BdDldefender | Undetected | | | |
| CAT-QuickHeal | Undetected | | | |
| CMC | Undetected | | | |
| Cyren | Undetected | | | |
| Emsisoft | Undetected | | | |
| ESETNOD32 | Undetected | | | |
| F-Secure | Undetected | | | |
| Fortinet | Undetected | | | |
| Ikarus | Undetected | | | |
| K7AntiVirus | Undetected | | | |
| Kaspersky | Undetected | | | |
| MalwareBytes | Undetected | | | |
| McAfee | Undetected | | | |
| AntigLab | Undetected | | | |
| ALYac | Undetected | | | |
| SecantAge APEX | Undetected | | | |
| Avast | Undetected | | | |
| AVG | Undetected | | | |
| Baidu | Undetected | | | |
| Bitav | Undetected | | | |
| ClamAV | Undetected | | | |
| Comodo | Undetected | | | |
| DrWeb | Undetected | | | |
| eScan | Undetected | | | |
| F-Prot | Undetected | | | |
| FireEye | Undetected | | | |
| GData | Undetected | | | |
| Jiangmin | Undetected | | | |
| K7GW | Undetected | | | |
| Kingsoft | Undetected | | | |
| McAfee-GW-Edition | Undetected | | | |

As you can see, we were successful! None of the AV applications detected my obfuscated shellcode!

## Summary

AV applications detect most malicious payloads and shellcode on the target system. For any chance to remain undetected, you will need to re-encode and obfuscate your shellcode (you can also write your own unique shellcode. I’ll show you how in a future book). OWASP-ZSC, by the OWASP Project, is one of the best AV evasion tools. Here we took shellcode from the shellcode database at shell-storm.org, and with some creative encoding and obfuscation, were able to get it past the major AV applications.

Of course, since I sent my shellcode to VirusTotal, it will be reported to all the major AV application developers, and now they will detect it (you are welcome!). To develop your own undetectable payload, you will need to try different combinations of payloads, encoding, and obfuscation. Be creative and persistent—two of the most important attributes of a master hacker!

### Exercises

- Download and install OWASP-ZSC.
- Select a shellcode from shell-storm.org.
- Obfuscate your shellcode.
- Encode your shellcode.
- Test your shellcode at scanii.com.
- If you know the antivirus application of the target, test your shellcode with it now.
- If your shellcode was detected, start over and try a different approach until your shellcode/payload is undetected.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_476_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_476_1.png)

## 14

### Covering Your Tracks

> *Stars, hide your fires;*
> *Let not light see my black and deep desires.*
>
> — Macbeth

**Hackers who want to remain long in this business need to make certain they leave behind little or no trace of evidence.**

The skilled and vigilant digital forensic investigator can find evidence in many places. In this chapter, we will focus on the log files, file timestamps, and bash command history. If the hacker can clean up the evidence in these three areas, it will be very difficult to trace them.

```
meterpreter > clearev
[*] Wiping 371 records from Application...
[*] Wiping 1344 records from System...
[*] Wiping 355 records from Security...
```

Now that you have exploited the Windows 7 system (Chapter 9) and retrieved the "goodies" such as: (1) Password hashes, (2) Microphone recordings, (3) Webcam recordings, (4) Keystrokes entered by the target system, then (5) Pivoting from the target system to the entire network.

At this stage, you need to make certain that no evidence is left behind to trace this attack back to you.

A digital forensic investigator is capable of recreating the events on a target system primarily from the log files and timestamps. This means that you need to remove all the log files or selectively remove certain log files that capture your activity. In addition, if you have accessed or modified any files, the timestamps on those files are clear evidence of tampering. Finally, if your system falls into the wrong hands, your command history can be incriminating.

Let’s see how you can minimize this evidence and cover your tracks!

### Covering Your Tracks with the Meterpreter

If you were able to plant Metasploit’s meterpreter on the target system, clearing log files is relatively simple. Most of the Windows meterpreters have a built-in
