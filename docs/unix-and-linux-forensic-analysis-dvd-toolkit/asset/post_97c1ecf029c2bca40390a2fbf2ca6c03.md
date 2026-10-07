
# The Hacking Top 10 • Chapter 5

is a very basic example of the power of Nessus. If you were to scan a host that had other functions apart from running a default Apache install, you would undoubtedly find a considerably greater amount of vulnerabilities.

- Synopsis: It is possible to enumerate Web directories.
- Description: This plug-in attempts to determine the presence of various common directories on the remote Web server.
- Risk Factor: None
- Plug-in Output: The following directories were discovered: /software

While this is not in and of of itself a bug, you should manually inspect these directories to ensure they are in compliance with company security standards.

- Other References: OWASP:OWASP-CM-006
- Nessus ID: 11032

# Try it Out

Here are the steps for configuring and running Nessus on Ubuntu Gutsy 7.10.

# Configuring Nessus

1. Create your user account
   - /usr/sbin/nessus-adduser
   - Select a username
   - Authentication [pass] = password
   - Choose a password
   - Validate your password
   - Enter the rules; just press Ctrl-D; this give you the defaults
   - Press Y if the information is OK

2. Create the certificate
   - /usr/bin/nessus-mkcert-client
   - Do you want to register? “Y"
   - Choose the default of “365” days

- Country Code = US
- State name = your state
- Town name = your town
- Organization name = your organization name
- Organization unit = your unit name
- Username #1 = your username
- Choose defaults for days, country, state, city, and organization
- Enter your e-mail address
- Ctrl-D
- Do not make another certificate unless you really want to

3. Register your copy of Nessus

- This will be done at download time. Tenable will send you an e-mail with your account code. You will need this number to download the latest patches. Don't worry, it's open source for personal use.
- Once you have your code, update nessus with the following commands:
   - /usr/bin/nessus-fetch --register <your_registration_code>
   - /usr/bin/nessus-update-plugins

Once you have performed these steps, you are ready to start nessud (server).
nessud -D

You can either be root or use sudo.
sudo nessus

This will start the client.

> NOTE
You would think that you should be able to run this as root, but the truth is, at least in Ubuntu, you cannot. If you try, the GUI will fail to initialize, and you will be frustrated and annoyed. By backing out of root and using the “sudo” command, the GUI fires right up and you can get to work.

Once ness GUI pops up, you can enter in your username and password. When you are connected, you will need to make a few configuration changes before you initiate a scan. Leave the defaults in place, and only make the following changes to these three tabs.

# Plug-ins

By default, all of the plug-ins are loaded. You either just leave them in place as is, or you can select the ones you need for the specific host(s) you are targeting. I would recommend leaving things as they are so that you do not accidentally miss something. However, there is always a chance that one of the plug-ins will crash a target. This does not happen often, but it can happen, so be careful. (Figure 5.5.)

# Figure 5.5 Nessus Plugin-Crashing a Target

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_120_0.png)

www.syngress.com

# Ports

Change the default value of 15000 to 65535, and check the box marked, “Do a reverse lookup on the IP before testing.” (See Figure 5.6.)

# Figure 5.6 Reverse Lookup

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_121_0.png)

# Target

Enter your target or targets on this line. You can scan up to 20 hosts at a time by default. You can also use this option to point nessus at a file with hostnames/IP addresses, a single value, and one entry per line. (See Figure 5.7.)

# 5.7 Nessus Scan of Hostname/IP Addresses

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_122_0.png)

Once you have set up nessus with the target hosts, you are ready to scan. To start your scan(s), simply click the Start the Scan button. Be sure to save your results in Hypertext Markup Language (HTML) format (they are the easiest to read).

So, like nmap, nessus is not a "hack tool" per se. But it does act as a great scout for the malicious attacker. It has the ability to gather a wealth of information about the target and compile that information into an easy-to-read HTML page, complete with any enumerated passwords, directories, and configuration settings. The attacker can then begin to create his attack plan like a sniper, rather than a proverbial bullseye.

# Nikto

According to the Nikto homepage, Nikto is an Open Source (GPL) Web server scanner that performs comprehensive tests against multiple items including potentially dangerous files, over 6700 version-specific problems, and over 550 servers. Scan items and plug-ins are frequently updated and can be automatically updated (if desired). Nikto came up as #1 on the top 100 security tools survey.

Nikto is not designed as an overly stealthy tool. It will test a Web server in the shortest time possible, and it's fairly obvious in log files. However, there is support for anti-IDS methods in case you want to give it a try. By default, Nikto installs to /usr/bin and has a block size of.

Arguably, Web-based applications are the favorite target today. Since they are so prolific and have so many items that need proper configuration, in fact, this is such a huge issue, there is an entire community dedicated to testing and protection of Web applications. This information is available at the Web Application Security Project.

In my example, I have a default installation of Apache 2.4 running in a Fedora VM at 192.168.1.21. I ran Nikto search. Nikto produced the results as seen in Figure 5.8.

> 6 http://nmap.org/project/nikto.shtml
> 7 www.owasp.org/www-project-web-security-testing/

# Figure 5.8 Nikto Search

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_124_0.png)

As you can see, Nikto identifies the hostname, the Web server version, which HTTP methods are allowed, several directories including cgi-bin (a favorite among hackers), and the installation manual. As a former tester, having Nikto scan back information with this meant that I could focus my attack on that specific Web server version, try some directory traversal attacks and break out of the web root, and create some credentials by posting data to .htaccess and passwd files.

Performing recon is always a hacker's first step in promising a target. Knowing what OS is running, what ports are open, what services are using those ports, version of all services will help significantly narrow the focus of any attack. This could quite literally mean the difference between days and minutes.

If any of these tools appear on systems that are part of an incident, you should definitely look at the network logs (provided the customer has them) and try to identify potential targets. A telltale sign of unusual activity is between two systems that normally do not communicate, or don't have a business need to communicate. Use the customer administration staff to help you to determine what is considered “normal” activity and what is not.

# Wireshark

I am beginning to think that my title of “The Hacking Top 10” is not a very appropriate title, although Wireshark does appear #2 on the top 100 security tools survey. The first three tools that I mentioned and described are not what one would think of as traditional hacking tools. They have legitimate uses by IT professionals, right? How can they, and now Wireshark, be in the Hacking Top 10? Well, simply stated, that is the whole point of hacking: making something in a way in which the developers never intended.

In this case, Wireshark, formerly known as Ethereal, is a utility that can sniff network traffic in PCAP format and display that information in a nice, colorful table. So wouldn’t it be just a utility used by the network administrators to perform some aspect of their daily activities? If Wireshark was installed on a system? Maybe, but then again, maybe not. Again, this is where the customer’s IT staff will help you to understand what is considered “normal.” If you find Wireshark on a system, and the administrators tell you it should not be there, then you have something worth looking into.

By default, Wireshark installs into /usr/bin and has a block size of. While its primary use is for network troubleshooting, like so many other tools, it can be used for so much more. Its usage really depends on what the user is trying to do.

It is also a pretty safe assumption that if you find these utilities on a system, it was not the primary target of the attack. There is a bigger fish out there the attacker is trying to find. Would again be a point in which the customer’s Information Technology (IT) staff can help you with a network diagram and what they would consider to be the high value targets; usually something with juicy data on credit card numbers, personally identifiable information, or proprietary information (like research). Remember, this is not always going to be the case. The host that was used for scanning may lead to several others that were used in the same manner to identify other targets. You will really have to be diligent in your analysis of the customer’s system and network log files.

> * www.wireshark.org/
